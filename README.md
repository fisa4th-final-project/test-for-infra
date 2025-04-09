# Testing from an infrastructure perspective
소프트웨어 테스트는 개발된 프로그램이 요구사항을 충족하고, 오류 없이 안정적으로 작동하는지 검증하는 과정이다. 이를 통해 결함을 조기에 발견하고, 제품의 품질을 향상시키며, 유지 보수성을 높일 수 있다.
<table>
  <tbody>
    <tr>
      <td align="center">
         <a href="https://github.com/JaeHee-devSpace">
          <img src="https://avatars.githubusercontent.com/u/193316939?v=4" width="150px;" alt=""/>
          <br /><sub><b> 박재희 </b></sub>
        </a>
        <br />
      </td>
      <td align="center">
          <a href="https://github.com/dyoun12">
          <img src="https://avatars.githubusercontent.com/u/107902336?v=4" width="150px;" alt=""/>
          <br /><sub><b> 김대연 </b></sub>
        </a>
        <br />
      </td>
      <td align="center">
        <a href="https://github.com/BlueRedOrange">
          <img src="https://avatars.githubusercontent.com/u/129985846?v=4" width="150px;" alt=""/>
          <br /><sub><b> 정파란 </b></sub>
        </a>
        <br />
      </td>
      <td align="center">
        <a href="https://github.com/EOTAEGYU">
          <img src="https://avatars.githubusercontent.com/u/123963462?v=4" width="150px;" alt=""/>
          <br /><sub><b> 어태규 </b></sub>
        </a>
        <br />
      </td>
    </tr>
  </tbody>
</table>


## 코드 테스트 - @JaeHee-devSpace
### 개요
코드 테스트는 소프트웨어 개발 과정에서 코드의 정확성, 안정성, 품질을 검증하기 위한 핵심 활동이다. 
> 💡 이를 통해 개발자는 버그를 조기에 발견하고, 유지 보수성을 높이며, 배포 전 안정성을 확보할 수 있다. 

### 유닛 테스트(Unit Test)
유닛 테스트란, 소프트웨어의 개별 단위(함수, 메서드, 모듈 등)를 독립적으로 테스트하는 과정으로 코드의 최소 단위를 검증하여 결함을 조기에 발견하고 유지 보수를 용이하게 한다.

#### 유닛 테스트 Library
| Lang | Lib |
| -- | -- |
| Java | JUnit, TestNG |
| Python | pytest, unittest |
| JavaScript | Jest, Mocha |
| C# | NUnit, xUnit |

#### 유닛 테스트 예시
```java
@Test
void testAddition() {
    Calculator calc = new Calculator();
    assertEquals(5, calc.add(2, 3));
}
```

### 통합 테스트(Integration Test)
통합테스트란 여러 모듈이 함께 동작하는지를 확인하는 테스트로 개별 단위가 올바르게 결합되고 데이터가 정상적으로 흐르는지 검증한다.

#### 통합 테스트 Library
| Lang | Lib |
| -- | -- |
| Java | Spring Boot Test, JUnit, TestContainers |
| Python | pytest-django, unittest |
| JavaScript | Cypress, Supertest |
| C# | MSTest, SpecFlow |

#### 통합 테스트 예시
```java
@SpringBootTest
@RunWith(SpringRunner.class)
public class UserServiceIntegrationTest {
    @Autowired private UserService userService;
    @Autowired private UserRepository userRepository;

    @Test
    public void testCreateUser() {
        User user = new User("Jahe", "jahe@example.com");
        User savedUser = userService.createUser(user);
        assertNotNull(savedUser.getId());
    }
}
```

### 소나큐브(SonarQube)
소나큐브는 코드 품질을 분석하고 정적 코드 검사를 수행하는 도구로 코드 스멜(Code Smell), 버그, 보안 취약점을 자동으로 탐지하고 코드 품질을 유지할 수 있도록 한다.

#### 통합 테스트 Library
- SonarQube
- SonarScanner (Gradle, Maven, Jenkins 등과 연동 가능)
- SonarLint (IDE 내장 분석)

#### 통합 테스트 예시
- CI/CD에서 SonarQube를 사용하여 코드 분석 자동화
- SonarQube 대시보드를 통해 코드 복잡도 및 보안 이슈 확인
    

<br>

---

<br>

## 성능 테스트 - @EOTAEGYU

