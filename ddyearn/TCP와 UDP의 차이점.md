## TCP와 UDP의 차이점

### 전송계층
전송계층은 IP에 의해 전달되는 패킷의 오류를 검사하고 재전송 요구 등의 제어를 담당하는 계층이다.
TCP와 UDP는 TCP/IP의 전송계층에서 사용되는 프로토콜이다. 패킷을 한 컴퓨터에서 다른 컴퓨터로 전달해주는 IP프로토콜을 기반으로 구현된다.

### TCP (Transmission Control Protocol)
TCP는 연결 지향형 프로토콜이고, 신뢰성 있는 데이터 전송을 보장한다. 
흐름 제어, 순서번호, 확인 응답 등을 통해 데이터가 순서대로 정확하게 전달되도록 한다.

### UDP (User Datagram Protocol)
UDP는 데이터를 데이터그램 단위로 전송하는 프로토콜이다.

### 공통점
포트 번호를 이용하여 주소를 지정하고 데이터 오류 검사를 위한 체크섬이 존재한다.

### 차이점
TCP는 가상 회선을 만들어 신뢰성을 보장하도록(흐름 제어, 혼잡 제어, 오류 제어) 하므로
따로 신뢰성을 보장하기 위한 절차가 없는 UDP에 비해 속도가 느린편이다.  
TCP는 파일전송과 같은 신뢰성이 중요한 서비스에 사용되고, 
UDP는 스트리밍, RTP와 같이 연속성이 더 중요한 서비스에 사용된다.

+) 하지만 UDP도 신뢰성을 UDP자체에서 보장하지 않는 것 뿐이지, 개발자가 직접 신뢰성을 보장하도록 할 수 있다.

TCP는 연결이 성공해야 통신이 가능한 연결형 프로토콜이고 UDP는 연결없이 통신이 가능한 비연결형 프로토콜이다.
TCP는 데이터의 경계를 구분하지 않는 Byte-Stream Service이고 UDP는 Datagram Service이다.

### 정리
| TCP (Transmission Control Protocol) | UDP (User Datagram Protocol)                 |
|-------------------------------------|----------------------------------------------|
| 신뢰성 있는 데이터 전송                       | 신뢰성 보장 X                                     |
| 속도 상대적으로 느림                         | 속도 상대적으로 빠름                                  |
| 연결형 프로토콜                            | 비연결형 프로토콜                                    |
| Byte-Stream Service                 | Datagram Service                             |
| 혼잡제어와 흐름제어 지원                       | 혼잡제어와 흐름제어 지원 X                              |
| 순서 보장                               | 순서 보장 X                                      |
| Segment 패킷                          | Datagram 패킷                                  |
| 일 대 일(Unicast) 통신                   | 일 대 일, 일 대 다(Broadcast), 다 대 다(Multicast) 통신 |

### 참고
https://madplay.github.io/post/network-tcp-udp-tcpip