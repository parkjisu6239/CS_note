# TCP vs UDP

- TCP와 UDP의 비교

  - UDP

    - `UDP(User Datagram Protocol, 사용자 데이터그램 프로토콜)`는 **비연결형 프로토콜** 이다. IP 데이터그램을 캡슐화하여 보내는 방법과 연결 설정을 하지 않고 보내는 방법을 제공한다.
    - `UDP`는 흐름제어, 오류제어 또는 손상된 세그먼트의 수신에 대한 재전송을 **하지 않는다.**
    - TCP에 비해 빠른 응답 속도를 가진다. 메시지의 양도 적다. 중간에 유실되는 것에 대해서는 재전송을 요청 하면 된다.
    - `UDP`를 사용한 것들에는 `DNS`가 있다. 어떤 호스트 네임의 IP 주소를 찾을 필요가 있는 프로그램은, DNS 서버로 호스트 네임을 포함한 UDP 패킷을 보낸다. 이 서버는 호스트의 IP 주소를 포함한 UDP 패킷으로 응답한다. 사전에 설정이 필요하지 않으며 그 후에 해제가 필요하지 않다.

  - TCP

    - 대부분의 인터넷 응용 분야들은 **신뢰성** 과 **순차적인 전달** 을 필요로 한다.

    - `TCP(Transmission Control Protocol, 전송제어 프로토콜)`는 신뢰성이 없는 인터넷을 통해 종단간에 신뢰성 있는 **바이트 스트림을 전송** 하도록 특별히 설계되었다.

    - TCP 서비스는 송신자와 수신자 모두가 소켓이라고 부르는 종단점을 생성함으로써 이루어진다.

    - 모든 TCP 연결은 전이중(full-duplex), 점대점(point to point)방식이다. 전이중이란 전송이 양방향으로 동시에 일어날 수 있음을 의미하며 점대점이란 각 연결이 정확히 2 개의 종단점을 가지고 있음을 의미한다. TCP 는 멀티캐스팅이나 브로드캐스팅을 지원하지 않는다.

    - TCP의 주요 성질

      ### 1. Connection oriented

      두 개 엔드포인트(로컬, 리모트) 사이에 연결을 먼저 맺고 데이터를 주고받는다. 여기서 'TCP 연결 식별자'는 두 엔드포인트의 주소를 합친 것으로, <로컬 IP 주소, 로컬 포트번호, 리모트 IP 주소, 리모트 포트번호> 형태이다.

      ### 2. Bidirectional byte stream

      양방향 데이터 통신을 하고, 바이트 스트림을 사용한다.

      ### 3. In-order delivery

      송신자(sender)가 보낸 순서대로 수신자(receiver)가 데이터를 받는다. 이를 위해서는 데이터의 순서가 필요하다. 순서를 표시하기 위해 32-bit 정수 자료형을 사용한다.

      ### 4. Reliability through ACK

      데이터를 송신하고 수신자로부터 ACK(데이터 받았음)를 받지 않으면, 송신자 TCP가 데이터를 재전송한다. 따라서 송신자 TCP는 수신자로부터 ACK를 받지 않은 데이터를 보관한다(buffer unacknowledged data).

      ### 5. Flow control

      송신자는 수신자가 받을 수 있는 만큼 데이터를 전송한다. 수신자가 자신이 받을 수 있는 바이트 수 (사용하지 않은 버퍼 크기, receive window)를 송신자에게 전달한다. 송신자는 수신자 receive window가 허용하는 바이트 수만큼 데이터를 전송한다.

      ### 6. Congestion control

      네트워크 정체를 방지하기 위해 receive window와 별도로 congestion window를 사용하는데 이는 네트워크에 유입되는 데이터양을 제한하기 위해서이다. Receive window와 마찬가지로 congestion window가 허용하는 바이트 수만큼 데이터를 전송하며 여기에는 TCP Vegas, Westwood, BIC, CUBIC 등 다양한 알고리즘이 있다. Flow control과 달리 송신자가 단독으로 구현한다.



------

[ 참고 사항 ]

