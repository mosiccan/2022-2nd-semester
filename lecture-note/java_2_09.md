# JAVA 2 09
Swing 컴포넌트

## Java의 GUI
- GUI 컴포넌트 이용
    - AWT - java.awt 패키지
    - Swing - javax.swing 패키지
    - JavaFX – javafx 패키지
–        GUI를 만드는 3가지 방법.
1. 이미 그려진 컴포넌트(버튼, 콤보박스,...)를 이용하여 만든다
2. 2D 그래픽을 컴포넌트에 직접 그려서(원, 사각형, …) 만든다.
3. 컴포넌트에 사진을 넣는다.

## 컨테이너
- 다른 컴포넌트를 포함할 수 있는 GUI 컴포넌트
- 다른 컨테이너에 포함될 수 있음
- JPanel, JFrame, JApplet, JDialog, JWindow
### 최상위 컨테이너
- 다른 컨테이너에 속하지 않고 독립적으로 존재 가능한 컨테이너
- 스스로 화면에 자신을 출력하는 컨테이너
  - 프레임으로 구성
  - JFrame, JDialog, JApplet
- 이를 제외한 모든 컴포넌트는 컨테이너에 포함되어야 비로소 화면에 출력 가능


## 컴포넌트
- 컨테이너에 포함되어야 비로소 화면에 출력될 수 있는 GUI 객체
- 다른 컴포넌트를 포함할 수 없음
- 스윙 컴포넌트는 모두 javax.swing.JComponent를 상속 받음

### Swing GUI 프로그램 만들기
1. JFrame으로 프레임을 만든다.
2. 컴포넌트(버튼, 텍스트 필드 등)를 만든다.
3. 컴포넌트를 프레임에 붙인다.
4. 프레임에 사이즈를 설정하고 보여준다. setSize(100,100), setVisible(true)

- 스윙 프로그램을 작성하기 위한 import문
    - import java.awt.*; // 그래픽 처리를 위한 클래스들의 경로명 
    - import java.awt.event.*; // AWT 이벤트 사용을 위한 경로명 
    - import javax.swing.*; // 스윙 컴포넌트 클래스들의 경로명 
    - import javax.swing.event.*; // 스윙 이벤트를 위한 경로명

## Layout Manager
- 컨테이너에 하나 이상의 컴포넌트가 붙여질 때 컴포넌트의 크기와 위치를 정해주기 위해 레이아웃 매니저 사용
- 컨테이너마다 하나의 배치관리자(Layout manager)가 존재
- 컨테이너에 컴포넌트가 들어오는 시점에 컴포넌트의 위치와 크기를 결정
- 컨테이너의 크기가 변하면 내부 컴포넌트들의 위치와 크기를 모두 재조절하고 재배치

### FlowLayout
- 배치방법
  - 컨테이너 공간 내에 왼쪽에서 오른쪽으로 배치하고 줄이 다 차면 다음 줄에 배치한다.
  - 레이아웃 정책: 각 컴포넌트의 선호 크기를 모두 따른다
```java
    FlowLayout()
    FlowLayout(int align)
    FlowLayout(int align, int hGap, int vGap)
// align : 컴포넌트의 정렬(5 가지중 많이 사용되는 3 가지)
    FlowLayout.LEFT(왼쪽정렬);
    FlowLayout.RIGHT(오른쪽 정렬);
    FlowLayout.CENTER(중앙 정렬, 디폴트);
// hGap : 좌우 두 컴포넌트 사이의 수평 간격, 픽셀 단위(디폴트 : 5) 
// vGap : 상하 두 컴포넌트 사이의 수직 간격, 픽셀 단위(디폴트 : 5)
```

### BorderLayout
-  컨테이너 영역을 다섯 개로 나누어 한 영역당 한 개의 컴포넌트만 넣는다. 
   - 영역: EAST, WEST, SOUTH, NORTH, CENTER
