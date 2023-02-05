> 정리
> 

### Map의 조건

- 모든 데이터는 키와 값이 존재한다.
- 키가 없이 값만 저장될 수는 없다.
- 값없이 키만 저장할 수 있다.
- 키는 해당 Map에서 고유해야만 한다.
- 값은 Map에서 중복 가능하다.

---

### Map 인터페이스를 구현한 클래스

- HashMap
- TreeMap
- LinkedHashMap
- HashTable

- HashTable은 Map 인터페이스를 구현하기는 했지만, 일반적인 Map 인터페이스를 구현한 클래스와는 다르다.
    - Map은 컬렉션 뷰를 사용한다.
        - HashTable은 Enumeration 객체를 통해서 데이터를 처리한다.
    - Map은 키, 값, 키-값 쌍으로 데이터를 순환하여 처리할 수 있다.
        - HashTable은 이 중에서 키-값 쌍으로 데이터를 순환하여 처리할 수 없다.
    - Map은 이터레이션을 처리하는 도중에 데이터를 삭제하는 안전한 방법을 제공한다.
        - HashTable은 그러한 기능을 제공하지 않는다.
        
    
    | 기능 | HashMap | HashTable |
    | --- | --- | --- |
    | 키나 값에 null 저장 가능 여부 | 가능 | 불가능 |
    | 여러 쓰레드 안전 여부 | 불가능 | 가능 |
- 위 표에서 차이가 발생하는 이유
    - 자바에 Collection이라는 인터페이스가 추가된 것은 JDK 1.2부터다.
        - 이 때 HashMap과 TreeMap이라는 클래스도 이 때 만들어졌다.
        - 더구나, LinkedHashMap은 JDK 1.4에서 추가되었다.
    - 허나, HashTable은 JDK 1.0부터 만들어져 사용된 클래스이기에 Map 인터페이스의 기능을 구현한 것은 JDK 1.2부터이다.
    - 즉, HashTable은 만들어진 Map에 맞춰 보완된 것이다.
    

---

### 자바의 자료 구조 특징

- List, Queue은 데이터 추가 순서가 중요하다.
- Set, Map은 데이터 추가 순서가 중요치 않다.
    - Set : 데이터가 중복되지 않는 것이 중요하다.
    - Map : 키가 중복되지 않는 것이 중요하다.

---

### TreeMap

- 해당 클래스는 저장하면서 키를 정렬한다. (SortedMap이란 인터페이스를 구현)
- 매우 많은 데이터를 TreeMap을 이용하여 보관하여 처리할 때는 HashMap보다 느릴 것이다.
    - 왜냐하면 키가 정렬되어 있기 때문이다.
- 허나 데이터가 방대하지 않을 경우 HashMap보다는 TreeMap을 권장한다.

---

### Map을 구현한 Properties 클래스

- HashTable을 확장하여 구현한 클래스이다.
- 고로 Map 인터페이스에서 제공하는 모든 메서드를 사용할 수 있다.

- Properties 클래스를 사용하는 이유는 무엇일까
    - 해당 클래스의 객체에 시스템 속성만 저장할 수 있는게 아니라, 애플리케이션에서 사용할 여러 속성값들을 저장하고 읽어들일 수 있기 때문이다.
    - 만약 해당 클래스가 없었다면, 개발자가 직접 파일을 읽는 메서드(  load() )도 만들고, 파일에 쓰는 메서드( store() )도 만들어야 한다.

---

- Collection
    - List
        - ArrayList
        - LinkedList (중복)
    - Set
        - HashSet
        - TreeSet
        - LinkedHashSet
    - Queue
        - LinkedList (중복)
        - PriorityQueue

- Collection의 데이터 처리 시 for문 뿐만 아니라, iterator()메서드를 통해 Iterator 객체를 얻어 각 데이터를 처리할 수 있다.

- Map
    - HashMap
    - TreeMap
    - LinkedHashMap

---
