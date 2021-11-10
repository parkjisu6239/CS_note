# Transaction

하나의 작업을 수행하기 위해 필요한 데이터베이스의 연산들을 모아놓은 것으로 DB의 논리적인 작업 단위이다. 데이터의 완전성을 보장하고, 회복과 병행제어가 가능하다. 100% 적용, 100% 미적용 둘중에 하나만 하게 한다. 50%는 적용되고, 그 절반은 그렇지 않은 경우를 방지

- **트랜잭션과 Lock**

  - 잠금(Lock)과 트랜잭션은 서로 비슷한 개념 같지만 사실 잠금은 동시성을 제어하기 위한 기능이고 트랜잭션은 데이터의 정합성을 보장하기 위한 기능이다.
  - 잠금은 여러 커넥션에서 동시에 동일한 자원을 요청할 경우 순서대로 한 시점에는 하나의 커넥션만 변경할 수 있게 해주는 역할을 한다.
  - 트랜잭션은 논리적인 작업 셋 자체가 100% 적용되거나 아무것도 적용되지 않아야 함을 보장하는 것이다.

- **트랜잭션의 특성 ACID**

  - **원자성(Atomicity)**

    만약 트랜잭션 중간에 어떠한 문제가 발생한다면 트랜잭션에 해당하는 어떠한 작업 내용도 수행되어서는 안되며 아무런 문제가 발생되지 않았을 경우에만 모든 작업이 수행되어야 한다.

  - **일관성(Consistency)**

    트랜잭션이 완료된 다음의 상태에서도 트랜잭션이 일어나기 전의 상황과 동일하게 데이터의 일관성을 보장해야 한다.

  - **고립성(Isolation)**

    각각의 트랜잭션은 서로 간섭없이 독립적으로 수행되어야 한다.

  - **지속성(Durability)**

    트랜잭션이 정상적으로 종료된 다음에는 영구적으로 데이터베이스에 작업의 결과가 저장되어야 한다.

- **트랜잭션의 상태**

  ![https://github.com/JaeYeopHan/Interview_Question_for_Beginner/raw/master/Database/images/transaction-status.png](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/raw/master/Database/images/transaction-status.png)

  - **Active**

    트랜잭션의 활동 상태. 트랜잭션이 실행중이며 동작중인 상태를 말한다.

  - **Failed**

    트랜잭션 실패 상태. 트랜잭션이 더이상 정상적으로 진행 할 수 없는 상태를 말한다.

  - **Partially Committed**

    트랜잭션의 `Commit` 명령이 도착한 상태. 트랜잭션의 `commit`이전 `sql`문이 수행되고 `commit`만 남은 상태를 말한다.

  - **Committed**

    트랜잭션 완료 상태. 트랜잭션이 정상적으로 완료된 상태를 말한다.

  - **Aborted**

    트랜잭션이 취소 상태. 트랜잭션이 취소되고 트랜잭션 실행 이전 데이터로 돌아간 상태를 말한다.

  - **Partially Committed 와 Committed 의 차이점**

    `Commit` 요청이 들어오면 상태는 `Partial Commited` 상태가 된다. 이후 `Commit`을 문제없이 수행할 수 있으면 `Committed` 상태로 전이되고, 만약 오류가 발생하면 `Failed` 상태가 된다. 즉, `Partial Commited`는 `Commit` 요청이 들어왔을때를 말하며, `Commited`는 `Commit`을 정상적으로 완료한 상태를 말한다.

- **트랜잭션을 사용할 때 주의할 점**

  트랜잭션은 꼭 필요한 최소의 코드에만 적용하는 것이 좋다. 즉 트랜잭션의 범위를 최소화하라는 의미다. 일반적으로 데이터베이스 커넥션은 개수가 제한적이다. 그런데 각 단위 프로그램이 커넥션을 소유하는 시간이 길어진다면 사용 가능한 여유 커넥션의 개수는 줄어들게 된다. 그러다 어느 순간에는 각 단위 프로그램에서 커넥션을 가져가기 위해 기다려야 하는 상황이 발생할 수도 있는 것이다.

- **교착상태**

  복수의 트랜잭션을 사용하다보면 교착상태가 일어날수 있다. 교착상태란 두 개 이상의 트랜잭션이 특정 자원(테이블 또는 행)의 잠금(Lock)을 획득한 채 다른 트랜잭션이 소유하고 있는 잠금을 요구하면 아무리 기다려도 상황이 바뀌지 않는 상태가 되는데, 이를 `교착상태`라고 한다.

  - **교착상태의 예(MySQL)**

    MySQL [MVCC](https://en.wikipedia.org/wiki/Multiversion_concurrency_control)에 따른 특성 때문에 트랜잭션에서 갱신 연산(Insert, Update, Delete)를 실행하면 잠금을 획득한다. (기본은 행에 대한 잠금)

    ![https://github.com/JaeYeopHan/Interview_Question_for_Beginner/raw/master/Database/images/deadlock.png](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/raw/master/Database/images/deadlock.png)

    트랜잭션 1이 테이블 B의 첫번째 행의 잠금을 얻고 트랜잭션 2도 테이블 A의 첫번째 행의 잠금을 얻었다고 하자. 트랜잭션을 commit 하지 않은채 서로의 첫번째 행에 대한 잠금을 요청하면 Deadlock 이 발생한다. 일반적인 DBMS는 교착상태를 독자적으로 검출해 보고한다.

  - **교착 상태의 빈도를 낮추는 방법**

    - 트랜잭션을 자주 커밋한다.
    - 정해진 순서로 테이블에 접근한다. 위에서 트랜잭션 1 이 테이블 B -> A 의 순으로 접근했고, 트랜잭션 2 는 테이블 A -> B의 순으로 접근했다. 트랜잭션들이 동일한 테이블 순으로 접근하게 한다.
    - 읽기 잠금 획득 (SELECT ~ FOR UPDATE)의 사용을 피한다.
    - 한 테이블의 복수 행을 복수의 연결에서 순서 없이 갱신하면 교착상태가 발생하기 쉽다, 이 경우에는 테이블 단위의 잠금을 획득해 갱신을 직렬화 하면 동시성을 떨어지지만 교착상태를 회피할 수 있다.
