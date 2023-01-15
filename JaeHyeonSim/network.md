
<details><summary>OSI 7계층과 그 존재 이유, TCP/IP 4계층에 대해 설명해보세요.</summary>
<p>

```html
- ksundong

OSI 7계층은 네트워크 통신을 구성하는 요소들 7개의 계층으로 표준화 한 것입니다.
이렇게 표준화하는 것의 장점은 통신이 일어나는 과정을 단계별로 파악할 수 있어,
문제가 발생하면 해당 문제를 해결하기 용이해집니다.

실제로 우리가 대부분 사용하는 네트워크는 TCP/IP 4계층입니다. 통신에 실제로 사용되는 계층이고
1,2 계층이 1계층, 5, 6, 7계층이 4계층으로 운영됩니다.
```

**OSI (Open System Interconnection)**

: 개방 시스템 상호 연결, 계층화된 구조

- OSI 모델의 목적
    1. 기본적인 하드웨어 또는 소프트웨어의 변경 없이 서로 다른 시스템간 개방 통신
    2. 안전하게 상호 연결이 가능한 네트워크 구조를 이해하고 설계하기 위한 모델

- OSI 7계층
    
    7 - application (응용)
    
    6 - presentation (표현)
    
    5 - session (세션)
    
    4 - transport (전송) : TCP와 UDP가 대표적인 통신 프로토콜
    
    3 - network (네트워크) : IP 주소, 라우터 장비와 연관
    
    2 - data link (데이터 링크) : MAC 주소, 스위치, 브릿지 장비와 연관
    
    1 - physical (물리) : 0/1의 전기 신호 전송/수신, 리피터 장비와 연관
    
    | 1, 2, 3 | 네트워크 지원 계층 | 하나의 장치에서 다른 장치로 전송되는 데이터의 물리적인 면을 처리 | 
    | --- | --- | --- | 
    | 4 | 전송 계층 | 네트워크 지원 계층과 사용자 지원 계층을 서로 연결 |
    | 5, 6, 7 | 사용자 지원 계층 | 관련 없는 소프트웨어 시스템간의 상호 운용성 제공 |
    
    data가 상위에서 하위 계층으로 내려가면서 header가 추가되고,
    
    하위에서 상위 계층으로 올라가면서 header가 삭제된다.
    

**TCP/IP (Transmission Control Protocol/Internet Protocol)**

: 전세계에서 가장 일반적으로 사용되는 프로토콜 세트 중 하나

컴퓨터 사이의 통신 표준 및 네트워크의 라우팅 및 상호연결에 대한 자세한 규칙을 지정

- TCP/IP 4계층
    
    : OSI 참조 모델을 기반으로 상업적이고 실무적으로 이용될 수 있도록 단순화된 모형
    
    4 - application (응용) : 응용 프로그램간 데이터를 교환하기 위해 사용되는 프로토콜
    
    3 - transport (전송) : 통신 노드 간의 연결 제어 및 자료 송수신
    
    2 - internet (인터넷) : 네트워크상 최종 목적지까지의 연결성 제공
    
    1 - network access (네트워크 액세스) : 물리적으로 데이터가 네트워크를 통해 어떻게 전송되는지 정의하고 장비간 데이터 전송
    
    | TCP/IP 4계층 | 역할 | 데이터 단위 | 전송 주소 | 예시 | 장비 | 
    | --- | --- | --- | --- | --- | --- |
    | 4(OSI 5, 6, 7) | 응용프로그램 간의 데이터 송수신 | Data/Message | - | 파일 전송, 이메일, FTP, HTTP, SSH, Telnet, DNS, SMTP 등 | - |
    | 3 (OSI 4) | 호스트 간의 자료 송수신 | Segment | port | TCP, UDP, RTP, RTCP 등 | 게이트웨이 |
    | 2 (OSI 3) | 데이터 전송을 위한 논리적 주소 지정 및 경로 지정 | Packet | IP | IP, ARP, ICMP, RARP, OSPF | 라우터 |
    | 1 (OSI 1, 2) | 실제 데이터 프레임을 송수신 | Frame | MAC | Ethernet, PPP, Token Ring 등 | 브릿지, 스위치 |

