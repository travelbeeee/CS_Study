# CPU 작동 원리

CPU는 컴퓨터에서 가장 핵심적인 역할을 수행하는 부분이다.

### 구성 요소

#### 연산 장치

산술연산, 논리 연산을 수행한다.

연산에 필요한 데이터를 레지스터에서 가져오고, 연산 결과를 다시 레지스터로 보낸다.

#### 제어 장치

명령어를 순서대로 실행할 수 있도록 제어한다. 

주기억장치 에서 프로그램 명령어를 꺼내 해독,

해독 결과에 따라 실행에 필요한 제어 신호를 기억장치, 연산장치, 입출력장치로 보낸다.

장치가 보낸 신호를 받아 다음 수행 동작을 결정한다. 

#### 레지스터

고속기억장치로 명령어주소, 데이터, 연산 결과 등을 임시로 저장한다. 

범용 레지스터 : 연산에 필요한 데이터나 연산 결과를 임시로 저장한다. 

특수 목적 레지스터 

- MAR(메모리 주소 레지스터)

  > 읽기와 쓰기 연산을 수행할 주기억장치 주소를 저장한다.

- PC(프로그램 카운터)

  > 다음에 수행할 명령어의 주소(주기억장치 주소)를 저장한다.

- IR(명령어 레지스터)

  > 현재 실행중인 명령어를 저장한다.

- MBR(메모리 버퍼 레지스터)

  > 주기억장치에서 읽어온 데이터나 저장할 데이터를 임시로 저장한다. 

- AC(누산기)

  > 연산 결과를 임시로 저장한다. 

### 동작 과정

![image-20211015191259389](D:\project\CS_Study\Bada\images\CPU작동원리_1)

1. 주기억장치가 입력장치에서 입력된 데이터나 보조기억장치에 저장된 프로그램을 읽어온다.
2. CPU는 프로그램 실행을 위해 주기억장치에 저장된 프로그램 명령어와 데이터를 읽어온다.
3. CPU는 2에서 읽어온 내용을 처리한다.
4. CPU가 3의 처리 결과를 다시 주기억장치에 저장한다.
5. 주기억장치는 처리 결과를 보조기억장치에 저장하거나 출력장치로 보낸다. 

6. 제어장치는 위 과정에서 명령어가 순서대로 실행되도록 각 장치를 제어한다. 

### 명령어 사이클

1. PC에 저장된 주소를 MAR에게 전달한다.
2. MAR에 저장된 주기억장치의 해당 주소에서 명령어를 인출한다.
3. 인출해온 명령어를 MBR에 저장한다.
4. MBR에 저장된 내용을 IR에게 전달한다. 
5. 다음을 위해 PC값을 증가시킨다. 

<img src="https://media.vlpt.us/images/emily0_0/post/5bc0a7ba-a263-4f0a-91fc-d444d6fe0b12/image.png" alt="img" style="zoom:50%;" />

### Context Switching 

멀티프로세스 환경에서 CPU가 어떤 하나의 프로세스를 실행하고 있는 상태에서, 다른 프로세스가 실행되어야 할 때 

1. 실행중인(이전) 프로세스의 상태 또는 레지스터 값(Context)를 보관하고
2. 새로 실행할 프로세스의 상태 또는 레지스터 값(Context)를 적재한다. 

이렇게 OS 스케줄러가 Context를 교체하는 작업을 Context Switching이라고 한다. 

![img](https://blog.kakaocdn.net/dn/mWCF3/btqEjPU7iYj/2H2hjt1Sog76az9IrGnkB0/img.jpg)

### Context?

OS에서 Context는 CPU가 해당 프로세스를 실행하는 데 필요한 해당 프로세스의 정보들이다. 

이 Context는 프로세스의 PCB(Process Control Block)에 저장된다. 

### PCB (Process Control Block)

프로세스를 실행하는 데 필요한 중요한 정보를 관리하는 자료 구조이다.

#### 저장되는 정보 

- 포인터 : 준비상태나 대기 상태에서 큐에 연결할 포인터
- 프로세스 상태 : 생성, 준비, 수행, 대기, 중지
- PID
- PC(프로그램 카운터) 
- 프로세스 우선순위 : 준비 상태에 있는 프로세스 중 우선순위가 높은 것을 실행 상태로 옮긴다. 
- 각종 레지스터
- 메모리 관리 정보

<img src="https://blog.kakaocdn.net/dn/q9Cda/btqEmwMRN34/a2nMadVTcblerkGk5yBfK0/img.png" alt="img" style="zoom:33%;" />

[출처](https://chosh95.tistory.com/330)

#### 언제 발생할까?

아래와 같은 인터럽트 요청이 올 때 Context Switching이 발생한다. 

1. I/O request (입출력 요청할 때)

2. time slice expired (CPU 사용시간이 만료 되었을 때)

3. fork a child (자식 프로세스를 만들 때)

4. wait for an interrupt (인터럽트 처리를 기다릴 때)

### CPU bound & I/O bound

프로세스는 크게 두 종류로 나누어볼 수 있다. 

1. **CPU bound process** :CPU burst가 큰 process

   사용자가 수행 중간에 관여하지 않는 것. (중간에 I/O 없음)

   ex) 연산처리가 많은 프로세스

   - 데이터 마이닝, 이미지 프로세싱 등...

2. **I/O bound process** : I/O burst가 큰 process

   대화형 process는 전부 I/O bound process이다.

#### CPU burst & I/O burst

process는 CPU burst와 I/O burst를 왔다 갔다 하면서 프로그램을 실행한다. 

CPU burst : CPU 명령을 실행하는 시간

I/O burst : I/O 요청 후 기다리는 시간

<img src="https://taes-k.github.io/images//posts/2021-06-05-cpu-io-bound/1.png" alt="1" style="zoom: 25%;" />

우리가 사용하는 많은 프로그램들의 CPU burst 시간 그래프는 아래와 같다.

그래프를 보면 대부분 짧은 CPU burst 시간을 가지는 것을 알 수 있다.

즉, 대부분의 프로세스가 I/O bound process라는 뜻이다. 

<img src="https://blog.kakaocdn.net/dn/bzPlY4/btqCM9URwYH/VHMbeHOpEDNw7cvRrqkSB1/img.png" alt="img" style="zoom: 50%;" />

#### 성능 개선

CPU bound process : 높은 성능의 CPU를 사용하거나 GPU를 사용한다. 

I/O bound process : 빠른 메모리를 사용하면 된다. HDD -> SSD로 교체, Non-blocking I/O를 통한 throughput 향상



https://taes-k.github.io/2021/06/05/cpu-io-bound/

https://jhnyang.tistory.com/25

https://devowen.com/234

