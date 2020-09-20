---
id: iterator
title: Iterator
---

## iterator usage
### for
```python
for element in [1, 2, 3]:
    print(element)
for element in (1, 2, 3):
    print(element)
for key in {'one':1, 'two':2}:
    print(key)
for char in "123":
    print(char)
for line in open("myfile.txt"):
    print(line, end='')
```

### next()
```python
#  for문은 iter()를 호출하고 이함수는 메소드 __next__()를 정의하는 이터레이터 객체를 돌려줍니다.

a = 'abc'
it = iter(s)
next(it) # a
next(it) # b
next(it) # c
next(it) 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    next(it)
StopIteration
```

### Class를 통한 Iterator Implement
```python
# __next__() 메서드를 가진 객체를 돌려주는 __iter__()를 정의합니다.
class Reverse:
    """Iterator for looping over a sequence backwards."""
    def __init__(self, data):
        self.data = data
        self.index = len(data)

    def __iter__(self):
        return self

    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]
```


## Generator 를 통한 Iterator Implement
- 제너레이터는 이터레이터를 만드는 가장 쉬운 툴입니다.
- 제너레이터로 할 수 있는 모든것은 클래스 기반 이터레이터로도 할 수 있습니다.
- 제너레이터가 간단한 이유는 __iter__()와 __next__()가 저절로 만들어지기 때문입니다.

```python
def reverse(data):
    for index in range(len(data)-1, -1, -1):
        yield data[index]

>>> for char in reverse('golf'):
...     print(char)
```


### Generator Expression
- list comprehension와 유사하지만 []대신 ()를 사용하고 list보다는 메모리를 적게 사용하는 경향이 있음

```python
>>> sum(i*i for i in range(10))                 # sum of squares
285
>>> xvec = [10, 20, 30]
>>> yvec = [7, 5, 3]
>>> sum(x*y for x,y in zip(xvec, yvec))         # dot product
260
>>> unique_words = set(word for line in page  for word in line.split())
``` 
