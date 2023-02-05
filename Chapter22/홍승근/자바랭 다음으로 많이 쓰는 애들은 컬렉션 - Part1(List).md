# 자바 컬렉션
> 자바에서 컬렉션은 목록성 데이터를 처리하는 자료 구조를 통칭한다. 자료구조는 영어로 "Data Structure"라고 한다. 즉, 어떤 정보를 담는
> 것을 의미하는 데, 하나의 데이터가 아닌 여러 데이터를 담을 때 사용한다.

### 자바에서의 데이터를 담는 자료 구조
- 순서가 있는 목록(List) 형
- 순서가 중요하지 않은 셋(Set) 형
- 먼저 들어온 것이 먼저 나가는 큐(Queue) 형
- 키-값 으로 저장되는 맵(Map) 형
> 자바에서 List, Set, Queue는 Collection이라는 인터페이스를 구현하고 있다. 유일하게 Map만이 Collection과 관련 없는 별도의 인터페이스로
> 선언되어 있다.

### Collection 인터페이스
> Collection 인터페이스는 Iterable라는 인터페이스를 확장했다. Iterable에 선언되어 있는 메소드는 iterator() 하나 뿐인데 이 말은
> Collection 인터페이스가 Iterable 인터페이스를 확장한 의미는, Iterator 인터페이스를 사용하여 데이터를 순차적으로 가져올 수 있다는 의미이다.
 
## ArrayList
- 가장 상위 부모는 Object 클래스이고, 그 다음으로 AbstractCollection, AbstractList의 순으로 확장했다.
- ArrayList가 구현한 모든 인터페이스는 Serializable, Cloneable, Iterable, Collection, List, RandomAccess이다.
- ArrayList 객체를 선언할 때 매개 변수를 넣지 않으면, 초기 크기는 10이다.
- ArrayList는 확장된 배열 타입이기 때문에 배열처럼 순서가 매우 중요하다.
- Shallow Copy를 하게 되면 객체가 생성되면서 참조 되고 있는 주소까지 사용하게 된다.
- ArrayList는 중복된 데이터를 넣을 수 있다.
- ArrayList는 쓰레드에 안전하지 않다.

**ArrayList가 구현한 인터페이스**
| 인터페이스        | 용도                                                        |
|--------------|-----------------------------------------------------------|
| Serializable | 원격으로 객체를 전송하거나 파일에 저장할 수 있음                               |
| Cloneable    | Object 클래스의 clone() 메소드가 제대로 수행될 수 있음을 지정, 복제가 가능한 객체임을 의미 |
| Iterable  | 객체가 "foreach" 문장을 사용할 수 있음을 지정                            |
| Collection | 여러 개의 객체를 하나의 객체에 담아 처리할 때의 메소드 지정                        |
| List      | 목록형 데이터를 처리하는 것과 관련된 메소드 지정                               |
| Collection | 목록형 데이터에 보다 빠르게 접근할 수 있도록 랜덤하게 접근하는 알고리즘이 적용된다는 것을 지정     |

## Stack
- 마지막에 들어온 데이터를 가장 처음에 꺼내는 LIFO 기능을 구현하려고 할 때 필요한 클래스다.
- ArrayDeque라는 클래스가 더 빠르기 때문에 LIFO 기능을 위해 사용하는 것을 권장하지 않는다.
  - 성능은 떨어지지만, 쓰레드에 안전한 LIFO 기능을 원한다면 Stack 클래스를 사용하면 된다.
- Stack 클래스의 부모 클래스는 Vector이다.
- Stack 클래스가 구현한 인터페이스는 ArrayList와 모두 동일하다.

## 정리
- Collection 인터페이스는 목록형 데이터를 대표한다.
- Collection 인터페이스를 확장하는 인터페이스는 List, Queue, Set이 있다.
