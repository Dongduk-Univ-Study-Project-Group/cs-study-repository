## RESTful이란
Restful API는 HTTP 통신을 Rest 설계 규칙을 잘 지켜서 개발한 API를 Restful한 API라고 합니다.

Rest 설계 규칙은 URI는 정보의 자원만 표현해야 하며, 자원의 상태와 행위는 HTTP Method에 명시하는걸 말합니다.

### REST의 정의
"REpresentational State Transfer" 의 약자로,  
자원을 이름(자원의 표현)으로 구분해 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미합니다.

REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에,
웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일입니다.  
REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나입니다.


### REST의 개념
어떤 자원에 대해 CRUD(Create, Read, Update, Delete) 연산을 수행하기 위해 URI(Resource)로  
GET, POST 등의 방식(Method)을 사용하여 요청을 보내며, 요청을 위한 자원은 특정한 형태(Representation of Resource)로 표현됩니다.

### REST API의 정의
REST의 특징을 기반으로 서비스 API를 구현한 것  
최근 OpenAPI(누구나 사용할 수 있도록 공개된 API: 구글 맵, 공공 데이터 등), 
마이크로 서비스(하나의 큰 어플리케이션을 여러 개의 작은 어플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처)
등을 제공하는 기업 대부분은 REST API를 제공합니다.

### REST API의 특징
REST API의 가장 큰 특징은 각 요청이 어떤 동작이나 정보를 위한 것인지를 그 요청의 모습 자체로 추론이 가능한 것 입니다.

### RESTful API란
RESTful은 REST의 설계 규칙을 잘 지켜서 설계된 API를 RESTful한 API라고 합니다.

즉, REST의 원리를 잘 따르는 시스템을 RESTful이란 용어로 지칭됩니다.

사람이 읽을 수 있는 API라는 것이 특징입니다. 
HTTP를 사용하기 때문에 HTTP의 특성을 그대로 반영합니다. 또한 별도의 인프라 구축이 필요없습니다.

**단점**으로는 명확한 표준이 존재하지 않는다는 점, 
RESTful을 완전히 만족하는 API를 만들기는 매우 까다롭다는 점(그런 REST API로 괜찮은가 참고), 
REST API가 분산환경에 적합하지 않다는 점이 있습니다.(멱등성을 보장하기 힘들기 때문)

**Reference**  
https://dev-coco.tistory.com/97