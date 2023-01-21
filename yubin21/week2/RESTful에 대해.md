>RESTful에 대해
## RESTful이란 무엇이며, 이것에 대해서 아는대로 설명해보세요.
### RESTful에 대해
REST 원칙을 지켜 설계하는 것을 의미한다.
1) HTTP URI를 통해 자원(Resource)를 명시하고
2) HTTP Method(POST,GET,PUT,DELETE)를 통해
3) 해당 자원(URI)에 대한 CRUD OPERATION을 적용함을 의미한다.
- 즉, REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.
- CRUD Operation  
  - Create : 생성(POST)  
  - Read : 조회(GET)  
  - Update : 수정(PUT)  
  - Delete : 삭제(DELETE)  
  - HEAD: header 정보 조회(HEAD)  

### REST의 장단점
**장점**  
- HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구출할 필요가 없다.
- HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.

**단점**
- 표준이 존재하지 않는다.
- 사용할 수 있는 메소드가 4가지 밖에 없다.
- HTTP Method 형태가 제한적이다.
- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 값이 왠지 더 어렵게 느껴진다.
- 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.
- PUT, DELETE를 사용하지 못하는 점
- pushState를 지원하지 않는 점

### REST가 필요한 이유
최근의 서버 프로그램은 다양한 브라우저와 안드로이폰, 아이폰과 같은 모바일 디바이스에서도 통신을 할 수 있어야 한다.
이러한 멀티 플랫폼에 대한 지원을 위해 서비스 자원에 대한 아키텍처를 세우고 이용하는 방법을 모색한 결과, REST에 관심을 가지게 되었다.

### RESTful 하지 못한 경우
Ex1) CRUD 기능을 모두 POST로만 처리하는 API  
Ex2) route에 resource, id 외의 정보가 들어가는 경우(/students/updateName)  


## 참고자료
[[Network] REST란? REST API란? RESTful이란?](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)