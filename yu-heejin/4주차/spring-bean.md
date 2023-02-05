> 객체 생성 → 의존 설정 → 초기화 → 사용 → 소멸 과정의 생명주기를 가지고 있습니다. Bean은 스프링 컨테이너에 의해 생명주기를 관리하며 빈 초기화방법은 @PostConstruct 를 빈 소멸에서는 @PreDestroy 를 사용합니다.
> 

---

## Spring Bean이란?

- Spring IoC 컨테이너가 관리하는 자바 객체
- 컨테이너에 의해 생명 주기가 관리되는 객체를 의미한다.
- 스프링 컨테이너에 의해 관리되는 자바 객체(POJO)
- IoC 컨테이너 안에 들어있는 객체로, 필요할 때마다 IoC 컨테이너에서 가져와 사용한다.
- @Bean 어노테이션을 사용하거나 xml 설정을 통해 일반 객체를 Bean으로 등록할 수 있다.
- 즉, Spring에서는 Bean은 ApplicationContext가 알고 있는 객체이며, ApplicationContext가 생성하고 직접 관리해주는 객체를 의미한다.

## Spring Container

- 스프링 컨테이너는 스프링 빈의 생명 주기를 관리하며, 생성된 스프링 빈들에게 추가적인 기능을 제공하는 역할을 한다.
- IoC와 DI의 원리가 스프링 컨테이너에 적용된다.
- 개발자는 new, 인터페이스 호출, 팩토리 호출 방식으로 객체를 생성하고 소멸하지만, 스프링 컨테이너를 사용하면 해당 역할을 대신 해준다.
    - 즉, 제어 흐름을 외부에서 관리하게 된다.
- 객체들 간의 의존 관계를 스프링 컨테이너가 런타임 과정에서 알아서 만들어준다.

## Spring Bean 등록 방법

### 컴포넌트 스캔

- Bean을 등록하는 첫번째 방법은 스프링에서 제공하는 **@Component 어노테이션**으로 클래스를 명시하여 컨테이너가 생성될 때 컴포넌트 스캔을 통해 자동으로 빈에 등록할 수 있다.
- @Controller, @Service, @Repository, @Configuration 어노테이션들은 @Component로 구성되어 있어 컴포넌트 스캔에 이용할 수 있다.
    - @Controller
        - 스프링 **MVC 컨트롤러**로 인식된다.
    - @Repository
        - 스프링 **데이터 접근 계층으로 인식**하고 해당 계층에서 발생하는 예외는 모두 DataAccessException으로 변환한다.
    - @Service
        - 특별한 처리는 하지 않으나, 개발자들이 핵심 비즈니스 계층을 인식하는데 도움을 준다.
    - @Configuration
        - 스프링 설정 정보로 인식하고 스프링 빈이 싱글톤을 유지하도록 추가 처리를 한다.
        - 단, 스프링 빈 scope가 싱글톤이 아니라면 추가 처리를 하지 않는다.
    - 이들 중 @Repository 에 접근해보면, 다음과 같이 컴포넌트의 특별한 형태로 제공됨을 알 수 있다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b1ddbc2a-054d-436d-9451-9406a395f74d/Untitled.png)
        
    - @Component 와 연관된 어노테이션들을 이용하여 클래스를 명시해주면, 스프링 컨테이너는 컴포넌트 스캔을 통해 자동으로 해당 클래스의 객체를 Bean으로 관리한다.
- 이때, Bean으로 등록된 모든 클래스의 객체들은 싱글톤(Singleton)으로 생성된다.

### 직접 Spring Bean 등록하기

- 컴포넌트 어노테이션을 사용하지 않고 직접 Bean으로 등록할 클래스들을 자바 코드로 정의하는 것도 가능하다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a29f2e12-b90e-487c-9336-12076f4b6a69/Untitled.png)
    
    - Configuration을 위한 클래스를 하나 만든 후, @Configuration으로 명시하면 된다.
    - 그 후 Bean으로 등록할 클래스를 @Bean 메소드로 생성하여 객체를 리턴하도록 한다.
    - 빈 등록을 위해 인스턴스를 생성하는 메소드 위에 명시해야한다.
    - @Bean은 메소드나 어노테이션에만 붙일 수 있으며 클래스에는 붙일 수 없다.
