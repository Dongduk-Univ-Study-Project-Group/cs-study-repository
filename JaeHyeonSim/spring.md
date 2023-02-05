
<details><summary>프론트 컨트롤러 패턴이란 무엇인가요?</summary>
<p>

```html
- ksundong

클라이언트의 다양한 요청마다 서블릿을 만들어서 사용한다고 하면 개발과 유지보수의 효율이 떨어질 수 밖에 없습니다.
프론트 컨트롤러 패턴을 사용함으로써 각 요청을 적절한 곳으로 위임해줌으로써 개발과 유지보수의 효율성이 증가하고
모든 요청에 대해 보안, 국제화, 라우팅 및 로그와 같은 일반적인 기능을 한 곳에서 캡슐화할 수 있습니다.
Spring에서는 DispatcherServlet이 프론트 컨트롤러 패턴을 사용한 예이며,
DispatcherServlet이 Bean으로 등록되어 package를 scan하고 @Controller, @RestController 애노테이션을 확인하여 어떠한 요청이 들어왔을 때 적절한 Handler Method에 위임해줍니다.
```

**프런트 컨트롤러 패턴 (Front Controller Pattern)**

: 디자인 패턴(Design Pattern) 중 하나로,

모든 요청을 프런트 컨트롤러가 받아, 그 후 담당하는 컨트롤러에 적절하게 할당

- 스프링 MVC의 구성 요소

| 객체 | 기능 개요 |
| --- | --- |
| DispatcherServlet | 모든 요청을 수신하는 프런트 컨트롤러 |
| Model | 컨트롤러에서 뷰에 넘겨주는 표시용 데이터 등을 저장하는 객체
(HttpServletRequest나 HttpSession과 같은 기능 제공) |
| View | 화면 표시 처리(ex - JSP 등) |
| Controller | 요청에 대응해서 처리할 내용이 있는 곳 |
| 서비스 처리 | 데이터베이스에 접속해서 데이터를 취득하거나 데이터를 가공하는 등 여러 가지 작업을 실행
개발자가 설계하고 구현(스프링 MVC과 관계 없음) |

- 스프링 MVC에서 요청을 받고 응답을 보낼 때까지의 흐름
    1. 클라이언트로부터 DispatcherServlet이 요청을 수신
    2. DispatcherServlet이 요청 핸들러 메서드 호출
    3. Controller는 비즈니스 로직 처리를 호출하고 처리 결과를 받음
    4. 처리 결과를 Model로 설정하고 View 이름을 반환
    5. 반환된 View 이름을 받아 DispatcherServlet이 View 이름에 대응하는 View에 화면 표시 처리 의뢰
    6. 클라이언트가 응답을 받고 브라우저에 화면이 표시

.

</details>


<details><summary>POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?</summary>
<p>

```html
- ksundong

POJO는 프레임워크 인터페이스, 클래스를 구현하거나 확장하지 않은 단순한 클래스로 Java에서 제공하는 API 외에 종속되지 않습니다.
특정 환경에 종속되지 않아 코드가 간결하고 테스트 자동화에 유리합니다.
스프링에서는 도메인과 비즈니스 로직을 수행하는 대상이 POJO대상이 될 수 있습니다.
```

**POJO (Plain Old Java Object)**

: 어떤 클래스를 상속하는 등의 특별한 처리를 하지 않는 보통의 자바 객체

1. 특정 환경에 종속되지 않음
2. 특정 규약에 종속되지 않음
3. 객체지향적 원리에 충실해야 함

- 스프링에서의 POJO
    
    도메인과 비즈니스 로직을 수행하는 대상
    
    스프링의 주요 기술 IoC/DI, AOP, PSA
    

