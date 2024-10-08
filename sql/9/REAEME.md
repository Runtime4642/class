
## 트랜잭션 (Transactions)
트랜잭션은 데이터베이스의 상태를 변화시키는 하나의 작업 단위를 의미합니다. 트랜잭션은 다음 네 가지 특성을 가집니다:
- **원자성 (Atomicity)**: 트랜잭션 내의 모든 작업들이 완벽하게 수행되거나 전혀 수행되지 않아야 함을 의미합니다.
- **일관성 (Consistency)**: 트랜잭션이 성공적으로 완료되면 데이터베이스의 모든 제약 조건이 만족되어야 합니다.
- **고립성 (Isolation)**: 동시에 실행되는 트랜잭션들이 서로 영향을 미치지 않도록 고립되어야 함을 의미합니다.
- **지속성 (Durability)**: 트랜잭션이 성공적으로 완료되면 그 결과는 영구적으로 데이터베이스에 저장되어야 합니다.

### 트랜잭션의 상태
트랜잭션은 다음과 같은 상태를 가질 수 있습니다:
- **활동 (Active)**: 트랜잭션이 실행 중인 상태
- **부분 완료 (Partially Committed)**: 트랜잭션이 마지막 연산을 실행한 직후의 상태
- **완료 (Committed)**: 트랜잭션이 성공적으로 완료된 상태
- **실패 (Failed)**: 트랜잭션이 실패한 상태
- **철회 (Aborted)**: 트랜잭션이 실패하여 되돌아간 상태

### 트랜잭션의 예
```
BEGIN;
UPDATE 테이블명 SET 열1 = 값1 WHERE 조건;
INSERT INTO 테이블명 (열1, 열2) VALUES (값1, 값2);
COMMIT;
```
- `BEGIN`은 트랜잭션의 시작을 알립니다.
- `COMMIT`은 트랜잭션이 성공적으로 완료되었음을 알립니다.

### 트랜잭션 격리 수준 (Transaction Isolation Levels)
트랜잭션 격리 수준은 동시에 실행되는 트랜잭션들이 서로에게 미치는 영향을 제어하는 데 사용됩니다. 주요 격리 수준은 다음과 같습니다:
- **READ UNCOMMITTED**: 트랜잭션이 커밋되지 않은 데이터를 읽을 수 있습니다.
- **READ COMMITTED**: 트랜잭션이 커밋된 데이터만 읽을 수 있습니다.
- **REPEATABLE READ**: 트랜잭션이 시작된 후 다른 트랜잭션이 변경한 데이터를 읽을 수 없습니다.
- **SERIALIZABLE**: 가장 엄격한 격리 수준으로, 트랜잭션이 완전히 순차적으로 실행되는 것처럼 동작합니다.

### REDO와 UNDO
- **REDO**: 트랜잭션이 성공적으로 완료된 후에도 시스템 장애가 발생할 경우, 트랜잭션 로그를 사용하여 트랜잭션을 재실행하는 과정입니다.
- **UNDO**: 트랜잭션이 실패하거나 철회될 경우, 트랜잭션 로그를 사용하여 이전 상태로 되돌리는 과정입니다.

### 예시
```
BEGIN;
-- 작업 수행
UPDATE 계좌 SET 잔액 = 잔액 - 1000 WHERE 사용자ID = 'A';
UPDATE 계좌 SET 잔액 = 잔액 + 1000 WHERE 사용자ID = 'B';
-- 트랜잭션 완료
COMMIT;
```
위의 예시는 두 개의 업데이트 작업을 하나의 트랜잭션으로 묶어 수행합니다. 첫 번째 업데이트가 실패할 경우, 두 번째 업데이트도 수행되지 않습니다.
