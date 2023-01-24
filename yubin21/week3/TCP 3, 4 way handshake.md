>TCP 3, 4 way handshake에 대해서 설명해보세요.
## TCP 3, 4 way handshake
3-Way Handshake 는 TCP의 접속,4-Way Handshake는 TCP의 접속 해제 과정이다.
### TCP 3 way handshake
연결하고자 하는 두 장치 간의 논리적 접속을 성립하기 위해 사용하는 연결 확인 방식으로, 3번의 확인 과정을 거친다고 해서 3 way handshake라고 부른다.

![tcp_ip_3way_4way_1](https://user-images.githubusercontent.com/80163835/214235209-a9c1a15a-3281-44f2-a6d9-d94874bdaf04.png)
#### 개념
- TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 연결을 설정(Connection Establish) 하는 과정
- 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작하기 전에 한 쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다.
- 즉, TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.

#### 작동방식
1) Client에서 Server에 연결 요청을 하기위해 SYN 데이터를 보낸다.
2) Server에서 해당 포트는 LISTEN 상태에서 SYN 데이터를 받고 SYN_RCV로 상태가 변경된다.
3) 그리고 요청을 정상적으로 받았다는 대답(ACK)와 Client도 포트를 열어달라는 SYN 을 같이 보낸다.
4) Client에서는 SYN+ACK 를 받고 ESTABLISHED로 상태를 변경하고 서버에 ACK 를 전송한다.
5) ACK를 받은 서버는 상태가 ESTABLSHED로 변경된다.

### TCP 4 way handshake
3 way handshake와 반대로 가상 회선 연결을 해제할 때 주고 받는 확인작업이다. 이 역시 4번의 확인과정을 거친다고 하여 4 way handshake라고 부른다.

![img1 daumcdn](https://user-images.githubusercontent.com/80163835/214234237-27384ec7-4f2a-45bc-8155-419cb97214fd.png)
#### Termination의 종류
TCP는 대부분의 connection-oriented 프로토콜과 같은 두 가지 연결 해제 방식이 있다.
1. Graceful connection release(정상적인 연결 해제)
   - 정상적인 연결 해제에서는 양쪽이 커넥션이 서로 모두 커넥션을 닫을 때까지 연결되어 있다.
2. Abrupt connection release(갑작스런 연결 해제)
   - 갑자기 한 TCP 엔티티가 연결을 강제로 닫는 경우
   - 한 사용자가 두 데이터 전송 방향을 모두 닫는 경우
#### 작동방식
1. 작동방식 (Abrupt)  
RST(TCP reset) 세그먼트가 전송되면 갑작스러운 연결 해제가 수행되는데, RST 세그먼트는 다음과 같은 경우에 전송된다.

   1) 존재하지 않는 TCP 연결에 대해 비SYN 세그먼트가 수신된 경우
   2) 열린 커넥션에서 일부 TCP 구현은 잘못된 헤더가 있는 세그먼트가 수신된 경우
      - RST 세그먼트를 보내, 해당 커넥션을 닫아 공격을 방지한다.
   3) 일부 구현에서 기존 TCP 연결을 종료해야 하는 경우
      - 연결을 지원하는 리소스 부족할때
      - 원격 호스트에 연결할 수 없고 응답이 중지되었을 때


2. 작동방식 (Graceful)  
연결 종료 요청 역시, 일반적으로 생각하는 우리가 일반적으로 생각하는 Client와 Server는 모두 서로 연결 요청을 먼저 할 수 있기 때문에, 연결 요청을 먼저 시도한 요청자를 Client로, 연결 요청을 받은 수신자를 Server쪽으로 생각하면 된다.


## 참고자료
[[네트워크] TCP/UDP와 3 -Way Handshake & 4 -Way Handshake](https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake)  
[[네트워크] TCP 3-way & 4-way handshake란?](https://seongonion.tistory.com/74)