-  컴포넌트 추가 방법
   - add(Component comp, BorderLayout.WEST) : comp를 WEST 영역에 배치
-  레이아웃 정책
   - EAST, WEST에서는 가로 선호크기는 따르고, 세로는 프레임 사이즈에 강제로 맞춘다
   - NORTH, SOUTH에서는 가로는 프레임 사이즈에 강제로 맞추고 세로 선호크기는 따른다
   - CENTER에서는 ESAT, WEST, SOUTH, NORTH에서 맞춰진 크기의 나머지에 강제로 맞춤

```java
    BorderLayout();
    BorderLayout(int hGap, int vGap);
// hGap : 좌우 두 컴포넌트 사이의 수평 간격, 픽셀 단위(디폴트 : 0)
// vGap : 상하 두 컴포넌트 사이의 수직 간격, 픽셀 단위(디폴트 : 0)
```
### GridLayout
- 배치방법
- 컨테이너 공간을 동일한 크기의 사각형 격자로 분할하고 각 셀당 하나의 컴포넌트 배치
  - 격자 구성은 생성자에서 행수와 열수로 지정
  - 셀에 왼쪽에서 오른쪽으로, 다시 위에서 아래로 순서대로 배치
- 레이아웃 정책
  - 컴포넌트의 선호 크기를 모두 무시하고 셀의 크기에 강제로 맞춘다


```java
    GridLayout(int rows, int cols)
    GridLayout(int rows, int cols, int hGap, int vGap) 
//   rows : 격자의 행수 (디폴트 : 1)
//   cols : 격자의 열수 (디폴트 : 1)
//   hGap : 좌우 두 컴포넌트 사이의 수평 간격, 픽셀 단위(디폴트 : 0) 
//   vGap : 상하 두 컴포넌트 사이의 수직 간격, 픽셀 단위(디폴트 : 0) 
//   rows x cols 만큼의 셀을 가진 격자로 컨테이너 공간을 분할, 배치

    container.setLayout(new GridLayout(4,3,5,5)); // 4×3 분할로 컴포넌트 배치 (4-세로, 3-가로)
    container.add(new JButton("1")); // 상단    왼쪽 첫 번째 셀에 버튼 배치
    container.add(new JButton("2")); // 그 옆 셀에 버튼 배치
```

### BoxLayout
- 기본적으로 FlowLayout와 동일하나 컴포넌트를 수평으로 또는 수직으로만 배치한다 (주로 수직 배치 용도로 쓰임) 
  - 한 줄이 다 차도 다음 줄로 넘어가지 않는다
- 레이아웃 정책: 각 컴포넌트의 선호 크기를 모두 따른다
- 생성자
```java
    BoxLayout(Container target, int axis)
    // target은 layout 설정 대상이 되는 컨테이너임
    // axis는 BoxLayout.X_AXIS (수평 정렬) 또는 BoxLayout.Y_AXIS (수직 정렬) 값을 가짐
```

### 배치 관리자가 없는 컨테이너
- 배치관리자가 없는 컨테이너 개념
  - 응용프로그램에서 컴포넌트의 절대 크기와 절대 위치를 스스로 결정
- 용도
  - 컴포넌트의 크기나 위치를 개발자 임의로 결정하고자 하는 경우
  - 게임 프로그램과 같이 시간이나 마우스/키보드의 입력에 따라 컴포넌트들의 위치와 크기가 수시로 변하는 경우
  - 여러 컴포넌트들이 서로 겹치는 효과를 연출하고자 하는 경우
- 컨테이너의 배치 관리자 제거 방법 
```java
Container.setLayout(null);

    JPanel p = new JPanel(); 
    p.setLayout(null);
```

### 여러 개 레이아웃을 같이 사용해야 할 때
- JPanel 컨테이너를 사용하여 각 JPanel 컨테이너마다 레이아웃 관리자를 다르게 설정해 주면 된다.

