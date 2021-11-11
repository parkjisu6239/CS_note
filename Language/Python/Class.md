- **클래스를 상속했을 때 메서드 실행 방식**

  인스턴스의 메서드를 실행한다고 가정할 때 `__getattribute__()`로 bound 된 method 를 가져온 후 메서드를 실행한다. 메서드를 가져오는 순서는 `__mro__`에 따른다. MRO(method resolution order)는 메소드를 확인하는 순서로 파이썬 2.3 이후 C3 알고리즘이 도입되어 지금까지 사용되고있다. 단일상속 혹은 다중상속일 때 어떤 순서로 메서드에 접근할지는 해당 클래스의 `__mro__`에 저장되는데 왼쪽에 있을수록 우선순위가 높다. B, C 를 다중상속받은 D 클래스가 있고, B 와 C 는 각각 A 를 상속받았을 때(다이아몬드 상속) D 의 mro 를 조회하면 볼 수 있듯이 부모클래스는 반드시 자식클래스 이후에 위치해있다. 최상위 object 클래스까지 확인했는데도 적절한 메서드가 없으면 `AttributeError`를 발생시킨다.

  ```markdown
  class A:
      pass
  
  class B(A):
      pass
  
  class C(A):
      pass
  
  class D(B, C):
      pass
  
  >>> D.__mro__
  (__main__.D, __main__.B, __main__.C, __main__.A, object)
  ```

  Python 2.3 이후 위 이미지와 같은 상속을 시도하려하면 `TypeError: Cannot create a consistent method resolution` 오류가 발생한다.