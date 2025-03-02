---
title: "구성 요소 이해"
linkTitle: "구성 요소 이해"
weight: 1
aliases: ["/documentation/ko/webdriver/understanding_the_components/"]
---

WebDriver를 사용하여 테스트 스위트를 빌드하려면 이해하고 이해해야합니다.
다양한 구성 요소를 효과적으로 사용합니다. 모든 것과 마찬가지로
소프트웨어, 다른 사람들은 동일한 아이디어에 대해 다른 용어를 사용합니다. 아래는
이 설명에서 용어가 사용되는 방식에 대한 분석.

### 술어

* **API:** _Application Programming Interface_. 이것은 "명령"세트입니다
WebDriver를 조작하는 데 사용합니다.
* **Library:** API와 필요한 코드를 포함하는 코드 모듈
그것들을 구현하기 위해. 라이브러리는 각 언어 바인딩에 따라 다릅니다 (예 : .jar).
Java 용 파일, .NET 용 .dll 파일 등
* **Driver:** 실제 브라우저를 제어합니다. 대부분의 운전자
브라우저 공급 업체 자체에 의해 생성됩니다. 드라이버는 일반적으로
브라우저 자체를 사용하여 시스템에서 실행되는 실행 가능 모듈
테스트 스위트를 실행하는 시스템에는 없습니다. (그것들이
참고 : _일부 사람들은 드라이버를 프록시라고합니다._
* **Framework:** WebDriver 지원으로 사용되는 추가 라이브러리
스위트. 이러한 프레임 워크는 JUnit 또는 NUnit과 같은 테스트 프레임 워크 일 수 있습니다.
또한 자연 언어 기능을 지원하는 프레임 워크 일 수도 있습니다.
오이 또는 로보 티움으로. 프레임 워크는 다음을 위해 작성되고 사용될 수도 있습니다.
테스트중인 시스템 조작 또는 구성, 데이터
제작, 테스트 오라클 등


### 부품과 조각
최소한 WebDriver는 드라이버를 통해 브라우저와 통신합니다. 통신
WebDriver는 드라이버를 통해 브라우저에 명령을 전달합니다.
동일한 경로를 통해 정보를 다시받습니다.

{{< figure src="/images/documentation/webdriver/basic_comms.png" class="img-responsive text-center" alt="기본 커뮤니케이션">}}

드라이버는 Google의 ChromeDriver와 같은 브라우저에 따라 다릅니다.
Chrome/Chromium, Mozilla Firefox 용 GeckoDriver 등 드라이버는 다음에서 실행됩니다.
브라우저와 동일한 시스템. 이것은 동일한 시스템 일 수도 있고 아닐 수도 있습니다.
테스트 자체가 실행 중입니다.

위의 간단한 예는 _direct_ 통신 입니다. 통신
브라우저는 Selenium 서버를 통한 _remote_ 통신 일 수도 있고
RemoteWebDriver. RemoteWebDriver는 드라이버와 동일한 시스템에서 실행됩니다.
그리고 브라우저.

{{< figure src="/images/documentation/webdriver/remote_comms.png" class="img-responsive text-center" alt="원격 커뮤니케이션">}}

Selenium Server 또는 Selenium을 사용하여 원격 통신을 수행 할 수도 있습니다.
그리드, 둘 다 호스트 시스템의 드라이버와 통신

{{< figure src="/images/documentation/webdriver/remote_comms_server.png" class="img-responsive text-center" alt="그리드와의 원격 통신">}}

## 프레임 워크가 적합한 곳

WebDriver에는 하나의 작업과 하나의 작업 만 있습니다.
위의 방법 중 하나입니다. WebDriver는 테스트에 대해 알지 못합니다.
사물을 비교하는 방법을 알고, 통과 또는 실패를 주장하며, 확실하지 않습니다
보고 또는 주어진 / 언제 / 그럼 문법에 관한 것.

다양한 프레임 워크가 등장합니다. 최소한 당신은 필요합니다
언어 바인딩과 일치하는 테스트 프레임 워크 (예 : .NET, JUnit 용 NUnit
Java, Ruby 용 RSpec 등

테스트 프레임 워크는 WebDriver 실행 및 실행을 담당합니다.
그리고 테스트의 관련 단계. 따라서, 당신은 비슷한 것으로 생각할 수 있습니다
다음 이미지에.

{{< figure src="/images/documentation/webdriver/test_framework.png" class="img-responsive text-center" alt="테스트 프레임 워크">}}

Cucumber와 같은 자연 언어 프레임 워크 / 도구는 그 일부로 존재할 수 있습니다.
위 그림의 테스트 프레임 워크 상자 또는 테스트 프레임 워크를 래핑 할 수 있습니다.
전적으로 자신의 구현에.