**+ 네트워킹 장비**

| 장비 | Layer | 역할 | 
| --- | --- | --- | 
| Repeater (리피터) | 1계층(physical) | 물리계층 상에서 세그먼트를 연결하여 연장. 전기신호 재생 및 증폭 장치(중계기) |
| Hub (허브) | 1계층(physical) | 네트워크 장비끼리 연결. 일종의 멀티포트 repeater 역할. 다양한 기기들로부터 오는 전기신호들을 받아서 증폭시키고 다른 기기로 뿌림 |
| Bridge (브리지) | 2계층(data link) | 패킷을 분석하여 다른 네트워크로 전송할 수 있는지 결정. 링크계층 네트워크를 결합시켜 LAN을 확장. 하나의 네트워크망 안에서 서로 다른 LAN 연결 |
| Switch (스위치) | 2계층(data link) | 목적지의 MAC 주소를 가지고 있는 포트에 프레임을 전송. 다양한 계층에서 동작 가능 |
| Router (라우터) | 3계층(network) | 패킷이 목적지까지 가기 위한 경로 설정. 패킷의 헤더에서 목적지 IP주소를 확인하고 네트워크 망으로 전송 |
| Gateway (게이트웨이) | 7계층(application) | 다른 네트워크로 들어가는 입구. 서로 다른 네트워크망 연결. 서로 다른 네트워크상의 통신 프로토콜 적절히 변환 |

+L2, L3, … 스위치 정리하기


