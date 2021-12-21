# SQL VS NOSQL

## ✨ SQL? NOSQL?

> SQL이란 SQL(Structured Query Language)로 원래의 의미는 RDB의 Query Language이지만, RDB에서만 쓰이므로 RDB를 SQL이라고 말하기도한다. 여기서도 SQL == RDB로 쓰겠다. 그리고, MySQL(SQL), MongoDB(NoSQL)기준으로 설명한다.
> 

### SQL

<aside>
💡 SQL은 스키마와 제약 조건을 중심으로 **일관성 있는 데이터를 중요시**하는 관계형 데이터베이스를 말한다.

</aside>

> 여기서 일관성이란 RDB는 데이터의 중복 저장을 피하기 위해서 여러 데이터를 여러 테이블에 분산하여 저장하고 관계를 정해줌으로써 지켜준다.
> 
- 모델링의 순서가 [ 테이블 → 쿼리 ]로, 테이블의 형태를 먼저 정하고 그에 맞는 쿼리를 작성하게 된다.
    
    > 이런 점은 데이터의 일관성을 중요시하는 RDB의 컨셉때문이다.
    > 

### NOSQL

<aside>
💡 NOSQL(Not only SQL)은 유연한 스키마를 통해서 **효율적인 쿼리를 중요시**하는 비관계형 데이터베이스를 말한다.

</aside>

> NoSQL은 데이터를 중복 저장하지만, 내가 원하는 정보를 한개의 document에 모두 담을 수 있다. 따라서, 대용량 데이터에 대해서 빠른 처리가 가능하다.(Join이 없으므로)
> 
- 모델링의 순서가 [ 쿼리 → 도큐멘트 ]로, 필요한 쿼리에 따라서 도큐멘트를 만들게 된다.

## 📝 용어

### 공통

- Schema: Table(Collection)의 구조를 정의한다.
    
    <aside>
    💡 NOSQL은 유연한 Schema를 가지므로 Schema validation은 개발자의 선택이다. 즉, SQL은 Schema에 맞는 데이터가 강제 / NOSQL은 선택이다.
    
    </aside>
    
- Join: RDB에서 관계를 가지는 테이블의 데이터도 함께 가져오고 싶을 때 사용하는 쿼리 기법
    
    <aside>
    💡 RDB에서만 사용되는데 왜 공통에 있을까? NOSQL에서도 Join과 동일한 Lookup이 존재한다. 하지만, 이 둘의 동작방식은 다르고, NOSQL은 Join이 없도록 데이터를 중복저장하는게 좋다.
    
    </aside>
    
    - Join 동작방식의 차이
        
        SQL
        
        - Join시 외래키를 통해서 추가적인 Table에 접근하고, 외래키는 해당 Record를 직접 참조하므로 매우 빠른 속도로 가져올 수 있다.
        
        NOSQL
        
        - Lookup시 추가로 찾는 Collection을 Full Scan해서 맞는 Document를 찾게된다.
        - 여기서, 적절한 Indexing을 통해서 Lookup의 성능을 높일 수 있다.
        - 또한, NOSQL은 스키마가 유연하고 모든 데이터가 들어갈 수 있으므로, Document의 Field에 Document자체가 들어갈 수 있다. 이러한 기법을 Embedding기법이라고 한다.
            
            <aside>
            💡 Embedding시 한개의 Document가 비대해질 수 있는걸 염두해두고 너무 커지는 Document인지 생각해보고, 그렇닫면 중복 저장이나 Link기법을 생각해볼 수 있다.
            
            </aside>
            
        - 또한, Link기법으로 특정 Document를 직접 참조할 수도 있다.

### SQL

- Table: 데이터를 저장하는 표(Table)
- Row(Record): Table에서 한개의 데이터를 나타낸다.
- Column(Field): Table에서 데이터가 가질 수 있는 각 속성이다.
- Relationship: Table과 Table의 관계이다.

