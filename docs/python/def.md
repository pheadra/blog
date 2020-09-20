---
id: def
title: Definition
---

### 변수의 선언
타임에 대한 정의나 변수에 대한 선언은 따로 없기 때문에 
쓰는 즉시 사용 가능


### 함수의 선언
```python
def function_name(param1, param2):
    pass;
```



### 자주 실수 할 수 있는 부분
```python
# 이렇게 하면 f를 호출하는 곳에서 L에 선언시 만들어진 []에 레퍼런스가 디폴드 값이기 때문에 []를 공유하여 사용함 
def f(a, L=[]]):
    L.append(a)
    return L

def f(a, L=None):
    if L is None:
        L = []
    L.append(a)
    return L
```


### 클래스의 정의
```python
class ClassName:
    <statement - 1>
    ...
    <statement - N>
```
- 클래스의 정의에 진입할 대 새 이름 공간이 만들어 지고 지역 스코프로 사용됩니다.