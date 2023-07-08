# Python

Python에 대해 알아보자. 
- [점프 투 파이썬](https://wikidocs.net/book/1)
- [Python 3.11 Documentation](https://docs.python.org/3/index.html)

## 파이썬이란?

- 파이썬은 인터프리터 언어이다. 인터프리터 언어란 한 줄씩 소스 코드를 해석해서 그때그때 실행해 결과를 바로 확인할 수 언어를 말한다.
- 파이썬의 특징
  - 파이썬은 간결하다
  - 파이썬은 인간다운 언어이다
  - 파이썬은 간결하다
- 파이썬으로 할 수 있는 일
  - 시스템 유틸리티 제작
  - GUI 프로그래밍
  - C/C++ 와의 결합: python은 Glue 언어
  - 웹 프로그래밍
  - 수치 연산 프로그래밍: NumPy (C로 작성한 모듈)
  - DB 프로그래밍
  - IoT
  - Machine Learning
- 파이썬으로 할 수 없는 일
  - 시스템같이 대단히 빠른 속도를 요구하거나 하드웨어를 직접 건드리는 작업
  - 모바일 프로그래밍

## 파이썬은 다이나믹한 언어인가?

[파이썬은 다이나믹한 **타입** 언어이다.](https://stackoverflow.com/questions/11328920/is-python-strongly-typed)

> Python is strongly, dynamically typed. **Strong** typing means that the type of a value doesn't change in unexpected ways. A string containing only digits doesn't magically become a number, as may happen in Perl. Every change of type requires an explicit conversion. **Dynamic** typing means that runtime objects (values) have a type, as opposed to static typing where variables have a type.

```python
bob = 1 # type(bob) returns int
bob = "bob" # type(bob) returns str
```

## 파이썬의 자료형

- 리스트: 모음을 표현
  - 리스트 = [요소1, 요소2, 요소3, ...]
  - 리스트 = [요소1, 요소2, [요소a, 요소b]]
  - a[0:2] 와 같이 0부터 2이전까지 슬라이싱할 수 있다
  - a \* 3 와 같이 리스트를 반복할 수 있다 ("abc" \* 3 = "abcabcabc"와 같은 이치)
  - 리스트의 길이를 구하고 싶다면? len(a)
  - 요소값을 삭제하고 싶다면? **del** a[1]
- 튜플: 요소 값을 바꿀 수 없다 + ()으로 둘러싼다
  - 튜플 = (요소1, 요소2)
  - 튜플의 요소값을 지우거나 변경할때 타입에러 발생: TypeError: 'tuple' object doesn't support item deletion
- 딕셔너리: 대응관계를 나타내는 자료형으로 key - value 짝으로 이루어진다
  - { key1: value1, key2: value2 }
  - key - value 쌍을 삭제하고 싶다면? **del** dict["요소1"]
  - 딕셔너리에서 Key는 고유한 값이므로 중복되는 Key 값을 설정해 놓으면 하나를 제외한 나머지 것들이 모두 무시된다: a = { 1: 'a', 1: 'b' }에서 a를 출력하면, { 1: 'b' }
  - Key에 리스트는 쓸 수 없다 왜냐하면 리스트는 immutable한 값이 아니라서
    - TypeError: unhashable type: 'list'
    - 단, 튜플은 Key로 쓸 수 있다
  - 해당 Key 가 딕셔너리 안에 있는지 조사하려면? 'key1' in dict
  - 순서가 없는 자료형이라 인덱싱을 지원하지 않는다
- 집합: 중복을 허용하지 않는다, 순서가 없다
  - s1 = set([1, 2, 3])
  - s2 = set("Hello")
  - 딕셔너리와 마찬가지로 순서가 없는 자료형이라 인덱싱을 지원하지 않는다
    - 인덱싱이 필요하다면? 리스트나 튜플로 변환하자 e.g. list(s1) 또는 tuple(s1)
  - 교집합: s1 & s2
  - 합집합: s1 | s2
  - 차집합: s1 - s2
  - 1개의 값을 추가할때는 s1.add(4), 여러개 추가할때는 s1.update([4, 5, 6])
  - 특정 값을 제거할때는 s1.remove(2)

## if문

- 조건을 판단하여 해당 조건에 맞는 상황을 수행하는 데 쓰는 것이 바로 if문이다.
- and, or, not
  - x and y: x와 y 모두 참이어야 참이다
  - x or y: x와 y 둘중에 하나만 참이어도 참이다
  - not x: x가 거짓이면 참이다
- in, not in 집합
  - 1 in [1, 2, 3] # returns True
  - 1 not in [1, 2, 3] # returns False
- pass: 조건문에서 아무일도 하지않게 설정한다
- 조건부 표현식: conditional expression
  - message = "success" if score >= 60 else "failure"

## for문

- 리스트나 튜플, 문자열의 첫번째 요소부터 마지막 요소까지 차례로 변수에 대입되어 명령을 수행한다

```python
for 변수 in 리스트(또는 튜플, 문자열): 
    수행할 문장1
```

- range 함수: 숫자 리스트를 만들어준다
  - a = range(10) # returns range(0, 10) 0부터 10미만의 숫자를 포함하는 range 객체
    - range(시작숫자, 끝 숫자) # 끝 숫자는 포함하지 않는다
- List comprehension: 리스트 안에 for문을 포함한다. [표현식 for 항목 in 반복가능객체 if 조건문]

```python
a = [1,2,3,4]
result = []
for num in a:
    result.append(num*3)
print(result)

# could be like this
a = [1,2,3,4]
result = [num * 3 for num in a]
print(result)

# 구구단
result = [x*y for x in range(2,10) for y in range(1, 10)]
```

## pass vs continue

- continue 는 더이상 남은 코드를 실행하지 않고 다음 차례로 넘어가는 반면에 pass 는 남은 코드를 실행한다
- pass는 일반적으로 앞으로 작성할 코드의 placeholder 역할에 쓰인다
- [resource](https://builtin.com/software-engineering-perspectives/pass-vs-continue-python)

```python
# **continue**
for num in range(0,10):
    if num == 5:
        continue
    print(f'Iteration: {num}')

"""
Iteration: 0
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
Iteration: 6
Iteration: 7
Iteration: 8
Iteration: 9
"""

# **pass**
for num in range(0,10):
    if num == 5:
        continue
    print(f'Iteration: {num}')

"""
Iteration: 0
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
Iteration: 5
Iteration: 6
Iteration: 7
Iteration: 8
Iteration: 9

"""
```

## Exception

- 실행 중 에러가 발생했을때 처리해보자

```python
try: 
  4/0
except:
  print("error")
```

- 정해진 오류에만 반응할 수 없을까

```python
try: 
  4/0
except (ZeroDivisionError, IndexError) as e:
  print(e)
```

- finally 문으로 에러가 발생하든 발생하지 않은 무조건 실행해보자

```python
try:
  4/0
except: 
  print("error")
finally: 
  print("good job")
```

## assertion

- assert 는 뒤의 조건이 True가 아니면 AssertError를 발생한다.
- assert 조건, '메시지'

```python
assert type(3) is int, 'this is not Integer'
assert a == 2
```

## Class

- 객체지향성 언어의 개념

```python
class temp:
  a = None

  def __init__(self, str): # 생성자. 객체가 만들어질때 반드시 실행됨
    self.a = str

  def driving(self, str): # 메서드. 반드시 첫번째 인자에 self를 넣어야함
    print("%s로 운전 중" % (str))

tory = temp("solid")
print(tory.a)
tory.driving("서울")
```

- 인스턴스가 생성된다는 것은 class에 bound된다는 의미이다.

```python
class Car:
    def __init__(self, num):
      self.horpower = num

    def get_horsepower(self):
      return self.horpower
# print(Car.get_horsepower()) returns TypeError: get_horsepower() missing 1 required positional argument: ‘self’
print(Car.get_horsepower(Car(120))) # 인자가 전달 
print(Car(120).get_horsepower()) # 인자가 전달 X

""" 
인자가 전달되지 않았는데도 작동하는 이유는 객체가 만들어지면 해당 메서드가 자동으로 연결(bound)된다는 것을 의미한다. 

print(Car(120).get_horsepower)
"""
```

```python
# 비슷한 예
s = 'hello'
s.upper() # returns 'HELLO'
str.upper(s) # returns "HELLO'

```

- setter and getter: 메서드를 은닉해보자

```python
class Car:
  def __init__(self):
    self.__horsepower = 100

  @property
  def horsepower(self): # getter
    return self.__horsepower

  @horsepower.setter
  def horsepower(self, str): # setter
    self.__horsepower = str
```

## Python tools

- flake8: a linting tool (such as PyLint)
- autopep8: autopep8 automatically formats Python code to conform to the PEP 8 style guide. (such as Prettier)
- Pip: the package installer for Python
