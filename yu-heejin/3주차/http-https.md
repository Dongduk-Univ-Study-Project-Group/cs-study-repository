## HTTP(HyperText Transfer Protocol)란?

- 하이퍼 텍스트 전용 프로토콜로, 간단히 말해 인터넷을 동작시키며, 웹 서버 및 웹 브라우저 상호 간의 데이터 전송을 위한 응용 계층 프로토콜
    - 서버/클라이언트 모델을 따라 데이터를 주고 받기 위한 프로토콜
    - 즉, HTTP는 인터넷에서 하이퍼텍스트를 교환하기 위한 통신 규약으로, 80번 포트를 사용하고 있다.
    - 따라서, HTTP 서버가 80번 포트에서 요청을 기다리고 있으며, 클라이언트는 80번 ㅍ트로 요청을 보내게 된다.
- 웹 사이트에 엑세스 하기 위해서는 프로토콜 변형이 필요한데, 이 때 웹 사이트 URL이 일반적으로 “http://www…”로 시작하며 URL에 해당하는 웹 페이지를 가져오기 위해 웹 사이트 서버에 명령을 보내 작동하게 된다.

### HTTP의 구조

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e49af25f-fd38-4926-823d-d01009c9d9ea/Untitled.png)

- HTTP는 애플리케이션 레벨의 프로토콜로 TCP/IP 위에서 작동한다.
- HTTP는 상태를 가지고 있지 않는 Stateless 프로토콜이며, Method, Path, Version, Headers, Body 등으로 구성된다.
- 하지만 HTTP는 **암호화되지 않은 평문 데이터를 전송하는 프로토콜**이기 때문에 HTTP로 비밀번호나 주민등록번호 등을 주고 받으면 제3자가 정보를 조회할 수 있다. → 이 문제를 해결하기 위해 HTTPS 등장

## HTTPS(HyperText Transfer Protocol Secure)란?

- 하이퍼 텍스트 전송 프로토콜 보안으로 표준 http와 동일한 방식으로 작동한다.
    - **HTTP에 데이터 암호화가 추가된 프로토콜**
- 서버와 주고받는 데이터가 암호화되기 때문에 웹 사이트에 추가적인 보호를 제공한다.
- 즉, 개인 데이터를 훔치거나 해킹하거나 볼 수 없도록 작동한다.
- HTTPS는 HTTP와 다르게 443번 포트를 사용하며, 네트워크 상에서 중간에 제 3자가 정보를 볼 수 없도록 암호화를 지원하고 있다.

### 대칭키 암호화와 비대칭키 암호화

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5ab5785f-e16b-4275-9141-88e1d8db9e42/Untitled.png)

- 대칭키 암호화
    - 클라이언트와 서버가 동일한 키를 사용해 암호화/복호화를 진행한다.
    - 키가 노출되면 매우 위험하지만 연산 속도가 빠르다.
- 비대칭키 암호화
    - 1개의 쌍으로 구성된 공개키와 개인키를 암호화/복호화 하는데 사용한다.
    - 키가 노출되어도 비교적 안전하지만 연산 속도가 느리다.
- 비대칭키 암호화는 공개키/개인키 암호화 방식을 이용해 데이터를 암호화하고 있다.
    - 공개 키 : 모두에게 공개가 가능한 키
    - 개인 키 : 나만 가지고 알고 있어야 하는 키
    - 공개키와 개인 키는 서로를 위한 한 쌍의 키이다.
- 공개키 암호화와 개인키 암호화
    - 공개키로 암호화를 하면 개인키로만 복호화할 수 있다 → 개인키는 나만 가지고 있으므로 나만 볼 수 있다.
    - 개인키로 암호화를 하면 공개키로만 복호화할 수 있다 → 공개키는 모두에게 공개되어 있으므로, 내가 인증한 정보임을 알려 신뢰성을 보장할 수 있다.

## HTTP, HTTPS 차이점

- HTTPS는 SSL(Secure Socket Layer) 인증서를 사용하는 HTTP
- SSL(or TLS) 인증서는 일반 HTTP 요청 및 응답을 암호화 한다.
- 따라서 HTTPS는 HTTP보다 더 안전한 보안용 프로토콜이다.
- HTTP는 암호화가 추가되지 않아 보안에 취약하지만, HTTPS는 안전하게 데이터를 주고받을 수 있다.
- 그러나, HTTPS는 암호화 및 복호화 과정이 필요하기 때문에 HTTP보다 속도가 느리다.
- HTTPS는 인증서를 발급하고 유지하기 위한 추가 비용이 발생한다.

