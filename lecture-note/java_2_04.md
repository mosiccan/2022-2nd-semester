# JAVA 2 04

## 다형성

### 캐스팅(강제 타입 변환)
- 종류: 업캐스팅, 다운캐스팅
  - **업캐스팅(upcasting)**
  - 서브 클래스의 객체를 슈퍼 클래스 타입으로 강제 변환하는 것
    - 업캐스팅 후 슈퍼 클래스의 멤버만 접근 가능
    - 명시적 타입 변환(우항에 Person괄호를 붙이는 것)을 생략할 수 있음 
- java에서 polymorphism(다형성)을 구현하는 수단

``` java
class Person { 
}
class Student extends Person { 
}
Student s = new Student();
Person p = (Person)s;
```

### 하위 객체는 그 자신으로 취급할 수도 있고 상위 객체로 취급할 수도 있다.
- 자바 클래스가 아무것도 상속하지 않으면 java.lang 패키지의 Object 클래스를 자동으로 상속한다.
- 때문에 모든 자바 클래스는 Object 클래스를 직접적 혹은 간접적으로 상속한다. 


### 모든 클래스가 Object 클래스를 직접 혹은 간접적으로 상속하므로, 다음 두 가지가 가능하다. 
- 자바의 모든 인스턴스는 Object 클래스의 레퍼런스로 참조 가능  
  ```Object obj = new MyClass();```
- 자바의 모든 인스턴스를 대상으로 Object 클래스에 정의된 메소드 호출 가능
``` java
MyClass myClass = new MyClass();
myClass.toString();
```

- 우리가 흔히 호출하는 println 메소드는 다음과 같이 정의되어 있다.  
```public void println(Object x) { . . . }```
  - 어떠한 객체를 넣어도 된다.
- 인자의 타입을 object로 쓰면 어떤 타입이든 담을 수 있다?!

```java
class Friend
{
    String myName;
    public Friend(String name) {
      myName=name; 
    }
    public String toString()  // object 클래스와 다르게 출력 위해
    {
      return "My name is "+myName; 
    }
}
class InheritanceTest
{
    public static void main(String[] args) {
      Friend fnd1=new Friend("Jack"); 
      Friend fnd2=new Friend("Jane");
      System.out.println(fnd1); 
      // Friend 객체를 넣어 주는 것도 가능, 그렇다면 어떤걸 print할까?
      System.out.println(fnd2); }
}

```

- 슈퍼클래스와 자식클래스의 같은 메소드가 있을때 자식 클래스의 메소드 먼저 쓰는 방식 : 오버라이딩

### 다운캐스팅(downcasting)
- 업캐스팅된 것을 다시 원래대로 되돌리는 것 
- 명시적으로 타입 지정
- 서브 클래스 멤버 전체 접근 가능 
- 괄호를 생략할 수 없음

``` java
class Person {
}
class Student extends Person {
}

Person  p;
Student s1 = new Student(“이재문”); 
p = (Person)s1; // 업캐스팅 발생
Student s2 = (Student)p; // 다운캐스팅, 강제타입변환

```

### instanceof 연산자
- 상속 관계를 바탕으로 타입 캐스팅이 가능한지 boolean 형으로 리턴하는 연산자
  - 객체레퍼런스명 instanceof 클래스명  
  ``` ex) p instanceof Student ```
  - p는 Student로 캐스팅 할 수 있는가?

### 메소드 오버라이딩(Method Overriding)
- 슈퍼 클래스의 메소드를 서브 클래스에서 재정의하는 것
  - 슈퍼 클래스의 메소드 이름, 메소드 인자 타입 및 개수, 리턴 타입 등 모든 것 동일하게 정의 
    - 이 중 하나라도 다르면 메소드 오버라이딩 실패