# spring-tutorial-23rd

--- 

## 1️⃣ spring이 지원하는 기술들(IoC/DI, AOP, PSA 등)

---
- **IoC(제어권의 역전)**: 제어권이 스프링 프레임워크에 있어 개발자가 제어권을 가지지 않음
    - 객체의 생성과 의존성 관리를 개발자가 아닌 스프링 컨테이너가 담당

  → 객체 간의 결합도를 낮추고, 코드의 유연성을 높임

- **DI(의존성 주입)**: 사용할 객체를 직접 생성하는 것이 아닌, 외부 컨테이너가 생성한 객체를 주입받아 사용
    - 객체 간의 의존성을 낮추고 유지보수 및 테스트를 용이하게 하는 핵심 기능
    - 어노테이션을 사용하여 의존성 주입

  → 객체 간의 결합도를 낮춤

- **AOP(관점 지향 프로그래밍)**: 관점 지향 프로그래밍을 통해 핵심 비즈니스 로직과 횡단 관심 사항을 **분리**하여 개발하는 기술
    - Logging, 트랜잭션 처리 등을 관점으로 분리하여 적용
    - 애플리케이션의 핵심적인 기능에서 부가적인 기능을 **분리**해 Aspect라는 독특한 모듈로 만들어서 설계하고 개발하는 방법

  → 코드의 중복을 줄이고, 유지보수를 쉽게 함

- **PSA(서비스 추상화)**: 환경과 세부 기술의 변화에 관계없이 일관된 방식으로 기술을 사용할 수 있게 해주는 서비스 추상화
    - 특정 기술에 종속되지 않도록 인터페이스로 추상화 계층을 둠
    - ex) 트랜잭션, Spring Web MVC

  → 특정 기술이나 라이브러리의 변화에 상관없이, 개발자가 작성한 비즈니스 로직을 수정하지 않고도 일관된 방식으로 서비스를 이용할 수 있게 해줌
- **Spring Boot**: 애플리케이션을 빠르게 구축하고 실행하기 위한 도구
- **Spring Data**: 데이터 액세스 기술을 추상화하고, NoSQL 및 관계형 데이터베이스에 대한 통합 지원을 제공
- **Spring Data JPA:** SQL을 직접 작성하지 않고 인터페이스만으로 DB를 조작할 수 있게 해줌
- **Spring Security**: 보안 기능을 제공하여 인증과 권한 부여를 관리하고 웹 애플리케이션의 보안 강화

---

## 2️⃣ Spring Bean 이 무엇이고, Bean 의 라이프사이클과 Bean Scope에 대해 조사해요

---
- **Spring Bean**: 스프링 프레임워크 내부에서 관리되는 객체
    - ex) UserService라는 클래스를 만들고 이것을 스프링 빈으로 등록하면 스프링 컨테이너가 그 객체의 생애 주기(생성, 소멸)를 관리
- **Spring Bean을 등록하는 방법**
    - 어노테이션 기반 설정: 클래스에 @Component, @Service, @Repository, @Controller 등의 어노테이션을 사용하여 빈을 등록
        - @Controller, @Service, @Repository 들은 @Component를 포함
    - @Configuration과 @Bean 어노테이션을 사용해 자바 클래스에서 빈을 직접 등록
- **Spring Bean의 생명주기(Lifecycle)**
    - 스프링 컨테이너 생성 → 빈 생성 → 의존관계 주입 → 초기화 콜백 → 빈 사용 → 소멸 전 콜백 → 스프링 종료
    - 콜백: 객체를 생성한 후, 의존관계까지 주입되었으니 사용이 가능하다고 알려주는 것
