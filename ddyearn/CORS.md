## CORS(Cross-Origin Resource Sharing)란?

CORS는 웹개발을 하다가 흔히 만날 수 있는 이슈이다. 
프론트엔드 개발시에 로컬에서 API 서버에 요청을 보낼 때 흔하게 발생한다.
서로 다른 도메인간에 자원을 공유하는 것을 뜻한다.
대부분의 브라우저에서는 이를 기본적으로 차단하며, 서버측에서 헤더를 통해서 사용가능한 자원을 알려준다.

교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)는 추가 HTTP 헤더를 사용하여, 
한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다. 
웹 애플리케이션은 리소스가 자신의 출처(도메인, 프로토콜, 포트)와 다를 때 교차 출처 HTTP 요청을 실행한다.

+ 교차 출처 요청의 예시: https://domain-a.com의 프론트 엔드 JavaScript 코드가 XMLHttpRequest를 사용하여 https://domain-b.com/data.json을 요청하는 경우.

보안 상의 이유로, 브라우저는 스크립트에서 시작한 교차 출처 HTTP 요청을 제한한다. 
예를 들어, XMLHttpRequest와 Fetch API는 동일 출처 정책을 따른다. 
즉, 이 API를 사용하는 웹 애플리케이션은 자신의 출처와 동일한 리소스만 불러올 수 있으며, 
다른 출처의 리소스를 불러오려면 그 출처에서 올바른 CORS 헤더를 포함한 응답을 반환해야 한다.

### CORS 동작 방법
기본적으로 웹 클라이언트 어플리케이션이 다른 출처의 리소스를 요청할 때는 HTTP 프로토콜을 사용하여 요청을 보내게 되는데, 
이때 브라우저는 요청 헤더에 Origin이라는 필드에 요청을 보내는 출처를 함께 담아보낸다.
이후 서버가 이 요청에 대한 응답을 할 때 응답 헤더의 Access-Control-Allow-Origin이라는 값에 “이 리소스를 접근하는 것이 허용된 출처”를 내려주고, 
이후 응답을 받은 브라우저는 자신이 보냈던 요청의 Origin과 서버가 보내준 응답의 Access-Control-Allow-Origin을 비교해본 후 이 응답이 유효한 응답인지 아닌지를 결정한다.

#### 출처
https://developer.mozilla.org/ko/docs/Web/HTTP/CORS#%EC%9D%B4_%EA%B8%80%EC%9D%80_%EB%88%84%EA%B0%80_%EC%9D%BD%EC%96%B4%EC%95%BC_%ED%95%98%EB%82%98%EC%9A%94