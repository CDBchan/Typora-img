## CS13. HTTP Client

- [x] DNS

- [ ] OSI 7계층

- [x] 소켓(웹소켓 뭔차이지?)

- [x] TCP, UDP

- [x] TCP 3-way HandShake

- [x] TCP 4-way HandShake

- [x] HTTP/1, HTTP/2, HTTP/3

  

- 미션
  - 잘 보냈는지 안보냈는지 OSI 3,4계층이 핵심이래
  - telnet이 먼지 확인하자 (telnt 주소 포트번호 -> 이런식으로 치면 연결이되네)
  - 목표는 4계층이 7계층에게 어떠한 정보를 주는지?  확인해보래
  - DNS를 lookup하는 라이브러리를 가져와서 쓰래, ip주소를 찾는방법을 알아보래
  - url 입력하면 DNS에서 주소를 찾고 그후 REQUEST를 보내면된데, REQUEST를 보내는걸 구현하라는듯



## DNS

<span style="color:red">DNS</span>란 Domain Name System의 약자로 사용자가 "www.naver.com"에 접속하려할때  해당 도메인에 대한 ip주소를 알아야 접속할수있다. 이때 ip주소를 알아내기위해  사용되는것이 DNS이다.

즉 **DNS란 웹사이트의 ip주소와 도메인조소를 이어주는 시스템이라 볼수있다.**



## Socket

![캡처](C:\Users\kdjin\OneDrive\바탕 화면\프로그래밍\mastersCode\정리자료\CS13(HTTP Client)\캡처.PNG)

<span style="color:red">Socket</span>이란 두 프로세스가 네트워크를 통해 통신할수 있도록 하는 소프트웨어 구조이다.

Socket은 IP주소와 포트번호를 결합하며, 일반적인 소켓 프로그래밍에서 두가지 통신 모드인 UDP와 TCP를 사용한다. 

클라이언트와 서버가 통신할때 2개의 소켓을 사용하며 각 소켓은 클라이언트와 서버에 각각 존재한다.



### 소켓 프로그래밍

![소켓 프로그래밍](C:\Users\kdjin\OneDrive\바탕 화면\프로그래밍\mastersCode\정리자료\CS13(HTTP Client)\소켓 프로그래밍.PNG)

소켓을 사용하여 어떻게 서버와 클라이언트가 통신을 하는지 알아보자.

클라이언트에  존재하는 소켓이 서버의 소켓에게 접속을하게되면 서버에 존재하는 소켓은 접속을한 해당 클라이언트의 소켓과 통신을 할수있는 소켓을 만든다.



## TCP 

<span style="color:red">TCP</span>란 신뢰성있는 데이터 통신을 가능하게 해주는 프로토콜이다.

우리가 네트워크를 통해 데이터를 보내는 과정에서 데이터가 손상되거나 데이터의 순서가 바뀔수있는데 TCP는 이 손실을 검색해 수정 및 재조합 해준다.



### TCP의 특징

1. 신뢰성 있는 통신을 가능하게한다.(따라서 UDP보다 속도가 느리다.)
2. 양방향 통신을 가능하게한다 (3-way HandShake, 4-way HandShake)
3. 흐름을 제어한다. 
   - CPU와 네트워크 대역폭의 차이때문에 서로 다른 데이터 속도로 동작을 할수있는데 이때 TCP는 데이터의 양을 제어하는 흐름 제어 매커니즘을 구현한다. 즉 **데이터 처리 속도를 조절한다고 생각하면 된다.**

4. 혼잡을 제어한다.
   - 네트워크 내의 패킷의 수가 과도하게 증가하지 않도록 제어한다.



### TCP 연결 및 연결 해제 

TCP는 Client와 Server간 <span style="color:blueViolet">연결을할때 3-way HandShake</span>를 <span style="color:blueViolet">연결을 해제할때 4-way Handshake</span>과정을 진행한다.

위 과정에서 **SYN, ACK**를 사용하며 SYN과 ACK는 아래와 같다.

> SYN (연결 요청 플래그): TCP에서 세션을 성립할떄 가장 먼저 보내는 패킷이며, 세션을 연결하는데 사용된다.
>
> ACK(응답): 상대방으로부터 패킷을 잘받았다고 알려주는 응답이다. 

<span style="color:yellowGreen">TCP 연결 과정(3-way Handshake)</span>

![3 way handshake](C:\Users\kdjin\OneDrive\바탕 화면\프로그래밍\mastersCode\정리자료\CS13(HTTP Client)\3 way handshake.PNG)

