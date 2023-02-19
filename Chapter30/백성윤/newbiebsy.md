# Chapter 30 Java7에서 달라진 것들은?

> Java 7에서 대표적인 변경 사항들은 다음과 같다.
> - 숫자 표시 방법 보완
> - switch문에서 String 사용
> - 제네릭을 쉽게 사용할 수 있는 Diamond
> - 예외 처리시 다중 처리 가능
>

### 달라진 숫자 표현법
> - 숫자 앞에 0을 넣어주면 8 진수로, 0x를 넣으면 16진수로 인식한다.
> - 0b를 앞에 추가하면 2진수로 인식한다.
> - 숫자 사이에 '_'를 넣어 단위에 표시를 해줄 수 있다.

### switch 문장도 확장되었대요
> 기존에 switch - case 문에서는 정수형만 사용할 수 있었으나, 7버전 부터는 String의 사용이 가능해졌다.   
> 한가지 주의할 점은 String 문자열이 null인 경우이다. (NPE를 발생시킴)

### 제네릭은 다이아몬드를 쓰면 쉬워요.
> JAVA 7 부터는 아래와 같이 생성자에 일일이 타입들을 명시해 줄 필요가 없다.
> ```java
> HashMap<String,Integer> map = new HashMap<>();
> ```
> 이름 그대로 "<>"로 표시한 것을 다이아몬드라고 명명했으며, 다이아몬드를 사용하면 컴파일러에서 알아서 해당 생성자의 타입을 지정해준다.

### 예외도 이렇게 보안 되었답니다.
> JAVA 7부터 Exception을 처리하는 try-catch 블록에서 조건식에 아래와 같이 파이프 사용이 가능해졌다.
> ```java
> Scanner scanner = null;
> try {
> scanner = new Scanner(new File(fileName),encoding);
> System.out.println(scanner.nextLine());
> } catch(IllegalArgumentException | FileNotFoundException) {
> exception.printStackTrace();
> }
> ```
> 
> 또한 "리소스와 함께 처리하는 try 문장"이 추가되었다.   
> try-with-resource 라고 이야기 하는데, 별도로 close()를 호출해 줄 필요가 없다.(**AutoCloseable 인터페이스를 구현한 클래스만 해당한다.**)
>
> 추가로, 만약 try의 소괄호 내에서 두 개의 객체를 생성할 필요가 있다면, "세미콜론" 으로 구분하여 두 객체를 생성해 주면 된다.

### JAVA 7부터 꼭 닫지 않아도 되는 애들이 있어요.
> java.io.Closeable 이라는 인터페이스가 있다. 이 인터페이스를 구현한 클래스들은 명시적으로 close() 메소드를 사용하여 닫아주어야만 했다.   
> 하지만 위에서 말했듯이 Java 7 부터는 해당 인터페이스는 다음과 같이 선언되어 있다.
> ```java
> public interface Closeable extends AutoCloseable
> ```
> AutoCloseable 인터페이스를 상속받은 것을 볼 수 있으며, 이 인터페이스를 구현한 클래스는 앞 절에서 살펴본 try-witch-resource 문장에서 사용할 수 있다.
> 많이 사용하는 클래스 중 이 AutoCloseable 과 관련있는 클래스들은 아래와 같다.
> - java.nto.channel.FileLock
> - java.beans.XMLEncoder
> - java.beans.XMLDecoder
> - java.io.ObjectInput
> - java.io.ObjectOutput
> - java.util.Scanner
> - java.sql.connection
> - java.sql.ResultSet
> - java.sql.Statement
>
> 이 외에도 해당 인터페이스를 구현해 놓은 클래스가 매우 많기 때문에, java.lang 패키지에 선언되어 있는 AutoCloseable 인터페이스의 API를 살펴보자.