- **Bean Scope**: Bean으로 등록한 객체가 생성되고 소멸 될 때까지 생존하는 범위
    - 어노테이션으로 설정: `@Scope("prototype")`
    - 6가지: Singletone(기본 Bean Scope) / Prototype / Request / Session / Application / WebSocket
        - **Singletone Scope**: 스프링 프레임워크의 기본 스코프, 스프링 컨테이너가 기동 될 때부터 종료 될 때까지 유지되는 가장 넓은 범위의 스코프
            - Bean 별로 1개의 인스턴스만 생성하고, Bean을 요청할 때 마다 항상 같은 인스턴스를 반환
        - **Prototype Scope**
            - 해당 Bean을 사용할 때 마다 매번 새로운 Bean 인스턴스를 생성하는 매우 짧은 범위의 스코프, 컨테이너는 빈의 생성과 의존관계 주입 그리고 초기화까지만 관여
        - **request Scope**
            - HTTP Request 요청이 올 때 마다, 해당 Bean의 인스턴스가 새로 생성되고 응답 이후 소멸되는 스코프
        - **session Scope**
            - HTTP Session이 생성될 때 마다 해당 Bean의 인스턴스가 생성되고, 세션이 종료되면 소멸되는 스코프
        - **application Scope**
            - Sevlet Context가 시작할 때 해당 Bean의 인스턴스가 생성되고, 종료될 때 같이 소멸되는 스코프
        - **websocket Scope**
            - WebSocket이 열릴 때 해당 Bean의 인스턴스가 생성되고, 연결이 닫힐 때 소멸되는 스코프
- **어노테이션:** 소스 코드에 `@` 기호를 사용하여 추가적인 정보를 제공하는 데이터
    - 역할:
        - 컴파일러에게 문법 에러를 체크하도록 정보를 제공
        - 프로그램을 빌드할 때 코드를 자동으로 생성할 수 있도록 정보를 제공
        - 런타임에 특정 기능을 실행하도록 정보를 제공
    - ex:
        - **@Override**: 컴파일러에게 메서드를 오버라이딩 하는것이라고 알림
        - **@SpringBootApplication:** Srping Boot를 자동으로 실행시켜주는 어노테이션
        - **@Configuration**: 스프링 IoC 컨테이너에게 해당 클래스가 Bean 구성 Class임을 알려주는 어노테이션
        - **@Component**: 개발자가 직접 작성한 Class를 Bean으로 등록하기 위한 어노테이션
        - **@Service:** Service class에서 쓰이는 어노테이션으로 비즈니스 로직을 수행하는 Class라는 것을 나타내는 용도

---

## 3️⃣ 스프링에서 어노테이션을 통해 Bean을 등록할 때, 어떤 일련의 과정이 일어날까?

---
1. **스캐닝 (Scanning)**
    - `@SpringBootApplication` 혹은 `@ComponentScan`이 설정된 메인 클래스가 실행되면, 지정된 패키지 경로를 전수 조사
    - 대상: `@Component`, `@Service`, `@Repository`, `@Controller`, `@Configuration` 등 `@Component`를 메타 어노테이션으로 가진 모든 클래스
2. **빈 정의 생성 (Bean Definition Metadata)**
    - 찾아낸 클래스들을 바로 객체로 만드는 것이 아니라, **BeanDefinition**이라는 설계도 객체를 먼저 생성
    - 클래스 타입, 스코프(Singleton/Prototype), 지연 로딩 여부, 의존 관계 설정 등의 메타데이터 포함
3. **빈 생성 및 인스턴스화 (Instantiation)**
    - 정의된 설계도(BeanDefinition)를 바탕으로 스프링 컨테이너가 실제 객체 생성
4. **의존성 주입 (DI)**
    - 빈들 간의 의존 관계를 연결
    - **@Autowired:** 타입을 기준으로 연관된 빈을 찾아 주입
5. **초기화 및 사용 (Initialization & Usage)**
    - 최종 세팅 수행
    - 빈의 초기화 콜백을 실행하여 사용 가능한 상태로 만듦
        - Callback: `@PostConstruct` 어노테이션이 붙은 메서드가 실행되어 초기 설정을 마침
    - 모든 세팅이 끝나면 스프링 컨테이너가 관리하는 **Singleton Bean Registry**에 등록되어 애플리케이션 어디서든 재사용될 수 있는 상태가 됨