- 참고 자료
    
    [https://doing7.tistory.com/81](https://doing7.tistory.com/81)
    
    : DOing - [Spring] POJO란?

.

</details>

<details><summary>스프링 기초 ('스프링 프레임워크 첫걸음' 3-6장 정리)</summary>
<p>

## 03장 스프링 프레임워크의 핵심 기능 알아보기

### 3-1 스프링 프레임워크의 핵심 기능

1. **의존성 주입** (Dependency Injection, **DI**)
    
    : 의존하는 부분을 외부에서 주입하는 것
    
2. **관점 지향 프로그래밍** (Aspect Oriented Programming, **AOP**)
    
    : ‘횡단적 관심사’를 추출하고 프로그램의 여러 곳에서 호출할 수 있게 설정함으로써
    
    개발자는 실현해야 할 기능인 ‘중심적 관심사’에만 집중해서 작성하면 되는 구조
    
    - 중심적 관심사(Primary Concern) : 실현해야 할 기능을 나타내는 프로그램
    - 횡단적 관심사(Crosscutting-Concerns) : 본질적인 기능은 아니지만 품질이나 유지보수 등의 관점에서 반드시 필요한 기능을 나타내는 프로그램

### 3-2 DI 컨테이너 알아보기

**의존성(Defendency)**

: A 클래스에서 B클래스를 사용하려면 new 키워드를 이용해 B 클래스의 인스턴스를 생성하고 B 클래스의 메서드 사용 가능

이때 B 클래스의 메서드를 변경하면 A클래스에서도 해당 메서드를 변경해야 한다.

이런 관계를 ‘A클래스는 B 클래스에 의존한다’ 라고 한다.

의존의 유형 2가지

- 클래스 의존(구현 의존)
- 인터페이스 의존

**클래스 의존**

ex) A 클래스에서 B 클래스의 methodX 메서드를 호출하는 경우

설계가 변경되어 B 클래스를 C 클래스로 변경하고 methodY를 호출하도록 변경

```java
// class A

xxx() {
	B b = new B();
	b.methodX();
}

변경 ↓↓↓

xxx() {
	C c = new C();
	c.methodY();
}
```

수정할 부분이 많아 실수가 발생할 확률이 높다.

**인터페이스 의존**

ex) I 인터페이스가 있고 그것을 구현한 B 클래스

A 클래스에서 B 클래스의 methodX 메서드를 호출하는 경우

(주의 - A 클래스에서는 인터페이스로 추상화된 I를 이용)

설계가 변경되어 B 클래스를 C 클래스로 변경하고 methodY를 호출하도록 변경

```java
// class A

xxx() {
	I i = new B();
	i.methodX();
}

변경 ↓↓↓

xxx() {
	I i = new C();
	i.methodY();
}
```

한 곳만 수정하면 된다.

<aside>
💡 클래스 의존보다는 인터페이스 의존을 사용하면 좋다

</aside>

### 3-3 어노테이션 역할 알아보기

**어노테이션 (annotation)**

: 주석을 의미하는 영어 표현

1. ‘@xx’ 와 같은 형태로 작성
2. 소스코드에서 외부 소프트웨어에 필요한 처리 내용 전달

```java
// (소스 파일 -> 외부 소프트웨어)
@Override  ->  자바 컴파일러      // 오버라이드 메서드의 시그니처를 체크
@Author    ->  Javadoc           // 도움말 문서 생성
@Component ->  스프링 프레임워크  // 인스턴스 생성
@NotEmpty  ->  Validator         // 입력란 체크
@Test      ->  JUnit             // 테스트 실행
```

- 레이어별로 사용할 인스턴스 생성 어노테이션
    
    ‘도메인 주도 설계(Domain-Driven Design)’의 레이어
    
    | 레이어 | 개요 | 어노테이션 |
    | --- | --- | --- |
    | 애플리케이션 레이어
    (Application Layer) | 클라이언트와의 데이터 입출력 제어 | @Controller |
    | 도메인 레이어
    (Domain Layer) | 업무 처리 수행 | @Service |
    | 인프라 레이어
    (Infrastructure Layer) | 데이터베이스에 대한 데이터 영속성 등을 담당 | @Repository |
    |  |  | @Component |
    
    Client → Application Layer → Domain Layer → Infrastructure Layer → Database
    

### 3-4 AOP(관점 지향 프로그래밍)의 기초 지식

**AOP** (Aspect Oriented Programming)

1. AOP에서는 프로그램을 중심적 관심사와 횡단적 관심사 2개 요소로 구성되어 있다고 생각
2. 중심적 관심사는 구현해야 할 기능을 나타내는 비즈니스 로직
3. 횡단적 관심사는 본질적인 기능은 아니지만 품질이나 유지보수 등의 관점에서 반드시 필요한 기능을 나타내는 부수적 프로그램
4. AOP에서는 횡단적 관심사를 분리함으로써 기존 코드를 수정하지 않아도 프로그램 중에 특정 기능(공통 처리) 추가 가능
5. 스프링 프레임워크는 다양한 공통 기능을 AOP에서 제공

