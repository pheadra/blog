---
id: class
title: Class
---

# Class
 - 클래스 자신도 객체(?)

## 클래스의 정의
```python
class MyClass:
    """A simple example class"""
    i = 123
    def method(self):
        return 'hello world'

# 클래스 정의가 정상적으로 끝나면 클래스 객체가 만들어집니다.

# 클래스 객체
MyClass.i
MyClass.method
MyClass.__doc__

x = MyClass() # 인스턴스 만들기 
```

- 생성자
```python
class MyClass:
    def __init__(self):
        self.data = []

x = MyClass()

class Complex:
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i = imagpart

x = Complex(3.-0, -4.5)
```

### instance object
- attribute references. (data attribute, method)


 - 클래스 객체에서 함수 참조와 인스턴스 객체에서 메소드 참조는 다르다.
 - 메서드는 인스턴스 객체가 함수의 첫 번째 인자로 전달됩니다.
 - x.f() == MyClass.f(x)와 동등합니다.

### 클래스 변수와 인스턴스 변수
```python

    kind = 'canine'         # class variable shared by all instances

    def __init__(self, name):
        self.name = name    # instance variable unique to each instance

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.kind                  # shared by all dogs
'canine'
>>> e.kind                  # shared by all dogs
'canine'
>>> d.name                  # unique to d
'Fido'
>>> e.name                  # unique to e
'Buddy'
```

- 레퍼런스 타입의 클래스 필드를 사용하면 공유하기 때문에 클래스의 올바른 설계는 인스턴스 변수를 사용하는 것입니다.
```python
class Dog:

    def __init__(self, name):
        self.name = name
        self.tricks = []    # creates a new empty list for each dog

    def add_trick(self, trick):
        self.tricks.append(trick)

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.add_trick('roll over')
>>> e.add_trick('play dead')
>>> d.tricks
['roll over']
>>> e.tricks
['play dead']
```

## Inheritance
```python
class DerivedClassName(BaseClassName):

# 베이스가 다른 모듈에 있을 때
class DerivedClassName(modname.BaseClassName):

class DerivedClassName(Base1, Base2, Base3):
```
- 클래스 객체가 만들어 질때 베이스 클래스가 기억됩니다.
- override가 가능하고 기본적으로 virtual 함수임

- 인스턴스의 type 검사 `isinstance()`
- 클래스 사속 검사 `issubclass()`



## Namespace
 - 모듈 이름 뒤에 오는것은 어트리뷰트의 참조 ex)modname.funcname (모듈객체.어트리뷰트)
 - 이름 공간은 서로 다른 순간에 만들어지고 서로 다른 수명을 갖습니다.built-in names들을 담는 이름 공간은 파이썬 인터프리터가 시작할 때 만들어지고 영원히 지워지지 않습니다. 
 - 모듈의 전역 이름 공간은 모듈의 정의를 읽는 동안 만들어집니다.
 - 함수의 지역 이름 공간은 함수가 호출될 때 만들어지고, 함수가 끝나거나 예외가 발생할때 삭제됩니다. 
 - 재귀적 호출은 각각 자기 자신만의 지역 이름 공간을 갖습니다.
 - Scope의 검색 순서
    - 가장 내부의 local namespace
    - 모듈의 inner global namespace
    - outer global namespace
    - built-in namespace
 - 이름을 global로 선언하면 모든 참조와 대입은 모듈의 전역 이름들을 포함하는 중간 스코프로 바로 갑니다.

### global, nonlocal 변수
- 아무것도 사용하지 않았을 때
```python
x = 10 # global
def foo():
    x = 30 # local 

foo()
print(x) # 15
```

- 함수에서 전역변수를 참조하고 하고 싶을때 
```python
x = 10 # global
def foo():
    global x
    x = 30 # local 

foo()
print(x) # 30
```

- 함수의 중첩에서 해당함수에 지역변수가 아니게 하고 싶을 때
```python
x = 10
def foo():
    x = 20

    def goo():
        nonlocal x 
        x = 40
    g()
    print(f'foo inner {x}') # 40

foo()
print(x) # 10
```

- nonlocal 주의 사항
```python
x = 10
def foo():
    nonlocal x 
    x = 20

foo() # SyntaxError: no binding for nonlocal 'x' found
```

-  대입은 데이터를 복사하지 않습니다 – 이름을 단지 객체에 연결할 뿐입니다. 삭제도 마찬가지입니다: 문장 del x 는 지역 스코프가 참조하는 이름 공간에서 x 의 연결을 제거합니다. 
- 클래스의 정의에 진입할 대 새 이름 공간이 만들어 지고 지역 스코프로 사용됩니다.
