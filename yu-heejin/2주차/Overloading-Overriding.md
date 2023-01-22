> 자바에서는 다형성을 지원하는 방법으로 메서드 오버로딩과 오버라이딩이 있다.
> 

## 오버로딩(Overloading)

- **같은 이름의 메서드 여러개**를 가지면서 **매개변수의 유형과 개수가 다르도록** 하는 기술
- 하나의 메서드 이름으로 여러 기능을 구현할 수 있다.
- 자바의 한 클래스 내에 이미 사용하려는 이름과 같은 이름을 가진 메서드가 있더라도, **매개변수의 개수나 타입이 다르면 같은 이름을 사용하여 메소드를 정의할 수 있다.**
- 사용 예시
    
    ```java
    class OverloadingTest{
        //이름이 cat인 메서드
        void cat(){
            System.out.println("매개변수 없음");
        }
        
        //매개변수 int형이 2개인 cat 메서드
        void cat(int a, int b){
            System.out.println("매개변수 :"+a+", "+b);
        }
        
        //매개변수 String형이 한 개인 cat 메서드
        void cat(String c){
            System.out.println("매개변수 : "+ c);
        }
        
    }
     
    public class OverTest {
        public static void main(String[] args) {
            
            //OverloadingTest 객체 생성
            OverloadingTest ot = new OverloadingTest();
            
            //매개변수가 없는 cat() 호출
            ot.cat();
            
            //매개변수가 int형 두개인 cat() 호출
            ot.cat(20, 80);
            
            //매개변수가 String 한개인 cat() 호출
            ot.cat("오버로딩 예제입니다.");
            
        }
     
    }
    ```
    

### 오버로딩의 장점

1. 같은 기능을 하는 메소드를 하나의 이름으로 사용할 수 있다.
2. 메소드의 이름을 절약할 수 있다.

## 오버라이딩(Overriding)

- 상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의해서 사용한다.
- 뿐만 아니라 하위 클래스에서 메서드를 재정의해서도 사용할 수 있다.
- 메서드의 이름이 서로 같고, 매개변수, 반환형이 같은 경우 상속받은 메서드를 덮어쓴다.
- 부모 클래스로부터 상속받은 메소드를 자식 클래스에서 재정의하는 것
    - 상속 받은 메소드를 그대로 사용할 수도 있지만, 자식 클래스에서 상황에 맞게 변경해야하는 경우 오버라이딩이 필요다.
- 사용 예시
    
    ```java
    class Woman{ //부모클래스
        public String name;
        public int age;
        
        //info 메서드
        public void info(){
            System.out.println("여자의 이름은 "+name+", 나이는 "+age+"살입니다.");
        }
        
    }
     
    class Job extends Woman{ //Woman클래스(부모클래스)를 상속받음 : 
     
        String job;
        
        public void info() {//부모(Woman)클래스에 있는 info()메서드를 재정의
            super.info();
            System.out.println("여자의 직업은 "+job+"입니다.");
        }
    }
     
    public class OverTest {
     
        public static void main(String[] args) {
            
            //Job 객체 생성
            Job job = new Job();
            
            //변수 설정
            job.name = "유리";
            job.age = 30;
            job.job = "프로그래머";
            
            //호출
            job.info();
            
        }
     
    }
    ```
    

## 오버로딩과 오버라이딩 성립 조건

| 구분 | 오버로딩 | 오버라이딩 |
| --- | --- | --- |
| 메서드 이름 | 동일 | 동일 |
| 매개변수, 타입 | 다름 | 동일 |
| 리턴 타입 | 상관 없음 | 동일 |
- 오버로딩 조건에서 **리턴 값만** 다른 것은 오버 로딩이 불가능하다.
- 또한, 오버로딩에서 접근 제어자도 자유롭게 지정할 수 있다.
    - 다만 접근 제어자만 다르게 한다고 오버로딩이 가능한 건 아니다.
- 결론적으로, **오버로딩은 매개변수의 차이로만 구현할 수 있다.**
- 오버라이딩은 부모 클래스의 메소드를 재정의하는 것이기 때문에, **자식 클래스에서는 오버라이딩하고자 하는 메소드의 이름, 매개변수, 리턴 값이 모두 똑같아야 한다.**

## @Override

- 오버라이딩을 검증하는 기능을 한다.
- 코드 상으로 검사했을 때 오버라이딩이 실제로 시행되지 않았다면 컴파일 시 오류를 출력한다.
- 부모 클래스의 메소드를 오버라이딩 하는 것은 **내용만을 새로 정의**하는 것이기 때문에 **선언부는 부모의 것과 완벽히 동일해야한다.**

## 오버라이딩 접근 제어자 설정 규칙

1. 자식 클래스에서 오버라이딩하는 메소드의 접근 제어자는 부모 클래스보다 더 좁게 설정할 수 없다.
2. 예외(Exception)는 부모 클래스의 메소드보다 많이 선언할 수 없다.
    1. 부모 클래스에서 어떤 예외를 throws 한다고 한다면, 자식 클래스에서는 그 예외보다 더 큰 범위의 예외를 throws 할 수 없다는 의미
3. static 메소드를 인스턴스의 메소드로 또는 그 반대로 바꿀 수 없다.
    1. 부모 클래스의 static 메소드를 자식에서 같은 이름으로 정의할 수 있지만, 이것은 다시 정의하는 것이 아니라 같은 이름의 static 메소드를 새로 정의하는 것이다.

## 참고 자료

- [https://private.tistory.com/25](https://private.tistory.com/25)
- [https://hyoje420.tistory.com/14](https://hyoje420.tistory.com/14)