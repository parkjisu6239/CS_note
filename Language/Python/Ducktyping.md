- **Duck Typing**

  Duck typing이란 특히 동적 타입을 가지는 프로그래밍 언어에서 많이 사용되는 개념으로, 객체의 실제 타입보다는 객체의 변수와 메소드가 그 객체의 적합성을 결정하는 것을 의미한다. Duck typing이라는 용어는 흔히 [duck test](https://en.wikipedia.org/wiki/Duck_test)라고 불리는 한 구절에서 유래됐다.

  > If it walks like a duck and it quacks like a duck, then it must be a duck.
  >
  > 만일 그 새가 오리처럼 걷고, 오리처럼 꽥꽥거린다면 그 새는 오리일 것이다.

  동적 타입 언어인 파이썬은 메소드 호출이나 변수 접근시 타입 검사를 하지 않으므로 duck typing을 넒은 범위에서 활용할 수 있다. 다음은 간단한 duck typing의 예시다.

  `class Duck: def walk(self): print('뒤뚱뒤뚱')

  ```
    def quack(self):
        print('Quack!')
  ```

  class Mallard:  # 청둥오리 def walk(self): print('뒤뚱뒤뒤뚱뒤뚱')

  ```
    def quack(self):
        print('Quaaack!')
  ```

  class Dog: def run(self): print('타다다다')

  ```
    def bark(self):
        print('왈왈')
  ```

  def walk_and_quack(animal): animal.walk() animal.quack()

  walk_and_quack(Duck())  # prints '뒤뚱뒤뚱', prints 'Quack!' walk_and_quack(Mallard())  # prints '뒤뚱뒤뒤뚱뒤뚱', prints 'Quaaack!' walk_and_quack(Dog())  # AttributeError : 'Dog' object has no attribute 'walk'`

  위 예시에서 `Duck` 과 `Mallard` 는 둘 다 `walk()` 와 `quack()` 을 구현하고 있기 때문에 `walk_and_quack()` 이라는 함수의 인자로서 **적합하다**. 그러나 `Dog` 는 두 메소드 모두 구현되어 있지 않으므로 해당 함수의 인자로서 부적합하다. 즉, `Dog` 는 적절한 duck typing에 실패한 것이다.

  Python에서는 다양한 곳에서 duck typing을 활용한다. `__len__()`을 구현하여 *길이가 있는 무언가* 를 표현한다던지 (흔히 [listy](https://cs.gmu.edu/~kauffman/cs310/w04-2.pdf)하다고 표현한다), 또는 `__iter__()` 와 `__getitem__()` 을 구현하여 [iterable](https://docs.python.org/3/glossary.html#term-iterable)을 duck-typing한다. 굳이 `Iterable` (가명) 이라는 interface를 상속받지 않고 `__iter__()`와 `__getitem__()`을 구현하기만 하면 `for ... in` 에서 바로 사용할 수 있다.

  이와 같은 방식은 일반적으로 `interface`를 구현하거나 클래스를 상속하는 방식으로 인자나 변수의 적합성을 runtime 이전에 판단하는 정적 타입 언어들과 비교된다. 자바나 스칼라에서는 `interface`, c++는 `template` 을 활용하여 타입의 적합성을 보장한다. (c++의 경우 `template`으로 duck typing과 같은 효과를 낼 수 있다 [참고](http://www.drdobbs.com/templates-and-duck-typing/184401971))