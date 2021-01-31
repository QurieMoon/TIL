# 11주차 과제: Enum \#11

## 목표

- 자바의 열거형에 대해 학습하세요.

## 학습할 것

- [enum 정의하는 방법](#enum-정의하는-방법)
- [enum 활용하는 방법](#enum-활용하는-방법)
- [enum이 제공하는 메소드 - values\()와 valueOf\()](#enum이-제공하는-메소드-values()와 valueOf())
- [java.lang.Enum](#java.lang.Enum)
- [EnumSet](#EnumSet)

## 학습 내용

- enum 정의하는 방법

  - enum(열거형)을 정의하는 방법은 아래와 같다.

    ```java
    enum 열거형이름 { 상수명1, 상수명2, ... }
    ```

    예시) `enum Animal { ELEPHANT, LION, TIGER, GIRAFFE }`
    
  - enum의 경우, 기본적으로 해당 enum 상수의 위치에 따라서 값을 갖는다. (java.lang.Enum의 `ordinal()` 참고)

    그렇지만, 각 enum 상수에 매핑되는 값을 다르게 주고 싶을 경우에는 아래와 같이 할 수 있다.

    ``````java
    enum Animal { ELEPHANT(2), LION(4), TIGER(3), GIRAFFE(5) }
    ``````

    또한, 지정된 값을 저장하고 싶은 경우, 아래와 같이 인스턴스 변수와 생성자를 추가하면 된다.

    ``````java
    enum Animal {
        ELEPHANT("코끼리"), LION("사자"), TIGER("호랑이"), GIRAFFE("기린");
    
        private String koreanName;
    
        Animal(String koreanName) {
            this.koreanName = koreanName;
        }
    
        public String getKoreanName() {
            return koreanName;
        }
    }
    
    public static void main(String[] args) {
        for(Animal animal : Animal.values()){
            System.out.println(String.format("%s의 한글명: %s", animal.name(), animal.getKoreanName()));
        }
    }
    
    ``````

    실행 결과)

    ```
    ELEPHANT의 한글명: 코끼리
    LION의 한글명: 사자
    TIGER의 한글명: 호랑이
    GIRAFFE의 한글명: 기린
    ```

  - **주의!** enum의 생성자는 묵시적으로 private 하기 때문에 enum 외부에서 생성자를 명시적으로 사용할 수 없다.

    ```java
    public static void main(String[] args) {
        Animal animal = new Animal("코끼리"); // 위 koreanName을 인스턴스 변수로 갖는 enum Animal
    }
    ```

    실행 결과) **에러 발생**

    ```
    java: enum types may not be instantiated
    ```

    

- enum 활용하는 방법

  - enum을 사용하는 방법은 아래와 같다.

    ```java
    void sampleMethod(){
      Animal animal = Animal.ELEPHANT;
    }
    ```

  - enum 값을 비교 시, 아래 연산자를 이용할 수 있다.

    - `==`

      - enum 비교 시, `equals()` 도 사용할 수 있다고는 한다.

        그렇지만 null을 고려했을 때는 `==` 사용이 낫다고도 한다. --> [참고 링크](https://github.com/LenKIM/everyone-is-effective-java-study/issues/2)

    - `compareTo()`

    > enum에 `>, <` 연산자는 사용할 수 없다.

- enum이 제공하는 메소드 (values()와 valueOf())

  - 아래 java.lang.Enum이 제공하는 메소드 내용 참고

- java.lang.Enum

  - `java.lang.Enum` : 모든 enum(열거형)의 조상

  - `java.lang.Enum`에서 제공하는 메소드

    - Class<E> getDeclaringClass()

      - return value: 해당 enum 타입에 대한 Class object

      - 예시 코드)

        ```java
        public static void main(String[] args) {
          System.out.println(Animal.ELEPHANT.getDeclaringClass());
          System.out.println(Animal.LION.getDeclaringClass());
        }
        ```

        실행 결과)

        ```
        class com.sample.Animal
        class com.sample.Animal
        ```

    - String name()

      - return value: 해당 enum 상수의 이름(문자열)

      - 예시 코드)

        ```java
        public static void main(String[] args) {
          System.out.println(Animal.ELEPHANT.name());
        }
        ```

        실행 결과)

        ```
        ELEPHANT
        ```

    - int ordinal()

      - return value: 해당 enum 상수가 위치한 순서 (0부터 시작)

      - 예시 코드)

        ```java
        public static void main(String[] args) {
          /* enum Animal {
             ELEPHANT, LION, TIGER, GIRAFFE;
             }
           */
          System.out.println(Animal.ELEPHANT.ordinal()); // 0부터 시작
          System.out.println(Animal.GIRAFFE.ordinal());
        }
        ```

        실행 결과)

        ```
        0
        3
        ```

    - T valueOf(Class<T> enumType, String name)

      - return value: enumType의 enum에서 name과 이름이 일치하는 enum 상수

      - 예시 코드)

        ```java
        public static void main(String[] args) {
          System.out.println(Animal.valueOf("LION"));
          System.out.println(Animal.valueOf("LION") instanceof Animal); // Animal.valueOf("LION")으로 return 되는 값은 (enum) Animal Object
        }
        ```

        실행 결과)

        ```
        LION
        true
        ```

    - T[] values()

      - return value: enumType 내 모든 enum 상수값들이 담긴 array

      - 예시 코드)

        ```java
        public static void main(String[] args) {
          /* enum Animal {
             ELEPHANT, LION, TIGER, GIRAFFE;
             }
           */
            for(Animal animal : Animal.values()){
                System.out.println(animal.name());
            }
        }
        ```

        실행 결과)

        ```
        ELEPHANT
        LION
        TIGER
        GIRAFFE
        ```

- EnumSet

  - enum type만을 위한 특별한 종류의 set

  - EnumSet의 모든 element는 **단일** enum type의 상수로만 구성되어야함

  - `iterator` 메소드 사용 시, enum 상수가 선언된 순서에 따라서 진행됨

  - Null element는 허용되지 않음

    - Null element를 넣으려고 할 경우, `NullPointerException` 발생

  - EnumSet 활용 예시

    ``````java
    public static void main(String[] args) {
        EnumSet<Animal> animalEnumSet;
    
        animalEnumSet = EnumSet.of(Animal.ELEPHANT, Animal.GIRAFFE);
    
        if(animalEnumSet.contains(Animal.LION)){
            System.out.println("wrong");
        }else{
            System.out.println("correct");
        }
    
    }
    ``````

    실행 결과)

    ``````java
    correct
    ``````

    




------

- 참고 자료

  - [Enum (Java Platform SE 7) - Oracle Help Center](https://docs.oracle.com/javase/7/docs/api/java/lang/Enum.html)
  - [EnumSet (Java Platform SE 8) - Oracle Help Center](https://docs.oracle.com/javase/8/docs/api/java/util/EnumSet.html)
  - [Java Enum 활용기](https://woowabros.github.io/tools/2017/07/10/java-enum-uses.html)
  - [What does EnumSet really mean?](https://stackoverflow.com/questions/11825009/what-does-enumset-really-mean)
  - 책 - Java의 정석(남궁성 지음)