- AOP 용어
    
    
    | 용어 | 내용 |
    | --- | --- |
    | 어드바이스
    (Advice) | 횡단적 관심사의 구현(= 메서드)
    로그 출력 및 트랙잭션 제어 |
    | 애스팩트
    (Aspect) | 어드바이스를 정리한 것(= 클래스) |
    | 조인포인트
    (JoinPoint) | 어드바이스를 중심적인 관심사에 적용하는 타이밍
    메서드(생성자) 실행 전, 메서드(생성자) 실행 후 등 실행되는 타이밍 |
    | 포인트컷
    (Pointcut) | 어드바이스를 삽입할 수 있는 위치
    예를 들어, 메서드 이름이 get으로 시작할 때만 처리하는 조건을 정의 가능 |
    | 인터셉터
    (Interceptor) | 처리의 제어를 인터셉트하기 위한 구조 또는 프로그램
    스프링 프로그램에서는 인터셉트라는 매커니즘으로 어드바이스를 중심 관심사에 추가한 것처럼 보이게 함 |
    | 타깃
    (Target) | 어드바이스가 도입되는 대상 |

- 어드바이스의 종류
    
    
    | 어드바이스 | 내용 | 어노테이션 |
    | --- | --- | --- |
    | Before Advice | 중심적 관심사가 실행되기 이전에 횡단적 관심사 실행 | @Before |
    | After Returning Advice | 중심적 관심사가 정상적으로 종료된 후 횡단적 관심사 실행 | @AfterReturning |
    | After Throwing Advice | 중심적 관심사로부터 예외가 던져진 후 횡단적 관심사 실행 | @AfterThrowing |
    | After Advice | 중심적 관심사의 실행 후  횡단적 관심사 실행(결과와 상관없이 진행) | @After |
    | Around Advice | 중앙적 관심사 호출 전후에 횡단적 관심사 실행 | @Around |

- 와일드카드
    
    
    | 와일드카드 | 내용 |
    | --- | --- |
    | *
    (애스터리스크) | 임의의 문자열
    패키지를 나타낼 때는 임의의 패키지 한 계층을 나타냄
    메서드의 인수에서는 한 개의 인수를 나타내 반환값으로도 이용 가능 |
    | ..
    (점 두 개) | 패키지를 나타내는 경우 0개 이상의 패키지를 나타냄
    메서드의 인수를 표현하는 경우 0개 이상의 임의의 인수를 나타냄 |
    | +
    (플러스) | 클래스명 뒤에 기술해 클래스와 그 서브 클래스 및 구현 클래스 모두를 나타냄 |

+ 메타 어노테이션(Meta Annotation)

: 커스텀 어노테이션에 정의를 추가하는 어노테이션

@Target, @Retention, @Documented, @Inherited

### 3-5 Spring Initializr 알아보기

**Spring Initializr**

: 스프링 부트에서 프로젝트를 시작할 때 통합 개발 환경(IDE, eclipse 등)에 의존하지 않는 방법을 원할 경우 사용

예를 들어 Spring Initializr에서 프로젝트를 만들고 eclipse에서 해당 프로젝트 가져오기 가능

---

## 04장 데이터베이스 작업

### 4-1 데이터베이스 생성

**데이터베이스** (Database, **DB**)

: 데이터를 보관하기 위한 상자, 규칙을 가지고 데이터 정리

**관계형 데이터베이스** (Relational Database, **RDB**)

: 데이터를 표 형식으로 표현하고, 여러 표에서 항목의 값 사이에 관계를 맺고 있는 데이터베이스

가장 일반적으로 사용

### 4-2 테이블 생성

**테이블(Table)**

: 데이터베이스 안에서 실제로 규칙을 가진 데이터가 저장되는 상자

**레코드(Record)**

: 테이블의 가로 행(row)

**칼럼(Column)**

: 테이블의 세로 열(column)

- 제약 조건
    
    테이블에 존재하는 데이터가 불일치 상태가 되지 않게 하는 규칙
    
    | 제약 조건 | 개요 |
    | --- | --- |
    | NOT NULL | NULL 입력을 허용하지 않음(필수 입력) |
    | UNIQUE | 중복값 입력을 허용하지 않음(고유한 값) |
    | CHECK | 지정한 조건을 만족하지 않는 값의 입력을 허용하지 않음 |
    | PRIMARY KEY | 테이블 안에서 레코드를 식별하는 기본키를 설정
    기본키는 NOT NULL과 UNIQUE가 함께 적용 |
    | FORIGN KEY | 관련된 테이블을 연결하는 설정(외부 키) |
    | DEFAULT | 칼럼의 초깃값을 설정 |

