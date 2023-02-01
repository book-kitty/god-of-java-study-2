# 자바랭 다음으로 많이 쓰는 애들은 컬렉션 - Part3(Map)

## Map
- Map은 키와 값으로 이루어져 있다.
- Map은 키와 같이 1:1로 저장되고 키의 중복은 없다.
- 모든 데이터는 키와 같이 존재하며, 키와 값 둘 중 하나라도 없다면 저장할 수 없다.

## Map 인터페이스와 Hashtable 클래스의 차이
- Map은 Collection View를 사용하지만 HashTable은 Enumeration 객체를 통해서 데이터를 처리한다.
- Map은 키, 값, 키-값 쌍으로 데이터를 순환하여 처리할 수 있지만, HashTable은 이 중에서 키-값 쌍으로 데이터를 순환하여 처리할 수 없다.
- Map은 이터레이션을 처리하는 도중에 데이터를 삭제하는 안전한 방법을 제공하지만, HashTable은 그러한 기능을 제공하지 않는다.

## HashMap
- HashMap에 담을 데이터의 개수가 많을 때에는 초기 크기를 지정해 주는 것을 권장한다.
- HashMap의 키는 기본 자료형과 참조 자료형 모두 될 수 있다.
- Map은 키가 중복되지 않는 것이 중요하다. 따라서, 데이터를 저장한 순서대로 결과가 출력되지 않는다.
- Map에 저장되어 있는 모든 값을 출력할 때에는 values() 메소드가 keySet() 메소드보다 더 간편하다.

## TreeMap
- 정렬되는 기본적인 순서는 숫자 > 알파벳 대문자 > 알파벳 소문자 > 한글 순으로 정렬된다.  
- 키를 정렬하여 저장하고, 정렬된 순서대로 키를 출력한다.
  - 매우 많은 데이터를 TreeMap을 이용해 보관하여 처리하면 키가 정렬되기 때문에 HashMap보다 느리다.
- TreeMap이 키를 정렬하는 것은 SortedMap 인터페이스를 구현했기 때문이다.

### 정리
- Collection을 구현한 것은 List, Set, Queue이며, Map은 별도의 인터페이스로 되어 있다.
- List의 대표적인 클래스로는 ArrayList, LinkedList가 있으면 보통은 ArrayList를 많이 사용한다.
- 데이터의 중복이 없고, 순서가 필요 없는 Set의 대표적인 클래스는 HashSet, TreeSet, LinkedList가 있다.
- 데이터가 들어온 순서대로 처리하기 위해서 사용하는 Queue의 대표적인 클래스는 LinkedList, PriorityQueue 등이 있다.
- Map의 대표적인 클래스에는 HashMap, TreeMap, LinkedHashMap이 있다.
