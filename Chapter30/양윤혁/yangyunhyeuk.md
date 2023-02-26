# [chapter 30]

> 정리
> 

## 자바 7에서 달라진 것은?

- 대표적인 변경사항들은 다음의 것들이 있다.
    - 숫자 표시 방법 보완
    - switch문에서 String 사용
    - 제네릭을 쉽게 사용할 수 있는 다이아몬드
    - 예외 처리 시 다중 처리 가능

---

- JDK 6까지만해도 숫자를 표현할 때
    - 아무런 접두사를 숫자 앞에 넣지 않으면 10진수로 인식한다.
    - 0을 숫자 앞에 넣어주면 8진수로 인식한다.
    - 0x를 숫자 앞에 넣어주면 16진수로 인식한다.
- 허나, JDK 7부터는 2진수 표현이 추가되었다.
    - 2진수를 나타내기 위해서 0b를 앞에 추가해주면 된다.
    - 만약 jdk 6이하에서 컴파일 수행 시 컴파일 에러가 발생해버린다.

---

- 우리나라에서는 돈, 숫자 단위를 표현할 때 1000 단위에 쉼표를 붙인다.
    - 이 과정에서 천 단위를 헷갈려할 수 있기에 개발자가 직접 제대로 입력했는지 확인해야한다.
    - 하지만, jdk 7버전부터 “_” 언더바를 사용할 수 있다.
        - int million = 1_000_000;
            - 참고로 언더바를 사용할 때에는 무조건 숫자 사이에 기재해주어야 한다.
            

---

- jdk 6까지만 해도 switch문에서 정수형만 사용 가능했으나, 
jdk 7부터는 switch문장 조건에 String 도 사용할 수 있다.
    - jdk 6 이하 버전에서는 String을 매개변수로 받는 메서드는 컴파일, 실행이 안되니 유의해야 한다.
- 그리고 switch 조건문에 String을 사용하는 상황에서 NPE가 발생할 수 있으니, NULL 체크는 권장이 아닌 필수다.

---

- jdk 7 이상부터는 생성자에 일일이 타입을 명시해줄 필요가 없다.
    - 이유는 이미 변수를 선언할 때 필요한 타입들을 지정해 놓았기 때문이다.
    
    ```jsx
    HashMap<String, Integer> map = new HashMap<>();
    Map<String, List<Integer>> map2 = new HashMap<>();
    ArrayList<String> list = new ArrayList<>();
    ```
    

---

- 자바의 제네릭을 사용하면서 발생 가능한 문제 중 하나가 “reifiable 하지 않은 varargs 타입”이다.
    - 이 문제는 자바에서 제네릭을 사용하지 않은 버전과의 호환성을 위해서 제공했던 기능때문에 발생한다.

- “reifiable”은 실행 시에도 타입 정보가 남아있는 타입을 의미하고,
- “non reifiable”은 컴파일 시 타입 정보가 손실되는 타입을 의미한다.

- 여러분들이 List의 addAll 메서드에서 가변 매개 변수를 사용할 경우에는 실제로 내부적으로 인자 타입이 Object의 배열로 처리된다.
    - 이 경우 큰 문제는 발생하지 않으나, 잠재적으로 문제가 발생할 수도 있다.
    - 이러한 경고를 없애기 위해서 @SafeVarargs라는 어노테이션을 메서드 선언부에 추가하면 된다.
    - Collection 클래스 내 addAll 메서드에도 자바 7부터는 해당 어노테이션이 적용되어 있다.
        - 해당 어노테이션은 다음의 경우에만 사용할 수 있다.
            - 가변 매개변수를 사용하고,
            - final이나 static으로 선언되어 있어야 한다.
        - 그리고 해당 어노테이션은 가변 매개 변수가 reifiable 타입이고 메서드 내에서 매개 변수를 다른 변수에 대입하는 작업을 수행하는 경우에는 컴파일러에서 경고가 발생한다.

---

- jdk 7 이후부터는 예외 처리에 관해서도 보완이 되었는데
    - catch문 내에서 마주하는 예외 정의에 관해서
    - 파이프 기호(”|”)로 연결하여 예외 상황을 여러 가지의 경우에서 처리할 수 있다.

- jdk 7 이전에는 close를 호출하기 위해서 try-catch-finally를 이용해서 null 체크와 함께 직접 호출하여 사용해야 했는데, 이 과정은 다음과 같은 단점을 갖는다

```jsx
public static void main(String args[]) throws IOException {
    FileInputStream is = null;
    BufferedInputStream bis = null;
    try {
        is = new FileInputStream("file.txt");
        bis = new BufferedInputStream(is);
        int data = -1;
        while((data = bis.read()) != -1){
            System.out.print((char) data);
        }
    } finally {
        // close resources
        if (is != null) is.close();
        if (bis != null) bis.close();
    }
}
```

- 자원 반납에 의해 코드가 복잡해진다.
- 작업이 번거롭다.
- 실수로 자원을 반납하지 못하는 상황이 발생한다.
- 에러로 자원를 반납하지 못하는 경우가 발생한다.
- 에러 스택 트레이스가 누락되어 디버깅이 어렵다.
- 허나, jdk 7 이후부터 자원을 자동으로 반납해주는 try-with-resource 문법이 추가되었다.
- 자바는 AutoCloseable 인터페이스를 구현하고 있는 자원에 대해서 try-with-resource를 적용 가능하도록 하였고, 이를 통해 코드가 유연해지고 누락되는 에러없이 모든 에러를 잡을 수 있게 되었다.
- try-with-resource문을 사용할 때에는 해당 인터페이스를 구현한 클래스(Class명 implements AutoCloseable)를 try() 내에 객체를 생성하면!!! 자동으로 close 메서드가 호출되어 finally에서 close 해주는 과정을 생략해도 된다.

- jdk 7부터는 Closeable 인터페이스가 AutoCloseable 인터페이스를 구현하여, 해당 인터페이스를 구현한 클래스에 한해서는 꼭 close를 안해줘도 되니, 이 점을 유의하며, AutoCloseable 인터페이스 API 문서에서 해당 클래스들을 확인해볼 수 있다.