### 개요
성능 테스트는 소프트웨어나 시스템이 다양한 부하 조건 하에서 얼마나 안정적이고 빠르게 동작하는지를 검증하는 과정이다. 
> 💡 이는 사용자 수 증가, 장시간 서비스 운영, 한계 부하 조건 등을 시뮬레이션하여 병목 현상과 성능 저하 원인을 사전에 식별하고, 시스템 확장성과 안정성을 확보하는 데 목적이 있다.

#### 성능 테스트의 목적 요약
| 목적 | 설명 |
| --- | --- |
| 병목 현상 식별 | CPU, 메모리, DB 쿼리, 네트워크 등 시스템의 한계점이나 병목 지점을 미리 파악 |
| 최대 처리량 측정 | 시스템이 감당할 수 있는 최대 사용자 수, 요청 수 등 처리 가능 범위를 측정 |
| 응답 속도 확인 | 평균 응답 시간, 최대 응답 시간 등 SLA(Service Level Agreement) 준수 여부 확인 |
| 확장성(Scalability) 평가 | 사용자 수 증가 시 시스템이 얼마나 잘 확장되는지 테스트 |
| 장시간 운영 안정성 테스트 | 장시간 서비스 운영 시 메모리 누수나 리소스 고갈 등의 문제가 발생하는지 확인 |


### 성능 테스트에 사용되는 대표적인 도구
| 도구 | 특징 |
| --- | --- |
| Apache JMeter | 가장 널리 사용되는 오픈소스 성능 테스트 도구. GUI 제공. HTTP, WebSocket, DB 등 지원 |
| Locust | Python 기반으로 사용이 쉬우며 코드로 시나리오 작성 가능 |
| k6 (Grafana) | 코드 기반의 경량 테스트 도구. CI/CD와의 연동에 강점 |
| Gatling | Scala 기반으로 코드 작성 방식. 비동기 처리 성능이 좋음 |
| Artillery | JavaScript 기반으로 Node.js 서비스에 적합 |
| wrk / hey | 간단한 벤치마킹용 CLI 도구 (고급 설정은 제한적) |


### 성능 테스트 흐름

#### 1단계. 테스트 계획 수립
- 목표 정의: 최대 동시 사용자 수, 응답 시간 목표 등
- 테스트 대상 정의: 어떤 API/기능을 테스트할 것인가?
- 시나리오 설계: 사용자 행동을 어떻게 시뮬레이션할 것인가?

#### 2단계. 테스트 환경 구성
- 실서비스와 유사한 테스트 환경 구축 (서버, DB, 네트워크 조건)
- 로그 및 모니터링 시스템 연결 (Grafana, Prometheus 등)

#### 3단계. 성능 시나리오 작성
- 예: 로그인 → 상품 조회 → 장바구니 담기 → 결제
- 도구에 따라 JSON, YAML, Python, Scala 등으로 작성

#### 4단계. 부하 테스트 실행
- Smoke Test: 간단히 테스트 구성 확인
- Load Test: 일정 부하에서 시스템 성능 측정
- Stress Test: 시스템 한계 초과 부하로 테스트
- Soak Test: 장시간 부하 테스트 (안정성 확인)

#### 5단계. 모니터링 및 로그 분석
- CPU, 메모리, 네트워크 사용량
- DB 쿼리 속도, 오류 로그
- APM(Application Performance Monitoring) 도구 사용 가능 (예: New Relic, Datadog)

#### 6단계. 결과 분석 및 병목 개선
- 응답 시간 초과, 오류율 증가 구간 확인
- 병목 지점(예: DB, 캐시 미사용, GC 등) 분석
- 개선안 수립 및 리팩토링

#### 7단계. 재테스트 및 문서화
- 개선 후 성능 다시 측정
- 테스트 결과 및 개선 내역 문서화


### 성능 테스트 시 유의할 점
- 실제와 유사한 데이터로 테스트 (Mock 데이터는 실제 부하를 반영 못 함)
- 네트워크 조건 반영 (예: 클라이언트와 서버 간의 지연 시간)
- 서버 외에 DB, 캐시 등 모든 구성 요소 포함
- 성능 테스트는 반복적으로 수행 (수정 후 재검증 포함)
- 자동화하여 CI/CD 파이프라인에 통합 가능 (예: GitHub Actions + k6)


