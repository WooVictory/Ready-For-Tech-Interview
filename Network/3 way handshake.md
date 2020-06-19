## 3 way handshake

TCP/IP 프로토콜을 이용하여 통신을 진행할 때, 두 종단 간 **정확한** 데이터 전송을 보장하기 위해 연결을 설정하는 과정이다.

<img src="https://user-images.githubusercontent.com/33534771/75338886-d77ea880-58d2-11ea-84c3-f8b60663f9c6.png" width="60%"/>


**[연결 과정]**

> SYN : Synchronize Sequence Number
>
> ACK : Acknowledgement

1) 클라이언트는 서버에 접속을 요청하는 SYN(a) 패킷을 보낸다.

2) 서버는 클라이언트의 요청인 SYN(a) 패킷에 대한 요청 수락 응답으로 ACK(a+1) 패킷과 클라이언트도 포트를 열어달라는 SYN(b) 패킷을 보낸다.

3) 클라이언트는 ACK(a+1) 패킷과 SYN(b) 패킷을 받고 이에 대한 응답으로 ACK(b+1) 패킷을 보내며 연결이 성립된다.



**[Q. 왜 2way가 아니라 3way일까?]**

**TCP**는 `양방향성 연결`이기 때문에 클라이언트에서 서버에게 자신의 존재를 알리고 패킷을 보낼 수 있는 것처럼 서버에서도 클라이언트에게 자신의 존재를 알리고 패킷을 보낼 수 있다는 신호를 보내야 하기 때문이다.



**[참고]**

**처음에 클라이언트에서 SYN 패킷을 보낼 때 Sequence Number에는 랜덤한 숫자가 담겨진다.** 

Connection을 맺을 때, 사용하는 포트(port)는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용한다. 따라서 이전에 사용한 포트 번호를 재사용할 가능성이 있다.

Sequence Number가 순차적인 숫자로 전송된다면 서버는 이전의 Connection으로부터 전송되는 패킷으로 인식할 수 있다. 따라서 이러한 문제를 해결하기 위해 난수로 초기 Sequence Number를 설정한다.



## 4 way handshake

TCP/IP 프로토콜을 이용한 통신 과정에서는 위에서 언급했던 것처럼 3 way handshake 과정을 통해 연결을 설정하고 4 way handshake 과정을 통해 연결 설정을 해제한다.

<img src="https://user-images.githubusercontent.com/33534771/75338959-ef562c80-58d2-11ea-99eb-1c09ec97e83a.png" width="60%"/>



**[연결 과정]**

1) 클라이언트는 서버에게 연결을 종료하겠다는 FIN 패킷을 보낸다.

2) 서버는 클라이언트의 요청(FIN)에 대한 응답으로 ACK 패킷을 보낸다.

​	2-1) 처리해야 할 자신의 통신이 끝날 때까지 기다린다.

3) 처리해야 할 모든 통신을 끝마쳤다면 연결을 종료하겠다는 FIN 패킷을 보낸다.

4) 클라이언트는 FIN 패킷에 대한 확인 응답으로 ACK 패킷을 보낸다.

5) 클라이언트의 ACK 패킷을 받은 서버는 소켓 연결을 close 한다.

6) 클라이언트는 아직 서버로부터 받지 못한 데이터가 있을 것을 대비해 기다리는 과정을 거친다.(TIME_WAIT)



[에러 발생]

클라이언트에서 FIN 패킷 전송 후 ACK 패킷을 기다리는 FIN_WAIT1과 서버의 ACK 패킷을 받은 후 FIN 패킷을 기다리는 FIN_WAIT2 에러 발생으로 인해 Time out이 되면 스스로 연결을 종료한다.



그러나, CLOSE_WAIT은 Application이 close()를 적절하게 처리하지 못하면 CLOSE_WAIT 상태로 계속 기다리게 되어 Socket Hang Up 에러가 발생할 수 있다.
