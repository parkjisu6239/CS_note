# TCP vs UDP



### ▪ TCP (Transmission Control Protocol)

-  IP 네트워크의 두 컴퓨터 간의 연결 지향 통신을 위한 전송 계층 호스트 간 프로토콜
- TCP는 기본적으로 unreliable network에서, reliable network를 보장할 수 있도록 하는 프로토콜
  - reliable network를 보장한다는 것은 4가지 문제점 존재
    - 손실 : packet이 손실될 수 있는 문제
    - 순서 바뀜 : packet의 순서가 바뀌는 문제
    - Congestion : 네트워크가 혼잡한 문제
    - Overload : receiver가 overload 되는 문제
- TCP는 network congestion avoidance algorithm을 사용
  - 흐름제어 (endsystem 대 endsystem)
    - 송신측과 수신측의 데이터 처리 속도 차이를 해결하기 위한 기법
    - Flow Control은 receiver가 packet을 지나치게 많이 받지 않도록 조절하는 것
    - 기본 개념은 receiver가 sender에게 현재 자신의 상태를 feedback 한다는 점
  - 혼잡제어 : 송신측의 데이터 전달과 네트워크의 데이터 처리 속도 차이를 해결하기 위한 기법



### ▪ UDP





------

[ 참고 사항 ]

