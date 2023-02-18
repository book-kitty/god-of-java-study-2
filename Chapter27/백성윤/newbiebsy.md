# Chapter27 Serializable과 NIO

### Serializable 에 대해서 살펴보자
> java.io 패키지에 있는 Serializable 이라는 인터페이스를 살펴보면, 변수나 메소드가 없다는 것을 알 수 있다.
> 
> 이 인터페이스가 있는 이유는, **클래스가 파일에 읽거나 쓸 수 있도록 하거나, 다른 서버로 보내거나 받는 것을 가동하도록 하기 위함이다.**
>
> Serializable 인터페이스를 구현하면 JVM 에서 해당 객체는 저장하거나 다른 서버로 전송할 수 있도록 해 준다.
> 그리고, 인터페이스를 구현한 후에는 serialVersionUID 라는 값을 지정하는 것을 권장한다.(반드시 static final long으로 선언해야 하며, 변수명도 serialVersionUID로 선언해야 한다.)
> ```
> static final long serialVersionUID = 1L;
> ```
> 만약 별도로 지정하지 않으면, 자바 소스가 컴파일될 때 자동으로 생성해준다.(값은 아무런 값이나 지정해 주면 된다.)
> 
> serialVersionUID 라는 값은 해당 객체의 버전을 명시하는 데 사용된다.

### 객체를 저장하는 ObjectOutputStream 과 읽는 ObjectInputStream
> ObjectOutputStream이라는 클래스를 사용하면 객체를 저장할 수 있다. 반대로, ObjectInputStream 이라는 클래스를 사용하면 저장한 객체를 읽을 수 있다.
> 
> **저장하거나 읽으려 하는 객체의 클래스는 반드시 Serializable 인터페이스를 구현해야 한다.**
> 
> serialVersionUID를 지정해 놓은 상태에서 저장되어 있는 객체와 읽는 객체가 다르다면, 예를 들어 변수명을 바꾼다면
> 바뀐 변수명은 존재하지 않기 떄문에 해당 값은 null 로 처리된다. (Serializable 을 구현한 상황에서 serialVersionUID를 명시적으로 지정하면 변수가 변경되더라도 예외를 발생시키지 않는다.)
> 
> 참고로  Serializable 한 객체의 내용이 바뀌었는데도 아무런 예외를 발생시키지 않으면 운영 상황에서 데이터가 꼬일 수 있기 때문에,
> 절대 권장하는 코딩 방법이 아니다.(데이터가 바뀌면 serialVersionUID의 값을 변경하는 습관을 가져야한다.)

### transient라는 예약어는 Serializable과 떨어질 수 없는 관계이다
> transient 라는 예약어를 사용하여 선언한 변수는 Serializable의 대상에서 제외된다. 
> 
> 예를 들어 패스워드를 보관하고 있는 변수 같은 곳에 보안상의 이유로 transient 를 사용할 수 있다.

### NIO란?
> JDK 1.4 부터 NIO가 추가 되었다. NIO가 생긴 이유는 단 하나, 바로 속도 때문이다.
> 
> NIO는 지금까지 사용한 스트림을 사용하지 않고 채널(Channel)과 버퍼(Buffer)를 사용한다.   
> 채널은 물건을 중간에서 처리하는 도매상이라고 생각하면 되고, 버퍼는 도매상에서 물건을 사고, 소비자에게 물건을 파는 소매상으로 생각하면 된다.
> (대부분은 소매상을 통해서 도매상과 이야기할 일은 없다.)
> 
> 파일 데이터를 다룰 때에는 ByteBuffer라는 버퍼와 FileChannel 이라는 채널을 사용하면 간단하게 처리할 수 있다.   
> Channel 의 경우 간단하게 객체를 생성하여 read() 나 write() 메소드만 불러주면 된다고 생각하면 된다.

### NIO 의 Buffer 클래스
> NIO에서 제공하는 Buffer 클래스는 java.nio.Buffer 클래스를 확장하여 사용한다.
> 종류로는
> - ByteBuffer, CharBuffer, DoubleBuffer, FloatBuffer, IntBuffer, LongBuffer, ShortBuffer
>
> 등이 존재한다.
>  
> 먼저 버퍼의 상태 및 속성을 확인하는 메소드는 다음과 같다.

| 리턴 타입    | 메소드           | 설명                      |
|----------|---------------|-------------------------|
| int      | capacity()    | 버퍼에 담을 수 있는 크기 리턴       |
| int      | limit()       | 버퍼에서 읽거나 쓸 수 없는 첫 위치 리턴 |
| int      | position()    | 현재 버퍼의 위치 리턴            |

> 버퍼는 위치가 있다. 버퍼에 데이터를 담거나, 읽는 작업을 수행하면 현재의 "위치"가 이동한다.(그래야 그 다음 "위치"가 있는 것을 바로 쓰거나, 읽을 수 있기 때문이다.)
> 
> - 현재의 "위치"를 나타내는 메소드가 position()이고,
> - 읽거나 쓸 수 없는 "위치"를 나타내는 메소드가 limit()
> - 버퍼의 크기(capacity)를 나타내는 것이 capacity()
>
> 메소드다.
> 이 값들의 관계는 다음과 같다.
> ```
> 0 <= mark <= position <= limit <= capacity(크기)
> ```

> NIO는 파일을 쓰고 읽을 때에만 사용하는 것이 아니라, 파일 복사를 하거나, 네트워크로 데이터를 주고 받을 때에도 사용할 수 있다.


