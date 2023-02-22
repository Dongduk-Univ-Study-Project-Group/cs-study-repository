>Spring Bean이란 무엇인가요?
### 스프링 빈(Spring Bean)
Spring IoC 컨테이너가 관리하는 자바 객체로, Spring IoC 컨테이너가 관리하는 Java 객체를 의미

>(추가 질문) 스프링 Bean의 생성 과정을 설명해주세요.

1. 자바 어노테이션(Java Annotation)을 사용하는 방법
- Bean을 등록하기 위해 @Component 어노테이션을 사용
- `@Component, @Controller, @Service, @Entity`등

2. Bean Configuration File에 직접 Bean을 등록하는 방법
- `@Configuration`과 `@Bean` 어노테이션을 이용해 Bean을 직접 등록

## 참고자료
[[Spring] 스프링 빈(Bean)의 개념과 생성 원리](https://atoz-develop.tistory.com/entry/Spring-%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B9%88Bean%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%83%9D%EC%84%B1-%EC%9B%90%EB%A6%AC)    
