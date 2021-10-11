### MVC

MVC 패턴은 사용자 인터페이스, 데이터 및 논리 제어를 구현하는데 널리 사용되는 디자인패턴의 일종이다.

비즈니스 로직 - 뷰(화면)을 구분하는 것이 주 목적이다. 이를 통해, 업무를 분리할 수 있으며 유지보수를 용이하게 한다. 

MVC에 기반을 둔 디자인 패턴에는 MVVM, MVP, MVW가 있다. 

#### 구성

##### Model 

 - 데이터와 비즈니스 로직을 관리한다.

   - 어플리케이션이 포함해야 할 데이터들을 관리하며, 데이터의 상태가 변경되면 뷰, 컨트롤러에게 알린다.

##### View

- 레이아웃과 화면을 처리한다.
- 어플리케이션에서 데이터를 보여주는 방식을 정의한다.
- 모델로부터 표시할 데이터를 받는다.

##### Controller

- 명령을 Model과 View로 라우팅한다.
- 어플리케이션의 사용자의 입력에 대한 응답으로 모델 혹은 뷰를 업데이트한다.
- 예를들어, 이름순으로 정렬되어 있던 데이터를 날짜순으로 정렬해서 보여주고자 할 때, 컨트롤러는 모델을 업데이트할 필요 없이 바로 처리해서 뷰에게 보내줄 수 있다.

![img](https://mblogthumb-phinf.pstatic.net/MjAxNzAzMjVfMjIg/MDAxNDkwNDM4ODMzNjI2.nzDNB5K0LuyP4joE2C4rIbL5Ue2F3at7wiI6ZpuTJN0g.WZ6V-WHZygLYW2WSdzcs7uAiAWgAJe3_H0XdkYKkutkg.PNG.jhc9639/1262.png?type=w800)

[출처](https://m.blog.naver.com/jhc9639/220967034588)

** 자기가 쓰는 프레임워크의 디자인패턴 알아두기 