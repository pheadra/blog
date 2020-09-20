---
id: list
title: Data structure
---
# 시퀀스형 자료구조 
## List
### List에 자주 사용되는 함수
- list.append(x) - 끝에 하나 추가 `a[len(a):] = [x]`
- list.extend(iterable) - 리스트 끝에 이터러블의 모든 항목을 덧붙임 `a[len(a):] = iterable`
- list.insert(i, x)
- list.remove(x)
- list.pop([i]) 
- list.clear()
- list.index(x[, start[, end]]) -- 리스터에서 x의 항목에 인덱스를 리턴 값이 없으면 ValueError를 리턴함
- list.count(x) - 리스트에서 x의 등장 횟수를 리턴
- list.sort(key=None, reverse=False) 
- list.reverse()
- list.copy() - 얇은 사본 `a[:]`와 동일

### Queue
```python
# 큐를 사용하고 싶을 때는 collections.deque 를 사용하라
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])
```

### 리스트 컴프리헨션
리스트 컴프리헨션은 리스트를 만드는 간결한 방법을 제공합니다. 
```python
squares = list(map(lambda x: x**2, range(10)))

squares = [x**2 for x in range(10)]
```


## Tuple
- tuple은 불변이고 다른 타입을 담을 수 있습니다
- 언패킹하거나 인덱스를 통해서 접근합니다.

### 항목이 없거나 하나만 있는 튜블
```python
>>> empty = ()
>>> singleton = 'hello',    # <-- note trailing comma
>>> len(empty)
0
>>> len(singleton)
1
>>> singleton
('hello',)
```


### Tuple Unpacking
```python
>>> t = 12345, 54321, 'hello!'
>>> x, y, z = t
>>> x
12345
>>> y
54321
>>> z
'hello!'
```

# 집합형 자료구조, 해시가능 
## Set
- 집합은 중복되는 요소가 없는 순서 없는 컬렉션
- 기본적인 용도는 멤버십 검사(exists)와 중복 엔트리 제거(unique)입니다. 
- 집합 객체는 합집합, 교집합, 차집합, 대칭 차집합과 같은 수학적인 연산들도 지원합니다.
- 빈집합은 {}가 아닌 Set() 입니다. {}은 dict에서 사용 

```python
>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> print(basket)                      # show that duplicates have been removed
{'orange', 'banana', 'pear', 'apple'}
>>> 'orange' in basket                 # fast membership testing
True
>>> 'crabgrass' in basket
False

>>> a = set('abracadabra')
>>> b = set('alacazam')
>>> a                                  # unique letters in a
{'a', 'r', 'b', 'c', 'd'}
>>> a - b                              # letters in a but not in b
{'r', 'd', 'b'}
>>> a | b                              # letters in a or b or both
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
>>> a & b                              # letters in both a and b
{'a', 'c'}
>>> a ^ b                              # letters in a or b but not both
{'r', 'd', 'b', 'm', 'z', 'l'}
```


### Set Comprehension
리스트의 경우 [], Set의 경우 {}
```python
>>> a = {x for x in 'abracadabra' if x not in 'abc'}
>>> a
{'r', 'd'}
```

# 매핑형 자료구조
## Dictionary (dict)
- 다른 언어에서는 associate memories, associative array
- 숫자로 인덱싱 되는 시퀀스와 달리, 딕셔너리는 키로 인덱싱되는데 모든 불변형을 사용할 수 있음
- 튜플이 문자열, 숫자, 튜플들만 포함하면, 키로 사용될 수 있습니다; 튜플이 직접적이나 간접적으로 가변 객체를 포함하면, 키로 사용될 수 없습니다. 
- 빈값은 {}
```python
>>> tel = {'jack': 4098, 'sape': 4139}
>>> tel['guido'] = 4127
>>> tel
{'jack': 4098, 'sape': 4139, 'guido': 4127}
>>> tel['jack']
4098
>>> del tel['sape']
>>> tel['irv'] = 4127
>>> tel
{'jack': 4098, 'guido': 4127, 'irv': 4127}
>>> list(tel) # 키가 얻어짐
['jack', 'guido', 'irv']
>>> sorted(tel) # 키를 정렬한 값
['guido', 'irv', 'jack']
>>> 'guido' in tel
True
>>> 'jack' not in tel
False
```

```python
# 튜블의 시퀀스를 통해서 dict를 생성
>>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])

# dict comprehansion
>>> {x: x**2 for x in (2, 4, 6)}

# 키가 문자인 경우 키워드 인자 방식으로 지정 가능
>>> dict(sape=4139, guido=4127, jack=4098)
```

### 자주사용하는 반복문 패턴
```python
>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> for k, v in knights.items():
...     print(k, v)

### 시퀀스를 반복할때 인덱스를 얻고 싶으면 enumerate를 사용
>>> for i, v in enumerate(['tic', 'tac', 'toe']):
...     print(i, v)

### sorted는 원본을 바꾸지 않고 정렬된 값을 받고 싶을때 사용
>>> basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
>>> for f in sorted(set(basket)):
...     print(f)
```