### 4-3 데이터 입력

**SQL (Structured Query Language)**

: 데이터베이스를 조작하기 위한 언어(구조화 질의어)

ANSI(American National Standard Institute)와 ISO(국제 표준화 기구)에서 사양이 표준화되어 있어 다른 데이터베이스에서도 거의 같은 방법으로 조작 가능

**CRUD**

: 영속적으로 데이터를 취급하는 4개의 기본적인 기능인

생성(Create), 읽기(Read), 갱신(Update), 삭제(Delete)

- SQL의 CRUD
    
    
    | CRUD | 명령어 | 개요 |
    | --- | --- | --- |
    | 생성(Create) | INSERT | 데이터를 등록 |
    | 읽기(Read) | SELECT | 데이터를 참조 |
    | 갱신(Update) | UPDATE | 데이터를 갱신 |
    | 삭제(Delete) | DELETE | 데이터를 삭제 |

- PostgreSQL의 CRUD
    
    
    | CRUD | 구문 |
    | --- | --- |
    | 생성(Create) | INSERT INTO 테이블명 (칼럼명, 칼럼명, …) VALUES(값, 값, …); |
    | 읽기(Read) | SELECT 칼럼명 FROM 테이블명; |
    | 갱신(Update) | UPDATE 테이블명 SET 칼럼명 = 값 WHERE 갱신할_레코드를_특정하는_조건;
    ※ WHERE로 조건을 지정하지 않는 경우 모든 레코드가 대상 |
    | 삭제(Delete) | DELETE FROM 테이블명 WHERE 삭제할_레코드를_특정하는_조건;
    ※ WHERE로 조건을 지정하지 않는 경우 모든 레코드가 대상 |

### 4-4 엔티티와 리포지토리 알아보기

**엔티티 (Entity)**

: 데이터를 담아두는 객체

데이터베이스 테이블의 한 행(레코드)에 대응하는 객체, 엔티티 필드 = 테이블 칼럼

```java
/**
	* Member 테이블: 엔티티
	*/

public class Member {
	/** id 칼럼 대응 */
	private Integer id;

	public Integer getId() {
		return id;
	}
	public void setId(Integer id) {
		this.id = id;
	}

}
```

**리포지토리 (Repository)**

: 데이터베이스를 조작하는 클래스

리포지토리 생성 시 반드시 인터페이스를 정의하고 구현 (리포지토리 인터페이스의 필드에 리포지토리 구현 클래스를 DI하여 특정 구현에 의존하는 것을 피할 수 있음)

### 4-5 스프링 데이터 JDBC 사용해보기

**O/R 매퍼 (Object-relational Mapper)**

: 어플리케이션에서 사용하는

O(Object): ‘객체’와

R(Relational): ‘관계형 데이터베이스’

의 데이터를 매핑하는 것

미리 설정된 객체나 관계형 데이터베이스 간의 대응 관계 정보를 가지고 인터페이스의 데이터에 대응하는 테이블에 내보내거나, 데이터베이스에서 값을 읽어 들여 인터페이스에 대입하는 작업을 자동으로 실행

**스프링 데이터 JDBC**

: O/R 매퍼

스프링 데이터가 제공하는 CrudRepository를 상속해서 자동으로 CRUD를 지원하는 메서드를 사용 가능

- 추가해야 할 의존성
    - Spring Boot DevTools(개발 도구)
    - Lombok(개발 도구)
    - Spring Data JDBC(SQL)
    - PostgreSQL Driver(SQL)

- application.properties 설정 항목
    
    
    | 항목 | 설명 |
    | --- | --- |
    | spring.datasource.driver-class-name | JDBC 드라이버의 클래스명을 지정
    여기서는 PostgreSQL의 드라이버를 설정 |
    | spring.datasource.url | 데이터베이스의 ‘접속 URL’을 설정 |
    | spring.datasource.username | 데이터베이스에 접속하는 ‘유저명’을 설정 |
    | spring.datasource.password | 데이터베이스에 접속하는 ‘패스워드’를 설정 |