- 왜 이런 과정이 필요할까 → **유연성**: 설계도를 먼저 만들고 나중에 객체를 생성하기 때문에, 중간에 설정을 바꾸거나 특정 상황에서 다른 객체를 끼워넣는 등 제어권의 역전을 완벽하게 구현 가능


### 💥`@ComponentScan` 과 같은 어노테이션을 사용하여 스프링이 컴포넌트를 어떻게 탐색하고 찾을까?

**1. 설정 정보의 파싱 (Configuration Parsing)**

* `ConfigurationClassPostProcessor`라는 핵심 클래스가 동작 → `@Configuration`이 붙은 설정 클래스를 읽고, 그 안에 적힌 `@ComponentScan`의 설정값(탐색 범위, 필터 등)을 분석

**2. 패키지 리소스 탐색 (Resource Scanning)**

  * **ASM**을 사용하여 클래스 파일을 직접 읽음

**3. 메타데이터 읽기 및 필터링 (Metadata Reading)**

  * 스프링은 클래스를 실행하지 않고도 바이트코드를 분석하여 정보를 추출(파일을 하나하나 실행하는 것이 아니라 파일의 내용만 읽음)

    - **MetadataReader:** `CachingMetadataReaderFactory`를 통해 각 클래스 파일의 메타데이터를 읽음
    - **Annotation Filter:** 읽어들인 클래스에 `@Component` 혹은 이를 포함한 `@Service`, `@Controller` 등이 있는지 확인
    - **Exclude/Include Filter:** 개발자가 설정한 제외 대상이나 포함 대상 필터를 적용하여 최종 후보를 선별

  **4. BeanDefinition 생성 및 등록**

* 조건에 부합하는 클래스를 찾으면, 이를 바탕으로 `ScannedGenericBeanDefinition` 객체를 생성

  - **식별자 생성:** `BeanNameGenerator`가 빈의 이름을 결정
  - **Scope 설정:** `@Scope` 어노테이션이 있다면 해당 설정(Singleton, Prototype 등)을 정의서에 기록
  - **Registry 등록:** 최종 완성된 `BeanDefinition`을 `BeanDefinitionRegistry`라는 저장소에 보관
### 💥하나의 interface를 구현한 service가 여러 개 있을때 어떻게 주입 해야할까?
1. `@Primary` 사용: 우선순위 정하기
2. `@Qualifier` 사용하기: 이름표 붙이기
    - 주입받는 시점에 이름표를 가진 빈을 명시하는 방법
3. List, Map 사용: 모두 다 가져오기
    - 모든 구현체를 다 가져와 상황에 맞게 골라 쓰고 싶을 때 사용

---
## 4️⃣ Spring MVC 심층 분석

---

- ### **MVC 패턴 vs Spring MVC**
    - **MVC 패턴 (이론적 개념)**: 소프트웨어 디자인 패턴 중 하나로, 애플리케이션의 역할을 세 가지로 나누어 관리
        - **Model:** 데이터와 비즈니스 로직을 담당
        - **View:** 사용자에게 보여지는 화면(UI)을 담당
        - **Controller:** 사용자의 요청을 받아 Model과 View 사이를 중개
    - **Spring MVC (구현체)**: MVC 패턴을 Spring 프레임워크의 철학에 맞춰 구현한 웹 모듈
        - Spring MVC에는 일반적인 MVC 패턴에 없는 특별한 컴포넌트들이 추가
            - **DispatcherServlet (Front Controller):** 모든 클라이언트 요청을 입구에서 한 번에 받음
            - **HandlerMapping:** 요청을 어떤 컨트롤러가 처리할지 찾아줌
            - **Controller:** 실제 비즈니스 로직을 호출하고 결과를 반환
            - **ViewResolver:** 컨트롤러가 보낸 뷰 이름을 실제 물리적인 경로로 연결
