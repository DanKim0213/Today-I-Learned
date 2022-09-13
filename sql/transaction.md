# Transaction
[Here](https://dev.mysql.com/doc/refman/8.0/en/commit.html)

- 하나의 정상적인 작업 단위로 생각하자 e.g. 계좌이체 (보낸사람- 받는사람 관계)
- "With START TRANSACTION, autocommit remains disabled until you end the transaction with COMMIT or ROLLBACK. The autocommit mode then reverts to its previous state."

e.g.
start transaction;
insert into test values('a');
insert into test values('b');
insert into test values('c');
insert into test values('d');
commit; // if error occur, rollback; 

- Note that: "By default, MySQL runs with autocommit mode enabled. This means that, when not otherwise inside a transaction, each statement is atomic, as if it were surrounded by START TRANSACTION and COMMIT. You cannot use ROLLBACK to undo the effect; however, if an error occurs during statement execution, the statement is rolled back."

Simply put, you don't need "commit;" when manipulating data without "start transaction;" because mysql runs with autocommit for you  by default. 
