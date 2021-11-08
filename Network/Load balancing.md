# Load balancing

[자세한 내용](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Network/로드 밸런싱(Load Balancing).md)

물리적 서버의 부하를 분산하고, 일부 서버가 동작을 멈추더라도 서버가 유연하게 이에 대응할 수 있게한다.

- [서버 선택 방법](https://www.educative.io/courses/grokking-the-system-design-interview/3jEwl04BL7Q)

  - **Round Robin Method**
  - **Weighted Round Robin Method**
  - **Least Response Time Method**
  - **Least Connection Method**
  - **Least Bandwidth Method**
  - **IP Hash**

- 로드 밸런서에 장애가 생길 경우에는 ?

  서버가 아니라 로드 밸런서에 문제가 생기는 경우에는 요청을 서버로 분배하지 못하기 때문서버가 건강하더라도 응답을 못하는 문제가 발생한다. 이를 대비하여 로드밸런서를 이중화한다.
