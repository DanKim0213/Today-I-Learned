# Join 

- 각 부서별 최고급여를 받는 사원의 부서, 이름, 급여를 구하라
	- select department_id, employee_id, first_name, salary from employees where **(department_id, salary)** in (select department_id, max(salary) from employees group by department_id) order by department_id; // in 은 포함여부
	- select a.department_id, e.employee_id, e.first_name, a.smax from employees e join (select department_id, max(salary) smax from employees group by department_id) a on e.department_id = a.department_id and e.salary = a.smax;

## Join 시 주의
- join-on, join-on, ..., join-on 식으로 묶자.
- n개의 테이블을 조인시 n-1개의 join 문이 필요하다.
- Inner Join 을 줄여서 join 으로 쓰기도 한다.
- 조인의 처리는 어느 테이블을 먼저 읽을지를 결정하는 것이 중요 (처리할 작업량이 상당히 달라진다)
	- Inner Join: 어느 테이블을 먼저 읽어도 결과가 달라지지 않는다: Optimizer가 조인의 순서를 조절해서 최적화 수행한다.
	- Outer Join: 반드시 Outer가 되는 테이블을 **먼저** 읽어야하므로 Optimizer가 조인 순서를 선택할 수 없다.

## 사번이 100인 사원의 사번, 이름, 급여, 부서이름을 구하라
- select e.employee_id, e.first_name, e.salary, e.department_id, d.department_name from employees e, departments d
where employee_id = 100 **and e.department_id = d.department_id**;
- select e.employee_id, e.first_name, e.salary, e.department_id, d.department_name from employees e **inner join** departments d
**on e.department_id = d.department_id**
where employee_id = 100;
