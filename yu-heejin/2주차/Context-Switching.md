> 멀티프로세스 환경에서 CPU가 어떤 하나의 프로세스를 실행하고 있는 상태에서 **인터럽트 요청에 의해 다음 우선순위의 프로세스가 실행되어야 할 때, 기존의 프로세스의 상태 또는 레지스터 값(Context)을 저장하고, CPU가 다음 프로세스를 수행하도록 새로운 프로세스의 상태 또는 레지스터 값을 교체**하는 작업
> 

## 컨텍스트란?

- CPU가 해당 프로세스를 실행하기 위한 **해당 프로세스의 정보들**
- 운영체제에서 Context는 CPU가 해당 프로세스를 실행하기 위한 해당 프로세스의 정보들을 말한다.
- 컨텍스트는 프로세스의 PCB(Process Control Block)에 저장된다.
    - 따라서 Context Switching 때 PCB의 정보를 읽어(적재) CPU가 전에 프로세스가 일 하던 것을 이어서 수행 가능하다.
- 컨텍스트 스위칭 시 해당 CPU는 아무 작업을 하지 못하며, 오버헤드가 발생하기 때문에 효율이 떨어진다.

## 인터럽트(Interrupt)

- 인터럽트는 CPU가 프로그램을 실행하고 있을 때 실행중인 프로그램 밖에서 예외 상황이 발생하여 처리가 필요한 경우, CPU에게 알려 예외 상황을 처리할 수 있도록 하는 것

### 컨텍스트 스위칭이 발생하는 인터럽트 요청

1. I/O request (입출력 요청)
2. time slice expired (CPU 사용 시간 만료)
3. fork a child (자식 프로세스 생성)
4. wait for an interrupt (인터럽트 처리를 기다릴 때)

- 이러한 컨텍스트 스위칭이 일어날 때, 다음번 프로세스는 스케줄러가 결정하게 된다.
- 즉, 컨텍스트 스위칭을 하는 주체는 스케줄러!

## 컨텍스트 스위칭이란?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d9732e26-abd6-4078-a3d4-fd1f077e2e63/Untitled.png)

- 여러개의 프로세스가 실행되고 있을 때, 기존에 실행되던 프로세스를 중단하고 다른 프로세스를 실행하는 것
    - 간단히 말해 CPU에 실행할 프로세스를 교체하는 기술
- CPU가 어떤 프로세스를 실행하고 있는 상태에서 인터럽트에 의해 다음 우선 순위를 가진 프로세스가 실행되어야할 때, **기존의 프로세스 정보들은 PCB에 저장하고, 다음 프로세스의 정보를 PCB에서 가져와 교체하는 작업**
- 이러한 컨텍스트 스위칭을 통해 멀티 프로세싱, 멀티 스레딩 운영이 가능하다.
- 컨텍스트 스위칭은 ms의 짧은 시간 단위로 일어나지만, 과도하게 많이 일어날 경우 오버헤드가 발생하게 된다.
    - 따라서 컨텍스트 스위칭 코드는 어셈블리어로 작성되어있는 경우가 많다.
- 아래 그림을 통해 더 자세히 살펴보자.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0e2bbbf5-1f39-4dd3-a830-2a45ad01d8b8/Untitled.png)
    
    - 프로세스 p0과 p1이 존재할 때, p0이 CPU를 점유중이고, p1이 대기중인 상태에서 얼마 후 p1이 실행되고 p0은 대기 상태가 된다.
    - 이때, p0이 실행중인 상태에서 대기로 변하게 될 때 지금까지 작업해오던 내용을 모두 어딘가에 저장해야하는데, 그것이 PCB
    - 즉, p0은 PCB에 저장해야하고, P1이 가지고 있던 데이터는 PCB에서 가져와야 한다.
    - 이러한 과정을 번갈아가며 실행하는 것을 컨텍스트 스위칭이라 한다.

### 컨텍스트 스위칭이 발생하는 상황

