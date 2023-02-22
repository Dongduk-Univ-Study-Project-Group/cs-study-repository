>JPA
## JPA
JPA(Java Persistence API)는 Java 진영에서 ORM 기술 표준으로 사용하는 인터페이스의 모음으로, 구현체로서 Hibernate, OpenJPA등을 사용한다.

### JPA의 이점
1. 특정 데이터베이스에 종속되지 않음
추상화한 데이터 접근 계층을 제공하기 때문에 설정 파일에 어떤 데이터베이스를 사용하는지 알려주면 얼마든지 데이터베이스를 변경할 수 있다.

2. 객체지향적 프로그래밍
JPA를 사용하면 데이터베이스 설꼐 중심의 패러다임에서 객체지향적으로 설계가 가능하다. 이를 통해 좀 더 직관적이고 비즈니스 로직에 집중할 수 있도록 도와준다.

> (추가 질문) JPA 영속성 컨텍스트의 이점(5가지)를 설명해주세요.
- 1차 캐시   
DB에 바로 저장하는 것이 아니라 영속성 컨텍스트에 의해 관리됨

- 동일성(identity) 보장    
영속성 컨텍스트에서 관리되는 엔티티를 가져왔을 경우 동일성을 보장

- 트랜잭션을 지원하는 쓰기 지연 (transactional write-behind)  
commit시 한번에 전송해 성능을 최적화

- 변경 감지(Dirty Checking)  
commit되는 시점에 엔티티와 스냅샷을 비교해 변경이 일어나면 이를 감지합니다.

- 지연 로딩(Lazy Loading)  
엔티티에서 해당 엔티티를 불러올 때 SQL을 날려 해당 데이터를 가져옵니다.

## 참고자료
[JPA란 무엇인가, 그리고 장단점은 뭐가 있을까?](https://velog.io/@dev_zzame/JPA%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EC%9E%A5%EB%8B%A8%EC%A0%90%EC%9D%80-%EB%AD%90%EA%B0%80-%EC%9E%88%EC%9D%84%EA%B9%8C)  
인프런 김영한님 [자바 ORM 표준 JPA 프로그래밍 - 기본편](https://www.inflearn.com/course/ORM-JPA-Basic)