TCP는 연결을 할때 <span style="color:yellowGreen">3-way Handshake</span>를 통해 진행한다.

1. A클라이언트는 B서버에 접속을 하기위해 SYN 패킷을 보낸다. 이때 Client는 SYN+ACK응답을 기다리는 SYN_SENT상태가 된다

2. B서버는 SYN요청을 받은후 A클라이언트에게 연결을 허용한다는 SYN+ACK 패킷을 보낸후 Client가 ACK응답을 보내기를 기다리는상태 SYN_RECEIVED 상태가 된다.
3. A클라이언트는 SYN+ACK응답을 받고 ACK응답을 Server에게 보내면서 연결이 이루어진다.



<span style="color:yellowGreen">TCP 연결 해제 과정(4-way Handshake)</span>

![4 way handshake](C:\Users\kdjin\OneDrive\바탕 화면\프로그래밍\mastersCode\정리자료\CS13(HTTP Client)\4 way handshake.PNG)

TCP는 세션을 종료할때 즉 연결을 해제할때<span style="color:yellowGreen"> 4-way Handshake</span> 를 진행한다.

1. 클라이언트가 연결을 종료하겠다는 FIN플래그를 Server에게 전송한다.
2. FIN플래그를 받은 Server는 ACK를 Client에게 보내 해당 포트에 연결되어있는 애플리케이션에게 close를 요청한다.
3.  그후 서버또한 종료 프로세스를 진행하며 Client에게 FIN을 보낸다.
4. FIN을 받은 Client는 ACK를 Server에게 보내며 상태를 TIME-WAIT로 바꾼다.
   - 이때 TIME-WAIT에서 일정시간이 지나면 Client는 closed되고 클라이언트로부터 ACK받은 서보또한 포트를 CLOSED로 닫는다.
   - **TIME-WAIT**: 연결을 먼저 끊는쪽에서 생성되는 소켓이다. 혹시모를 전송실패를 대비하여 존재하는 소켓이며 TIME-WAIT가 없다면 패킷의 손실이 발생되거나 연결해제가 잘 되지 않을수 있다. (FIN이후에 네트워크의 지연으로 인해 데이터가 도착할수 있기때문에 TIME-WAIT를 통해 잉여 패킷을 기다리는 과정을 거치는 것이다.)



## UDP

<span style="color:red">UDP</span>는 비연결형 프로토콜이며 TCP와 다르게 각각의 패킷이 서로 다른경로를 통해 전송이 된다.



### UDP의 특징

1. 데이터 수신 여부를 확인하지 않는다.
2. 신뢰성이 낮다
   - UDP는 신뢰성보다는 연속성이 있는 전송을 필요로할때 사용한다. ex) Streaming
3. TCP보다 속도가 빠르다
4. 1:1 & 1:N & N:N 통신이 가능하다. 
   - TCP는 일대일 통신만 가능하지만 UDP는 1:N 통신 또한 가능하다. 이이유는 UDP는 비연결성 프로토콜이라 연결설정을 따로 하지 않기 때문이다.



### TCP & UDP 특징정리

![TCP UDP 특징 정리](C:\Users\kdjin\OneDrive\바탕 화면\프로그래밍\mastersCode\정리자료\CS13(HTTP Client)\TCP UDP 특징 정리.PNG)



|             | TCP                                         | UDP                                     |
| ----------- | ------------------------------------------- | --------------------------------------- |
| 연결 방식   | 연결형 프로토콜                             | 비연결형 프로토콜                       |
| 신뢰성      | 신뢰성 있는 데이터 전송                     | 신뢰성 없는 데이터 전송                 |
| 통신 방식   | 일대일 통신                                 | 일대일, 일대다 통신                     |
| 데이터 경계 | 데이터 경계 구분 안함(바이트 스트림 서비스) | 데이터 경계 구분함 (데이터 그램 서비스) |
| 속도        | 느리다                                      | 빠르다                                  |



## HTTP/1 & HTTP/2 & HTTP/3

### <span style="color:gray">HTTP/1</span>

![HTTP1](C:\Users\kdjin\OneDrive\바탕 화면\프로그래밍\mastersCode\정리자료\CS13(HTTP Client)\HTTP1.PNG)

<span style="color:red">HTTP/1</span>: HTTP/1을 사용하면 클라이언트가 서버에 같은 요청을 할때마다 개별적인 TCP connection이 필요했다.  



### <span style="color:gray">HTTP/1.1</span>

