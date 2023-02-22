# ❓30장 Java 7에서 달라진 것들에는 ?
달라진 숫자 표현법<br>
0b : 2진수로 나타내기 위해 숫자 앞에 추가함<br>
ex) 0b100011010<br>
_ : 숫자 사이에 구분 표시함<br>
ex) int million = 1_000_000<br>
switch문 확장<br>
switch-case 문장에 String을 사용할 수 있다<br>
만약 문자열이 null일 경우 NullPointerException 발생하니 주의<br>
제네릭<br>
생성자에 타입들을 명시해 줄 필요가 없다<br>
Non reifiable varargs 타입<br>
reifiable : 실행시에도 타입 정보가 남아있는 타입<br>

non reifiable : 컴파일시 타입 정보가 손실되는 타입<br>

자바의 제네릭을 사용하면서 발생 가능한 문제 중 하나가 "reifiable 하지 않은 varargs 타입" 이다<br>

Collections 클래스에 addAll() 메소드는 API 문서에<br>
public static boolean addAll(Collection<? super T> c, T... elements) 라고 선언되어 있다.<br>
하지만 가변 매개 변수를 사용할 경우 실제 내부는 Object의 배열로 처리된다. 이렇게 Object 배열로 처리되면 잠재적으로 문제가 발생할 수 있다.<br>
