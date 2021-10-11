## Override vs Overload

JAVA에서 다형성을 지원하는 방법으로, Method Overried와 Overload가 있다. 

### Overloading

같은 이름의 메서드 여러개를, parameter의 type과 개수가 다르도록 만들어서 다양한 유형의 호출에 응답할 수 있게 한다. 

메서드 오버로딩과 생성자 오버로딩은 같은 개념이다. 

```java
class Test{
	void func(){
        System.out.println("매개변수 없음");
    }
    void func(String name){
        System.out.println("매개변수 :"+name);
    }
    void func(int x){
        System.out.println("매개변수 :"+x);
    }
}
```



### Overriding

상위 클래스의 메서드를 하위 클래스가 재정의해서 사용하는 기술이다. 

하위 클래스에서 상위 클래스의 메서드의 이름, parameter, return type을 동일하게 재정의 할 경우, 상속받은 메서드를 덮어쓴다. 

> 부모 클래스의 메서드를 무시하고, 자식 클래스의 메서드를 이용하겠다. 

super.func()를 이용하면 부모 클래스의 내용을 실행 후 이어서 실행할 수 있다. 

```java
class Shapes{
    public void info() {
        System.println("나는 도형입니다.");
    }
}

class Triangle extends Shapes {
    public void info() {
        super.info(); // 부모 클래스의 함수를 실행 후 이어서 실행할 수 있다. 
        System.println("나는 삼각형입니다.");
    }
}
```

