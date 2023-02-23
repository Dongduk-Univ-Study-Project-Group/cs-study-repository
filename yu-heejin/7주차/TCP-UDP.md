> TCP는 연결 지향형 프로토콜이고 UDP는 데이터를 데이터그램단위로 전송하는 프로토콜입니다.
> 

> TCP는 가상 회선을 만들어 신뢰성을 보장하도록(흐름 제어, 혼잡 제어, 오류 제어) 하는 프로토콜로 따로 신뢰성을 보장하기 위한 절차가 없는 UDP에 비해 속도가 느린편입니다.
> 

> TCP는 그래서 파일전송과 같은 신뢰성이 중요한 서비스에 사용되고, UDP는 스트리밍, RTP와 같이 연속성이 더 중요한 서비스에 사용됩니다.
> 

> +) 하지만 UDP도 신뢰성을 UDP자체에서 보장하지 않는 것 뿐이지, 개발자가 직접 신뢰성을 보장하도록 할 수 있습니다. 그래서 HTTP/3은 QUIC이라는 프로토콜을 기반으로 하는데, QUIC은 UDP를 기반으로 합니다. 즉, UDP 자체는 신뢰성을 보장하지 않지만, 추가적인 정의를 통해 신뢰성을 보장받을 수 있습니다.
> 

---

## TCP (Transmission Control Protocol)

- 연결 지향적 프로토콜
    - 클라이언트와 서버가 연결된 상태에서 데이터를 주고받는 프로토콜을 의미한다.
- 장치들 사이의 논리적인 접속을 성립하기 위해 **연결을 설정해 신뢰성을 보장하는 연결형 서비스이다.**
- 네트워크에 연결된 컴퓨터에서 실행되는 프로그램 간에 일련의 옥텟(데이터, 메시지, 세그먼트 등의 블록 단위)을 안정적으로, 순서대로, 에러 없이 교환할 수 있게 해준다.

### 특징

> TCP는 연결형 서비스, 신뢰성을 보장하기 때문에 다음과 같은 특징을 가진다.
> 
1. 연결형 서비스로 가상 회선 방식 제공
    1. 3 way handshaking 과정을 통해 연결을 설정
        1. 발신지와 수신지 사이에 논리적인 접속(세션)을 성립하는 과정
    2. 4 way handshaking 과정을 통해 연결을 해제
    3. 가상 회선 방식
        1. 발신지와 수신지를 연결하여 패킷을 전송하기 위한 논리적 경로를 배정한다는 의미
2. 흐름 제어(Flow Control)
    1. 데이터 처리 속도를 조절하여 수신자의 버퍼 오버플로우를 방지
3. 혼잡 제어(Congestion Control)
    1. 네트워크 내의 패킷 수가 과도하게 증가하지 않도록 방지
4. 높은 신뢰성을 보장
    1. 신뢰성이 높은 전송을 하기 때문에 UDP보다 속도가 느리다.
5. 전이중(Full-Duplex), 점대점(Point to Point) 방식
    1. 전이중 : 전송이 양방향으로 동시에 일어날 수 있다.
    2. 점대점 : 각 연결이 정확히 2개의 종단점을 갖고 있다.

### 연결 과정(3-way handshake)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/121caa3a-0f40-4653-8be3-009b61453838/Untitled.png)

- SYN(synchronize sequence numbers)
    - 연결 확인을 보내는 무작위의 숫자 값
- ACK(ackonwledgements)
    - 클라이언트 혹은 서버로부터 받은 SYN에 1을 더해 SYN을 잘 받았다는 ACK

![스크린샷 2023-02-23 오전 8.48.53.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/16659eff-289d-4363-ad09-4af13bc103e3/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-02-23_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_8.48.53.png)

1. 먼저 Open한 클라이언트가 SYN을 보내고 SYN_SENT 상태로 대기한다.
2. 서버는 SYN-RECEIVED 상태로 바꾸고 SYN과 응답 ACK을 보낸다.
3. SYN과 응답 ACK를 받은 클라이언트는 ESTABLISHED 상태로 변경하고, 서버에게 응답 ACK을 보낸다.
4. 응답 ACK를 받은 서버는 ESTABLISHED 상태로 변경한다.

