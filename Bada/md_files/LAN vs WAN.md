# LAN vs WAN 

네트워크는 전송매체의 연결로 구성된 장치들의 모임이다.

네트워크는 크기에 따라 LAN, MAN, WAN으로 나눈다. 

LAN < MAN < WAN 순서로 크기가 크다. 

이렇게 크기에 따라 나누는 이유는 트래픽을 최소화하기 위해서이다. 

교통에 비유하자면, 차가 목적지에 가기 위한 최소한의 도로만을 경유하도록 해서 혼란스럽지 않게 하기 위함이다. 동네 마트에 가려는 사람이 고속도로를 타게되는 일을 막는다는 것이다. 

따라서 LAN 내에서 이루어지는 통신은 LAN 내부에서 해결하도록 하고, MAN 내에서 이루어지는 통신은 MAN 범위 안에서만 해결하도록 한다. 

### LAN (Local Area Network)

말 그대로, 가까운 거리에 위치한 장비들의 네트워크이다. 

예를들면 학교, 회사, 집 내에서 장비들을 서로 연결한 것이다. 

장비들을 1:1로 직접 연결하는 것이 아니라, 공유기나 스위치등을 이용해서 연결한다. 

네트워크 구성시에 드는 비용과 전기세를 제외하고 따로 유지보수비용이 들어가지 않는다. 

통신시에 이더넷 프로토콜을 주로 사용한다. 

### WAN (Wide Area Network)

LAN과 LAN사이(혹은 MAN)를 연결해서 광범위한 지역 단위로 구성된 네트워크를 말한다. 

> 이와 관련해서 WAN의 정의를 
>
> 1. LAN을 벗어나, 다른 LAN과 연결되면 WAN이다.
> 2. LAN이 모여 MAN이고, MAN이 모여 WAN이 된다. 
>
> 위처럼 사람들마다 다르게 이야기 하는데. 이걸 구분하는게 크게 중요하지는 않은 것 같다!

<img src="..\images\LAN_WAN_1" alt="image-20211018180405235" style="zoom: 67%;" />

### LAN과 WAN 연결 형태 비교

![lan-wan](https://juner417.github.io/assets/post_images/2018-03-21-network-101-lan-wan/lan-wan.png)

> L2 Switch 로 연결된 네트워크 : LAN
>
> L3 Router로 연결된 네트워크 : WAN

[출처](https://juner417.github.io/blog/network-101-lan-wan/)

### 추가 ) MAN (Metropolitan Area Network)

LAN과 WAN사이의, 도시규모로 연결된 네트워크를 말한다. 



### 인터넷은 어떻게 동작하는가?

https://developer.mozilla.org/ko/docs/Learn/Common_questions/How_does_the_Internet_work



궁금했던 것들에 대해 뇌피셜로 적어본 답변들

### Q) 인터넷은 뭔가?

인터넷은 전 세계 컴퓨터들을 하나로 연결하는 거대한 컴퓨터 통신망을 의미한다.

즉, 엄청 큰 네트워크를 의미하는 것으로 WAN과 비슷한 개념이다. 

### Q) TCP, IP 이런건 어디에 쓰이는데?

LAN은 이더넷 프로토콜로 통신하고, 

WAN은 PPP 등으로 통신한다고 한다.

근데 여기서 이더넷과 PPP는 모두 2계층(링크계층) 프로토콜이다!

그리고 TCP는 4계층, IP는 3계층 프로토콜이기 때문에 

결과적으로 TCP, IP는 LAN WAN어디서든 쓰일 수 있다. 

TCP를 IP로 싸고, IP를 LAN에서는 이더넷프로토콜로 전송하는거고, WAN에서는 다른 프로토콜로 전송하는 방식~~인 것 같다.~~

** HTTP는 7계층 프로토콜이다. 





https://www.guru99.com/lan-vs-wan.html

https://better-together.tistory.com/110