# Congestion 관리 방법

4계층(전송계층)에서 사용하는 주된 프로토콜에는 TCP, UDP가 있다.

이 중 TCP는 신뢰성을 보장하기 때문에 congestion제어 기능을 제공하고, UDP는 제공하지않는다. 

따라서 TCP의 Congestion 관리 방법에 대해 알아보자.



### Congestion control이란?

congestion(혼잡) : 네트워크 수용량보다 많은 패킷을 보내 오버플로우가 발생해 패킷이 손실되는 현상을 말한다.

네트워크 계층에서 트래픽이 많아져 네트워크 응답 시간이 느려지는 것을 말한다. 

congestion이 발생하면, 딜레이가 증가하고 성능이 나빠진다. 딜레이가 증가하면 재전송이 발생하여 상황을 더 나쁘게 만든다. 

congestion을 제어한다는 것은, 송신측과 수신측의 데이터 처리 속도 차이를 해결해서 오버플로우가 발생하지 않도록 하는 것이다. 

다르게 말하면, 네트워크 내에 패킷 수가 과도하게 증가하지 않도록 조절하는 것이다. 

1. #### AIMD (Additive Increase / Multiplicative Decrease)

   처음에 패킷을 한 개씩 보낸다. (window크기 = 1)

   이것이 문제없이 도착하면 한 주기마다 window크기를 1씩 늘려서 전송하는 방법이다.

   ** window 크기 : 단위 시간 내에 전송하는 패킷의 수 

   패킷 전송에 실패하면, window 크기를 절반으로 줄인다. 

   특징

   - 공평한 방식이다. 

     > 여러 호스트가 하나의 네트워크를 공유할 때 처음에는 나중에 들어온 호스트가 불리하지만, 시간이 흐르면 평형상태로 수렴한다. 

   문제점

   - 초기에 높은 대역폭을 사용하지 못하고, 전송 속도를 올리기까지 시간이 많이 걸린다.

   - 네트워크가 혼잡해지는 상황을 미리 감지하지 못한다.

     > 소 읽고 외양간 고치는 방법

   ![img](https://media.vlpt.us/images/mu1616/post/16298aa0-246f-4d22-8c29-19ec49b28ce6/image.png)

2. #### Slow Start (느린 시작)

   전송 속도를 올리는데 시간이 오래걸리는 AIMD의 단점을 해결하기 위해 등장했다. 

   1. 처음에 패킷을 한 개씩 보낸다(window 크기 =1)

   2. 패킷이 문제없이 도착하면 각 ACK마다 window 크기를 1씩 늘려준다. (Congestion Avoidance 상태)

      > 이렇게 하면 한 주기마다 window 크기가 2배씩 증가한다. 

   3. 대신에 전송이 실패하면(혼잡이 발생하면) window 크기를 1로 만든다.

   특징

   - 처음에는 네트워크 수용량을 예상할 수 없지만, 한 번 congestion이 발생하고 나면 네트워크 수용량을 어느정도 예측할 수 있다. 

   임계점(ssthresh) : 여기 까지만 slow start를 사용하겠다. 

   > 윈도우 크기를 지수적으로 증가시키다보면 크기가 기하급수적으로 늘어나 제어가 힘들어지기 때문이다.
   >
   > 따라서 전송 데이터의 크기가 임계점 (Threshold)에 도달하면 선형적으로 1씩 윈도우를 증가시킨다.

   ![img](https://media.vlpt.us/images/mu1616/post/71182a17-fef8-4d94-938b-2a19a628b7f1/image.png)

3. #### Fast Restransmit (빠른 재전송)

   수신 측에서, n번 패킷을 기다리고 있는데 n+i번 패킷(n번 다음의 패킷)이 먼저 도착하게 되는 경우에도 ACK 패킷을 보낸다. 

   이 때, ACK 패킷에 n번 패킷의 번호를 실어서 보낸다. 

   송신 측에서는 순번이 중복된 ACK 패킷을 3개 받게되면 문제가 되는 패킷을 재전송한다. 

   timeout을 기다리지 않고 바로 패킷을 재전송할 수 있기 때문에 보다 빠르다. 

   ![img](https://media.vlpt.us/images/mu1616/post/878686ca-8073-420d-8e63-6afc79622f5d/image.png)

4. #### Fast Recovery (빠른 회복)

   Fast Retransmit 후 Slow Start 아닌 Congestion Avoidance 상태에서 전송하는 기법이다.
   
   임계점 밑으로 떨어지면 지수승으로 증가시킴. 

**  Congestion Avoidance 상태 : window 크기를 1씩 증가시키는 것

모두 적용하면 아래와 같다. 

![img](https://t1.daumcdn.net/cfile/tistory/256E39425715F10103)

#### ** Leaky Bucket Algorithm

콩쥐팥쥐에 나오는 "밑빠진 독"(Leaky Bucket)을 이용하는 방식이다. 

밑에 구멍이 있는 버켓에 물을 부으면, 물이 빠른 속도로 들어와도 밑의 구멍으로 빠져나오는 물의 양은 일정하다. 

![Leaky Bucket](https://media.geeksforgeeks.org/wp-content/uploads/leaky.jpg)

1.  host가 패킷을 보내면 그 패킷은 버킷으로 들어온다.
2. 버킷은 매 시간마다 일정한 양의 패킷을 내보낸다. (네트워크가 일정한 속도로 패킷을 전송한다.)
3. 한번에 많은 양의 트래픽이 들어와도, 리키 버킷이 일정한 트래픽으로 바꾸어준다.
4. 버킷은 시간당 일정한 output을 내보내는 큐처럼 동작한다. 
5. 버킷이 꽉 찼을 때 들어오는 패킷들은 유실된다. (물이 가득찬 버킷에 물을 더 부으면 흘러넘친다.)

#### ** Token Bucket Algorithm

Leaky Bucket 알고리즘은, 트래픽이 아무리 burst해도 항상 일정한 속도를 유지한다. 이렇게되면 burst한 상황에서 버킷이 꽉 차서 유실되는 패킷이 생길 수 있다. 

따라서 burst한 상황을 좀 더 유연하게 처리하여 유실되는 패킷을 줄이려고 Token Bucket 알고리즘이 등장했다. 

1. 일정한 시간 간격으로 버킷에 토큰이 하나씩 들어온다.
2. 버킷이 가질 수 있는 토큰의 max값은 정해져있다. 
3. 패킷이 들어왔을 때, 버킷이 가지고있는 토큰을 하나 버리고 패킷을 전송한다.
4. 버킷에 토큰이 한 개도 없으면 패킷을 보낼 수 없다. 

아래 사진과 같은 상황에서, 버킷의 3개의 토큰을 가지고있었다고 할 때,

5개의 패킷이 우르르 들어오면 버킷은 토큰 3개를 버리고 패킷 3개를 전송한다.

남은 패킷 2개는 버킷에 토큰이 생길 때 까지 대기한다.

이렇게 하면 트래픽이 몰리는 상황에서 버킷 내 토큰 수만큼 한꺼번에 내보낼 수 있으므로 버킷이 꽉 차는 상황을 줄일 수 있다.

![image0031](https://media.geeksforgeeks.org/wp-content/uploads/leakybuk.jpg)

https://www.geeksforgeeks.org/congestion-control-in-computer-networks/



** 서버 직군에서 중요한 주제