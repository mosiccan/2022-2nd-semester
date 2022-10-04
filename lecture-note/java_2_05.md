# JAVA 2 05
interface, enum, inner class

## 인스턴스의 생성을 허용 안 하는 abstract 클래스
- abstract 메소드는 하위 클래스에서 해당 메소드를 반드시 오버라이딩해야 한다.
- 만약 **인스턴스를 생성**하려고 하거나 **오버라이딩 하지 않으면** 컴파일 오류가 발생한다. 이는 코드의 안전성을 높인다.
- 하나 이상 abstarct 메소드를 포함하는 클래스는 abstract로 선언되어야 한다.

- 서브 클래스가 추상 클래스가 되지 않기 위해서는 위와 같이 추상 메소드를 “모두” 오버라이딩하여 구현해야 한다.


### abstract class, method overriding을 활용한 speak() 구현
``` java
  abstract class Animal 
  {
      public abstract String printSpeak(); 
  }
  class Dog extends Animal 
  {
  public String printSpeak() 
  {
      return "woof"; }
  }
  class Cat extends Animal 
  {
  public String printSpeak() 
  {
      return "meow"; }
  }
  public class Test {
      public static void main(String[] args){ 
              Animal dog=new Dog();
              Animal cat=new Cat(); 
              speak(dog);
              speak(cat); 
      }
      public static void speak(Animal a) 
      {
          System.out.println(a.printSpeak()); 
      }
  }

```

### 인터페이스
- 인터페이스(interface)
  - 모든 메소드가 추상 메소드인 클래스
  - 인터페이스는 상수와 메소드만 갖는다. 멤버 변수는 없음
- 인터페이스 선언
  - interface 키워드로 선언
  - ex) ```public interface Pet{…}```
- 인터페이스 구현
  - 인터페이스의 추상 메소드를 클래스에서 구현하는 것 implements 키워드 사용   
  - ex) ```public class Dog implements Pet{…}```
- 인터페이스의 특징
  - 모든 메소드는 public abstract 메소드이며 키워드 생략 가능 
  - 모든 변수는 public static final이며 키워드 생략 가능
  - 객체 생성 불가, new Clock();은 오류
  - 레퍼런스 변수 타입으로 사용 가능, Clock clock;은 가능

### 인터페이스 특성
- 인터페이스는 둘 이상을 동시에 구현 가능  
``` class OurClass implements MyInterface, YourInterface```
- 인터페이스 간 상속 가능
- 단 이 때는 implements가 아닌 extends를 사용한다.

## enum

- ```values()```
  - Enum에 정의된 순서대로 배열을 만들어 리턴함
- ```valueOf(String arg)```
  - String으로 넘긴 값을 기준으로 enum의 원소를 가져옴
- ```name()```
  - enum 원소의 값을 String으로 리턴함

### enum에 멤버 변수 넣기
- Enum에 별도의 멤버 변수를 만들 수 있고 이를 생성자를 통해 설정할 수 있다.

## inner 클래스
- 클래스의 정의가 다른 클래스의 내부에 삽입될 수 있다. 
- 이 때 외부의 클래스를 가리켜 Outer 클래스라 하고, 내부의 클래스를 가리켜 Inner 클래스라 한다. 
- Outer 클래스의 인스턴스 생성 후에야 Inner 클래스의 인스턴스 생성이 가능하다.
- Inner 클래스 내에서는 Outer 클래스의 모든(private 포함) 멤버에 접근 가능하다.

## Anonymous 클래스
- 클래스 이름이 없는 Inner 클래스
- 선언과 동시에 객체를 만들고자 할 때 사용
- abstract 클래스나 interface를 override한 후 객체를 한번만 생성할 경우에 사용됨

```java
    abstract class AnonymousInner{ 
      public abstract void mymethod();
      }
    public class Test {
        public static void main(String args[]){
            AnonymousInner inner = new AnonymousInner(){
                public void mymethod(){
                    System.out.println("anonymous class"); 
                }
        };
        inner.mymethod(); 
      }
    }

```

- 동일 객체가 여러 번 참조될 때에는 사용하지 않는 것이 좋다.
- Anonymous 클래스로 바꿀 경우 greet 함수를 매번 구현해야 함