# Aggregation

## Group by clause

(prerequisite: ONLY_FULL_GROUP_BY 설정 필요)
아래의 쿼리는 **Error** 발생:
select emplyee_id, max(salary), min(salary)
from emplyees
where department_id = 80;

왜냐하면 emplyee_id 는 다중행인데 반해 max(salary), min(salary)는 단일행이기 때문이다. 

- Database는 선택 목록의 집계함수(e.g. max(), min())를 각 행 그룹에 적용하고 각 그룹에 대해 단일 결과행을 반환한다.
- Group by 절을 생략하면 Database는 집게함수를 모든 행에 적용한다.
- **Select 절의 모든 요소는 Group by 절의 표현식( group by department_id 에서 department_id), 집계함수를 포함하는 표현식(e.g. max(), min()), 또는 상수(e.g. 5*10)만 가능하다.**  

## Having clause

부서별 평균급여가 7000 이상인 부서번호, 평균급여를 구하라:
만약 집계함수를 where 절에 쓰면 **Error** 발생한다 왜냐하면 where 절이 group by 절 보다 먼저 실행되기 때문이다.
select department_id, avg(salary)
from employees
~~where avg(salary) > 7000 ~~
group by department_id
having avg(salary) > 7000;

- Group by 한 결과에 조건을 추가할 경우 having 절을 사용한다.
- Query의 실행 순서를 보면 where 절이 group by 절 보다 먼저 실행되기 때문에 aggregate 조건은 having 절에 작성한다.