- 직접 Spring Bean을 등록하여 얻을 수 있는 장점은 **인터페이스로 구현된 Repository 클래스가 다른 클래스로 변경될 때 간단하게 Configuration의 리턴 클래스 객체만을 수정해주면 된다는 점이다.**

## 의존 관계 설정

- Controller, Service, Repository의 경우, 스프링 빈을 등록한다고 해서 끝나는 것은 아니고, **싱글톤 객체로 생성되어 관리되는 클래스들의 의존 관계를 연결해주어야 한다.**

### 자동 의존 관계

- 컴포넌트 스캔을 이용해 스프링 빈을 등록했을 경우, 클래스의 생성자에 @Autowired 어노테이션을 명시해주면 된다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/739a3566-6356-49c1-8891-542051197786/Untitled.png)
    

### 수동 의존 관계

- 컴포넌트 어노테이션을 이용하지 않고 Configuration을 통해 직접 빈을 등록한 경우, 새롭게 추가할 것은 없고 **실제 클래스의 구현된 생성자의 형태와 동일하게 Configuration에서도 객체를 리턴해주면 된다.**
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bac11f93-c6e3-4418-9f38-ff1aecbc112c/Untitled.png)
    

## XML 기반의 Bean 정의 방법

```java
<!-- 간단한 빈 정의 -->
<bean id="..." class="..."></bean>

<!-- scope와 함께 빈 정의 -->
<bean id="..." class="..." scope="singleton"></bean>

<!-- property와 함께 빈 정의 -->
<bean id="..." class="...">
	<property name="beaninit" value="Hello World!"/>
</bean>

<!-- 초기와 메소드와 함께 빈 정의 -->
<bean id="..." class="..." init-method="..."></bean>
```

## Spring Bean의 생명 주기

```java
// 생성 관련한 인터페이스
public interface InitializingBean { 
	void afterPropertiesSet() throws Exception;
}

// 소멸 관련한 인터페이스
public interface DispoasableBean { 
	void destroy() throws Exception;
}

public class Test implements **InitializingBean, DisposableBean** {

    @Override
    public void afterPropertiesSet() throws Exception {
    	//빈 생성후 메소드 호출
        System.out.println("afterPropertiesSet() 실행");
    }
    
    @Override
    public void destroy() throws Exception {
    	// 소멸을 진행하는 메소드
        System.out.println("destroy() 실행");
    }
   
    
}
```

- **객체 생성 → 의존 설정 → 초기화 → 사용 → 소멸 과정**의 생명 주기를 가지고 있다.
- **Bean은 스프링 컨테이너에 의해 생명 주기를 관리**한다.
- 스프링 컨테이너가 초기화 될 때 **먼저 빈 객체를 설정에 맞춰 생성**하며, **의존 관계를 설정**한 뒤 해당 프로세스가 완료되면 **빈 객체가 지정한 메소드를 호출해서 초기화를 진행**한다.
- 객체를 사용해 **컨테이너가 종료될 때 Bean이 지정한 메소드를 호출해 소멸 단계를 거친다.**
- **스프링은 InitializingBean 인터페이스와 DisposableBean을 제공**하며 **Bean 객체의 클래스가 InitializingBean Interface 또는 DisposableBean을 구현**하고 있으며, **해당 인터페이스에서 정의된 메소드를 호출**해 빈 객체의 초기화 또는 종료를 수행한다.
- 어노테이션을 이용한 Bean 초기화 방법에는 @PostConstruct와 Bean 소멸에는 @PreDestroy를 사용한다.

### Bean 객체의 생명 주기

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ed3cd282-a05e-4bd4-a3f1-0f721b3840b5/Untitled.png)

1. Spring 컨테이너를 초기화 할 때, 가장 먼저 Bean 객체를 생성한다.
2. Bean 객체 생성 후 property 태그로 지정한 의존성을 설정한다.
    1. 의존 주입도 이 단계에서 수행된다.
