- **PyPy 가 CPython 보다 빠른 이유**

  py 파일에는 소스코드가 포함되어 있지만, pyc 파일은 컴파일한 바이트 코드를 갖고 있다. 일반적으로 pyc파일이 있으면, 이 파일을 사용하고 아니면 py 파일을 사용한다.

  간단히 말하면 CPython 은 일반적인 인터프리터인데 반해 PyPy 는 [실행 추적 JIT(Just In Time) 컴파일](https://en.wikipedia.org/wiki/Tracing_just-in-time_compilation)을 제공하는 인터프리터기 때문이다. PyPy 는 RPython 으로 컴파일된 인터프리터인데, C 로 작성된 RPython 툴체인으로 인터프리터 소스에 JIT 컴파일을 위한 힌트를 추가해 CPython 보다 빠른 실행 속도를 가질 수 있게 되었다.

  ### **PyPy**

  PyPy 는 파이썬으로 만들어진 파이썬 인터프리터다. 일반적으로 파이썬 인터프리터를 다시 한번 파이썬으로 구현한 것이기에 속도가 매우 느릴거라 생각하지만 실제 PyPy 는 [스피드 센터](http://speed.pypy.org/)에서 볼 수 있듯 CPython 보다 빠르다.

  ### **실행 추적 JIT 컴파일**

  메소드 단위로 최적화 하는 전통적인 JIT 과 다르게 런타임에서 자주 실행되는 루프를 최적화한다.

  ### **RPython(Restricted Python)**

  [RPython](https://rpython.readthedocs.io/en/latest/index.html)은 이런 실행 추적 JIT 컴파일을 C 로 구현해 툴체인을 포함한다. 그래서 RPython 으로 인터프리터를 작성하고 툴체인으로 힌트를 추가하면 인터프리터에 실행추적 JIT 컴파일러를 빌드한다. 참고로 RPython 은 PyPy 프로젝트 팀이 만든 일종의 인터프리터 제작 프레임워크(언어)다. 동적 언어인 Python 에서 표준 라이브러리와 문법에 제약을 가해 변수의 정적 컴파일이 가능하도록 RPython 을 만들었으며, 동적 언어 인터프리터를 구현하는데 사용된다.

  이렇게 언어 사양(파이썬 언어 규칙, BF 언어 규칙 등)과 구현(실제 인터프리터 제작)을 분리함으로써 어떤 동적 언어에 대해서라도 자동으로 JIT(Just-in-Time) 컴파일러를 생성할 수 있게 되었다.