# 14주차 과제: 제네릭 \#14

## 목표

- 자바의 제네릭에 대해서 학습하세요.

## 학습할 것

- [제네릭 사용법](#제네릭-사용법)
- [제네릭 주요 개념 (바운티드 타입, 와일드 카드)](#제네릭-주요-개념)
- [제네릭 메소드 만들기](#제네릭-메소드-만들기)
- [Erasure](#Erasure)

## 학습 내용

- 제네릭 사용법
  - type parameter를 사용한다.
  - 클래스, 메소드 둘 다 제네릭을 사용할 수 있다.

- 제네릭의 장점

  - 타입 안정성 제공
    - 컴파일 시점에서 잘못된 타입을 잡아낼 수 있다.
  - 코드가 간결해진다.
    - 코드에 명시적으로 타입 체크와 형변환 코드를 추가하지 않아도 된다.

- 제네릭 주요 개념

  - 바운디드 타입

    - "bounded" ==> "restricted"

      따라서 특정 제네릭 메소드에서 "바운디드 타입"이 사용되었다는 말은 해당 메소드에서 사용할 수 있는 타입이 제한되어 있다는 뜻이다.

    - upper bound, lower bound

    - multiple bounds

      - type의 여러 개의 bound를 두고 싶을 경우, 아래와 같이 쓸 수 있다.

        ```java
        class FruitBox<T extends Fruit & Eatable> extends Box<T>{}
        ```

        - 이때, classs는 첫번째 항목에만 위치할 수 있다. (위 예제 코드에서 `Fruit` 클래스 위치)

          나머지 항목은 모두 인터페이스여야한다.
          --> 자바에서는 다중 상속이 불가능하기 때문에 여러 개의 super class를 지정할 수 없다.

  - 와일드 카드

    - 와일드 카드는 아래 상황과 같이, 제네릭 타입에 **다형성**을 부여하고 싶을 때, 사용된다.

      1) 특정 type과 해당 type의 subtype으로 이루어진 **collection** 에 대한 메소드를 작성하고 싶을 때

      예시)

      ```java
      public static void goToSchool(List<? extends Student> students){
        ...
      }
      ```

      - 위 예시 메소드의 경우, `Student` 클래스를 상속받은 sub class로 이루어진 List를 parameter로 받을 수 있다.
        예시) `Student` 클래스를 상속받은 `HighSchoolStudent` 클래스가 있다면, `List<HighSchoolStudent>` 로 위 `goToSchool` 메소드 호출 가능함

      2) 특정 type을 lower bound 처럼 지정하여, 제네릭 메소드를 작성하고 싶을 때

      예시)

      ```java
      public static void MethodforSchool(List<? super School> school){
        ...
      }
      ```

      - 위 예시 메소드의 경우, `School` 클래스 혹은 `School` 클래스의 superclass만 parameter 값으로 받을 수 있다.

    - <참고> 자바에서 wildcard는 "?"로 표시되고, unknown type을 가리킬 때 사용된다.

      > <참고> `Object`는 모든 java class의 supertype이지만, `Object` 가 사용된 collection은 해당 없다.
      > 예시) List\<Object\> 는 List\<String\>의 supertype이 아니다.

- 제네릭 메소드 만들기

  - 제네릭 메소드란

    - 메소드의 선언부에 제네릭 타입이 선언된 메소드

    > Generic methods are those methods that are written with a single method declaration and can be called with arguments of different types
    > (출처: https://www.baeldung.com/java-generics)

  - 제네릭 메소드 특징

    - 메소드 선언부에서 리턴 타입 앞에 **type parameter** 를 가진다.

      메소드 리턴 타입이 void 여도 type paramter 명시되어야한다.

      - 주의! type parameter는 `int` 와 같은 primitive type일 수 없다.

        컴파일 시점에 type parameter가 Object 타입으로 대치된다는 점에서, type parameter는 Object로 항상 변환이 가능해야한다. 하지만, primitive type의 경우, Object class 를 상속받지 않기 때문에 Object class로 변환될 수 없다.
        --> 따라서, type parameter에서는 primitive type을 사용할 수 없다. **단, boxed primitives는 사용 가능하다. (예시: `Integer`)**

      - 주의! static 멤버변수는 type parameter를 사용할 수 없다.

        --> 주의! 지네릭 메소드 선언부 내 type parameter가 위치한 것과 혼동하지 말기!!

      - 주의! type parameter 타입의 배열을 선언할 수는 있지만, type parameter 타입으로 배열을 생성(new 연산자 사용)할 수 없다.

    - type parameter 중에서는 바운디드 타입(bounded type)이 들어올 수 있다.

    - 제네릭 메소드는 여러 개의 타입 파라미터를 가질 수 있다.

    - 제네릭 메소드의 body는 일반 메소드 body와 동일하다.

  - 제네릭 메소드 예시

    - 

- Erasure

  - 제네릭 사용에 따른 runtime 시, overhead를 줄이기 위하여,
    컴파일러는 컴파일 시점에 **type erasure** 라는 절차를 도입했다.
  - type erasure: 컴파일 시점에 type parameter를 해당 type parameter의 bounds 혹은 Object로 변환함으로써, 자바 바이트코드에는 일반 클래스만 남게 하는 것이다.




------

- 참고 자료

  - 책 - Java의 정석(남궁성 지음)
  - [The Basics of Java Generics](https://www.baeldung.com/java-generics)
  - [Difference between superclass and supertype and the difference between subclass and subtype](https://stackoverflow.com/questions/15315876/difference-between-superclass-and-supertype-and-the-difference-between-subclass)
  - [Java Generics: Multiple Bounds](https://stackoverflow.com/questions/30343161/java-generics-multiple-bounds)