3. 모든 의존 설정이 완료되면 빈 객체를 초기화한다.
    1. 빈 객체를 초기화하기 위해 빈 객체의 지정한 메서드를 호출한다.
4. 스프링 컨테이너를 종료하면, 스프링 컨테이너는 빈 객체를 소멸시킨다.
    1. 빈 객체의 소멸을 처리하기 위해 빈 객체의 지정한 메서드를 호출한다.

## Spring Bean의 범위

- Bean Scope는 기본적이로 Bean이 존재하는 범위를 뜻한다.
- Bean의 객체는 기본적으로 singleton의 범위를 가지며, singleton은 스프링 컨테이너의 시작과 종료까지 단 하나의 객체만을 사용하는 방식이다.
- request, session, global session의 scope는 일반 spring 어플리케이션이 아니라 Spring MVC Web Application에서만 사용된다.
- Bean 의 **객체 범위를 prototype으로 설정하면 객체를 매번 새롭게 생성한다는 특징**이 있으며, prototype으로 설정하면 @Scope 어노테이션을 @Bean 어노테이션과 함께 사용해야 한다.

| Scope | 설명 |
| --- | --- |
| singleton | 하나의 Bean 정의에 대해 Spring IoC Container에서 단 하나의 객체만 존재한다. |
| prototype | 하나의 Bean 정의에 대해 다수의 객체가 존재할 수 있다. |
| request | 하나의 Bean 정의에 대해 하나의 HTTP request 생명주기 안에 단 하나의 객체만 존재한다. 각각의 HTTP request는 자신만의 객체를 가지며, Web-aware Spring Application Context 안에서만 유효한 특징이 있다. |
| session | 하나의 Bean 정의에 대해 하나의 HTTP Session의 생명주기 안에서 단 하나의 객체만 존재한다. Web-aware Spring Application Context 안에서만 유효한 특징이 있다. |
| global session | 하나의 Bean 정의에 대해 하나의 global HTTP Session의 생명 주기 안에서 단 하나의 객체만 존재한다. 일반적으로는 portlet context 안에서만 유효하며, Web-aware Spring Application Context 안에서만 유효한 특징이 있다. |

### Singleton

```java
// xml 설정
<bean id="..." class="..." scope="singleton"></bean>

// annotaion 설정 (대상 클래스에 적용)
@Scope("singleton")
```

- singleton bean은 **Spring 컨테이너 안에서 딱 한 번 생성**되며, 컨테이너가 사라질 때는 Bean도 같이 사라진다.
- **생성된 하나의 인스턴스는 single bean cache에 저장**되며, 해당 bean에 대한 요청과 참조가 있을 때마다 캐시된 객체를 반환한다.
- 기본적으로 **모든 bean은 scope이 명시적이지 않으면 singleton scope를 가진다.**

### Prototype

```java
// xml 설정
<bean id="..." class="..." scope="prototype"></bean>

// annotaion 설정 (대상 클래스에 적용)
@Scope("prototype")
```

- Prototype Bean은 **모든 요청에서 새로운 객체로 생성하는 것**이며, **의존성 관계의 Bean이 주입될 때마다 새로운 객체가 생성되어 주입된다.**
- GC에 의해 Bean이 자동으로 제거된다.

## @Bean vs @Component

### @Bean

- **개발자가 컨트롤이 불가능한 외부 라이브러리**들을 Bean으로 등록하고 싶은 경우 사용된다.
- **메소드나 어노테이션 단위**에 붙일 수 있다.

### @Component

- **개발자가 직접 컨트롤이 가능한 클래스**들의 경우에 사용된다.
- **클래스 또는 인터페이스 단위**에 붙일 수 있다.

## 참고 자료

- [https://developer-ellen.tistory.com/198?category=921298](https://developer-ellen.tistory.com/198?category=921298)
- [https://devwithpug.github.io/spring/spring-1/](https://devwithpug.github.io/spring/spring-1/)