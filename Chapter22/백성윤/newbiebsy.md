# 컬렉션(List)

### 자바 컬렉션
> 자바에서 컬렉션은 목록성 데이터를 처리하는 자료 구조(Data Structure)를 통칭한다.   
> 자바에서 데이터를 담는 자료 구조는 크게 다음과 같이 분류할 수 있다.
> - 순서가 있는 List
> - 순서가 중요하지 않은 Set
> - 먼저 들어온 것이 먼저 나가는 Queue (선입선출,FIFO)
> - 키-값 으로 저장되는 Map
>
> 자바에서 List, Set, Queue 는 Collection 이라는 인터페이스를 구현하고 있다.

> Collection 인터페이스는 java.util 패키지에 선언되어 있으며,
> 여러개의 객체를 하나의 객체에 담아 처리할 때 공통적으로 사용되는 여러 메소드들을 선언해 놓았다.   
>> 위에서는 Map 만이 Collection 과 관련 없는 별도의 인터페이스로 선언되어 있다.

#### Collection 인터페이스에 대해서 살펴보자
> Collection 인터페이스는 다음과 같이 선언되어 있다.
> ```
> Public interface Collection<E> extends Iterable<E>
>```
> 선언문을 확인하면 Iterable< E> 이라는 인터페이스를 확장 했다는 것을 확인할 수 있다.
> Iterable 인터페이스에 선언되어 있는 메소드는 단지 하나다.

| 리턴 타입        | 메소드 이름 및 매개 변수 |
|--------------|----------------|
| Iterator< T> | iterator()     |
> > Iterator 라는 인터페이스에는 추가 데이터가 있는지 확인하는 hasNext() 메소드, 현재 위치를 다음 요소로 넘기고 그 값을 리턴해주는 next() 메소드, 데이터를 삭제하는 remove() 메소드가 있다.   
> 
> *결론적으로, Collection 인터페이스가 Iterable 인터페이스를 확장했다는 의미는, Iterator 인터페이스를 이용하여 데이터를 순차적으로 가져올 수 있다느 의미이다.*
> 
> 아래는 Collection 인터페이스에 선언된 주요 메소드들의 목록이다.

| 리턴 타입   | 메소드 이름 및 매개 변수          | 설명                                                                                   |
|---------|-------------------------|--------------------------------------------------------------------------------------|
| boolean | add(E e)                | 요소를 추가한다.                                                                            |
| boolean | addAll(Collection)      | 매개 변수로 넘어온 컬렉션의 모든 요소를 추가한다.                                                         |
| void    | clear()                 | 컬렉션에 있는 모든 요소 데이터를 지운다.                                                              |
| boolean | contains(Object)        | 매개 변수로 넘어온 객체가 해당 컬렉션에 있는지 확인한다. 동일한 값이 있으면 true를 리턴한다.                              |
| boolean | containsAll(Collection) | 매개 변수로 넘어온 객체들이 해당 컬렉션에 있는지 확인한다. 매개 변수로 넘어온 컬렉션에 있는 요소들과 동일한 값들이 모두 있으면 true를 리턴한다. |
| boolean | equals(Object)          | 매개 변수로 넘어온 객체와 같은 객체인지 확인한다.                                                         |
| int     | hashCode()              | 해시 코드값을 리턴한다.                                                                        |
 

### List 인터페이스와 그 동생들

> "목록"은 List 인터페이스로부터 시작되며, List 인터페이스는 Collection 인터페이스를 확장했다.
> 따라서, 몇몇 추가된 메소드를 제외하고는 Collection 에 선언된 메소드와 큰 차이는 없다.
> 
> List 인터페이스와 Colleciton을 확장한 다른 인터페이스의 가장 큰 차이점은 List 인터페이스는 배열처럼 "순서"가 있다는 것이다.
> 
> List 인터페이스를 구현한 클래스 중에서는 ArrayList, Vector, Stack, LinkedList 를 많이 사용한다.   
> 이 중에서 ArrayList 와 Vector 클래스의 사용법은 거의 동일하고 기능도 비슷하다. 이 두 클래스는 "확장 가능한 배열"이라고 생각하면 된다. (Vector 는 thread safe 하고 ArrayList 는 thread safe 하지 않다. ) 
>
> 그 다음에 있는 Stack 이라는 클래스는 Vector 클래스를 확장하여 만들었다. 이 클래스를 만든 가장 큰 이유는 LIFO(Last In First Out, 선입후출) 를 지원하기 위함이다.   
> 그 다음엔 LinkedList 라는 클래스가 있는데, 이 클래스는 "목록" 에도 속하지만 "큐" 에도 속한다. 

## ArrayList 생성자

> ArrayList 는 "확장 가능한 배열" 이다. 먼저 생성자를 살펴 보자.
 
| 생성자                                  | 설명                                                          |
|--------------------------------------|-------------------------------------------------------------|
| ArrayList()                          | 객체를 저장할 공간이 10개인 ArrayList 를 만든다.                           |
| ArrayList(Collection<? extends E> c) | 매개 변수로 넘어온 컬렉션 객체가 저장되어 있는 ArrayList 를 만든다.                 |
| ArrayList(int initialCapacity)       | 매개 변수로 넘어온 initialCapacity 개수만큼의 저장 공간을 갖는 ArrayList 를 만든다. |

> ArrayList 객체를 선언할 때 매개 변수를 넣지 않으면, 초기 크기는 10이다. 10개 이상의 데이터가 들어간다면 내부적으로 크기를 늘리는 작업이 수행되므로 저장되는 데이터의 크기가 어느정도 예측이 된다면 초기 크기를 지정할 것을 권장한다.

## 얕은 복사(Deep Copy), 깊은 복사(Shallow Copy)
> ```
> public class CopyTest {
>   public static void main(String[] args) {
>       ArrayList<String> list = new ArrayList<>();
>       list.add("A");
> 
>       ArrayList<String> list2 = list;
>       list.add("Shallow Copy Test");
> 
>       for(String tempData : list2) {
>           System.out.println(tempData);
>       }
>   }
> }
> ```
> 위와 같은```list2 = list``` 문장은 list2 가 list 의 값 뿐만이 아니라 참조되어 있는 주소까지도 사용하겠다는 말이다.(Shallow Copy)
> 
> Shallow Copy : 주소 값 복사
> Deep Copy : 실제 값을 새로운 메모리 공간에 복사
> 
> 따라서, 하나의 Collection 관련 객체를 복사할 일이 있을 때에는 생성자를 사용하거나, addAll() 메소드를 사용할 것을 권장한다.