1. I/O interrupt
2. CPU 사용시간 만료
3. 자식 프로세스 Fork
4. 인터럽트 처리를 기다릴 때

## PCB(Process Control Block)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/591cc41f-4f08-4cce-b2a3-2790d04f3351/Untitled.png)

- 컨텍스트 스위칭은 **PCB 라고 하는 메모리의 별도 공간**에 process 상태 값들을 저장하고, 해당 값들을 찾는 방법으로 구현된다.
- PCB는 쉽게 말해 프로세스가 실행중인 상태를 스냅샷으로 찍어 저장하는 공간이라고 생각하면 된다.

### PCB에 저장되는 내용

![스크린샷 2023-01-22 오후 8.39.01.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/92404912-abfe-444c-b68a-062a7eb1f6e4/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-01-22_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_8.39.01.png)

- Process ID (PID)
- 레지스터 값 (PC, SP 등)
- Sheduling info (프로세스 상태)
- Memory info (메모리 사이즈 limit) - 전체 프로세스 사이즈 등

## 컨텍스트 스위칭 작동 순서

![스크린샷 2023-01-22 오후 8.39.48.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8dce2aa2-47a6-44f7-af41-41038eacfe2f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-01-22_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_8.39.48.png)

A 프로세스가 running 상태이고, B 프로세스가 ready 상태라고 가정하자.

1. 스케줄러가 A 프로세스의 실행을 중단하고 B 프로세스를 실행할 것을 요청한다.
2. A 프로세스에서 Stack의 데이터 위치를 가리키고 있는 SP(Stack Pointer)의 값과 다음 실행해야하는 코드의 주소값을 가지고 있는 PC(Program Counter)의 값을 PCB에 저장한다. (운영체제에서 관리)
    1. SP와 PC는 모두 중앙처리장치 안의 레지스터이다.
3. A 프로세스는 ready 또는 block 상태로 바뀌고, CPU에서 B 프로세스를 실행한다.
    1. 위 과정을 통해 B 프로세스의 상태가 ready에서 running으로 바뀌는데, 이 작업을 **디스패치(dispatch)**라고 한다.
4. 반대로 다시 B 프로세스에서 A 프로세스로 컨텍스트 스위칭을 할 경우, B프로세스의 SP 값과 PC 값을 PCB에 저장하고, (이 때 PCB는 A 프로세스의 위치값을 저장하는 PCB와는 별도로 생성되는 메모리 공간이다.) A 프로세스의 PCB에서 SP 값과 CP 값을 찾아 SP와 PC에 덮어 씌운다.

## 스레드 vs 프로세스

- 스레드가 프로세스보다 빠른 이유도 컨텍스트 스위칭이 한 몫 한다.
- 스레드는 컨텍스트 스위칭될 때 text, data, heap 영역은 프로세스 것이기 때문에, 자신의 PCB에는 스택 및 간단한 정보만 저장하므로 프로세스 스위칭보다 빠르다.

## [추가] 우선 순위

- 우선 순위는 해당 OS의 스케줄러가 우선 순위 알고리즘에 의해 정해지고 수행하게 되어있다.
- 라운드로빈 스케줄링은 시분할 시스템을 위해 설계된 선점형 스케줄링의 하나이다.
    - 쉽게 설명하자면, 순서대로 시간 단위(Time Quantum)를 CPU에 할당하는 방식이다.
    - 꽤 효율적인 스케줄링 알고리즘이지만, 이 시간 단위를 작게 설정하면 CPU가 조금 일하고 Context Switching을 반복하므로 아까 말했듯이 효율이 떨어진다.

## 참고 자료

- [https://applefarm.tistory.com/105](https://applefarm.tistory.com/105)
- [https://hyunie-y.tistory.com/31](https://hyunie-y.tistory.com/31)
- [https://jeong-pro.tistory.com/93](https://jeong-pro.tistory.com/93)
- [https://www.crocus.co.kr/1364](https://www.crocus.co.kr/1364)