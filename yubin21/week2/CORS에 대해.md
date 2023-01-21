>CORS란 무엇이며 이것에 대해서 설명해보세요.
## CORS란 무엇이며 이것에 대해서 설명해보세요.
### CORS에 대해
CORS(Cross-Origin Resource Sharing)는 출처가 다른 자원들을 공유한다는 뜻으로, 한 출처에 있는 자원에서 다른 출처에 있는 자원에 접근하도록 하는 개념이다. 다른 출처에 있는 자원을 요청한다고 하면, 이를 교차 출처 요청이라고 부른다.

### 출처 
url의 구성요소 중에서 Protocol + Host + Port 3가지가 같으면 동일 출처(Origin)라고 한다.

동일 출처 예시  

|                                                                        |                                                     |
|:----------------------------------------------------------------------:|:---------------------------------------------------:|
|               http://Example.com:80  http://example.com                |           기본 Port인 80번이 생략되어있으므로 동일 출처이다.           | 
| http://example.com/app1/index.html  http://example.com/app2/index.html | Protocol, Host, Port(생략)이 같으며, Path부터 다르므로 동일 출처이다. |


다른 출처 예시

|                                                                      |                     |
|:--------------------------------------------------------------------:|:-------------------:|
|          http://example.com/app1  https://example.com/app2           |   Protocol이 다르다.    |
| http://example.com  http://www.example.com  http://myapp.example.com |     Host가 다르다.      |
|             http://example.com  http://example.com:8080              | 80, 8080으로 포트가 다르다. |

다른 출처 요청일 경우, CORS 정책에 준수하여 요청해야만 정상적으로 응답을 받는다.

1.단순요청(Simple Request)
- GET, HEAD, POST 요청만 가능하다.
- Accept, Accept-Language, Contet-Language, Content-Type과 같은 CORS 안전 리스트 헤더 혹은 User-Agent 헤더
- Contet-Type 헤더는 application/x-www-form-urlencoded, multipart/form-data and text/plain만 가능
- ReadableStream 객체가 사용되지 않는다.
- XMLHttpRequest 객체를 사용하여 요청하면, 요청에서 사용된 XMLHttpRequest.upload에 의해 반환되는 객체에 어떠한 이벤트 리스너도 등록되지 않는다.

2.프리 플라이트(Preflight Request)  
프리 플라이트는 OPTIONS 메서드로 HTTP 요청을 미리 보내 실제 요청이 전송하기에 안전한지 확인한다. 다른 출처 요청이 유저 데이터에 영향을 줄 수 있기 때문에  미리 전송한다는 의미이다.


요청 헤더에는 다음 값이 포함된다.  
origin : 어디서 요청을 했는지 서버에 알려주는 주소  
access-control-request-method : 실제 요청이 보낼 HTTP 메서드  
access-control-request-headers : 실제 요청에 포함된 header


응답 헤더에는 다음 값이 포함된다.  
access-control-allow-origin : 서버가 허용하는 출처  
access-control-allow-methods : 서버가 허용하는 HTTP 메서드 리스트  
access-control-allow-headers : 서버가 허용하는 header 리스트  
access-control-max-age : 프리 플라이트 요청의 응답을 캐시에 저장하는 시간  

3.신용 요청(Credentialed Request)  
신용 요청은 쿠키, 인증 헤더, TLS 클라이언트 인증서 등의 신용정보와 함께 요청한다. 기본적으로, CORS 정책은 다른 출처 요청에 인증정보 포함을 허용하지 않는다. 요청에 인증을 포함하는 플래그가 있거나 access-control-allow-credentials가 true로 설정 한다면 요청할 수 있다.

### Spring에서 CORS 에러를 해결하기 위한 방법
교차 출처 리소스 공유(Cross-Origin Resource Sharing)은 Origin이 다른 경우에도(Cross-Origin)리소스를 공유할 수 있음을 의미한다. 하지만 웹브라우저는 원래 동일 출처 원칙(Same Origin Policy)을보안상의 이유로 요구한다. CORS에러를 피하기 위해서는 request origin과 response origin을 일치시키는 작업이 필요하다.  

Spring 에서는 아래의 3가지 방식으로 처리할 수 있다.

1.CorsFilter를 생성해 직접 response에 header를 넣어주기  
2.Controller에서 @CrossOrigin annotation 추가하기  
3.WebMvcConfigurer를 이용해서 처리하기

## 참고자료
[Yunseok's Dev Blog - CORS란 무엇인가?](https://hannut91.github.io/blogs/infra/cors)

[CORS란 무엇인가?](https://escapefromcoding.tistory.com/724)