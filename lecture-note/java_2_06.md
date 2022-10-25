# JAVA 2 06
컬렉션 프레임워크(List, Set, Map)

## 컬렉션
- 자바의 JDK는 주요 자료 구조들을 컬렉션으로 만들어 제공
- 요소(element)라고 불리는 가변 개수의 객체들의 모음
  - 객체들의 컨테이너라고도 불림
  - 요소의 개수에 따라 컬렉션은 자동 크기 조절
  - 컬렉션은 요소의 삽입, 삭제에 따른 요소의 이동 자동 관리
- 고정 크기의 배열을 다루는 어려움 해소

### 컬렉션을 위한 인터페이스와 클래스
- **인터페이스(클래스)**
  - Collection(Set, List, Queue)
  - Set(HashSet)
  - List(ArrayList)
  - Queue(LinkedList)
  - Map(HashMap)

## List
- ArrayList<E>, LinkedList<E>
- List<E> 인터페이스를 구현 클래스의 인스턴스 저장 특징
  - 동일한 인스턴스의 중복 저장을 허용한다.
  - 인스턴스의 저장 순서가 유지된다.

### ArrayList
- ArrayList<E>의 특성
  - java.util.ArrayList, 가변 크기 배열을 구현한 클래스
    - <E>에서 E 대신 요소로 사용할 특정 타입으로 구체화
  - 내부적으로 배열로 구현되며, 공간이 더 필요할 경우 현재 공간의 0.5배씩 늘림
    - LinkedList의 경우 doubly linked list로 구현되며, add(), remove() 성능이 뛰어나나, random element를 접근해야 하는 get(), set()은 성능 뒤짐
  - ArrayList에 삽입 가능한   것
    - 객체, null
    - 기본 타입(Wrapper 객체로 만들든지, 자동박싱/언박싱 사용하든지) 
  - ArrayList에 객체 삽입/삭제
    - 리스트의 맨 뒤에 객체 추가 : 공간이 모자라면 자동 늘림
    - 리스트의 중간에 객체 삽입 : 삽입된 뒤의 객체는 뒤로 하나씩 이동
    - 임의의 위치에 있는 객체 삭제 가능 : 객체 삭제 후 자동 자리 이동
### ArrayList, LinkedList 차이
- ArrayList<E>
  - 저장소의 용량을 늘리는 과정에서 많은 시간이 소요된다. 
  - 데이터의 삭제에 필요한 연산과정이 길다. 
  - 데이터의 참조가 용이해서 빠른 읽기가 가능하다.
- LinkedList<E>
  - 저장소의 용량을 늘리는 과정이 간단하다.
  - 데이터의 삭제가 매우 간단하다
  - 데이터의 참조가 다소 불편하다

### Iterator
- Iterator<E> 인터페이스
  - ArrayList<E>, LinkedList<E>, Set<E>가 상속받는 인터페이스
    - 리스트 구조의 컬렉션에서 요소의 순차 검색을 편리하게 할 수 있도록 해 줌


### Set
- 데이터의 저장순서를 유지하지 않는다.
- 데이터의 중복저장을 허용하지 않는다. 
  - 단, 동일 데이터에 대한 기준은 프로그래머가 정의   즉, ‘집합’의 성격을 지닌다. 

- 어떤 컬렉션 타입이든 iteratere 사용하면 검색?

### Hash 알고리즘
- 여러가지 데이터가 있을 때 특정 카테고리로 나누고 싶을 때 사용
  - ex) 
  - 데이터를 3으로 나머지 연산하였을때 얻게 되는 나 머지 값을 ‘해시 값’으로 하여 총 세 개의 부류를 구 성하였다.
  - 정수 12가 저장되어있는지 확인할 경우 12의 해시
값(0)을 구한다. 그 다음에 해시 값에 해당하는 부 류(연산결과0)에서만 정수 12의 존재 유무를 확인 하면 된다.. 

### HashMap
- 키(Key)와 값(Value)의 쌍으로 구성되는 자료 구조를 다루는 컬렉션
  - 키는 중복될 수 없음
- 키가 프로그래머가 만든 클래스일 경우 HashSet과 마찬가지로 중복 기준을 정해 주어야 함
  - 하나의 키는 하나의 값과 매핑됨
  - 요소의 위치로 값을 찾는 것이 아니라 키로 찾을 경우 사용됨
- 키와 값이 한 쌍으로 삽입됨
- 값을 검색하기 위해서는 반드시 키 이용, 인덱스 이용 불가
- 삽입되는 순서와 들어있는 위치는 관계가 없음

- put 
  - HashMap에 값을 추가하려면 put(key,value) 메소드를 사용하면 됩니다. 
  - 선언 시 HashMap에 설정해준 타입과 같은 타입의 Key와 Value값을 넣어야 합니다.
  - 하지만 입력되는 키 값이 HashMap 내부에 존재한다면 **기존의 값은 새로 입력되는 값**으로 대치됩니다.

``` java
  Map<String, Integer> fruits = new HashMap<>();
  fruits.put("apple", 1);
  fruits.put("banana", 2);
  fruits.put("kiwi", 3);
  fruits.put(null, 4);
  fruits.put("kiwi", 5);
  System.out.println("fruits: " + fruits);

  // output : fruits: {banana=2, null=4, apple=1, kiwi=5} 

```

