## TRANSACTION 과 LOCK

데이터베이스 세계에서 모든건 순서가 있다. 동시에 일어나는 것 같아 보여도. 

```jsx
START TRANSACTION;
USE mayo;
UPDATE role SET min_salary = 4000 WHERE id = 4; 
UPDATE employee SET salary = 4000 WHERE salary < 4000 ADN( 오타) role_id = 4;

COMMIT;
(ROLLBACK;)

```

커밋까지의 트랜젝션이 실패하면 롤백을 시키는 쿼리문 

- **ACID 특성을 트렌젝션은 만족시킨다.**
    - Atomicity : 하나의 단위
    - Consistency : 수정하고 나서도 정상적인 데이터를 가지고 있어야한다.
    - Isolation : 트렌젝션간에는 서로 영향을 주지 않는다.( 동시라는 개념X, 다 순서가 있다. ) - > **LOCK , Trigger, Stored Procedure, View**
    - Durability : 실패하면 완전히 원상태로 복구된다.

- 격리 수준
    - READ Uncommitted
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b76d7d9-1d86-4b34-8431-142dffd59e5d/Untitled.png)
        
        이런게 
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/082c7710-869a-4fff-8625-8fa60729bd16/Untitled.png)
        순서가 꼬여서 이런식으로 될 수가 있다.  Commit이 아니라 rollback 이면 B의 update 구문은 잔액이 10만원이지만 3만원으로 인식해서 실행되지 않는다. (**Dirty Read**) ⇒ 커밋되지 않은 데이터(A의 업데이트 구문)를 읽어버림
        
        Rollback 일 때 ⇒ dirty read
        
    - READ Committed  ⇒ non-repeatable READ
        
       ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/45adb379-44a9-4620-b305-bcd5e4d0cf4e/Untitled.png)
        Commit 일때 ⇒ non-repeatable READ는 아래와 같이 select의 내용이 둘이 다름 
        
    - Repeatable READ ex) InnoDB
        
        위의 문제가 해결됨. 커밋 다음에 select가 되도록 함 LOCK !
        
    - Serializable
        
        몰라도됨 
        

### 함수 느낌의 Stored Procedure

쿼리 안의 특정 값이 반복될 때 함수처럼 사용할 수 있다. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/aa33ad0e-c725-4ecf-b155-5c269625982d/Untitled.png)

- 프로시져 생성

```jsx
DELIMITER //
CREATE PROCEDURE increaseMinSalary(monet INT, rid INT)
BEGIN
(내용)
END//
DELIMITER; 
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f8935775-7983-4bce-a887-64c29368098b/Untitled.png)

- 프로시져 사용

```jsx
CALL increaseMinSalary(5500, 3);
```

쿼리 날릴 때 성능 문제가 있을 수 있다. 잘 쓰면 편하다. 

### trigger

ex) 업데이트 할 때 updated_at → UPDATE TRIGGER , 데이터 수정시! , 백업용! 

- 생성 쿼리

```jsx
DELIMITER //
CREATE TRUGGER updateSalaryWhenMinSalaryChange AFTER UPDATE ON mayo.role
FOR EACH ROW 
BEGIN
(내용) 
END //
DELIMITER;
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6ee68046-6f19-4328-80c5-1ebfa476fa40/Untitled.png)
- 트리거 보기

```jsx
SHOW TRIGGERS;
```

- 트리거 삭제

```jsx
DROP TRIGGER updateSalaryWhenMinSalaryChange ;
```

### View

테이블을 통해서 가상의 테이블을 하나 만들어 내는 것. 

파생 테이블 개념 

```jsx
CREATE OR REPLACE VIEW mayo.ep_view
AS (쿼리문)
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/af7d6890-f38d-4294-b826-5822b97ca885/Untitled.png)

ep_view가 없으면 만들고 없다면 교체하는 것. 

create만 써도 된다. 

뷰안에서 쿼리를 날릴 수도 있다. 문제는 성능이 안좋을 수 있다.
