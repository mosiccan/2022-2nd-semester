# JAVA 2 03

## 상속

클래스의 공통된 특성 (필드, 메소드)을 하위 클래스에 물려주는 것
### 슈퍼 클래스 (superclass = 부모클래스 = parent class = 상위 클래스 = base class = 기초 클래스)
- 공통된 특성을 모아놓은 클래스
### 서브 클래스 (subclass = 자식클래스 = child class = 하위 클래스 = derived class = 유도 클래스)
- 공통된 특성을 물려 받는 하위 클래스
- 공통된 특성은 물려 받고, 자신만의 특성(필드, 메소드)만 추가하여 구현
- 공통된 특성을 그대로 물려 받지 않고 수정하는 것 : 오버라이딩(overrriding)
- 상위 클래스에서 하위 클래스로 갈수록 구체적 
  - 예) 폰 -> 모바일폰 -> 뮤직폰
- 상속을 통해 간결한 서브 클래스 작성
  - 동일한 특성을 재정의할 필요가 없어 서브 클래스가 간결해짐 
  - 코드 재활용 가능
  - polymorphism(다형성) 구현 가능


```java
    extends ```상속받을 클래스``` 입력을 통해
    "상속받을 클래스"의 함수등을 사용 가능

    # (x,y)의 한 점을 표현하는 Point 클래스와 이를 상속받아, 컬러 점을 표현하는 ColorPoint 클래스를 만들어보자

class Point {
    int x, y;

    void set(int x, int y) {
            this.x = x; 
            this.y = y;
    }
    void showPoint() {
            System.out.println("(" + x + "," + y + ")");
    }
}


public class ColorPoint extends Point {
String color;
    void setColor(String color) {
            this.color = color;
    }
    void showColorPoint() {
            System.out.print(color);
            showPoint();
    }
    public static void main(String[] args) {
            ColorPoint cp = new ColorPoint(); 
            cp.set(3, 4);
            cp.setColor("red"); 
            cp.showColorPoint();
    }
}
```

### IS-A 테스트
- 한 방향으로만 IS-A 테스트가 성립해야 한다.

### 서브 클래스의 객체와 멤버 접근
- 슈퍼 클래스의 private 멤버는 서브 클래스의 객체에 포함은 되나 **직접 접근 불가**
- 슈퍼 클래스의 private 멤버는 ***슈퍼 클래스의 public 메소드***를 통해 접근

```java
    ex) sudo 코드
    Super 
        private a
        public getA();
    Sub a

    s.a 로 불가능
    s.getA()로 가능 // 직접 접근이 아닌 getA를 통한 간접 접근
```

## java의 접근 지정자
### 자바의 접근 지정자 4 가지
- public, protected, default, private
  - 상속 관계에서 주의할 접근 지정자는 private와 protected

- 슈퍼 클래스의 private 멤버
  - 슈퍼 클래스의 private 멤버는 모든 클래스가 접근 불가
- 슈퍼 클래스의 protected 멤버
    - 같은 패키지 내의 클래스는 접근 가능
    - 동일 패키지 여부와 상관없이 서브 클래스에서 슈퍼 클래스의 protected 멤버 접근 가능

- new에 의해 서브 클래스의 객체가 생성될 때
  - 슈퍼클래스 생성자와 서브 클래스 생성자 모두 실행됨 
  - 호출 순서
    - 서브클래스의 생성자가 먼저 “호출”되고, 서브 클래스의 생성자가 실행하기 전 슈퍼 클래스의 생 성자 “호출”
  - 실행 순서
    - **슈퍼 클래스의 생성자가 먼저 “실행”된 후 서브 클래스의 생성자 “실행”**
    - 부모가 먼저 실행!


## 서브 클래스와 슈퍼 클래스의 생성자 짝 맞추기
- 서브클래스의 객체 생성 시, 실행 가능한 슈퍼 클래스와 서브 클래스의 생성자 조합
  - 컴파일러는 기본적으로 슈퍼 클래스의 기본 생성자를 호출하며, 슈퍼 클래스에 **기본 생성자 가 없을 경우 컴파일 오류가 발생함**
  - 개발자가 서브 클래스의 생성자에 슈퍼 클래스의 생성자를 직접적으로 지정하면 기본 생성자 외에 매개 변수를 가진 생성자도 호출할 수 있음
    - super() 키워드 이용

- 자동으로 삽입된 super 사례
- 결과적으로 어떠한 형태로건(프로그래머가 직접 삽입하건, 컴파일러가 삽입하건) 상위 클래스의 생성자 는 반드시 호출이 이뤄진다!
- super() 부모 클래스의 생성자를 생성하라!