### 예시 시나리오 (e.g. 쇼핑몰)
1. 100명의 사용자가 동시에 로그인 시도
2. 상품 목록을 500명이 조회
3. 장바구니에 200명이 상품 담기
4. 결제 API에 대해 10초당 50건 요청
5. 위 시나리오를 30분 동안 반복 실행

<br>

---

<br>

## 사용자 테스트 - @dyoun12

### 개요

사용자 테스트는 서비스를 제공받는 유저의 입장에서 유즈케이스별 액션 체인을 만들어 테스트를 진행한다. 

> 💡 실 서비스 제공 시에도 유발할 트래픽과 엔드포인트 별 요청에 대한 테스트를 진행할 수 있으며, 다양한 유저환경(브라우저 별 테스트)에 대한 검증이 이루어질 수 있다.

### 예시 기준
유저 테스트는 일반적으로 서비스 CI/CD 파이프라인 내에 릴리즈 직전에 수행되는 마지막 테스트로 테스트 기준을 명확하게 설정해야한다.

| 항목 | 기준 |
| --- | --- |
| 시나리오 전체 성공률 | 100% 또는 중요 시나리오 기준 95% 이상 성공 |
| 중요 기능 실패 | 로그인, 결제, 인증 관련 시나리오 실패 시 무조건 실패 처리 |
| 테스트 시간 제한 | 테스트 수행 시간은 10분 이내 (CI 파이프라인 고려) |
| 에러 로그 | 콘솔/서버 에러 발생 시 실패로 간주 |
| 릴리즈 승인 트리거 | 테스트 완료 후 관리자가 승인해야만 배포되도록 설정 (예: GitHub Action의 환경 승인 단계 사용) |

### 적용 예시

| Skil | 설명 |
| --- | --- |
| Spring Boot | 테스트 대상 애플리케이션, 필요 시 테스트 중 임시 실행 가능 |
| JUnit | 테스트 러너, Cucumber 테스트를 실행하는 데 사용 |
| Gitlab (github) | CI/CD 파이프라인에서 사용될 코드 저장소 |
| Cucumber | Gherkin 문법으로 유즈케이스 별 시나리오를 작성 (`.feature` 파일) |
| Selenium | 실제 브라우저를 자동 조작 (ChromeDriver 등 사용) |

#### Gherkin 시나리오

```gherkin
# login.feature

Feature: 로그인 기능

  Scenario: 유저가 올바른 자격으로 로그인한다
    Given 사용자는 로그인 페이지에 접속했다
    When "testuser"와 "password123"를 입력하고 로그인 버튼을 누르면
    Then 마이페이지로 이동해야 한다
```

#### Step 정의

```java
// LoginSteps.java

package stepdefinitions;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import support.SeleniumHooks;
import io.cucumber.java.en.*;

public class LoginSteps {
    WebDriver driver = SeleniumHooks.driver;

    @Given("사용자는 로그인 페이지에 접속했다")
    public void 접속했다() {
        driver.get("http://localhost:8080/login");
    }

    @When("\"{word}\"와 \"{word}\"를 입력하고 로그인 버튼을 누르면")
    public void 로그인_입력(String username, String password) {
        driver.findElement(By.id("username")).sendKeys(username);
        driver.findElement(By.id("password")).sendKeys(password);
        driver.findElement(By.id("login-btn")).click();
    }

    @Then("마이페이지로 이동해야 한다")
    public void 마이페이지_이동() {
        String url = driver.getCurrentUrl();
        assert url.contains("/mypage");
    }
}
```

#### Selenium 설정

```java
// SeleniumHooks.java

package support;

import io.cucumber.java.After;
import io.cucumber.java.Before;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class SeleniumHooks {
    public static WebDriver driver;

    @Before
    public void setup() {
        // ChromeDriver 경로 설정
        System.setProperty("webdriver.chrome.driver", "/usr/bin/chromedriver");
        driver = new ChromeDriver();
    }

    @After
    public void tearDown() {
        if (driver != null) {
            driver.quit();
        }
    }
}
```

#### 테스트 러너 작성

```java
// TestRunner.java

package runners;

import io.cucumber.junit.Cucumber;
import io.cucumber.junit.CucumberOptions;
import org.junit.runner.RunWith;

@RunWith(Cucumber.class)
@CucumberOptions(
    features = "src/test/resources/features",
    glue = {"stepdefinitions", "support"},
    plugin = {"pretty", "html:target/cucumber-reports"},
    monochrome = true
)
public class TestRunner {}
```

