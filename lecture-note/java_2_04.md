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


## super 키워드
- 서브클래스는 기본적으로 오버라이딩된 메소드를 호출하지만 오버라이딩되지 않은 슈퍼 클래스의 메소드를 호출하고자 한다면 super 키워드를 사용함
- super는 서브클래스에서 슈퍼 클래스의 멤버를 접근할 때 사용되는 슈퍼클래스 타입의 레퍼런스.
- 상속관계에 있는 서브 클래스에서만 사용됨
- 오버라이딩된 슈퍼 클래스의 메소드 호출 시 사용

자식 클래스에서 슈퍼 클래스의 무언가를 호출하고 싶을때!  

## Override
- 오버라이딩하는 메소드 앞에 @Override를 붙여 주자
- 컴파일러가 오버라이딩이 가능한 메소드인지 확인해 준다.
- readability가 좋다.

## 상속의 목적
- 부모 클래스는 인스턴스화 되지 않는다.
- 다만 자녀 클래스의 상위 클래스로만 의미를 지닌다.
- 부모 클래스의 showBasicInfo 메소드를 하위 클래스에서 각각 오버라이딩 하고 있다.
- 부모 클래스의 showBasicInfo 메소드는 비어있다!   

- 그렇다면! 굳이 Friend 클래스를 정의하면서까지 HighFriend 클래스와 UnivFriend 클래스를 상속의 관계에 두는 이유는 무엇인가! 
- 그 이유를 FriendInfoHandler 클래스에서 찾아 보자
- FriendInfoHandler 클래스는 Friend의 하위 클래스의 인스턴스를 하위 클래스 종류에 상관 없이 Friend 배열로 저장 및 관리한다.
- FriendInfoHander 클래스 입장에서는 HighFriend 클래스의 인스턴스도, UnivFriend 클래스의 인스턴 스도 모두 Friend 클래스의 인스턴스로 간주한다.
- showBasicInfo 메소드를 오버라이딩 했기 때문에 Friend 클래스의 참조변수를 통해서도 하위 클래스의 showBasicInfo 메소드를 호출할 수 있다! 이것이 바로 showBasicInfo 메소드를 오버라이딩의 관계에 둔 이유이다!

## final 클래스와 메소드
### final 클래스
- 더 이상 클래스 상속 불가능
### final 메소드
- 더 이상 오버라이딩 불가능
- sub 클래스가 super 클래스의 특정 메소드를 오버라이딩하지 못하게 하고 무조건 상속받아 사용 하도록 해야 할 경우
```java
public class SuperClass {
    protected final int finalMethod() { ... } }

class DerivedClass extends SuperClass { 
    protected int finalMethod() { ... } // ERROR
}
```

### final 필드
- 상수를 정의할 때 사용 (c++의 const 같은 개념)
- 상수 필드는 선언 시에 초기 값을 지정하거나 생성자에서 지정해야 한다
- 상수 필드는 한 번 정의되면 값을 변경할 수 없다


## 연습 문제
- 앞의 Animal 예제를 메소드 오버라이딩 을 활용하여 instanceof 연산자를 사용 하지 않는 형태로 변환하라. 단, main 함 수는 수정하지 않으며, 실행 결과는 동일 해야 한다.
- 앞의 상속의 예제에서 Friend 클래스를 제거하여 상속 관계를 없애고 동일한 결과를 내도록 만들어 보자.