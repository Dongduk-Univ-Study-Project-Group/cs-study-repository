## TCP 3, 4 way Handshake

### TCP 3 way Handshake
연결하고자 하는 두 장치 간의 가상회선을 수립하는 단계이다.  
클라이언트는 서버에 요청을 전송할 수 있는지, 서버는 클라이언트에게 응답을 전송할 수 있는지 확인하는 과정이다.  
SYN, ACK 패킷을 주고받으며, 임의의 난수로 SYN 플래그를 전송하고, ACK 플래그에는 1을 더한값을 전송한다. 
+ SYN (synchronize sequence numbers) : 연결 확인을 위해 보내는 무작위의 숫자값
+ ACK (acknowledgements) : Client 혹은 Server로부터 받은 SYN에 1을 더해 SYN을 잘 받았다는 ACK
정확한 순서는 SYN(n) -> ACK(n + 1), SYN(m) -> ACK(m + 1) 순으로 일어난다.

#### 임의의 난수를 지정하는 이유 
Connection을 맺을 때 사용하는 포트는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용된다.
따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용할 가능성이 존재한다.

서버 측에서 패킷의 SYN을 보고 패킷을 구분하게 되는데 난수가 아닌 순차적인 숫자가 전송된다면 이전의 connection으로부터 오는 패킷으로 인식할 수 있어 
이러한 문제 발생 가능성을 줄이기 위해 ISN을 무작위 난수로 사용하는 것이다.

### TCP 4 way Handshake
TCP연결을 해제하는 단계로, 
클라이언트는 서버에게 연결해제를 통지하고 
서버가 이를 확인하고 클라이언트에게 이를 받았음을 전송해주고 최종적으로 연결이 해제된다. 
FIN(C2S) -> ACK(S2C) -> FIN(S2C) -> ACK(C2S), TIME-WAIT
+ FIN (Finish) : TCP 연결을 종료하겠다는 메시지
+ TIME-WAIT : 먼저 연결을 끊는 (active closer) 쪽에 생성되는 소켓으로, 혹시 모를 패킷 전송 실패에 대비하기 위하여 존재하는 소켓이다.

#### Time-wait 이 없다면?
패킷의 손실이 발생하거나 통신자 간 연결 해제가 제대로 이루어지지 않을 수 있다
+ Passive Closer의 FIN 메시지 전송
+ Active Closer가 수신 후 ACK 메시지 전송 후, 통신 끊음 (Time-wait X)
+ Passive Closer가 ACK를 수신하지 못함
+ 일정 시간 후, ACK를 수신하지 못한 Passive Closer가 다시 FIN 메시지 전송.
+ Active Closer는 이미 Closed 상태이기 때문에 FIN 메시지 수신 불가

-> TCP 통신이 제대로 끊기지 않음