## 이벤트 기반 프로그래밍
- 이벤트 기반 프로그램의 구조
  - 프로그램에서 처리하고자 하는 이벤트의 이벤트 처리 리스너 구현
- 이벤트 처리 순서
  - 이벤트 발생(예 :마우스나 키보드의 움직임 혹은 입력) 
  - 이벤트 객체 생성
    - 현재 발생한 이벤트에 대한 여러 정보를 가진 객체
  - 이벤트 리스너 찾기 (어느 함수 호출하게 할 것 인지)
  - 이벤트 리스너 호출
    - event 객체가 리스너에 전달됨
  - 이벤트 리스너 실행

### 이벤트 처리 관련 용어
- 이벤트 소스(event source)
    - 이벤트를 발생시킨 GUI 컴포넌트 
    - 예) 버튼
- 이벤트 객체(event object)
    - 발생한 이벤트에 대한 여러 속성을 가진 객체
    - 이벤트 종류, 이벤트 소스, 이벤트가 발생한 화면의 좌표, 마우스 버튼의 종류, 눌러진 키의 코드 값 등의 정보를 가짐
- 이벤트 리스너(event listener) 
    - 이벤트를 처리하는 코드 
    - 이벤트 소스에 등록되어야 함
- 이벤트 분배 스레드(event dispatch thread - EDT)
    - JVM으로 부터 이벤트 발생을 통지 받으면 이벤트 객체를 생성하여 이벤트 리스너를 찾아 호출함   
    - 접수된 이벤트는 이벤트 큐에 쌓여 한 이벤트 처리가 완전히 끝나야 다음 이벤트가 처리되므로 이벤트 리스너는 가능하면 짧은 시간 내 수행되도록 작성해야 함

## 이벤트 리스너 작성 방법
1. 독립 클래스
2. 내부 클래스
   - 버튼을 눌렀을 때 프레임 제목을 바꾸고 싶다!
3. 익명 클래스
   - 각 컴포넌트마다 리스너를 등록하기 위해 내부 클래스를 작성하려니 너무 번거로운데, 좀더 편한 방법은 없을까? 
   - 익명 클래스란?
     - (클래스 정의 + 인스턴스 생성)을 한번에 작성
     - 간단한 리스너의 경우 익명 클래스 사용 추천
     - 동일한 리스너를 여러 컴포넌트에 등록할 때에는 사용하면 안됨
     - 익명 클래스도 일종의 내부 클래스이므로 클래스 멤버에 마음대로 접근 가능
     - (가독성은 조금 떨어진다.)
     - 등록할 버튼이 여러개 일 때는 부적합
4. Lambda Expression
   - 이벤트 발생 시 호출할 함수를 별도로 만들고 이를 호출하는 방식
   - 이벤트 발생 시 호출할 함수를 별도로 만들지 않고 { }안에 정의하는 방식
```java 
  btn.addActionListener(e -> {
    if (btn.getText().equals("Action")) btn.setText("액션");
    else
        btn.setText("Action");
    setTitle(btn.getText()); // JFrame.setTitle() 호출 });
```

### CardLayout
- 컴포넌트들을 포개어 배치
- 컴포넌트 크기는 컨테이너와 일치
- CardLayout으로 설정된 컨테이너에 컴포넌트 추가하기    
    ```<Containter>.add(<Component>, String name)```
- CardLayout으로 설정된 컨테이너에 특정 컴포넌트 보여주기
    ```<CardLayout>.show(<Container>, String name)```
- 여러 CardLayout을 넣었을 때 가장 먼저 넣은 CardLayout을 디폴트로 보여줌

## WindowBuilder
### WindowBuilder
- GUI로 Swing의 레이아웃을 작성할 수 있는 플러그인

### GroupLayout
- 각 컴포넌트의 ```anchor point```를 어디에 둘 것인지를 설정함으로써 배치를 함
- 창을 늘렸을때 ```anchor point```에 따라 해당 위치에 고정됨