## HTTPS의 동작 과정

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ab4da4ac-96d2-4d4b-8ea2-d6f546266636/Untitled.png)

- HTTPS는 대칭키 암호화와 비대칭키 암호화를 모두 사용하여 빠른 연산 속도와 안정성을 모두 얻고있다.
- HTTPS 연결 과정(Hand-Shaking)에서는 먼저 서버와 클라이언트 간에 세션키를 교환한다.
    - 여기서 **세션 키는 주고 받는 데이터를 암호화하기 위해 사용되는 대칭키**이며, 데이터 간의 교환에는 빠른 연산 속도가 필요하므로 세션 키는 대칭 키로 만들어진다.
    - 문제는 **이러한 세션키를 클라이언트와 서버가 어떻게 교환할 것이냐인데, 이 과정에서 비대칭키가 사용된다.**
    - 즉, **처음 연결을 성립하여 안전하게 세션키를 공유하는 과정에서 비대칭키가 사용되며, 이후 데이터를 교환하는 과정에서 빠른 연산 속도를 위해 대칭키가 사용된다.**
- 실제 HTTPS 연결 과정이 성립되는 흐름을 보면 다음과 같다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6502f3cb-9d55-436a-92e2-ad6b62bf8cf7/Untitled.png)
    
    1. 클라이언트(브라우저)가 서버로 최초 연결을 시도한다.
    2. 서버는 공개키(인증서)를 브라우저에게 넘겨준다.
    3. 브라우저는 인증서의 유효성을 검사하고 세션키를 발급한다.
    4. 브라우저는 세션키를 보관하며 추가로 **서버의 공개키로 세션키를 암호화하여 서버로 전송한다.**
    5. **서버는 개인키로 암호화된 세션키를 복호화하여 세션키를 얻는다.**
    6. 클라이언트와 서버는 **동일한 세션키를 공유하므로 데이터를 전달할 때 세션키로 암호화 및 복호화를 진행한다.**

## HTTPS의 발급 과정

- **서버는 클라이언트와 세션키를 공유하기 위한 공개키를 생성해야 한다.**
- 일반적으로는 인증된 기관에 공개키를 전송하여 인증서를 발급받는다.

### 발급 과정

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/61a3a58a-c3b8-436c-acd6-c46430b5e165/Untitled.png)

1. A 기업은 HTTP 기반의 애플리케이션에 HTTPS를 적용하기 위해 공개키/개인키를 발급한다.
2. CA 기업에게 돈을 지불하고, 공개키를 저장하는 인증서의 발급을 요청한다.
3. CA 기업은 CA 기업의 이름, 서버의 공개키, 서버의 정보 등을 기반으로 인증서를 생성하고, CA 기업의 개인키로 암호화하여 A 기업에게 이를 제공한다.
4. A 기업은 클라이언트에게 암호화된 인증서를 제공한다.
5. 브라우저는 CA 기업의 공개키를 미리 다운 받아 갖고 있으며, 암호화된 인증서를 복호화한다.
6. 암호화된 인증서를 복호화하여 얻은 A 기업의 공개키로 세션키를 공유한다.

- 인증서는 CA의 개인키로 암호화되었기 때문에 신뢰성을 확보할 수 있고, 클라이언트는 A기업의 공개키로 데이터를 암호화했기 떄문에 A기업만 복호화하여 원본의 데이터를 얻을 수 있다.
- 여기서 인증서에는 A 기업의 공개키가 포함되어있기 때문에 A 기업의 공개키라고 봐도 무방하다.
- 또한, 브라우저에는 인증된 CA 기관의 정보들이 사전에 등록되어 있어 인증된 CA 기관의 인증서가 아닐 경우에는 다음과 같은 형태로 브라우저에 보여지게 된다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b8f69851-88dc-4776-8e58-7d76b1ed30b5/Untitled.png)
    

## Google 순위 요소로서의 SSL

- 웹 사이트를 https에서 실행하려면 SSL(Security Sockets Layer) 인증서가 필요하다.
- Netscape에서 개발한 이 인증서는 웹사이트의 데이터를 암호화하고, 웹사이트 방문자에게 당신의 웹사이트가 안전하다는 것을 증명하는 역할을 한다.
- 구글은 https의 필요성을 매우 강조하여 이를 기반으로 하는 알고리즘 업데이트도 출시했고, https 보안이 없는 사이트는 SERP에서 높은 순위를 얻기 어렵다.

## 참고 자료

- [https://www.ascentkorea.com/difference-between-http-and-https/](https://www.ascentkorea.com/difference-between-http-and-https/)
- [https://mangkyu.tistory.com/98](https://mangkyu.tistory.com/98)