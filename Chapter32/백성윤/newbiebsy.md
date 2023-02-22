# Chapter 32 Java 8에 추가된 것들에는?

### Optional
> Optional 클래스는 null 처리를 보다 간편하게 하기 위해서 만든 클래스이고, java.util 패키지에 속해 있다.
> NullPointerException이 발생하는 상황을 간단하게 처리해준다.(단 잘못된 값을 넣으면 NoSuchElementException이 발생할 수도 있다.)

### Default method
> 인터페이스는 구현된 메소드가 있으면 안됐지만, Java 8 부터는 default 키워드를 이용하여 메소드 구현이 가능해졌다.   
> 하위 호환성 문제를 해결하기 위해서 나왔다.(기존 인터페이스를 구현하던 클래스의 코드를 수정하지 않아도 된다.)

### 날짜 관련 클래스들
> Java 8 이전에 사용하던 Date나 SimpleDateFormatter 같은 클래스들은 쓰레드에 안전하지 않다.(API 구성또한 복잡하게 되어 있었다.)
> 
> 위와 같은 문제점을 해결하기 위해 Java 8 에서는 java.time 패키지를 만들었다.
> Local과 Locale은 다르다는 것을 주의해야 한다.(각각 시간과 지역을 의미하는 클래스이다.)   
> DayOfWeek enum을 사용하여 요일 표현을 더 쉽게 할 수 있다.

### 병렬 배열 정렬(Parallel array sorting)
> 자바에서 배열을 정렬하는 가장 편한 방법은 java.util 패키지의 Arrays 클래스를 사용하는 것이다.
> Java 8 에서는 **parallelSort()** 라는 정렬 메소드가 제공되는데, 이 메소드는 Fork-Join 프레임웍이 내부적으로 사용된다.
> 
> 기존 sort() 메소드와의 차이점은
> - sort() 의 경우는 단일 쓰레드로 수행된다.
> - parallelSort() 는 여러 개의 쓰레드로 나뉘어 작업하기 때문에 CPU를 더 많이 사용하는 대신 처리 속도는 더 빠르다.
>   - 실제 성능을 비교하면 5,000개 정도부터 parallelSort()의 성능이 더 빨라지는 것을 볼 수 있다.

### StringJoiner
> 문자열을  처리할 때 사용한다.