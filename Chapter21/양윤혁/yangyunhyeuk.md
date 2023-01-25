
> 정리
> 

자바의 패키지 중에서 유일하게 java.lang 패키지에 있는 클래스들은 import 없이 사용이 가능하며, 동시에 개발에서 꼭 필요한 여러 기능들을 제공한다. 

### java.lang 패키지

| 구분 | 타입 | 항목들 |
| --- | --- | --- |
| 언어 관련 기본 | 인터페이스 | Cloneable, Comparable, Iterable, Readable |
|  | 클래스 | Class, ClassLoader, Compiler, Enum, Object, Package, System, Void, StackTraceElement, SecurityManager |
|  | 예외 및 에러 | ArrayIndexOutOfBoundsException, ClassNotFoundException, IllegalAccessException… |
| 문자열 관련 | 인터페이스 | Appendable, CharSequence |
|  | 클래스 | String, StringBuilder, StringBuffer |
|  | 예외 및 에러 | StringIndexOufOfBoundsException |
| 기본 자료형 및 숫자 관련 | 클래스 | Boolean, Byte, Character, Subset, Character, Double, Float, Integer, Long, Math, Number, Short |
|  | 예외 및 에러 | AthrimethicException, NumberFormatException |
| 쓰레드 관련 | 인터페이스 | Runnable |
|  | 클래스 | Thread, ThreadGroup |
|  | 예외 및 에러 | IllegalMonitorStateException |
| 예외 관련 | 클래스 | Throwable |
|  | 예외 및 에러 | Exception |
| 런타임 관련 | 클래스 | Process, ProcessBuilder, Runtime, RuntimePermission |
|  | 예외 및 에러 | IllegalStateException |

---

- 자바는 가상 머신에서 메모리를 관리하지만 프로그램이 잘못 작성되었거나, 설정이 제대로 되어 있지 않을 경우 메모리가 부족하여 OutOfMemoryError가 발생할 수 있다.
- 자바에서는 스택이라는 영역에 어떤 메서드가 어떤 메서드를 호출했는지에 대한 정보를 관리하는데, 호출 정보의 한계를 넘어서는 경우 호출된 메서드의 깊이가 너무 깊어서 StackOverFlowError가 발생한다.

---

자바에서는 간단한 계산을 할 때 대부분 기본 자료형을 사용한다. 

기본 자료형의 경우 힙 영역이 아닌, 스택이라는 영역에 저장되어 관리된다. 

**기본 자료형 (primitive data type)**

- 특징
    - 자바 컴파일러에 의해 해석되는 자료형태를 의미한다.
    - 총 8가지로 구성되어, 사용 전 선언되어야만 한다.
    - OS에 따라 자료형의 길이가 변하지 않는다.
    - 비객체 타입으로 NULL값을 가질 수 없다.
    - 스택 메모리에 저장된다.
- 종류
    - 논리형 : boolean
    - 문자형 : char
    - 정수형 : byte, short, int, long
    - 실수형 : float, double

**참조 자료형 (reference data type)**

- 특징
    - 기본형을 제외한 타입으로, Object 클래스를 상속하는 모든 클래스를 의미한다.
    - 객체 타입으로 빈 객체를 의미하는 NULL이 존재한다.
    - 문법 상 에러는 없으나, 런타임 에러가 발생할 수 있다. (NPE)
    - new 예약어를 통해 생성하는 것들은 힙 영역에 생성되며, 가비지 컬렉터가 돌며 GC 수행한다.
    - 힙 메모리에 생성된 인스턴스는 메서드나 각종 인터페이스에 접근하기 위해 JVM의 Stack 영역에 존재하는 Frame에 일종의 포인터인 참조값을 갖고 있어 이를 통해 인스턴스를 핸들링한다.
- 종류
    - class type (클래스)
    - interface type (인터페이스)
    - array type (배열)
    - enum type (열거)
    - 기타..

### 참조 자료형 중에서 특이한 점

- Btye, Short, Integer, Long, Float, Double 타입은 필요 시 기본 자료형처럼 사용할 수 있다.
- 따라서 new를 사용하여 객체를 만들지 않아도 값을 할당할 수 있다.

```jsx
public void numberTypeCheck(){
	Integer int1;
	int1 = 100;
	sout(int1.doubleValue());
}
```

그렇다면 왜 혼동되게 숫자를 처리하는 참조 자료형을 만들었을까?

1. 매개 변수를 참조 자료형으로만 받는 메서드를 처리하기 위해 
2. 제네릭과 같이 기본 자료형을 사용하지 않는 기능을 사용하기 위해 
3. MIN_VALUE, MAX_VALUE 같이 클래스에 선언된 상수 값을 사용하기 위해
4. 문자열을 숫자로, 숫자를 문자열로 쉽게 변환하고 2,8,10,16 진수 변환을 용이하게 하기 위해

---

### 로킹 작업 시 System.out.println()을 기피해야 하는 이유

1. 당시에는 확인 가능하나, 에러 발생 시 추적할 수 있는 최소한의 정보가 남지 않기 때문에 
2. 로그 출력 레벨을 컨트롤할 수 없기 때문에 
    - 에러, 장애 발생 시 DEBUG, WARN, ERROR 등의 로그 출력 레벨을 컨트롤하지 못하고 어떤 환경에서든 동일한 로그가 출력되어 정작 중요한 정보를 얻기 힘들 수 있다.
3. 성능 저하의 원인이 될 수 있기 때문에 
    - println 메서드 내부에 newLine() 메서드를 호출하는 부분이 있는데, newLine() 내부에 synchronized가 존재한다.
        - **synchronized : 메서드나 블록 코드에 동기화 영역을 표시하는 것으로 동기화된 블록은 한 시점에 1개의 스레드만 접근이 가능한데, 여러 쓰레드 사용 시 오버헤드가 발생되어 프로세스 성능에 악영향을 미쳐 처리가 늦어진다.**
        - **즉, System.out.println() 메서드가 끝나기 전까지 아무 일을 실행할 수 없고, 대기만을 해야하는 상황에 성능 저하가 발생하는 것이다.**
