---
title: "Generating application state"
linkTitle: "Generating application state"
weight: 5
aliases: ["/documentation/nl/guidelines_and_recommendations/generating_application_state/"]  
---

{{% pageinfo color="warning" %}}
<p class="lead">
   <i class="fas fa-language display-4"></i> 
   Page being translated from 
   English to Dutch. Do you speak Dutch? Help us to translate
   it by sending us pull requests!
</p>
{{% /pageinfo %}}

Selenium should not be used to prepare a test case.  All repetitive
actions and preparations for a test case, should be done through other
methods.  For example, most web UIs have authentication (e.g. a login
form). Eliminating logging in via web browser before every test will
improve both the speed and stability of the test. A method should be
created to gain access to the AUT* (e.g. using an API to login and set a
cookie).  Also, creating methods to pre-load data for
testing should not be done using Selenium.  As mentioned previously,
existing APIs should be leveraged to create data for the AUT*.

***AUT**: Application under test