![http1.1](C:\Users\kdjin\OneDrive\바탕 화면\프로그래밍\mastersCode\정리자료\CS13(HTTP Client)\http1.1.PNG)

<span style="color:red">HTTP/1.1</span>: `keep-alive`라는 매커니즘을 통해 서버에 요청을 할떄마다 TCP connection이 필요한게 아닌 connection을 재사용할수있도록 했다. 이렇게 함으로서 request latency를 줄일수 있었는데 이 이유는 TCP연결을 시작할때 해야하는 3-WAY-Handshake 과정을 매번 하지 않아도 되기 때문이다.



![http1.1 (2)](C:\Users\kdjin\OneDrive\바탕 화면\프로그래밍\mastersCode\정리자료\CS13(HTTP Client)\http1.1 (2).PNG)

HTTP/1.1에서 새롭게 추가된 **pipelining** 기능을통해 Client는 서버로부터 응답이 오기전 여러개의 요청을 할수있게 되었다.



하지만  **pipelining**기능을 사용했을때, 서버가 하나의 response를 보내는데 많은 시간이 소요되면 그이후에 보내는 응답들또한 지연이되는 현상이 발생했다. 이때 먼저 전송이되야하는 response가 blocked되면 (ex) packet loss) 같은 connection에 존재하는 요청들에게도 영향이 가는 현상이 발생했다. 이러한 현상을 **HOLB** (Head-of-line Blocking) 라고 한다. (TCP는 패킷을 순서대로 처리해야하기때문에 HOLB가 발생한다.)  



**HOLB**때문에 여러웹브라우저들이 pipelining사용을 막았으며, 여러 통신을 하기위해선 병렬적으로 여러개의 connection을 사용해 데이터를 가져와야했다. 



### <span style="color:gray">HTTP/2</span>

![http2](C:\Users\kdjin\OneDrive\바탕 화면\프로그래밍\mastersCode\정리자료\CS13(HTTP Client)\http2.PNG)

<span style="color:red">HTTP/2</span>: HTTP/2부터는 하나의 TCP connection을 통해 여러개의 request를 stream의 형태로 보낼수 있게되었다.

이로인해 HTTP/1.1 pipelining을 사용하지 못해 여러개의 connection을 사용하여 병렬적으로 데이터를 가져와야하는 문제를 해결했다.(각각의 stream은 서로 독립적이기 때문에 하나가 block되더라도 다른 하나에 영향을 주지 않는다) 즉 **HOLB**가 Application layer에서는 해결이 되었지만  TCP를 사용하는 transport layer에서는 HOLB문제를 해결하지는 못했다. 



### <span style="color:gray">HTTP/3</span>

![http3](C:\Users\kdjin\OneDrive\바탕 화면\프로그래밍\mastersCode\정리자료\CS13(HTTP Client)\http3.PNG)

<span style="color:red">HTTP/3</span>: 새로운 protocol **QUIC**이 등장한다. QUIC은 UDP를 base로 만들어졌으며 TCP가 가지고있던 HOLB와 같은 문제점을 해결하며 레이턴시의 한계를 뛰어넘고자 구글이 개발한 UDP기반의 protocol이다.  



QUIC는 위에서 말했듯 UDP를 기반으로 만들어졌다. 따라서 TCP보다 속도가 빠르며, handShake과정또한 필요로 하지않는다(따라서 레이턴시가 감소한다). 하지만 UDP가 TCP에비해 신뢰도가 떨어진다는 사실을 알것이다. 그럼 QUIC는 신뢰도를 떨어뜨리는 대신 빠른 UDP를 사용하냐? 이건 아니다. 왜냐하면 UDP의 장점중 하나가 바로 **커스터마이징이다.** 



커스터마이징, 말그래도 UDP를 커스터마징을 통해 신뢰도를 TCP와 비슷한 수준으로 높일수 있다. 

그외에도 패킷 손실 감지에 걸리는 시간을 단축시키며, 멀티플렉싱을 지원... 등 여러 장점들이 있다.  자세한건 [HTTP/3는 왜 UDP를 선택한 것일까?](https://evan-moon.github.io/2019/10/08/what-is-http3/) 이 블로그를 참조하자.




- Reference
  - [소켓 관련 영상](https://www.youtube.com/watch?v=dX82Wuc18wk)
  - [3-way HandShake](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake)
  - [HTTP/1 & HTTP/2 & HTTP/3](https://www.youtube.com/watch?v=a-sBfyiXysI)