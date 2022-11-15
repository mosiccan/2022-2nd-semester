# JAVA 2 07
예외처리

## 예외(Exception)
- 실행 중 발생하는 에러는 컴파일러가 알 수 없음
- 자바에서는 실행 중 발생하는 에러를 예외로 처리응용
  - 프로그램에서 예외를 처리하지 않으면, 예외가 발생한 프로그램은 강제 종료

### try~catch
- try는 예외발생의 감지 대상을 감싸는 목적으로 사용된다. 
- catch는 발생한 예외상황의 처리를 위한 목적으로 사용한다. 

``` java
    try
    {
        // try영역에서 발생한 AAA 예외 상황은
    }
    catch(AAA e)
    {
        // catch 영역에서 처리된다.
    }
```
- try영역에서 예외가 하나라도 발생하면 try영역은 전부 실행 안된다...?
- 예외 발생할 수 있는 코드 외에 무엇을 더 try영역을 넣어야 되는지 생각해보자.

### e.getMessage(), e.printStackTrace();

- 모든 예외 클래스는 Throwable 클래스를 상속하며, 이 클래스에는 getMessage(), printStackTrace()가 정의되어 있다.
- String getMessage()
  - 예외가 발생한 원인정보를 문자열의 형태로 반환한다.
- void printStackTrace()
  - standard error stream(System.err)으로 예외에 대한 정보를 출력한다.

```java
    System.err.println(e.getMessage()); 
    e.System.out.println("프로그램을 종료합니다.");
    // err과 out은 순서가 뒤섞여 출력될 수 있다.
    // err은 오류메세지만 쉽게 필터링해서 출력해주기 위해 사용됨. 
    // catch문에 System.out을 사용해도 됨
```

## 둘 이상의 catch 블록에서 catch가 결정되는 방법

- 첫 번째 catch 블록에서부터 위에서부터 순서대로 찾아 내려온다.
- catch 블록의 매개변수가 해당 예외 인스턴스 참조 값을 받을 수 있는지를 확인하고, 받을 수 있다면 그 catch 블록에서 예외처리를 진행하고 나머지 catch 블록은 건너뛴다

### finally
- try 블록으로 일단 진입을 하면, 무조건 실행되는 finally 블록 
  - 예외 발견 시, catch 블록 실행 후 finally 블록 실행
  - 예외 미발견 시, try 블록을 모두 실행 후 finally 블록 실행
- **중간에 return문을 실행하더라도** finally 블록이 실행된 다음에 나간다. 