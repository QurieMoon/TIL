# 6주차 과제: 상속 \#6

## 목표

- 자바의 상속에 대해 학습하세요.

## 학습할 것(필수)

- 자바 상속의 특징
- super 키워드
- 메소드 오버라이딩
- 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)
- 추상 클래스
- final 키워드
- Object 클래스

## 학습 내용

- 자바 상속의 특징

  - 상속: 기존의 클래스를 재사용하여, 새로운 클래스를 작성하는 것

    - 용어
      - 부모 클래스(superclass, base class, parent class)
      - 자손 클래스(subclass, derived class, extended class, child class)

  - 장점

    - 코드의 재사용성을 높이고
    - 코드 간 불필요한 중복을 제거하여, 유지보수를 용이하게 함

  - 자바에서 상속을 구현하는 방법: `extends` 키워드 사용

    ```java
    class Parent(){}
    
    class Child extends Parent(){
      // ...
    }
    ```

  - 자바 상속의 특징

    - 자손 클래스는 조상 클래스의 모든 멤버(fields, methods, and nested classes)를 상속받습니다.
      단, 생성자와 초기화 블럭은 상속되지 않습니다.

      > 구체적으로, 자손 클래스는 부모 클래스의 모든 public/protected member를 상속 받고,
      >
      > 자손 클래스가 부모 클래스와 같은 패키지에 있는 경우에는 package-private(default) 멤버를 상속 받을 수 있으나,
      >
      > 부모 클래스의 private memeber는 자손 클래스가 상속받을 수 없습니다.

    - 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 많습니다.

    - 자바에서는 단일 상속만이 허용됩니다.
      따라서 아래와 같은 코드는 작성할 수 없습니다.

      ```java
      class Liger extends Lion, Tiger(){
        // ...
      }
      ```

- super 키워드

  - `super` 키워드는 자손 클래스에서 조상 클래스의 멤버를 참조하고 싶거나
    메소드 오버라이딩을 한 이후에 조상 클래스 내 선언된 메소드를 불러오고 싶을 때, 사용합니다.

- 메소드 오버라이딩

  - 메소드 오버라이딩: 조상 클래스로부터 상속받은 메서드의 내용을 변경하는 것

  - 메소드 오버라이딩 시, 유의점

    1. 메소드의 선언부(메소드명, 매개변수, 반환타입)은 기존 조상 클래스에서 선언된 내용과 완전히 일치해야함
    2. 접근 제어자와 예외만 특정 상황에서 변경 가능
       - 이때, 접근 제어자를 조상 클래스에서 선언된 메서드의 접근 제어자보다 좁은 범위로 변경할 수 없습니다.
       - 예외는 조상 클래스에서 선언된 것보다 더 많이 선언할 수 없습니다.

    > 오버라이딩(overriding) vs. 오버로딩(overloading)
    >
    > - 오버라이딩: 조상클래스를 상속받은 자손클래스에서 메서드 내용 부분만을 새로 작성
    > - 오버로딩: 메서드명만 같은 전혀 새로운 메서드를 정의하는 것

- 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)

  - 다이나믹 메소드 디스패치: 오버라이딩된 메소드가 호출되었을 때, 관련된 메소드(오버라이딩된 메소드, 오버라이딩한 메소드, ...) 중에서 어떤 메소드를 호출해야할지 결정을 **런타임**에 하는 것(**컴파일 타임에 메소드 결정하는 것 아님**)
    - 런타임 시, 오버라이딩된 메소드 중 어느 메소드를 호출할지 결정의 기준: 해당 메소드를 호출한 object의 type
  - 다른 말로, "runtime polymorphism" 이라고도 부름
  - 특징
    - 오버라이딩된 멤버 메소드에만 적용됨(static 메소드에는 적용 안 됨)

- 추상 클래스

  - 추상 클래스는 `abstract` 라는 키워드로 표시됩니다.
    추상 클래스는 추상 메서드를 포함한 클래스로, 추상 메서드는 메서드의 선언부만 작성되고, body가 빈 메서드입니다.

    ```java
    abstract class AbstractClass(){
      abstract void abstractMethod();
    }
    
    AbstractClass a = new AbstractClass();
    ```

    - 추상 클래스의 경우, 인스턴스를 생성할 수 없습니다.

    - `abstract` 키워드가 사용될 수 있는 곳: 클래스, 메소드

- final 키워드

  - `final` 키워드는 어떤 대상을 더 이상 변경할 수 없게 만드는 키워드입니다.
    구체적으로, 변수에 `final` 키워드가 붙으면 해당 변수에 대입된 값을 변경할 수 없으며, 메서드에 `final` 키워드가 사용되면 오버라이딩을 할 수 없습니다. 또한, 클래스에 `final` 키워드가 사용되면 자신의 자손클래스를 가질 수 없게 됩니다.
    - `final` 키워드가 사용될 수 있는 곳: 클래스, 메서드, 멤버변수, 지역변수

- Object 클래스

  - Object 클래스: 모든 클래스의 최상위 조상 클래스

    --> 모든 클래스는 Object 클래스의 자손 클래스

    > Object 클래스는 부모 클래스가 없습니다.

  - 모든 클래스가 Object 클래스를 상속 받아서 유용한 점

    : Object 클래스의 `toString()` 이나 `equals(Object o)` 와 같은 메서드를 새로 생성한 클래스에서 바로 사용 가능합니다.

------

- 참고 자료

  - [The Java Tutorials, Oracle - Inheritance](https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html)
  - [The Java Tutorials, Oracle - Using the Keyword super](https://docs.oracle.com/javase/tutorial/java/IandI/super.html)
  - [RIP Tutorial - Java Language, Dynamic Method Dispatch](https://riptutorial.com/java/topic/9204/dynamic-method-dispatch)
  - [Oracle Database Object-Relational Developer's Guide - Dynamic Method Dispatch](https://docs.oracle.com/cd/B28359_01/appdev.111/b28371/adobjbas.htm#i468270)
  - 책 - Java의 정석(남궁성 지음)
