# PORT 개념

### PORT란

PORT는 `논리적인 접속장소` 이다. 

하나의 컴퓨터에는 여러 개의 서버가 있을 수 있기 때문에, 이 서버들을 식별하기 위해 PORT 번호를 이용한다.

네트워크 상의 두 기기가 TCP/IP통신을 할 때, IP를 토대로 해당 서버가 있는 컴퓨터에 접근하고,

PORT 번호를 이용해서 컴퓨터 내의 어느 서버에 접근해야 하는지를 알 수 있다. 



주소로 예를 들자면, 

서울시 동작구 xx-yy번지 : IP주소

102호, 204호 : PORT번호

### PORT 번호

- 16비트이다.

- 0번 ~ 65535번까지 존재한다. 

  > 2^16 = 65,536개

- 0번 ~ 1023번 : well-known port

  - 잘 알려진 특정한 프로그램의 사용을 위해 예약되어있다.
  - 국제 도메인 관리기구의 통제를 받는다.
  - root권한으로만 열 수 있다. 

  - 예시 
    - 80번 : http 기본 포트 
    - 443 : https 기본 포트

- 1024번 ~ 49151번 : registered port

  - 국제 도메인 관리기구에 등록되어 있다.

- 49152번 ~ 65535번 : dynamic port

  - 임시포트들이기 때문에, 프로세스들이 임의로 사용할 수 있다. 



명확하게 와닿는 설명이 없었다. 내가 이해한 바로는 

well-known port : 다같이 특정 용도로 사용하자고 약속해놓은 포트들 

ex) http, https 등..

registered port : 내가 서버를 열고 싶을 때 사용

ex) react 서버, nodejs 서버 등..

dynamic port : 계속 열어두는 용도의 포트가 아니라, 임시로 연결이 필요할 때?

ex) unity ml-agents 

라고 표현할 수 있을 것 같다. 



##### 추가 ) well-known port 종류

![TCP/IP가 보이는 그림책(이정현, 임세진, 윤재웅). 제4장 트랜스포트층 | by Jeong Hyeon Lee | Quantum  Ant | Medium](https://miro.medium.com/max/1400/1*LvRY4esQeu040YkAjfkLCw.jpeg)

[출처](https://medium.com/quantum-ant/tcp-ip%EA%B0%80-%EB%B3%B4%EC%9D%B4%EB%8A%94-%EA%B7%B8%EB%A6%BC%EC%B1%85-%EC%9D%B4%EC%A0%95%ED%98%84-%EC%9E%84%EC%84%B8%EC%A7%84-%EC%9C%A4%EC%9E%AC%EC%9B%85-b905f8244239)

### 웹 서버 관련 추가 내용

http로 특정 URL에 접속할 때, 뒤에 포트번호를 생략하면 자동으로 80번포트로 접속이 된다.

> http://localhost 에 접속하면, 결국 http://localhost:80 에 접속하는 것이다. 
>
> 80이외의 포트에 접근하고 싶을 때에는
>
> http://localhost:8080 과 url 뒤에 같이 포트 번호를 명시해주어야한다.

웹 서버를 더 열고 싶을 때에는, well-known port가 아닌 다른 port에 열어서 사용한다.

관습적으로 8080을 많이 이용한다. 

