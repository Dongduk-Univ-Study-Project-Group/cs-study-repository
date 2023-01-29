## OSI 7계층과 TCP/IP 4계층

### OSI(Open Systems Interconnection) 7계층
+ 통신이 일어나는 과정을 7단계로 정의한 국제 통신 표준 규약이다.
+ 계급, 상하구조가 존재한다.
+ 각 계층은 독립되어있다.
+ 암기 Tip : All People Seem To Need Data Processing

1. 물리(Physical Layer) : 데이터를 전기적인 신호로 변환해서 주고받는 기능을 진행하는 공간. (통신 케이블, 허브)
2. 데이터 링크(Data Link Layer) : 물리계층으로 송수신되는 정보를 확인하고 오류가 없는 통신을 위해 여러 역할을 수행한다. MAC 주소를 통해 통신한다. (브릿지, 스위치)
3. 네트워크(Network Layer)데이터를 목적지까지 가장 안전하고 빠르게 전달하는 기능. 라우터를 통해 경로를 선택하여 IP주소를 지정하고 경로에 따라 패킷을 전달해준다. (라우터)
4. 전송(Transport Layer) : 두 호스트 시스템으로부터 발생하는 데이터의 흐름을 제공한다.
5. 세션(Session Layer) : 통신 시스템 사용자간의 연결을 유지 및 설정한다.
6. 표현(Presentation Layer) : 세션 계층 간의 주고받는 인터페이스를 일관성있게 제공한다.
7. 응용(Application Layer) : 사용자가 네트워크에 접근할 수 있도록 서비스를 제공한다.

### TCP/IP 4계층
TCP/IP 4계층은 TCP/IP 프로토콜 통신 과정에 초점을 맞추어, OSI 7계층을 좀 더 단순화 시킨 계층을 의미한다.
통신에 실제로 사용되는 계층이고 1,2 계층이 1계층, 5, 6, 7계층이 4계층으로 운영된다.
+ 각 계층별 처리 역할이 다르기 때문에, 계층별 간섭을 최소화할 수 있다.
+ 특정 계층에서 문제가 생기면, 해당 계층을 살펴보면 되기 때문에, 유지 보수가 편리하다.
+ 다른 계층끼리는 데이터의 전달 과정을 구체적으로 알 필요가 없기 때문에, 데이터의 캡슐화와 은닉이 가능하다.

#### 1계층 네트워크 액세스 계층(Network Access Layer or Network Interface Layer)
OSI 7계층의 물리계층과 데이터 링크 계층에 해당한다.
물리적인 주소로 MAC을 사용한다.
LAN, 패킷망, 등에 사용된다.

#### 2계층 인터넷 계층(Internet Layer)
OSI 7계층의 네트워크 계층에 해당한다.
통신 노드 간의 IP패킷을 전송하는 기능과 라우팅 기능을 담당한다.
프로토콜 – IP, ARP, RARP

#### 3계층 전송 계층(Transport Layer)
OSI 7계층의 전송 계층에 해당한다.
통신 노드 간의 연결을 제어하고, 신뢰성 있는 데이터 전송을 담당한다.
프로토콜 – TCP, UDP

#### 4계층 응용 계층(Application Layer)
OSI 7계층의 세션 계층, 표현 계층, 응용 계층에 해당한다.
TCP/UDP 기반의 응용 프로그램을 구현할 때 사용한다.
프로토콜 – FTP, HTTP, SSH

#### 참고
https://jungeun960.tistory.com/181
https://hahahoho5915.tistory.com/15
https://wooono.tistory.com/507