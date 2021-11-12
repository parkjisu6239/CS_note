- **JavaScript Event Loop**

  JS Engine은 Call Stack, Task Queue, Heap, 그리고 Event Loop로 이루어진다.

  - `콜스택`은 말그대로 함수 콜스택이다. 스택에 가장 위에 있는 함수부터 수행되고, 수행이 완료되면 스택에서 빠진다.
  - `Heap` 에는 동적으로 생성된 인스턴스가 할당된다.
  - `Task Queue` : 처리해야하는 Task를 임시로 저장하는 대기열로, 콜스택이 비어졌을 때 대기열에 먼저 들어온 순서로 콜스택으로 옮긴다. JS에서 비동기로 호출되는 함수는 바로 콜스택으로 가는 것이 아니라, task queue로 온다. 예를 들면 이벤트 핸들러나, setTimeout 등. 그리고 WebAPI 영역의 코드도 비동기로 처리되기 때문에 여기로 넘어온다.
  - `EventLoop` : 콜스택이 비었는지 확인하여, 비었다면 Task Queue의 작업을 옮기는 역할