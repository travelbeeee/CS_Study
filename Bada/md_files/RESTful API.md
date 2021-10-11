## RESTful API

REST(Representational State Transfer)아키텍처의 6가지 제약 조건을 준수하는 API를 의미한다. 

REST한 방식으로 프로그램간 정보 교환 등의 상호작용을 가능하게 하는 것이 RESTful API이다.

** API : 컴퓨터 프로그램간 상호작용을 도와주며, 서로 정보를 교환할 수 있도록 한다 

### 구성

REST ? : 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것

URI을 통해 자원을 명시하고, HTTP Method(POST, GET, PUT, DELETE 등)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것이다.

1. Resource (자원) - URI

   모든 자원에 고유한 HTTP URI이 존재하고, 이 자원은 Server에 존재한다. 

   Client는 URI를 이용하여 자원을 지정하고, 해당 자원의 상태에 대한 조작을 Server에 요청한다.

2. Verb (행위) - HTTP METHOD

   POST, GET, PUT, DELETE 4가지를 가장 많이 사용하며,

   이 4가지 이외에도 HEAD, OPTION등의 METHOD를 사용할 수 있다. 

3. Representations (표현)

   Client의 요청에 따라 Server는 이에 적절한 응답(Representation)을 보낸다.

   REST에서 자원은 JSON, XML, TEXT 등 여러 형태의 Representation으로 나타내어질 수 있다. 

   JSON, XML을 통해 주고받는 것이 일반적이다. 

### 6가지 제약 조건

#### Server-Client 구조

자원을 가진쪽이 Server, 요청하는 쪽이 Client이다. 

#### Stateless

HTTP 프로토콜과 마찬가지로 REST역시 stateless하다. 

** stateless하다? 

> Server에 Client의 context를 저장하지 않는다. 

#### Cache

HTTP의 가장 강력한 특징중 하나인 캐싱 기능을 사용할 수 있다. 

cache-control 헤더를 통해 캐시 여부를 명시할 수 있다. 

#### Uniform interface

URI로 지정한 자원에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다. 

HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다. 

#### Layered system 

REST Server는 여러 계층으로 구성될 수 있다. 

API Server에서는 순수 비즈니스 로직을 수행하고, 앞단에 보안, 로드밸런싱, 인증 등을 추가하여 구조상에 유연성을 줄 수 있다. 

#### Code-on-demand (optional)

Server로 부터 스크립트를 받아서 Client에서 실행한다. 

반드시 만족할 필요는 없다.

### 설계 시 중요한 점

**첫 번째,** URI는 정보의 자원을 표현해야 한다.
**두 번째,** 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.



### 요약 

Q)REST란 무엇인가?

REST는 Representational State Transfer의 약자로, 간단히 말해서 URI와 HTTP 메소드를 이용해 객체화된 서비스에 접근하는 것입니다. REST의 요소로는 크게 리소스, 메소드, 메세지 3가지 요소로 구성됩니다. 

예를 들어 "이름이 Tom인 사용자를 생성한다." 라는 호출이 있을 때 "사용자"는 리소스, "생성한다."라는 행위는 메소드, 그리고 "이름이 Tom인 사용자"는 메세지가 됩니다. 

즉 리소스는 http://myweb/users라는 형태의 URI로 표현되며, 메소드는 HTTP Post, 메세지는 JSON 문서를 이용해서 표현됩니다. 

HTTP에는 여러가지 메소드가 있지만 REST에서는 CRUD에 해당하는 4가지의 메소드 GET, POST, PUT, DELETE를 사용합니다. REST는 리소스 지향 아키텍쳐 스타일이라는 정의에 맞게 모든 것을 명사로 표현하며 각 세부 리소스에는 id를 붙입니다. 

Q) RESTful하게 API를 디자인 한다는 것은 무엇인가?

Restful하게 API를 디자인한다는 것은 URI를 규칙에 맞게 잘 설계했는지의 여부입니다. 규칙의 항목으로는 아래와 같습니다.

1. 동일한 URI(End point)의 행위에 맞게 POST, GET, DELETE, PATCH등의 메소드를 사용한다.

2. 명사를 사용한다. 리스트를 표현할 때는 복수형을 사용한다.
3. URI Path에 불필요한 파라미터를 넣지 않는다. 즉, 단계를 심플하게 설계한다.

[출처](https://wooaoe.tistory.com/51)