---

## 05장 MVC 모델 알아보기

### 5-1 MVC 모델 알아보기

**MVC 모델**

: 프로그램의 처리 역할을 나누어서 프로그램을 작성하는 방법

Model, View, Controller의 세 역할로 분류

**모델 (Model, M)**

: 시스템에서 비즈니스 로직(Business Logic)을 담당

시스템의 코어, 목적을 처리하는 부분

**뷰 (View, V)**

: 시스템에서 표현 부분을 담당

 웹 애플리케이션에서느 외형, 사용자 입력과 결과 출력 등 주로 화면을 담당

**컨트롤러 (Controller, C)**

: 서비스 처리를 담당하는 모델과 화면 표시를 담당하는 뷰를 제어하는 역할

사용자가 입력한 내용을 뷰에서 받고, 받은 데이터를 기준으로 모델에 내용을 전달, 또는 모델에서 받은 데이터를 뷰에 전달해서 화면에 표시하는 역할

- MVC 모델의 이점
    1. 역할 분담을 통해 효율적인 개발 가능
    2. 개발하는 엔지니어의 분업화가 용이
    3. 설계 변경에 유연하게 대응 가능

### 5-2 스프링 MVC 알아보기

**스프링 MVC**

: 웹 애플리케이션을 간단하게 만들 수 있는 기능을 제공하는 프레임워크

**프런트 컨트롤러 패턴 (Front Controller Pattern)**

: 디자인 패턴(Design Pattern) 중 하나로,

모든 요청을 프런트 컨트롤러가 받아, 그 후 담당하는 컨트롤러에 적절하게 할당

- 스프링 MVC의 구성 요소

| 객체 | 기능 개요 |
| --- | --- |
| DispatcherServlet | 모든 요청을 수신하는 프런트 컨트롤러 |
| Model | 컨트롤러에서 뷰에 넘겨주는 표시용 데이터 등을 저장하는 객체
(HttpServletRequest나 HttpSession과 같은 기능 제공) |
| View | 화면 표시 처리(ex - JSP 등) |
| Controller | 요청에 대응해서 처리할 내용이 있는 곳 |
| 서비스 처리 | 데이터베이스에 접속해서 데이터를 취득하거나 데이터를 가공하는 등 여러 가지 작업을 실행
개발자가 설계하고 구현(스프링 MVC과 관계 없음) |

- 스프링 MVC에서 요청을 받고 응답을 보낼 때까지의 흐름
    1. 클라이언트로부터 DispatcherServlet이 요청을 수신
    2. DispatcherServlet이 요청 핸들러 메서드 호출
    3. Controller는 비즈니스 로직 처리를 호출하고 처리 결과를 받음
    4. 처리 결과를 Model로 설정하고 View 이름을 반환
    5. 반환된 View 이름을 받아 DispatcherServlet이 View 이름에 대응하는 View에 화면 표시 처리 의뢰
    6. 클라이언트가 응답을 받고 브라우저에 화면이 표시

### 5-3 스프링 MVC 사용해보기

**POJO (Plain Old Java Object)**

: 어떤 클래스를 상속하는 등의 특별한 처리를 하지 않는 보통의 자바 객체

- @RequestMapping의 속성
    
    
    | 속성 | 기능 개요 |
    | --- | --- |
    | value | - 매핑할 URL 경로(path)를 지정
    - value는 처음의 / 생략 가능
    - URL 경로만 지정하는 경우에는 속성에서 value를 생략 가능
    - URL 경로는 여러 개 지정 가능 |
    | method | - GET과 POST 등의 HTTP 메서드 지정
    - GET을 지정하는 경우에는 RequestMethod.GET 사용
    - POST를 사용하는 경우에는 RequestMethod.POST 사용
    - HTTP 메서드 여러 개 지정 가능
    - 클래스에 @RequestMapping을 부여하는 경우 지정 불가 |

- 스프링 부트에서의 URL 표기
    
    일반적으로 URL은
    
    http://<서버 이름>(:포트 번호)/<컨텍스트 패스>/<매핑 URL>
    
    형식으로 애플리케이션에 액세스하지만 스프링 부트에서는 기본적으로 컨텍스트 패스(애플리케이션 이름)이 생략됨
    

