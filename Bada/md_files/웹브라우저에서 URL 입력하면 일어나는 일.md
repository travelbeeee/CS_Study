### 웹브라우저에서 URL 입력하면 일어나는 일

<img src="https://blog.kakaocdn.net/dn/wiMFO/btqRQRyz99s/nye4ypShfR7YKZrPa3mVK0/img.png" alt="img" style="zoom:50%;" />

웹 브라우저 

** URL 파싱

** hsts

 DNS 통해서 IP주소 받아옴

받아온 IP 주소로 http 요청 생성

요청 보내기 전에 3-way handshake로 연결 확립

<img src="https://blog.kakaocdn.net/dn/Cf0j1/btqR6vncCyJ/41eiRm1Vh0me2uXDvan9sk/img.png" alt="img" style="zoom:50%;" />

TCP헤더, IP헤더 붙인 후 만들어진 패킷을 서버에 전달

<img src="https://blog.kakaocdn.net/dn/cAEOt7/btqR9lLnjND/xKZUx4qmrRPBwM0QslAcA0/img.png" alt="img" style="zoom:50%;" />

서버는 받은 패킷을 해석해서 응답 메세지를 생성한다

<img src="https://blog.kakaocdn.net/dn/dK57yl/btqRTRE6Z3Q/LsJs8QkzSKi92RfasKzrdK/img.png" alt="img" style="zoom:50%;" />

응답 메세지를 다시 브라우저에세 전송하면,

<img src="https://blog.kakaocdn.net/dn/bGy0bw/btqR9mDxn1b/ygcK56uMAP04pZjqWpq4d1/img.png" alt="img" style="zoom:50%;" />

브라우저는 해당 패킷을 해석해 HTML을 화면에 렌더링해준다. 

#### DNS?

Domain Name System의 약자로, 호스트의 도메인 이름을 네트워크 주소로 변환 혹은 그 반대의 변환을 할 수 있도록 개발되었다. 

DN (Domain Name) : www.naver.com (문자열의 탈을 쓴 IP)

##### 사용 이유

길고 복잡한 IP주소를 일일이 외우기가 힘들어서 문자 주소(DN)을 사용하기 위해 DNS를 이용한다.

##### 동작 과정

![img](https://www.netmanias.com/ko/?m=attach&no=1997)

#### Router?

전용 회선을 통해 LAN에 연결된 컴퓨터들이 동시에 인터넷을 사용할 수 있게 해주는 장비이다.

데이터를 목적지까지 전달하는 기능을 수행한다.

IP네트워크, 서브넷을 관리하면서 다른 네트워크를 거쳐 패킷을 전송하는 역할을 하는 장비이며, 라우팅은 그 패킷을 보낼 경로를 선택하는 과정이다. 

##### 동작 원리

패킷의 전송 경로를 결정하기 위해 

1. 랜 테이블

   라우터에 연결되어 있는 랜 세그먼트 내 장치의 주소들을 관리한다.

   패킷의 목적지가 같은 네트워크 내에 있는지 필터링하는 역할을 한다.

2. 네트워크 테이블

   네트워크 상의 모든 라우터 주소를 보관한다.

   패킷을 전달할 네트워크 주소를 찾는데 사용한다. 

3. 라우팅 테이블

   각 경로에 대한 정보를 유지한다.

   패킷의 가장 효율적인 경로를 결정하는데 사용한다.

을 사용한다. 

라우터는 이를 이용해 네트워크에 연결된 모든 장치들의 주소를 인식하고, 이를 바탕으로 패킷을 어디로 전송할지 결정한다. 

#### ARP (Address Resolution Protocol)?

논리 주소인 IP를 물리 주소인 MAC 주소로 바꾸는 역할을 하는 '주소 해석 프로토콜'이다. 

데이터 전송시에 라우터(3계층)에서 ARP를 이용해 IP -> MAC 주소로 바꾸고, 해당 MAC주소를 넣어 Encapsulation한 후에 2계층으로 내려보낸다.

##### 동작 방식

송신 컴퓨터가 수신지의  MAC 주소를 모르면, 수신지의 IP주소를 이용해 MAC 주소를 찾는 요청을 브로드캐스트로 보낸다. (ARP 요청)

이 요청에 대해, 지정된 IP주소와 다른 IP의 컴퓨터는 응답하지 않고, 

지정된 IP 주소를 가진 컴퓨터는 자신의 MAC 주소를 응답으로 보낸다. (ARP 응답)

이 응답을 이용해서, 송신 컴퓨터는 수신지의 MAC 주소를 얻고 캡슐화 후에 2계층으로 보낼 수 있다. 

송신 컴퓨터는 ARP 응답으로 얻은 MAC주소들을 ARP테이블에 보관한다. 후에 ARP 테이블을 참고하여 전송하고, 없으면 또 다시 ARP 요청을 하게 된다. 

하지만 IP주소는 변경될 수 있기 때문에, IP가 변경되면 ARP에 저장된 정보도 쓸모가 없어진다. 

따라서 ARP 테이블에서는 보존기간을 지정하고, 일정시간이 지나면 삭제후에 다시 ARP 요청을 한다. 

![ARP 테이블](https://miro.medium.com/max/1354/1*3aDsuN_mSh3fpqwyGz1yEw.png)

[사진출처](https://medium.com/pocs/tcp-ip-%EC%9D%B4%EB%A1%A0-arp-%EC%BA%90%EC%8B%9C-%ED%85%8C%EC%9D%B4%EB%B8%94-1e07ab2ae28d)