- **Generator**

  참고 : http://pythonstudy.xyz/python/article/23-Iterator와-Generator

  - Generator, Iterator, Iterable 객체 차이
    - Interable은 반복 가능한 객체로 list,set,tuple,dict가 포함된다.
    - Iterator는 값을 차례대로 꺼낼 수 있는 객체로, Iterable한 객체의 내장함수인 iter()로 만들어질 수 있다. 이렇게 생성된 Iterator는 Iterable 객체에 있는 값을 하나씩 꺼내며, next() 함수를 통해 순차적으로 값을 가져오게 할 수있다.
    - Gernerator는 Iterator의 일종으로, `yield` 를 이용해 필요한 순간에만 Lazy하게 Iterable한 객체를 만들 수 있다.

  ## Generator

  [Generator(제네레이터)](https://docs.python.org/3/tutorial/classes.html#generators)는 제네레이터 함수가 호출될 때 반환되는 [iterator(이터레이터)](https://docs.python.org/3/tutorial/classes.html#iterators)의 일종이다. 제네레이터 함수는 일반적인 함수와 비슷하게 생겼지만 `yield 구문`을 사용해 데이터를 원하는 시점에 반환하고 처리를 다시 시작할 수 있다. 일반적인 함수는 진입점이 하나라면 제네레이터는 진입점이 여러개라고 생각할 수 있다. 이러한 특성때문에 제네레이터를 사용하면 원하는 시점에 원하는 데이터를 받을 수 있게된다.

  ### **예제**

  ```python
  >>> def generator():
  ...     yield 1
  ...     yield 'string'
  ...     yield True
  
  >>> gen = generator()
  >>> gen
  <generator object generator at 0x10a47c678>
  >>> next(gen)
  1
  >>> next(gen)
  'string'
  >>> next(gen)
  True
  >>> next(gen)
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  StopIteration
  ```

  ### **동작**

  1. yield 문이 포함된 제네레이터 함수를 실행하면 제네레이터 객체가 반환되는데 이 때는 함수의 내용이 실행되지 않는다.
  2. `next()`라는 빌트인 메서드를 통해 제네레이터를 실행시킬 수 있으며 `next()` 메서드 내부적으로 iterator 를 인자로 받아 이터레이터의 `__next__()` 메서드를 실행시킨다.
  3. 처음 `__next__()` 메서드를 호출하면 함수의 내용을 실행하다 yield 문을 만났을 때 처리를 중단한다.
  4. 이 때 모든 local state 는 유지되는데 변수의 상태, 명령어 포인터, 내부 스택, 예외 처리 상태를 포함한다.
  5. 그 후 제어권을 상위 컨텍스트로 양보(yield)하고 또 `__next__()`가 호출되면 제네레이터는 중단된 시점부터 다시 시작한다.

  > yield 문의 값은 어떤 메서드를 통해 제네레이터가 다시 동작했는지에 따라 다른데, **next**()를 사용하면 None 이고 send()를 사용하면 메서드로 전달 된 값을 갖게되어 외부에서 데이터를 입력받을 수 있게 된다.

  ### **이점**

  List, Set, Dict 표현식은 iterable(이터러블)하기에 for 표현식 등에서 유용하게 쓰일 수 있다. 이터러블 객체는 유용한 한편 모든 값을 메모리에 담고 있어야 하기 때문에 큰 값을 다룰 때는 별로 좋지 않다. 제네레이터를 사용하면 yield 를 통해 그때그때 필요한 값만을 받아 쓰기때문에 모든 값을 메모리에 들고 있을 필요가 없게된다.

  > range()함수는 Python 2.x 에서 리스트를 반환하고 Python 3.x 에선 range 객체를 반환한다. 이 range 객체는 제네레이터, 이터레이터가 아니다. 실제로 next(range(1))를 호출해보면 TypeError: 'range' object is not an iterator 오류가 발생한다. 그렇지만 내부 구현상 제네레이터를 사용한 것 처럼 메모리 사용에 있어 이점이 있다.

  ```python
  >>> import sys
  >>> a = [i for i in range(100000)]
  >>> sys.getsizeof(a)
  824464
  >>> b = (i for i in range(100000))
  >>> sys.getsizeof(b)
  88
  ```

  다만 제네레이터는 그때그때 필요한 값을 던져주고 기억하지는 않기 때문에 `a 리스트`가 여러번 사용될 수 있는 반면 `b 제네레이터`는 한번 사용된 후 소진된다. 이는 모든 이터레이터가 마찬가지인데 List, Set 은 이터러블하지만 이터레이터는 아니기에 소진되지 않는다.

  ```python
  >>> len(list(b))
  100000
  >>> len(list(b))
  0
  ```

  또한 `while True` 구문으로 제공받을 데이터가 무한하거나, 모든 값을 한번에 계산하기엔 시간이 많이 소요되어 그때 그때 필요한 만큼만 받아 계산하고 싶을 때 제네레이터를 활용할 수 있다.

  ### **Generator, Iterator, Iterable 간 관계**

  https://camo.githubusercontent.com/b9f263e15badcde98f562297225d770eac1f0ef29291a822e01d09d43239945e/687474703a2f2f6e7669652e636f6d2f696d672f72656c6174696f6e73686970732e706e67