### NoSQL

- Collection: == RDB의 Table
- Document: == RDB의 Row(Record)
- Field: == RDB의 Column(Field)

## ⚡️ Transaction

<aside>
💡 Transaction이란 논리적으로 1개의 단위를 가지는 여러 작업을 모아놓은 단위를 말한다. 쉽게 말해서 개발자가 원하는 최소 작업을 말한다.

</aside>

### ACID

> Transaction을 보장하기 위해서는 아래 4가지 조건을 만족해야 한다.
> 
- Atomicity(원자성): 모든 연산에 대해서 모두 처리/실패 → all-or-nothing
- Consistency(일관성): 데이터는 미리 정의된 규칙(제약조건, 도메인, ...)에 부합
- Isolation(일관성): 트랜잭션동안 다른 트랜잭션 간섭 불가
- Durability(지속성): 트랜잭션 이후 데이터들의 영구 보존

### SQL

<aside>
💡 SQL은 트랜잭션을 중요시한다. 데이터의 일관성을 중요시하는것과 일맥상통한다.

</aside>

### NOSQL

<aside>
💡 NOSQL은 트랜잭션을 지원한지 비교적 얼마 되지 않았다. MongoDB의 경우 Replica Set을 구축해두었을 경우 Transaction을 활용할 수 있다.

</aside>

- MongoDB Manual의 내용
    
    > In version 4.0, MongoDB supports multi-document transactions on replica sets.
    In version 4.2, MongoDB introduces distributed transactions, which adds support for multi-document transactions on sharded clusters and incorporates the existing support for multi-document transactions on replica sets.
    
    To use transactions on MongoDB 4.2 deployments (replica sets and sharded clusters), clients must use MongoDB drivers updated for MongoDB 4.2.
    > 
    
    4.0부터 Multi-Document의 Transaction을 지원하기 시작했으며, 이 때부터 DB로써 사용할 수 있는 역량을 갖췄다고 평가된다. 그 아래는 4.2부터는 샤딩을 통해 확장된 상태에서 지원한다고 써있다.
    
