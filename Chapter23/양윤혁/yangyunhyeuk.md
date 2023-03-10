> 정리
> 

- HashSet
    - 순서가 필요없는 데이터를 해시 테이블에 저장한다.
    - Set 중에 가장 성능이 좋다.
- TreeSet
    - 저장된 데이터의 값에 따라서 정렬되는 셋이다.
    - red-black이라는 트리 타입으로 값이 저장되며 HashSet 보다 약간 성능이 느리다.
        - red-black : 각 노드의 색을 적색, 흑색으로 구분하여 데이터를 빠르게 쉽게 찾을 수 있는 이진트리를 말한다.
- LinkedHashSet
    - 연결된 목록 타입으로 구현된 해시 테이블에 데이터를 저장한다.
    - 저장된 순서에 따라서 값이 정렬된다.
    - 대신 성능이 이 셋 중 가장 나쁘다.

---

- HashSet의 생성자 종류 중 매개 변수에 로드 팩터를 사용하는 생성자가 있다.
    - 로드 팩터
        - (데이터의 개수) / (저장 공간)을 의미한다.
        - 만약 데이터의 개수가 증가하여 로드 팩터보다 커지면 저장 공간의 크기는 증가되고 해시 재정리 작업을 해야만 한다.
        - 데이터가 해시 재정리 작업에 들어가면 내부에 갖고 있는 자료 구조를 다시 생성하는 단계를 거쳐야하므로 성능에 영향이 발생한다.

---

### 배열의 중간에 있는 데이터가 지속적으로 삭제되고, 추가될 경우 LinkedList가 배열보다 메모리 공간 측면에서 훨씬 유리하다.

- 배열과 같은 ArrayList와 Vector는 각 위치가 정해져 있고, 그 위치로 데이터를 찾는다.
- 근데 맨 앞의 값을 삭제하면 그 뒤에 있는 값들은 하나씩 앞으로 위치를 이동해야 제대로 된 위치값을 갖게 된다.
- 그에 반해 LinkedList는 중간에 있는 데이터를 삭제하면 지운 데이터의 앞에 있는 데이터와 뒤에 있는 데이터가 연결되어 위치를 맞추기 위해 값을 이동하는 단계를 거칠 필요가 없다.
- 그래서 LinkedList의 경우 일반적인 배열 타입과 다르게 생성자로 객체를 생성 시 처음부터 크기를 지정하지 않는다. 그 이유는 각 데이터들이 앞뒤로 연결되는 구조이기에 미리 공간을 만들어놓을 필요가 없기 때문이다.

---

### LinkedList 클래스가 구현한 인터페이스 중 자바 6에서 추가된 Deque라는 것이 있다.

- “Double Ended Queue”의 약자이다.
- Queue 인터페이스를 확장하였기에 Queue의 기능을 전부 포함한다.
- 맨 앞에 값을 넣거나 빼는 작업, 맨 뒤에 값을 넣거나 빼는 작업을 수행하는데 용이하다.

---
