# 트랜잭션의 ACID

### 원자성 (Atomicity)
한 트랜잭션 내에서 실행한 작업들은 하나의 작업으로 간주한다. 모두 성공 또는 모두 실패되어야 한다. 

### 일관성 (Consistency) 
모든 트랜잭션은 일관성 있는 데이타베이스 상태를 유지한다. 이를테면 DB에서 정한 무결성 조건을 항상 만족.

### 격리성 (Isolation)
동시에 실행되는 트랜잭션들이 서로 영향을 미치지 않도록 격리 해야한다.

### 지속성 (Durability)
트랜잭션을 성공적으로 마치면 그 결과가 항상 저장되어야 한다.


## 트랜잭션 격리 수준 (Isolation Level)
트랜잭션이 발생하면 락(Lock)이 걸리는데, 
SELECT 시에는 공유 락, CREATE/INSERT/DELETE 시에는 배타적 락이 걸린다


격리성을 완벽히 보장하기 위해 모든 트랜잭션을 순차적으로 실행한다면 동시성 처리 이슈가 발생한다. 
반대로 동시성을 높이기 위해 여러 트랜잭션을 병렬처리하게 되면 데이터의 무결성이 깨질 수 있다.

격리수준이라는 말을 이해하면 좀 더 좋을것 같은데
트랜잭션 간 얼마나 `고립되어있는가` 를 생각하면 좋을것 같다. 

즉, 간단하게 말해 특정 트랜잭션이 다른 트랜잭션에 변경한 데이터를 볼 수 있도록 허용할지 말지를 결정하는 것이다.

고립 정도가 높아지면 성능이 떨어진다.
따라서 충분한 이해를 하고 써야함

디폴트 설정
oracle = READ COMMITTED, mysql = REPEATABLE READ

## 격리성 관련 문제점
### Dirty Read 
한 트랜잭션(T1)이 데이타에 접근하여 값을 'A'에서 'B'로 변경했고 아직 커밋을 하지 않았을때, 
다른 트랜잭션(T2)이 해당 데이타를 Read 하면?

T2가 읽은 데이타는 B가 될 것이다. 

하지만 T1이 최종 커밋을 하지 않고 종료된다면, T2가 가진 데이타는 꼬이게 된다.

### Non-Repeatable Read
한 트랜잭션(T1)이 데이타를 Read 하고 있다. 
이때 다른 트랜잭션(T2)가 데이타에 접근하여 값을 변경 또는, 데이타를 삭제하고 커밋을 하면?

그 후 T1이 다시 해당 데이타를 Read하고자 하면 변경된 데이타 혹은 사라진 데이타를 찾게 된다.

### Phantom Read
트랜잭션(T1) 중에 특정 조건으로 데이타를 검색하여 결과를 얻었다. 
이때 다른 트랜잭션(T2)가 접근해 해당 조건의 데이타 일부를 삭제 또는 추가 했을때, 
아직 끝나지 않은 T1이 다시 한번 해당 조건으로 데이타를 조회 하면 T2에서 추가/삭제된 데이타가 함께 조회/누락 된다. 

그리고 T2가 롤백을 하면? 데이타가 꼬인다

## 격리 수준 

### Read uncommitted
### Read committed
### Repeatable reads
### Serializable


------------
| Isolation Level	| Dirty Read	| Non repeatable Read | Phantom Read |
| --- | ----| ------| ------ |
| READ UNCOMMITTED	| Permitted	| Permitted | Permitted |
| READ COMMITTED	| — | Permitted	| Permitted |
| REPEATABLE READ	| — | — | Permitted |
| SERIALIZABLE | — | — | — |
------------

## 참고
* https://feco.tistory.com/45
* https://nesoy.github.io/articles/2019-05/Database-Transaction-isolation