- NOSQL도 ACID를 만족한다고?
    
    아래 MongoDB의 Manual을 읽어보면 그러한거 같다. 이제 ACID Transactions 된다고 자랑하는 글
    
    [ACID Transactions Basics](https://www.mongodb.com/basics/acid-transactions)
    

## 🌝 특성

### ACID of SQL

### BASE of NOSQL

<aside>
💡 SQL과 다르게 유연성과 가용성을 중요시하는 NOSQL의 특성이다.

</aside>

> ACID와 대조되는 가용성과 성능을 중시하는 특징
> 
- Basically Available(가용성): 데이터는 항상 접근이 가능, 데이터는 중복 저장
- Soft-state(독립성): 노드의 상태는 외부의 정보를 통해 결정
- Eventually Consistent(일관성): 일정 시간 경과시 데이터의 일관성을 유지

### BASE VS ACID

| 항목 | BASE | ACID |
| --- | --- | --- |
| 적용대상 | NoSQL | RDBMS |
| 범위 | 시스템 전체 대상 | 개별 트랜잭션 적용 |
| 일관성 | 약한 일관성 | 강한 일관성 |
| 중점사항 | 성능과 가용성 | 무결성, 일관성 |
| 관리주체 | 주로 개발자 | DBMS 트랜잭션 |
| 데이터처리 | 유사 응답 허용 | 처리 순서 보장 |
| 변경성 | 변경 어려움 | 변경 용이 |
| 디자인 | 쿼리 디자인 중요 | 테이블 디자인 중요 |
| CAP이론 | C+P, A+P 만족 | C+A 만족 |
| 적용사례 | Big Table | Oracle RAC |

## 👾 CAP 이론

<aside>
💡 어떠한 분산 시스템도 일관성, 가용성, 분할내성을 동시에 만족시킬 수 없다는 이론이다.

</aside>

- Consistency(일관성): 모든 노드들은 같은 시간에 동일한 항목에 대하여 같은 내용의 데이터를 제공한다.
- Availability(가용성): 모든 사용자들이 읽기및 쓰기가 가능하며, 몇몇 노드의 장애시 다른 노드에 영향을 끼치지 않는다.
- Partition-tolerance(분할 내성): 메시지 전달이 실패하거나 일부 시스템이 망가져도 시스템은 정상 동작해야 한다.

> 현재 DB들은 이중에 2가지를 만족하도록 만들어진다.
> 

> SQL(CA), NoSQL(CA, AP)
> 

## 👐 확장

> 확장이란 성능 또는 용량 초과로 인한 DB의 확장이다.
> 

### 수평 확장 of NOSQL

<aside>
💡 수평 확장이란 서버(DB)를 늘려서 확장하는 형태를 말한다.

</aside>

> NOSQL은 비교적 쉬운 수평 확장을 샤딩을 통해서 지원한다. 샤딩이란 같은 Collection내의 Document를 분산하여 저장하는 방식이다.
> 
- 샤딩을 통한 비교적 쉬운 수평 확장
- 유연한 스키마 변경을 통한 확장

### 수직 확장 of SQL

<aside>
💡 수직 확장이란 서버(DB)의 HW(CPU, RAM, ...)을 업그레이드하는 형태를 말한다.

</aside>

> SQL은 Schema변경이 거의 불가능하므로 수직 확장만이 가능하다. 수평 확장도 가능하지만, 매우 매우 어렵다고 볼 수 있다.
> 

> NOSQL은 수직 확장이 안되는가? 수평 확장이 인력과 서버 비용 모두 통틀어서 더 좋은 선택이므로 수직 확장할 필요는 없다.
> 

## 👀 정규화와 비정규화

### 정규화(Normalization)

<aside>
💡 정규화란 DB가 얼마나 잘 설계되었는가, 잘못된 설계는 아닌가를 평가하는 지표이다.

</aside>

> 정규화를 통해서 이상(Anomaly)현상을 방지할 수 있다. 이상 현상이란 개발자가 원하지 않는 데이터의 삭제 / 삽입 / 갱신되는것을 말한다.
> 

### 비정규화(Denormalization)

<aside>
💡 비정규화는 정규화의 반대이다. 데이터를 중복 저장되게 함으로써 성능을 높일 때 사용된다. 데이터를 중복 저장하게 됨으로써 Join이 줄어듦으로 성능을 얻는다.

</aside>

> 정규화는 1 ~ 5단계가 있으며, 숫자가 높아질수록 데이터의 중복이 없다. 현업에서는 보통 3단계 정도까지를 사용한다.
> 

### SQL & NOSQL

- SQL: 정규화를 통해서 데이터의 중복을 없애는것을 지향한다.
- NOSQL: 비정규화를 통해서 빠른 성능과 가용성을 지향한다.

## 👍 장점과 단점

<aside>
💡 SQL은 데이터의 일관성을 중시, NoSQL은 유연성과 가용성을 중시한다고 볼 수 있다.

</aside>

- SQL
    - 장점: 관계를 통해서 데이터의 일관성을 강제하므로 설계만 잘 해놓으면 사용시 편리하다.
    - 단점: 일관성, 트랜잭션을 위해서 잘못된 설계시 많은 성능 저하가 일어날 수 있다, 설계/수정이 어렵다.
- NoSQL
    - 장점: 대용량 데이터에 좋은 성능을 기대할 수 있다, 설계 / 수정 / 확장이 쉽다
        
        > 대용량 데이터일 경우, 
        1. 데이터가 많아짐으로써 DB를 확장할 때 샤딩을 통해 쉽게 할 수 있다.
        2. 형태가 다른 데이터를 모두 받아서 사용할 수 있다.
        > 
    - 단점: 데이터의 일관성을 개발자가 신경써주어야 한다.

## 😭 예상 질문

- SQL과 NOSQL의 차이는 무엇인가요?
    - 가장 큰 차이점은 데이터의 일관성을 중요시할 것이냐, 가용성과 확장성을 중요시할 것이냐 입니다. SQL은 일관성을 잘 지킬 수 있으며, NOSQL은 쉬운 수정과 수평 확장을 할 수 있습니다.
- SQL의 장점과 단점은 무엇인가요?
    - SQL의 장점은 설계된 Table과 Schema를 통해서 데이터의 일관성을 보장받을 수 있습니다. 단점은 잘 못 설계된 Table과 Schema는 성능을 저하시킬 수 있고, Schema의 수정이 힘드며 확장시 수직 확장을 해야함이 있습니다.
- NOSQL의 장점과 단점은 무엇인가요?
    - NOSQL의 장점은 가용성과 유연성입니다. 유연한 Schema를 통해서 Agile한 DB 설계를 할 수 있으며 확장시에도 상대적으로 쉬운 샤딩을 통한 수평확장입니다. 단점은 중복 저장으로 데이터의 일관성이 보장되지 않을 수 있고, DB 스토리지를 낭비할 수 있으며 업데이트 쿼리시 Document크기에 따라서 성능이 저하될 수 있습니다.
- 언제 SQL을 사용하고, 언제 NOSQL을 사용해야 할까요?
    - 데이터의 형태가 정해져 있고, 일관성이 중요하고 DB 스토리지가 넉넉하지 않다면 SQL을, 유연한 수정과 확장성을 고려한다면 NOSQL 사용을 고려해볼 수 있습니다.
- 대용량 데이터 처리가 NoSQL 이 더 유리한가?
    - 유연한 데이터 유형
    - 서버의 수평확장에 유리한 구조
- SQL과 NOSQL의 사용 경험에 대해서 말해주세요
- 개발시 어떤 sql를 사용할 것인가?
    - 관계에 따라
    - 보안이 중요하다면 SQL을 사용하는 것이 유리하다.
        
        > 트랜잭션의 안정성, 유연한 Schema로 SQL Injection에 취약하다.
        > 
    - 둘 다 적절히 사용

## 👨‍💻 참고

- 그룹 프로젝트 정리 노션
    
    [SQL VS NoSQL](https://www.notion.so/SQL-VS-NoSQL-13a24463cac04934adbee88b8bd96fd2) 

- 정규화
    
    [#02. 이상(Anomaly)현상과 정규화(Normalization)](https://movenpick.tistory.com/29)
    
    [데이터베이스 정규화 1NF, 2NF, 3NF, BCNF](https://3months.tistory.com/193)
    
- 비교
    
    [SQL과 NOSQL의 차이 | 👨🏻‍💻 Tech Interview](https://gyoogle.dev/blog/computer-science/data-base/SQL%20&%20NOSQL.html)
    
    [SQL vs NoSQL](https://velog.io/@thms200/SQL-vs-NoSQL)
    
- 모델링
    
    [NoSQL 데이터 모델링](https://more-learn.tistory.com/5)
    
    [MongoDB 데이터 관계 모델링](https://devhaks.github.io/2019/11/30/mongodb-model-relationships/)
    
- 트랜잭션
    
    [[DB기초] 트랜잭션이란 무엇인가?](https://coding-factory.tistory.com/226)
    
    [What is NoSQL? NoSQL Databases Explained](https://www.mongodb.com/nosql-explained)
    
- BASE
    
    [NoSQL 데이터베이스 접속 시 보안 고려사항](http://channy.creation.net/project/dev.kthcorp.com/2012/01/26/security-considerations-in-accessing-nosql-databases/index.html)
    
- 보안
    
    [NoSQL BASE 속성 > 도리의 디지털라이프](http://blog.skby.net/nosql-base-%EC%86%8D%EC%84%B1/)