- 뷰 생성 규칙
    
    스프링 부트의 프로젝트에서 템플릿 엔진을 사용하는 경우 뷰를 두는 곳이 지정됨
    
    - resorces/templates 폴더 밑에 뷰 생성
    - 뷰가 많이 필요한 경우 기능별로 폴더를 만들어서 보관
    - 폴더를 나눈 경우는 templates 폴더 이하의 폴더명을 요청 핸들러 메서드의 반환값에 지정
    - CSS나 자바스크립트 등은 resources/static 폴더에 배치

---

## 06장 템플릿 엔진 알아보기

### 6-1 템플릿 엔진 개요

**템플릿 엔진**

: 데이터를 미리 정의된 템플릿에 바인딩해서 뷰의 표시를 도와주는 것

**타임리프 (Thymeleaf)**

: 데이터와 미리 정의한 템플릿을 바인딩해서 뷰에 표시할 때 도움을 주는 HTML 기반의 템플릿 엔진

1. 정해진 문법으로 작성하면 페이지를 동적으로 조립해줌(조건 분기나 반복 구문 등 사용 가능)
2. 최종 출력을 생각하면서 뷰 생성 가능(디자이너와 쉽게 분업)

- 스프링 MVC 구조에서의 요청-응답 흐름
    1. DispatcherServlet이 클라이언트에게 요청을 받음(프런트 컨트롤러 패턴)
    2. DispatcherServlet이 컨트롤러의 요청 핸들러 메서드 호출
    3. 컨트롤러는 비즈니스 로직 처리를 실행하여 처리 결과 취득
    4. 처리 결과를 Model로 설정하고 뷰 이름 반환
    5. DispatcherServlet은 뷰 이름에 대응하는 뷰에 대해서 화면 표시 처리를 의뢰
    6. 클라이언트가 응답을 받고 브라우저에 화면 표시

### 6-2 Model 인터페이스의 사용법

**Model 인터페이스**

1. 처리한 데이터를 뷰에 표시하고 싶을 경우 데이터를 전달하는 역할
2. 스프링 MVC에 의해 관리되며, 수동 또는 자동으로 객체를 저장하고 관리하는 기능 제공
3. Model을 이용하고 싶은 경우 요청 핸들러 메서드의 인수에 Model 타입을 전달
    
    → 스프링 MVC가 자동으로 Model 타입 인스턴스를 제공
    

- 중요 메서드
    
    addAttribute : 특정 이름에 대해 값을 설정
    
    ```java
    Model addAttribute(String name, Object value)
    ```
    
    저장하고 싶은 값에 별명을 붙이고, 뷰에서는 별명 사용
    
    | name | 이름(별명) |
    | --- | --- |
    | value | 값(저장하고 싶은 객체) |

> **새니타이즈(Sanitize)**
- 위험한 코드나 데이터를 변환 또는 제거하여 무력화하는 것
> 

### 6-3 타임리프 사용법

- 타임리프의 특징 3가지
    1. 스프링 부트에서 추천하는 템플릿 엔진
    2. HTML로 템플릿을 작성하기 때문에 웹브라우저로 파일의 내용을 표시하고 확인하면서 뷰 생성 가능
    3. 스프링 부트의 기본 설정으로 src/main/resources/templates 폴더 아래에
        
        ‘ 요청 핸들러 메서드 반환값  + .html ’ 파일이 참조됨
        

