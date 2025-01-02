>**SQL(Structured Query Language)**
>
>관계형 데이터베이스 관리 시스템 (RDBMS)을 위한 표준 언어
>
>1986년에 처음 표준화되었으며, 이후 40년간 주요 데이터베이스 언어로 자리잡음


## SQL 언어의 5가지 구성 요소

### 1. DDL (**Data Definition Language,** 데이터 정의 언어)

- 데이터베이스 구조를 정의하거나 수정

| **명령어** | **설명** | **예시** |
| --- | --- | --- |
| `CREATE` | 데이터베이스, 테이블, 뷰, 인덱스 생성 | `CREATE TABLE users (id INT, name VARCHAR(50));` |
| `ALTER` | 기존 구조 수정 | `ALTER TABLE users ADD COLUMN age INT;` |
| `DROP` | 데이터베이스, 테이블 삭제 | `DROP TABLE users;` |
| `RENAME` | 이름 변경 | `RENAME TABLE old_users TO new_users;` |

### 2. DQL (**Data Query Language,** 데이터 질의 언어)

- 데이터를 검색하고 질의하는데 사용

| **명령어** | **설명** | **예시** |
| --- | --- | --- |
| `JOIN` | 여러 테이블 연결 | `SELECT [users.name](http://users.name/), orders.amount FROM users INNER JOIN orders ON [users.id](http://users.id/) = orders.user_id;` |
| `WHERE` | 조건 필터링 | `SELECT * FROM users WHERE age > 30;` |
| `GROUP BY, HAVING` | 그룹화 및 그룹 조건 설정 | `SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 10;` |
| `ORDER BY` | 정렬 (ASC, DESC) | `SELECT name FROM users ORDER BY age DESC;` |
| `LIMIT` | 결과 수 제한 | `SELECT * FROM users LIMIT 5;` |

### 3. DML (**Data Manipulation Language,** 데이터 조작 언어)

- 데이터 추가, 수정, 삭제

| **명령어** | **설명** | **예시** |
| --- | --- | --- |
| `INSERT` | 데이터 추가 | `INSERT INTO users (id, name, age) VALUES (1, 'Alice', 25);` |
| `UPDATE` | 데이터 수정 | `UPDATE users SET age = 26 WHERE id = 1;` |
| `DELETE` | 데이터 삭제 | `DELETE FROM users WHERE id = 1;` |

### 4. DCL (**Data Control Language,** 데이터 제어 언어)

- 데이터베이스 접근 제어 및 권한 설정

| **명령어** | **설명** | **예시** |
| --- | --- | --- |
| `GRANT` | 권한 부여 | `GRANT SELECT, INSERT ON users TO 'username';` |
| `REVOKE` | 권한 회수 | `REVOKE INSERT ON users FROM 'username';` |

### 5. TCL (Transaction **Control Language,** 트랜잭션 제어 언어)

- 트랜잭션 관리를 통해 데이터 일관성 유지

| **명령어** | **설명** | **예시** |
| --- | --- | --- |
| `START TRANSACTION` | 트랜잭션 시작 | `START TRANSACTION;` |
| `COMMIT` | 변경 사항 저장 | `COMMIT;` |
| `ROLLBACK` | 변경 사항 취소 | `ROLLBACK;` |
