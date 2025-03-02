---
title: "Toml Options"
linkTitle: "Toml Options"
weight: 3
description: Grid configuration examples using Toml files.
---

{{% pageinfo color="warning" %}}
<p class="lead">
   <i class="fas fa-language display-4"></i> 
   Page being translated from 
   English to Korean. Do you speak Korean? Help us to translate
   it by sending us pull requests!
</p>
{{% /pageinfo %}}

All the options shown in [CLI options]({{< ref "cli_options.md" >}}) can be configured through
a [TOML](https://github.com/toml-lang/toml) file. This page shows configuration examples for the
different Grid components.

{{% pageinfo color="primary" %}}
Note that this documentation could be outdated if an option was modified or added
but has not been documented yet. In case you bump into this situation, please check
the ["Config help"]({{< ref "config_help.md" >}}) section and feel free to send us a
pull request updating this page.
{{% /pageinfo %}}


## Overview

Selenium Grid uses [TOML](https://github.com/toml-lang/toml) format for config files. 
The config file consists of sections and each section has options and its respective value(s).

Refer to the [TOML documentation](https://toml.io/en/) for detailed usage guidance. In case of 
parsing errors, validate the config using [TOML linter](https://www.toml-lint.com/).

The general configuration structure has the following pattern: 

```toml
[section1]
option1="value"

[section2]
option2=["value1","value2"]
option3=true
```

Below are some examples of Grid components configured with a Toml file, the component can be
started in the following way:

```
java -jar selenium-server-<version>.jar <component> --config /path/to/file/<file-name>.toml
```


### Standalone

A Standalone server, running on port 4449, and a new session request timeout of 500 seconds. 

```toml
[server]
port = 4449

[sessionqueue]
session-request-timeout = 500
```

### Specific browsers and a limit of max sessions

A Standalone server or a Node which only has Firefox and Chrome enabled by default.

```toml
[node]
drivers = ["chrome", "firefox"]
max-sessions = 3
```

### Configuring and customising drivers

Standalone or Node server with customised drivers, which allows things like having Firefox Beta 
or Nightly, and having different browser versions. 

```toml
[node]
detect-drivers = false
[[node.driver-configuration]]
max-sessions = 100
display-name = "Firefox Nightly"
stereotype = "{\"browserName\": \"firefox\", \"browserVersion\": \"93\", \"platformName\": \"MAC\", \"moz:firefoxOptions\": {\"binary\": \"/Applications/Firefox Nightly.app/Contents/MacOS/firefox-bin\"}}"
[[node.driver-configuration]]
display-name = "Chrome Beta"
stereotype = "{\"browserName\": \"chrome\", \"browserVersion\": \"94\", \"platformName\": \"MAC\", \"goog:chromeOptions\": {\"binary\": \"/Applications/Google Chrome Beta.app/Contents/MacOS/Google Chrome Beta\"}}"
[[node.driver-configuration]]
display-name = "Chrome Dev"
stereotype = "{\"browserName\": \"chrome\", \"browserVersion\": \"95\", \"platformName\": \"MAC\", \"goog:chromeOptions\": {\"binary\": \"/Applications/Google Chrome Dev.app/Contents/MacOS/Google Chrome Dev\"}}"
webdriver-executable = '/path/to/chromedriver/95/chromedriver'
```

### Standalone or Node with Docker

A Standalone or Node server that is able to run each new session in a Docker container. Disabling 
drivers detection, having maximum 2 concurrent sessions. Stereotypes configured need to be mapped 
to a Docker image, and the Docker daemon needs to be exposed via http/tcp.


```toml
[node]
detect-drivers = false
max-sessions = 2

[docker]
configs = 
    [
        "selenium/standalone-chrome:93.0", "{\"browserName\": \"chrome\", \"browserVersion\": \"91\"}", 
        "selenium/standalone-firefox:92.0", "{\"browserName\": \"firefox\", \"browserVersion\": \"92\"}"
    ]
url = "http://localhost:2375"
video-image = "selenium/video:latest"
```

### Relaying commands to a service endpoint that supports WebDriver

It is useful to connect an external service that supports WebDriver to Selenium Grid.
An example of such service could be a cloud provider or an Appium server. In this way,
Grid can enable more coverage to platforms and versions not present locally.

The following is an en example of connecting an Appium server to Grid.

```toml
[server]
port = 5555

[node]
detect-drivers = false

[relay]
# Default Appium server endpoint
url = "http://localhost:4723/wd/hub"
status-endpoint = "/status"
# Stereotypes supported by the service
configs = [
  "1", "{\"browserName\": \"chrome\", \"platformName\": \"android\", \"appium:platformVersion\": \"11\"}"
]
```

### Basic auth enabled

It is possible to protect a Grid with basic auth by configuring the Router/Hub/Standalone with
a username and password. This user/password combination will be needed when loading the Grid UI
or starting a new session.

```toml
[router]
username = "admin"
password = "myStrongPassword"
```

Here is a Java example showing how to start a session using the configured user and password.

```java
URL gridUrl = new URL("http://admin:myStrongPassword@localhost:4444");
RemoteWebDriver webDriver = new RemoteWebDriver(gridUrl, new ChromeOptions());
```