- 타임리프 사용법
    
    직접 문자를 삽입
    
    ```html
    <h1 th:text="'hello world'">표시하는 부분</h1>
    ```
    
    인라인 처리
    
    ```html
    <h1>안녕하세요! [[${name}]]씨</h1>
    ```
    
    값 결합
    
    ```html
    <h1 th:text="'오늘의 날씨는' + '맑음' + '입니다'">표시하는 부분</h1>
    ```
    
    값 결합(리터럴 치환)
    
    ```html
    <h1 th:text="|안녕하세요 ${name}씨|">표시하는 부분</h1>
    ```
    
    지역 변수
    
    ```html
    <div th:with="a=1,b=2">
    	<span th:text="|${a} + ${b} = ${a+b}|"></span>
    </div>
    ```
    
    비교와 등가
    
    ```html
    <span th:text="1 > 10"></span>
    <span th:text="1 < 10"></span>
    <span th:text="1 >= 10"></span>
    <span th:text="1 <= 10"></span>
    <span th:text="1 == 10"></span>
    <span th:text="1 != 10"></span>
    <span th:text="길동 == 길동"></span>
    <span th:text="길동 != 길동"></span>
    ```
    
    조건 연산자
    
    ```html
    <p th:text="${name} == '길동'? '길동입니다!':'길동이가 아닙니다"></p>
    ```
    
    조건 분기(true)
    
    ```html
    <div if="${name} == '길동'">
    	<p>길동 씨입니다!</p>
    </div>
    ```
    
    조건 분기(false)
    
    ```html
    <div unless="${name} == '영희'">
    	<p>영희 씨가 아닙니다</p>
    </div>
    ```
    
    switch
    
    ```html
    <div th:switch="${name}">
    	<p th:case="길동" th:text="|${name}입니다!|"></p>
    	<p th:case="영희" th:text="|${name}입니다!|"></p>
    	<p th:case="철수" th:text="|${name}입니다!|"></p>
    	<p th:case="*">명부에 없습니다</p>
    </div>
    ```
    
    참조(데이터를 결합한 객체)
    
    ```html
    <p th:text="${mb.id}">ID</p>
    <p th:text="${mb.name}">이름</p>
    <p th:text="${mb['id']}">ID: []로 접근</p>
    <p th:text="${mb['name']}">이름: []로 접근</p>
    ```
    
    참조(th:object)
    
    ```html
    <div th:object="${mb}">
    	<p th:text="*{id}">ID</p>
    	<p th:text="*{name}">이름</p>
    	<p th:text="*{['id']}">ID: []로 접근</p>
    	<p th:text="*{['name']}">이름: []로 접근</p>
    </div>
    ```
    
    참조(List)
    
    ```html
    <p th:text="${list[0]}">방위</p>
    <p th:text="${list[1]}">방위</p>
    <p th:text="${list[2]}">방위</p>
    <p th:text="${list[3]}">방위</p>
    ```
    
    참조(Map)
    
    ```html
    <p th:text="${map.kim.name}">이름 1</p>
    <p th:text="${map.lee.name}">이름 2</p>
    <p th:text="${map['kim']['name']}">이름 1 : []로 접근</p>
    <p th:text="${map['lee']['name']}">이름 2 : []로 접근</p>
    ```
    
    반복
    
    ```html
    <div th:each="member : ${members}">
    	<p>[[${member.id}] : [${member.name}]]</p>
    </div>
    ```
    
    반복 상태
    
    ```html
    <div th:each="member, s : ${members}" th:object="${member}">
    	<p>
    		index-> [[${s.index}]], count-> [[${s.count}]],
    		size-> [[${s.size}]], current-> [[${s.current}]],
    		even-> [[${s.even}]], odd-> [[${s.odd}]],
    		first-> [[${s.first}]], last-> [[${s.last}]],
    		[[*{id}]] : [[*{name}]]
    	</p>
    </div>
    ```
    
    유틸리티 객체
    
    | 유틸리티 객체 | 기능 개요 |
    | --- | --- |
    | #strings | 문자 관련 편의 기능 |
    | #numbers | 숫자 서식 지원 |
    | #bools | 불리언(Boolean) 관련 기능 |
    | #dates | java.util.Date 서식 지원 |
    | #objects | 객체 관련 기능 |
    | #arrays | 배열 관련 기능 |
    | #lists | LIst 관련 기능 |
    | #sets | Set 관련 기능 |
    | #maps | Map 관련 기능 |
    
    다른 템플릿 삽입하기
    
    프래그먼트(fragment) = 단편
    
    프래그먼트화
    
    : 여러 템플릿에서 같은 내용이 사용되는 경우 공통 내용을 별개의 파일로 만들고 필요한 부분에 추가하는 것
    
    레이아웃
    
    레이아웃화
    
    : 여러 템플릿에서 같은 디자인 레이아웃을 사용하는 경우 공통 레이아웃을 만들고 공유하는 것
    
    전용 라이브러리인 thymeleaf-layout-dialect 필요(단점 - 전체 화면 타임리프의 변환 처리 후 확인 가능)
    

### 6-4 타임리프를 사용해서 프로그램 만들기

- 타임리프의 장점
    1. HTML 태그에 th:XX를 포함하여 HTML 파일을 그대로 자바에서 사용 가능
    2. HTML 파일에 영향을 주지 않고 개발할 수 있어 디자이너와의 업무 분장이 쉬움

.

</details>