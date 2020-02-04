## 인터페이스란?

- 인터페이스는 인터페이스를 구현하는 모든 클래스에 대해 특정한 메소드가 반드시 존재하도록 강제한다.
- 인터페이스의 목적은 구현 객체가 같은 동작을 한다는 것을 보장하는 것이다.
- 일종의 추상 클래스다. 하지만 추상 클래스보다 추상화 정도가 높아서 추상 메소드 이외의 일반 메소드나 멤버 변수를 구성원으로 가질 수 없다. 오직 추상 메소드와 상수만 멤버로 가질 수 있으며, 그 외의 요소는 허용하지 않는다.



추상 클래스를 부분적으로만 완성된 미완성 설계도라고 한다면 인터페이스는 구현된 것이 아무것도 없는 기본 설계도라 할 수 있다. 



- 제약 사항
  - 모든 멤버 변수는 public static final 이어야 하며, 생략 가능.
  - 모든 메소드는 public abstract 이어야 하며, 생략 가능.
  - JDK 1.8부터 인터페이스에 static 메소드와 디폴트 메소드의 추가를 허용했다.



```java
interface PlayCard {
  public static final int NUMBER = 4;
  
  final int DIAMOND = 3;
  static int HEART = 2;
  int CLOVER = 1;
  // 위의 상수는 모두 public static final이며, 생략된 형태이다.
  
  public abstract int getCardNumber();
  
  String getCardKind();
  
  // public 생략.
  default void getNewCard() {
    
  }
  
  // public 생략.
  static void staticMethod() {
    
  }
}
```



### [인터페이스의 상속]

- 인터페이스는 인터페이스로부터만 상속(extends) 받을 수 있다. 클래스와는 달리 다중 상속, 즉 여러 개의 인터페이스로부터 상속 받는 것이 가능하다.
- 클래스에서 여러 인터페이스를 다중 구현하는 것 또한 가능하다.



### [인터페이스의 구현]

- 추상 클래스와 마찬가지로 자신이 직접 인스턴스를 생성할 수 없다. 따라서 인터페이스가 포함하고 있는 추상 메소드를 구현해 줄 클래스를 작성해야 한다.
- 상속은 클래스를 확장한다는 의미의 키워드인 extends를 사용하며, 인터페이스는 구현한다는 의미의 키워드인 implements를 사용한다.



```java
interface Movable {
  void move(int x, int y);
}

interface Attackable {
  void attack(Unit n);
}

interface Fightable implements Movable, Attackable {
  
}

abstract class Fighter implements Fightable {
  public void move(int x, int y){
    ...
  }
}
```



만약 모든 추상 메소드의 구현을 원하지 않는다면 위의 코드처럼 Fighter 클래스를 abstract 키워드를 붙여 추상 클래스로 선언해야 한다.

위에서는 move() 함수만을 구현했다. attack()을 구현하지 않았기 때문에 abstract Fighter인 추상 클래스로 선언을 했다.

자바에서는 상속과 구현을 동시에 할 수 있다.

```java
class Fighter extends Unit implements Fightable {
  public void move(int x, int y) { ... }
  public void attack(Unit u) { ... }
}
```



### [클래스를 이용한 다중 상속의 문제점]

- 다중 상속이 된다고 가정했을 때, 아래의 코드를 확인해보자.

```java
class Animal {
  public void cry(){
    System.out.println("짖기!");
  }
}

class Cat extends Animal {
  @Override
  public void cry(){
    System.out.println("냐옹냐옹!");
  }
}

class Dog extends Animal{
  @Override
  public void cry(){
    System.out.println("멍멍!");
  }
}

class MyPet extends Cat, Dog { ... }
// 1.

public class Test {
  public static void main(String[] args){
    MyPet pet = new MyPet();
    pet.cry();
    // 2.
  }
}
```



다중 상속을 허용할 경우, 발생할 수 있는 문제는 **메소드 출처의 모호성**이다. 

주석을 달아놓은 2에서 MyPet 클래스의 인스턴스인 pet이 cry() 메소드를 호출하면 이 메소드가 Dog 클래스의 cry() 메소드인지, Cat 클래스의 cry() 메소드인지 구분할 수 없는 모호성이 생긴다.

이와 같은 이유로 자바에서 다중 상속을 지원하지 않는다.



하지만, 인터페이스를 이용해 다중 구현을 하게되면 위와 같은 메소드 호출의 모호성을 방지할 수 있다.

```java
interface Animal {
  void cry();
}

interface Cat extends Animal {
  void cry();
}

interface Dog extends Animal {
  void cry();
}

class Pet implements Cat, Dog {
  @Override
  public void cry(){
    System.out.println("멍멍~ 냐옹냐옹~")
  }
}

public class Test{
  public static void main(String[] args){
    Pet pet = new Pet();
    pet.cry();
  }
}

// 결과
멍멍~ 냐옹냐옹~
```



Cat, Dog 인터페이스를 동시에 구현한 Pet 클래스에서만 cry() 메소드를 정의하므로, 앞의 예제에서 발생한 메소드 호출의 모호성이 없다. 



### [인터페이스를 통한 다형성]

자손 클래스의 인스턴스를 조상 타입의 참조 변수로 참조하는 것이 가능하다.

인터페이스도 인터페이스를 구현한 클래스의 조상이라고 할 수 있으므로, 해당 인터페이스 타입의 참조 변수로 이를 구현한 클래스의 인스턴스를 참조할 수 있다.



### [장점]

1. 대규모 프로젝트 개발 시 일관되고 정형화된 개발을 위한 표준화가 가능하다.
2. 클래스의 작성과 인터페이스의 구현을 동시에 진행할 수 있으므로, 개발 시간을 단축할 수 있다.
3. 클래스와 클래스 간의 관계를 인터페이스로 연결하면 클래스마다 독립적인 프로그래밍이 가능하다.