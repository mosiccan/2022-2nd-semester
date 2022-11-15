# JAVA 2 08
파일 입출력

## 스트림
- 스트림은 입출력 장치와 프로그램을 연결하며, 이들 사이의 데이타 흐름을 처리하는 인스턴스 
  - 입력 스트림
    - 입력 장치로부터 자바 프로그램으로 전달되는 데이터의 흐름 혹은 데이터 전송 인스턴스
  - 출력 스트림
    - 자바 프로그램에서 출력 장치로 보내는 데이터의 흐름 혹은 데이터 전송 인스턴스
- 입출력 스트림 기본 단위 : 바이트
- 자바 입출력 스트림 특징
  - 단방향 스트림, 선입선출 구조
  - 한번 스트림을 열었으면 반드시 닫아줘야 함

### 자바 입출력 스트림
- 문자 입출력 스트림
  - 문자의 흐름으로 처리
  - 해당 운영체제의 기본 인코딩 방식에 맞춰서 자동으로 문자가 인코딩되어 처리되도록 함
  - 문자가 아닌 바이너리 데이터는 스트림에서 처리하지 못함
  - 정수, 실수, 문자열 같은 기본 데이터 처리
- 바이트 입출력 스트림
  - 단순 바이트의 흐름으로만 처리
  - **인스턴스를 통째**로 입출력 할 경우 사용
  - 예) 바이너리 파일을 읽는 입력 스트림

### 문자 입출력 스트림
- 파일에 쓰기
  - 사용할 객체  
  - ```BufferedWriter(new FileWriter(“textfile.txt”))```  
- BufferedWriter를 통해 파일에 쓰기
  - ```void write(String s) throws IOException```  
  - ```void newline() throws IOException```  
  - ```void close() throws IOException```  
- 파일 읽기
  - 사용할 객체
  - ```BufferedReader(new FileReader(“textfile.txt"))```

  - BufferedReader를 통해 파일 읽기  
  - ```String readLine() throws IOException```  
  - ```void close() throws IOException``` 
- ```IOException```이 발생하기 때문에 항상 ```try~catch```문 사용해야함

- main함수에 throw를 해서 넘길 수 있지만 무책임한 방법, java 가상머신이 받아 그냥 종료함  
- 개행방법
```java
out.newLine();
\n  // 유닉스
\r  // 맥
\r\n  // 윈도우
System.lineSeparator();
```  

- 기본적으로 txt 파일을 생성하면 프로젝트 파일에 생성된다.
- 읽기 모드로 변경한다면 파일 수정 불가!

- out.close도 IOException이 발생하기에 finally 구문에 넣어 사용해야한다.

### 좀 더 close를 간단하게 하기 : try-with-resources
- try() 안에 AutoCloseable 인터페이스를 구현한 자원을 넣을 경우 close()을 직접 호출하지 않아도 try{}를 빠져나갈 때 자동으로 호출된다.

### 스트림을 통한 인스턴스의 입출력
- 용어 정리
    - 직렬화(Serialize): 객체 정보를 파일에 저장하기 위해 바이트 스트림으로 변환하는 과정
    - 역직렬화(Deserialize): 직렬화로 파일에 저장된 객체 정보를 읽어 들이는 과정
    - Socket 기반 네트워크 통신 시에도 사용됨
- 직렬화는 리소스 소모가 많은 작업
  - 과도한 직렬화는 성능에 영향을 끼침 (CPU)
  - 그림을 저장하거나 할 때는 스트림 입출력이 필요, 대부분의 경우엔 문자 입출력 방식으로 가능
  - 빈번하지 않다면 매우 편리하게 자료를 입출력할 수 있음

### 바이트 입출력을 위해 필요한 것들
- 파일에 쓰기
  - ```ObjectOutputStream(new FileOutputStream("data.bin"))```
    - ```void writeObject(Object obj) throws IOException```
    - ```void close() throws IOException```
  - 기존 파일에 이어서 쓰기 불가능
    - 기존 파일을 모두 읽은 후 새로운 내용을 추가하여 파일에 새로 써야함
- 파일 읽기
  - ```ObjectInputStream(new FileInputStream("data.bin"))```
    - ```Object readObject() throws IOException, ClassNotFoundException```
    - ```void close() throws IOException```
  - 읽을 직렬화 가능한 클래스가 정의되지 않았을 경우 ClassNotFoundException 발생  

- 입출력 대상이 되는 인스턴스의 클래스는
  - java.io.Serializable 인터페이스를 직접 구현하거나 구현하는 클래스를 상속해야 함 
  - 이 클래스의 인스턴스는 직렬화를 해도 괜찮습니다.. 라는 의미