### 연결 해제 과정(4-way handshake)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d4632d47-5426-4929-be73-9a8ee0922ccc/Untitled.png)

![스크린샷 2023-02-23 오전 8.55.42.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9bc86e4b-2633-44c4-82c2-2cf7d1edff54/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-02-23_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_8.55.42.png)

1. 먼저 close를 실행한 클라이언트가 FIN을 보내고 FIN-WAIT-1 상태로 대기한다.
2. 서버는 CLOSE-WAIT로 바꾸고, 응답 ACK를 전달한다.
    1. 동시에 해당 포트에 연결되어 있는 애플리케이션에게 close를 요청한다.
3. ACK을 받은 클라이언트는 상태를 FIN-WAIT-2로 변경한다.
4. close 요청을 받은 서버 애플리케이션은 종료 프로세스를 진행하고 FIN을 클라이언트로 보내 LAST_ACK 상태로 바꾼다.
5. FIN을 받은 클라이언트는 ACK를 다시 전송하고, TIME-WAIT로 상태를 바꾼다.
    1. TIME-WAIT에서 일정 시간이 지나면 CLOSE된다. ACK을 받은 서버도 포트를 CLOSED로 닫는다.
    2. TIME-WAIT
        1. 먼저 연결을 끊는 쪽에서 생성되는 소캣으로, 혹시 모를 전송 실패에 대비하기 위해 존재하는 소캣이다.
        2. TIME-WAIT이 없다면, 패킷의 손실이 발생하거나 통신사 간 연결 해제가 제대로 되지 않을 수 있다.

## UDP(User Datagram Protocol)

- 비연결형 프로토콜
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6ec4bafa-10b4-4a60-8218-6e1fef8699a3/Untitled.png)
    
    - 연결을 위해 할당되는 논리적인 경로가 없고, 각각의 패킷은 다른 경로로 전송되며 독립적인 관계를 지닌다.

### 특징

1. 비연결형 서비스로 데이터그램 방식을 제공한다.
    1. 데이터의 전송 순서가 바뀔 수 있다.
    2. 비연결형 서비스이기 때문에 연결을 설정하고 해제하는 과정이 존재하지 않는다.
    3. 서로 다른 경로로 독립적으로 처리한다.
2. 데이터의 수신 여부를 확인하지 않는다.
    1. TCP 3-way handshaking과 같은 과정을 거치지 않는다.
3. 신뢰성이 낮다.
    1. 흐름 제어가 없기 때문에 제대로 전송되었는지, 오류가 없는지 확인할 수 없다.
    2. 흐름제어, 혼잡 제어 같은 기능을 처리하지 않기 때문에 TCP보다 속도가 빠르고 네트워크 부하가 적다는 장점이 있다.
4. TCP보다 속도가 빠르다.
5. 1:1 & 1:N & N:N 통신이 가능하다.
6. 신뢰성보다는 연속성 있는 전송이 필요할 때 사용하는 프로토콜로, 실시간 서비스(streaming)에 자주 사용된다.

## TCP vs UDP

![TCP](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/68380960-40c7-4d88-91bf-ae3380c31a2d/Untitled.png)

TCP

![스크린샷 2023-02-23 오전 9.01.57.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/53e10639-9286-4827-a0c3-8619331afc98/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-02-23_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_9.01.57.png)

- TCP는 연속성보다 신뢰성 있는 전송이 중요할 때 사용되는 프로토콜
- UDP는 TCP보다 빠르고 네트워크 부하가 적다는 장점이 있지만, 신뢰성 있는 데이터 전송을 보장하지 않는다.
    - 신뢰성보다는 연속성이 중요한 실시간 스트리밍 서비스에 자주 사용된다.

## 참고 자료

- [https://dev-coco.tistory.com/144](https://dev-coco.tistory.com/144)