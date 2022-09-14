# View

- view 를 read-only 목적으로 쓴다
- view를 update 하는건 가능하지만 오직 read only 목적으로 쓴다
- view를 subquery나 join 문에 많이 쓰는데 (optimizer ), 단일 테이블에서도 쓰인다: confidentials info 를 감추거나 자주 read 하는 칼럼들을 묶거나 할때. 
- view는 DML에 의한 데이터 변경이 발생하면 자동으로 업데이트 된다
