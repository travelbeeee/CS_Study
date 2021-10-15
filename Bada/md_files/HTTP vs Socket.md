# HTTP vs Socket

네트워크를 통해 서버에서 데이터를 가져오기 위한 통신 방식은 HTTP, Socket으로 크게 두 가지로 구분할 수 있다. 

가장 큰 차이점은  `접속(Connection)`을 유지하느냐/안하느냐 입니다.

접속을 유지함 : Socket

접속을 유지 안함 : HTTP



### HTTP

> Client의 요청(Request)이 있을 때만 Server가 응답(Response)하고 곧바로 연결을 종료하는 방식

Socket연결 위에서 맺어지는 애플리케이션 계층(7번째 계층)에서 이루어지는 연결 방식이다. 

클라이언트의 요청이 있을 때, 서버가 자료를 전송하고 곧바로 연결을 끊는다. 

서버의 부하를 줄여서 다른 접속을 원활하게 처리하기 위함이다. 

필요한 경우에만 Server에 요청하는 콘텐츠 위주의 데이터를 사용할 때 좋다. 

<img src="https://t1.daumcdn.net/cfile/tistory/99926F335C6939EA38" alt="img" style="zoom:50%;" />

### Socket

> Server와 Client가 특정 Port를 통해 실시간으로 양방향 통신을 하는 방식

~~TCP를 기반으로 맺어진 네트워크 연결 방식이다.~~ 

** TCP, UDP 둘다 가능하다 

** 웹소켓?

클라이언트와 서버가 접속이 되면, 둘 중 하나에서 강제로 접속을 해제할 때 까지 접속이 유지된다. 

따라서 서버의 능력에 따라 동시 접속 가능한 클라이언트의 수가 제한된다. 

동영상 스트리밍, 채팅 등 실시간으로 통신이 필요한 경우에 좋다. 

<img src="https://t1.daumcdn.net/cfile/tistory/9939C6385C6939FD26" alt="img" style="zoom:50%;" />