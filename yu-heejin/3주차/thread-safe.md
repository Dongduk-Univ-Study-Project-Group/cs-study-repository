> 두 개 이상의 스레드가 race condition에 들어가거나 같은 객체에 동시에 접근해도 연산결과의 정합성이 보장될 수 있게끔 메모리 가시성이 확보된 상태를 의미합니다.
> 
- java.util.concurrent 패키지 하위의 클래스를 사용합니다.
- 인스턴스 변수를 두지 않습니다.
- Singleton 패턴을 사용합니다.(이 때, 일반적으로 구현하는 Singleton Pattern은 Thread-safe 하지 않습니다.)[참고]([https://github.com/ksundong/TIL/blob/master/DesignPattern/singleton-pattern.md](https://github.com/ksundong/TIL/blob/master/DesignPattern/singleton-pattern.md))
- 동기화(syncronized) 블럭에서 연산을 수행합니다.

---

## Thread Safe란?

- 멀티 스레드 프로그래밍에서, 어떤 공유 자원에 여러 스레드가 동시에 접근해도, 프로그램 실행에 문제가 없는 상태
    - 멀티 스레드 프로그래밍에서 일반적으로 어떤 함수나 변수, 객체가 여러 스레드로부터 동시에 접근이 이루어져도 프로그램 실행에 문제가 없음을 의미
    - 하나의 함수가 한 스레드로부터 호출되어 실행 중일 때, **다른 스레드가 그 함수를 호출하여 동시에 함께 실행되더라도 각 스레드에서의 함수의 수행 결과가 올바로 나오는 것으로 정의한다.**
- 두 개 이상의 스레드가 race condition에 들어가거나 같은 객체에 동시에 접근해도 연산 결과는 정합성이 보장될 수 있게 메모리 가시성이 확보된 상태
- Thread Safe 하지 않은 코드에는 다음 코드가 있다.
    
    ```java
    int num;
    boolean is_even;
    
    int inc(int n) {
    	num += n;
    
    	if ((num % 2) == 0)
    		is_even = true;
    	else
    		is_even = false;
    
    	return num;
    }
    ```
    
    - 싱글 스레드에서는 문제가 없지만, 멀티 스레드 환경에서는 문제를 발생시킬 수 있다.
    - 만약 두개의 스레드가 해당 코드를 동시에 수행한다고 가정하자.
        
        ```java
        a = inc(1);
        ```
        
        1. 먼저 1번 스레드가 다음 라인까지 수행한다.
            
            ```java
            num += n;   // num: 1, n: 1
            
            if ((num % 2) == 0)
            ```
            
            - NUM이 1인 상황에서 1을 더했으니 num % 2는 0이다.
        2. 그 후 is_even에 true를 설정하기 바로 직전 다른 스레드가 다음 코드를 수행했다고 하자.
            
            ```java
            num += n;   // 2 + 1 = 3
            ...
            else
            	is_even = false;
            
            return num;
            ```
            
            - 1번 쓰레드가 num을 2로 세팅했기 때문에 num += n을 계산하면 3이 된다.
            - 3은 홀수이므로 is_even = false
        3. 이때, 다시 1번 스레드가 수행되어 is_even = true;를 수행한다.
    - 위와 같은 과정을 거치면 num의 값은 3인데 is_even은 true이다.
    - 따라서 의도와는 다른 결과가 나왔으므로 Thread-Safe하지 않다.

## 스레드 안전의 여부 판단 방법

1. 전역 변수나 힙, 파일과 같이 여러 스레드가 동시에 접근할 수 있는 자원을 사용하는가?
2. 핸들과 포인터를 통한 데이터의 간접 접근이 가능한가?
3. 부수 효과를 가져오는 코드가 있는가?

## Thread Safe를 지키기 위한 방법

### Mutual Exclusion (상호 배제)

- 공유 자원에 하나의 스레드만 접근할 수 있도록, 세마포어/뮤텍스로 lock을 통제하는 방법
    - 일반적으로 가장 많이 사용하는 방식이다.
- 예를 들어, 파이썬은 Thread Safe하게 메모리를 관리하지 않기 때문에 GIL(Global Interpreter Lock)을 사용해 Thread Safe를 보장한다.
- 공유 자원을 꼭 사용해야 할 경우 해당 자원의 접근을 세마포어 등의 락으로 통제한다.

### Atomic Operation (원자 연산)

- 공유 자원에 원자적으로 접근하는 방법
- 공유 자원에 접근할 때 원자 연산을 이용하거나 원자적으로 정의된 접근 방법을 사용함으로써 상호 배제를 구현할 수 있다.
- Atomic
    - 공유 자원 변경에 필요한 연산을 원자적으로 분리한 후, 실제로 데이터의 변경이 이루어지는 시점에 Lock을 걸고, 데이터를 변경하는 시간 동안 다른 쓰레드의 접근이 불가능하도록 하는 방법

### Thread-local storage (쓰레드 지역 저장소)

- 공유 자원의 사용을 최대한 줄이고, 각각의 스레드에서만 접근 가능한 저장소들을 사용함으로써 동시 접근을 막는 방법
- 일반적으로 공유 상태를 피할 수 없을 때 사용하는 방식
- 이 방식은 동기화 방법과 관련되어 있고, 공유 상태를 피할 수 없을 때 사용하는 방식이다.
- 전역 변수 사용을 자제하라는 의미

### Re-entrancy (재진입성)

- 쓰레드 호출과 상관 없이 프로그램에 문제가 없도록 작성하는 방법
- 어떤 함수가 한 스레드에 의해 호출되어 실행 중일 때, 다른 스레드가 그 함수를 호출하더라도 그 결과가 각각에게 올바로 주어져야 한다.
- 즉, 스레드끼리 독립적으로 동작할 수 있도록 코드를 짤 것

## Java에서 Thread-Safe하게 설계하는 방법

- java.util.concurrent 패키지 하위의 클래스를 사용한다.
- 인스턴스 변수를 두지 않는다.
- 싱글톤 패턴 사용
    - 일반적으로 구현하는 싱글톤 패턴은 스레드 안전하지 않는다.
- 동기화(Syncronized) 블럭에서 연산을 수행한다.

### 싱글톤 패턴

- 싱글톤 패턴이란 애플리케이션이 시작되고 하나의 클래스 인스턴스를 보장해서 전역적인 접근점을 제공하는 패턴
- 장점
    - 전역 변수를 사용하지 않기 때문에 디버깅이 쉽고, 네임 스페이스가 망가지는 일이 없다.
    - 유일하게 존재하는 인스턴스로의 접근으로 통제가 가능하며, 데이터 공유가 쉬워진다.
- 단점
    - 싱글톤 인스턴스가 너무 많은 일을 하거나 너무 많은 데이터를 가질 경우 결합도가 높아진다.
    - 멀티스레드 환경에서 동기화 처리를 하지 않으면 여러 개가 생성될 수 있다.

### 멀티 스레드 환경에서 안전한 싱글톤 인스턴스 만들기

- 게으른 초기화(Syncronized 블록 사용)
    - 속도가 느려서 권장되지 않는다.
- Double-Check Locking
    - if문으로 존재 여부 체크하고, Syncronized 블록을 사용하는 방법
    - 어느정도 문제 해결은 가능하나 완벽하지 않다.
- Holder에 의한 초기화
    - 클래스 안에 클래스(Holder)를 두어, JVM Class Loader 매커니즘을 이용한 방법
    - 개발자가 직접 동기화 문제를 해결하기 보다는 JVM의 원자적인 특성을 이용해 초기화의 책임을 JVM으로 이동하는 방법
    - 일반적으로 Singletone을 이용하는 방법
- [참고] 스프링에서는 이런 싱글톤 패턴을 통해 빈을 관리하는데 있어서 복잡해지는 것을 방지하기 위해 싱글톤 레지스트리인 Application Context를 가지고 있다.

## 참고 자료

- [https://wooono.tistory.com/523](https://wooono.tistory.com/523)
- [https://gompangs.tistory.com/entry/OS-Thread-Safe란](https://gompangs.tistory.com/entry/OS-Thread-Safe%EB%9E%80)
- [https://developer-ellen.tistory.com/205](https://developer-ellen.tistory.com/205)
- [https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=complusblog&logNo=220985528418](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=complusblog&logNo=220985528418)
- [https://steadily-worked.tistory.com/577](https://steadily-worked.tistory.com/577)