- 참고자료
    
    [https://www.ibm.com/docs/ko/aix/7.1?topic=management-transmission-control-protocolinternet-protocol](https://www.ibm.com/docs/ko/aix/7.1?topic=management-transmission-control-protocolinternet-protocol)
    
    : IBM - TCP/IP
    
    [https://velog.io/@jehjong/개발자-인터뷰-TCPIP-4계층](https://velog.io/@jehjong/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0-TCPIP-4%EA%B3%84%EC%B8%B5)
    
    : jehjong - [개발자 인터뷰] TCP/IP 4계층
    
    [http://www.ktword.co.kr/test/view/view.php?m_temp1=4842](http://www.ktword.co.kr/test/view/view.php?m_temp1=4842)
    
    : kt - 네트워킹 장비 (리피터, 허브, 스위치, 브릿지, 라우터)
    
    [https://siahn95.tistory.com/entry/Network장비-Hub허브-Bridge브릿지-Switch스위치-Router라우터-Gateway게이트웨이란](https://siahn95.tistory.com/entry/Network%EC%9E%A5%EB%B9%84-Hub%ED%97%88%EB%B8%8C-Bridge%EB%B8%8C%EB%A6%BF%EC%A7%80-Switch%EC%8A%A4%EC%9C%84%EC%B9%98-Router%EB%9D%BC%EC%9A%B0%ED%84%B0-Gateway%EA%B2%8C%EC%9D%B4%ED%8A%B8%EC%9B%A8%EC%9D%B4%EB%9E%80)
    
    : [Network][장비] Hub(허브), Bridge(브릿지), Switch(스위치), Router(라우터), Gateway(게이트웨이)란?
    
    [https://velog.io/@kimyeji203/네트워크-OSI-7계층-네트워크-장비-스위치-종류](https://velog.io/@kimyeji203/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-OSI-7%EA%B3%84%EC%B8%B5-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%9E%A5%EB%B9%84-%EC%8A%A4%EC%9C%84%EC%B9%98-%EC%A2%85%EB%A5%98)
    
    : kimyeji203 - [네트워크] OSI 7계층 - 네트워크 장비, 스위치 종류
    

.

</details>


<details><summary>TCP와 UDP의 차이</summary>
<p>



</details>


<details><summary>TCP 3, 4 way handshake</summary>
<p>



</details>


<details><summary>CORS란 무엇이며 이것에 대해서 설명해보세요.</summary>
<p>

```html
- ksundong

CORS는 웹개발을 하다가 흔히 만날 수 있는 이슈입니다.
대개는 프론트엔드 개발시에 로컬에서 API 서버에 요청을 보낼 때 흔하게 발생합니다.

서로 다른 도메인간에 자원을 공유하는 것을 뜻합니다.
대부분의 브라우저에서는 이를 기본적으로 차단하며, 서버측에서 헤더를 통해서 사용가능한 자원을 알려줍니다.

preflight request는 실제 요청을 보내도 안전한지 판단하기 위해 사전에 보내는 요청입니다.
OPTIONS 메서드로 요청하며 CORS를 허용하는지 확인합니다.
CORS가 허용된 웹서버라면 사용 가능한 리소스를 헤더에 담아 응답합니다.
```

**SOP (Same Origin Policy)**

: 동일 출처 정책

다른 출처의 리소스를 사용하는 것을 제한하는 보안 매커니즘

두 개의 URL이 존재할 때,

출처 = 프로토콜, 포트(지정된 경우), 호스트(도메인 주소)가 동일한 경우 두 URL의 Origin이 같다.

요청 헤더에 포함되는 값

```html
origin: 어디서 요청을 했는지 서버에 알려주는 주소
access-control-request-method : 실제 요청이 보낼 HTTP 메서드
access-control-request-headers : 실제 요청에 포함된 header
```

응답 헤더에 포함되는 값

```html
access-control-allow-origin : 서버가 허용하는 출처
access-control-allow-methods : 서버가 허용하는 HTTP 메서드 리스트
access-control-allow-headers : 서버가 허용하는 header 리스트
access-control-max-age : 프리 플라이트 요청의 응답을 캐시에 저장하는 시간
```

**CORS (Cross-Origin Resource Sharing)**

: 교차 출처 리소스 공유

다른 출처에서 자원을 요청할 수 있도록 허용하는 구조
    

- 다른 출처에서 자원을 요청하는 방법 3가지
    1. Simple Request : 단순 요청
        
        바로 서버에 요청
        
        1. GET, POST, HEAD 요청만 가능
        2. access-control-allow-origin은 어떤 요청을 허용할지 결정
        3. 허용되는 Header와 Content-Type이 정해져 있음
    2. Preflight Request : 사전 요청
        
        먼저 OPTIONS 메소드를 사용해 HTTP 요청을 다른 출처 리소스로 전송하여
        
        실제 요청이 안전한지(요청 가능 여부) 확인
        
        1. 웹브라우저에서 XMLHttpRequest를 특정 URL로 요청하기 전에 HTTP OPTIONS 호출
        2. 서버는 해당 URL에 접근할 수 있는 Origin URL과 HTTP 메소드 반환
    3. Credential Request : 인증 요청
        
        쿠키, 인증 헤더, TLS 클라이언트 인증서 등의 신용정보와 함께 요청
    

- CORS 해결 방법
    1. 프론트 프록시 서버 설정
    2. 직접 헤더 설정
    3. 스프링부트 cross-origin 설정

- 참고자료
    
    [https://dongwooklee96.github.io/post/2021/03/23/sopsame-origin-policy-란-무엇일까.html](https://dongwooklee96.github.io/post/2021/03/23/sopsame-origin-policy-%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C.html)
    
    : 이동욱 - SOP(Same-origin policy) 란 무엇일까?
    
    [https://velog.io/@frankle97/CORS란](https://velog.io/@frankle97/CORS%EB%9E%80)
    
    : frankle97 - CORS란
    
    [https://escapefromcoding.tistory.com/724](https://escapefromcoding.tistory.com/724)
    
    : 코동이 - CORS란 무엇인가? (코드 예시 포함)
    
    [https://fomaios.tistory.com/entry/Network-CORS란-feat-보안HTTP](https://fomaios.tistory.com/entry/Network-CORS%EB%9E%80-feat-%EB%B3%B4%EC%95%88HTTP)
    
    : Fomagran - CORS란? (디테일한 설명)
    

.

</details>


<details><summary>HTTP 메서드와 이것이 하는 역할에 대해서 설명해보세요.</summary>
<p>



</details>