- ### **Servlet**
    - **Servlet**: 자바를 사용하여 웹 페이지를 **동적**으로 생성하는 서버 측 프로그램
        - **스레드 방식:** 요청이 올 때마다 프로세스를 새로 만드는 게 아니라, 기존 프로세스 안에서 스레드를 생성해 처리하므로 효율적
- **웹 요청 처리 과정**
![img_1.png](img_1.png)

1. 사용자(클라이언트)가 URL을 입력하면 HTTP Request가 servlet Container로 전송
2. 요청을 전송받은 Servlet Container는 HttpServletRequest, HttpServletResponse 객체를 생성
3. web.xml을 기반으로 사용자가 요청한 URL이 어느 서블릿에 대한 요청인지 찾음
4. 해당 서블릿에서 service메소드를 호출한 후 클리아언트의 GET, POST여부에 따라 doGet() 또는 doPost()를 호출
5. doGet() or doPost() 메소드는 동적 페이지를 생성한 후 HttpServletResponse객체에 응답 전송
6. 응답이 끝나면 HttpServletRequest, HttpServletResponse 두 객체를 소멸
- **Servlet 컨테이너: Servlet을 관리해주는 컨테이너(Tomcat)**
    - **통신 지원:** 소켓을 만들고 특정 포트를 리스닝하는 복잡한 네트워크 통신을 대신 수행
    - **생명주기 관리:** 서블릿 클래스를 로딩해서 인스턴스화하고, 적절한 시점에 메모리를 정리
    - **멀티스레드 지원:** 동시에 여러 요청이 들어와도 안전하게 스레드를 생성하고 관리
- ### **Tomcat/WAS**
    - **Tomcat**: 오픈소스 WAS(Web Application Server)이며, 자바 서블릿(Servlet)과 JSP를 실행할 수 있는 환경을 제공
        - Servlet 컨테이너라고도 불림
    - **WAS**: 자바 코드를 실행하여 동적인 결과를 만들어내는 서버
        - Web Server + Web Container(Servlet Container)의 형태
- ### **Dispatcher Servlet**
    - **Dispatcher Servlet**: 모든 HTTP 요청을 가장 먼저 받아 적절한 컨트롤러로 배분하는 중앙 컨트롤러(Front Controller)
        - **중앙 집중 제어:** 모든 요청의 입구 역할을 하여 보안, 로깅, 인코딩 등의 공통 로직을 한곳에서 처리
        - **어댑터 역할:** 다양한 방식(애노테이션 기반, 인터페이스 기반 등)으로 작성된 컨트롤러를 유연하게 호출
        - **뷰 렌더링 중계:** 컨트롤러가 반환한 논리적인 뷰 이름을 실제 화면으로 연결
    - **DispatcherServlet 동작 흐름**

![img.png](img.png)
1. **클라이언트 요청:** 사용자가 웹브라우저나 앱을 통해 HTTP 요청을 보내고 가장 먼저 **Dispatcher Servlet**이 요청을 받음
2. **Handler Mapping:** Dispatcher Servlet은 이 URL 주소와 HTTP 메서드(GET, POST 등)를 처리할 컨트롤러가 누구인지를 찾기 위해 **Handler Mapping**에 조회를 요청
3. **Handler Adapter:** 찾은 Handler(컨트롤러)를 실행해 줄 수 있는 **Handler Adapter**를 찾음
4. **컨트롤러 호출:** 어댑터가 실제 **RestController**를 호출
5. **서비스 및 리포지토리 실행:** **Service** 레이어에서 핵심 로직을 수행하고, 필요하다면 **Repository**를 통해 **Database**에서 데이터를 가져오거나 저장
6. **ResponseEntity 생성:** 로직 처리가 완료되면 결과 데이터와 HTTP 상태 코드(예: 200 OK)를 담은 **ResponseEntity** 객체를 생성하여 반환
7. **결과 전달:** 컨트롤러가 반환한 결과는 다시 Handler Adapter를 거쳐 **Dispatcher Servlet**으로 전달(JSON 형식)
8. **최종 응답:** Dispatcher Servlet은 최종적으로 가공된 응답 데이터를 클라이언트에게 전송