> 테스트가 종료되면 HTML 리포트를 생성하거나 CI 파이프라인에서 이를 아티팩트로 포함함으로써 GitLab에서 관리자 확인 및 이슈등록 자동화가 가능하다.

<br>

---

<br>

## 장애 테스트 - @BlueRedOrange

### 개요
장애 테스트(Failure Testing)는 시스템이 예상치 못한 장애나 자원 고갈 상황에서 어떻게 반응하고 복구하는지를 검증하는 과정이다. 시스템의 복원력(Resilience)과 고가용성(High Availability)을 보장하기 위해 필수적으로 수행되며, 특히 클라우드 네이티브 인프라나 마이크로서비스 아키텍처에서 중요도가 높다.

> 시스템이 장애 시 자체 복구하거나, 사용자 영향 없이 운영 지속 가능한지를 확인하는 것이다.


### 컨테이너(Container) 장애 테스트

#### 체크포인트
- Pod/Container 하나 죽었을 때 자동 복구되는지 확인
- 네트워크/스토리지 장애 발생 시 서비스 레벨 영향 분석

#### 장애테스트 주요 툴
- Chaos Mesh (Kubernetes 장애 실험용)
- Kube-monkey (랜덤으로 Pod 죽이는 Chaos Monkey 스타일 툴)

#### 실제 예시
| 테스트 종류 | 방법 | 체크포인트 |
| --- | --- | --- |
| Pod 강제 종료 | `kubectl delete pod [pod-name]` | ReplicaSet/Deployment가 새 Pod 자동 생성하는지 |
| 네트워크 끊김 | Chaos Mesh로 네트워크 패킷 드롭 주입 | 다른 서비스 호출 실패 후 복구되는지 |
| Container CPU 100% | Chaos Mesh CPUStress 주입 | HPA(Horizontal Pod Autoscaler)로 자동 스케일 되는지 |
| ConfigMap 업데이트 오류 | 잘못된 ConfigMap 롤아웃 → 복구 여부 | 롤백 자동화 확인 (`kubectl rollout undo`) |

---

### VM(Virtual Machine) 장애 테스트

#### 체크포인트
- VM 자체가 장애났을 때 (서버 다운) Auto-recovery 되는지
- VM 간 통신 장애(네트워크 분할) 발생 시 서비스 복구되는지
- 디스크 장애, CPU 오버로드 상황에서 안정성 검증

#### 주요 툴
- AWS Fault Injection Simulator (AWS 기반 장애 주입)
- Azure Chaos Studio (Azure 클라우드용)
- Stress-ng: CPU, Memory, IO 부하 걸기
- TC: 네트워크 지연, 패킷 손실 시뮬레이션

#### 실제 예시
| 테스트 종류 | 방법 | 체크포인트 |
| --- | --- | --- |
| VM 강제 중단 | AWS EC2 Stop/Start, Azure VM Restart | Auto Scaling Group 복구 정상 여부 |
| 디스크 Full 테스트 | 임의 파일로 디스크 채우기 (`fallocate` 명령어) | 애플리케이션 데이터 쓰기 실패 감지 |
| 네트워크 단절 테스트 | `tc` 명령어로 패킷 드랍 | 분산 시스템 노드 간 재시도/복구 전략 정상 작동 여부 |
| CPU 100% 점유 | `stress --cpu 8` | VM 모니터링 시스템(CPU Alert) 정상 감지 여부 |

### 장애 테스트 단계별 요약
| 단계 | 주요 목표 | 대표 툴 | 예시 |
| --- | --- | --- | --- |
| 네트워크 장애 | 통신 문제 복원력 확인 | tc, Chaos Mesh | API 서버-DB 500ms 지연 |
| 서버 리소스 고갈 | 오토스케일링, 리소스 회복 테스트 | stress, Chaos Mesh | CPU 100% 부하 실험 |
| 서버 강제 종료 | 무중단 서비스 유지 확인 | Chaos Monkey | Kubernetes Pod 죽이기 |
| DB 장애 및 Failover | 데이터 일관성 + 자동 복구 테스트 | RDS, Patroni, DBChaos | RDS Failover 시 애플리케이션 복구 여부 |
| 네트워크 분할 | Consistency/Availability 확인 | Toxiproxy, Chaos Mesh | Redis 노드 분리 테스트 |
| 스토리지 장애 | 데이터 저장 계층 복원력 확인 | IOChaos | ElasticSearch 디스크 오류 시나리오 |
