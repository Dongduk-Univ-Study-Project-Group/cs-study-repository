>RDBMS vs NOSQL에 대해서 설명해주세요.
## RDBMS vs NOSQL
### RDBMS
- 다른 테이블들과 관계를 맺고 모여있는 집합체로 이해할 수 있다.
- 이러한 관계를 나타내기 위해 **외래 키(foreign key)라는 것을 사용한 테이블 간 Join이 가능**
- 장점: 정해진 스키마에 따라 데이터가 저장되므로 데이터 구조가 명확하고, 각 관계를 따라 저장된 데이터는 중복 없음이 보장된다.
- 단점: 테이블 간 관계로 얽혀 있어 시스템이 커진다면 쿼리가 복잡해질 수 있다.

### NoSQL
- RDBMS와는 달리 테이블 간 관계를 정의하지 않는다.
- 데이터 테이블은 그냥 하나의 테이블이며 따라서 일반적으로 테이블 간 Join도 불가능. 
- 빅데이터의 등장으로 인해 데이터와 트래픽이 기하급수적으로 증가함에 따라 RDBMS에 단점인 성능을 향상시키기 위해 등장.
- 장점: 스키마가 없기 떄문에 데이터 구조가 자유롭다. 데이터 분산이 용이 -> 대량의 데이터를 빠르게 처리해야 하는 요즘 상황에 적합할 수 있다.
- 단점: 데이터 중복 문제가 발생할 수 있고 스키마가 존재하지 않으므로 데이터 구조가 명확하지 않다.

> 어떤 기준으로 DB를 선택할 수 있죠?

- 데이터베이스를 구축하는 방법을 선택하는 것에 완벽한 솔루션은 없다. 그렇기 때문에 많은 개발자들은 유저의 요구를 충족하기 위해 관계형, 비관계형 데이터베이스를 모두 사용하여 서비스에 맞게 설계하고 있다.
- NoSQL 기반의 비관계형 데이터베이스는 확장성이나 속도면에서 더 뛰어나다. 또한 막대한 데이터를 저장해야 할 필요가 있고 작성 속도가 빨라야 하는 데이터 분석, 빠른 트로토타입 작업 등에서 사용할 수 있다.
- RDBMS는 데이터 구조가 명확하고 명확한 스키마가 중요할 때 사용할 수 있다. 데이터 중복이 없음이 보장된다.

> 각 DB를 사용하는 케이스를 자세히 들어주세요.  

#### SQL 기반의 관계형 데이터베이스를 사용하는 케이스  
    1.  데이터베이스의 ACID 성질을 준수해야 하는 경우  
    2. 소프트웨어에 사용되는 데이터가 구조적이고 일관적인 경우  

#### NoSQL 기반의 비관계형 데이터베이스를 사용하는 케이스  
    1. 데이터의 구조가 거의 또는 전혀 없는 대용량의 데이터를 저장하는 경우  
    2. 클라우드 컴퓨팅 및 저장공간을 최대한 활용하는 경우  
    3. 빠르게 서비스를 구축하는 과정에서 데이터 구조를 자주 업데이트 하는 경우  

## 참고자료
[[데이터베이스] SQL(구조화 쿼리 언어) vs NoSQL(비구조화 쿼리 언어)](https://hanamon.kr/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-sql-vs-nosql/)