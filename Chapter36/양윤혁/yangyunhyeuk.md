
> 정리

# 자바 언어와 관련하여 알아두어야 할 것

## Group 1

- 알고리즘
- 멀티스레드 관련 패턴들
- 자바 NIO 및 네트워킹에 대한 자세한 내용
- 자바 메모리 관리와 GC
- 리팩토링
    - 메서드 하나의 최대 크기는 65Kbyes
- 이클립스나 인텔리제이 같은 IDE 사용법
- 적어도 한 가지 이상의 방법론
- 자바 기반의 UI 기술
- UML과 같은 모델링 언어

## Group 2

- XML 및 JSON
    - 대부분 WAS나 프레임워크에서 사용하는 설정은 XML 파일이나, 키-값 쌍으로 이뤄진 properties 파일로 이뤄진다.
- JSP, Servlet에 대한 보다 자세한 내용
- JDBC에 대한 자세한 내용
- J2EE 디자인 패턴
- Spring 프레임워크를 비롯한 각종 프레임워크
- JUnit 테스트 스크립트 작성 방법과 사용법
- Subversion, CVS 등 형상관리 툴 사용법
- Ant, Maven과 같은 통합 빌드 툴 사용법
- Jenkins와 같은 통합 빌드 툴 사용법
- Apache와 같은 오픈 소스 프로젝트에 대한 지속적인 관심
- DBMS
- NoSQL DB 및 Cache
- ElasticSearch와 같은 검색 서버

## Group 3

- Python과 같은 스크립팅 언어
- Scala와 같은 JVM 위에 사용할 수 있는 스크립팅 언어
- 모바일 앱 개발
- 성능
- 테스트
- OS
- TCP/IP 개념과 네트워크
- 시스템 구성 방법

---


# [부록 Part 2]

# 6. jar

- jar 명령은 여러 개의 클래스 파일을 하나의 파일로 묶기 위해서 사용한다.
- 주요 옵션은 다음과 같다.
    - -c : jar 만들기
    - -u : jar 수정하기
    - -x : jar 풀기
    - -t : jar 내의 파일 목록 확인하기
- 그리고 이 옵션들에 붙여, 사용할 수 있는 다음의 옵션도 있다.
    - 다음의 옵션 중 -f 옵션을 통해 파일 명을 지정하지 않으면 파일을 처리할 수 있음을 숙지해야 한다.
    - -f : 파일명 지정
    - -v : verdose 로그 출력
    - -m : manifest 파일 지정 (manifest 파일이란 jar 파일의 각종 속성이 정의되어 있는 MANIFEST.MF라는 파일의 위치를 의미한다.)

# 7. classpath와 자바 옵션들

- 클래스 패스에 디렉터리만 지정해준다면 해당 디렉터리가 프로그램을 실행하는 기본 위치가 된다.
- - classpath 옵션은 줄여서 cp라고도 한다.
    
    ```jsx
    $ java -classpath c:/godofjava Calculator
    $ java -cp c:/godofjava Calculator
    ```
    
- 만약 여러 개의 jar 파일이나 경로를 클래스패스에 지정할 때에는 구분자를 주어 경로를 나열해준다.
    - 윈도우의 경우 세미콜론을, 기타 다른 유닉스 계열의 os에서는 콜론을 사용한다.
    - 또한 여러 개의 jar 파일이 하나의 디렉토리에 존재할 경우 와일드카드 문자를 사용해도 좋다.
    - 허나 클래스패스 경로 사이에는 공백을 두어서는 안된다.
- 일일이 클래스패스를 지정하는 방법도 있으나, 이 외에 환경변수를 지정하는 방법도 있다.
- 옵션 설정하기에 따라, JVM 시작 크기 및 최대 크기를 지정할 수 있으며 쓰레드의 스택 크기 또한 지정할 수 있다.

# 8. javadoc

- 코드 작성 시 주석을 달면, 주석 내에 있는 내용들을 api로 자동 생성해주는 프로그램이 javadoc이다.
- 해당 프로그램은 jdk/bin 디렉토리에 있다.
- 한 줄 주석(//), 블록 주석(/* */)은 javadoc으로 실행해도 api 문서에 추가되지 않는다.
- javadoc을 위한 주석은 /**로 시작하고 */로 끝나야만 한다.
- javaDoc 주석은 다음의 항목에 지정 가능하다.
    - 패키지
    - 클래스 및 인터페이스
    - 필드 (인스턴스 및 클래스 변수)
    - 생성자 및 메서드
- 다음의 규칙을 따른다.
    - 선언된 대상의 바로 윗줄에 있어야 한다.
        - import문 위에선 인식되지 않는다.
    - 선언된 대상에 대한 설명은 가장 처음에 있어야 한다.
    - 만약 한 줄에 설명과 tag section까지 추가하려면 중괄호로 tag section을 묶어줘야 한다.
    - 일부 특수 기호는 변환해서 써야한다.
        - & → &amp;
    - javaDoc의 둘째줄부터 맨 앞에 있는 *는 무시된다.
    - 가장 첫 문장은 Summary에 표시된다.
    - 헤더 태그는 지양해야 한다.

# 9. Formatter는 알아두면 매우 유용

- Formatting
    - 데이터의 가독성을 높여 빠르게 이해할 수 있게 돕는 기능
- 자바에서 제공하는 Formatting 종류
    - 숫자 및 통화
        - NumberFormat 클래스
            - getInstance()
                - 현재 jvm의 기본 지역으로 일반적인 목적의 숫자 format 제공
            - getInstance(Locale inLocale)
                - 매개 변수로 제공된 지역으로 숫자 format 제공
            - getCurrencyInstance()
                - 현재 jvm의 기본 지역으로 통화 foramt 제공
            - getCurrencyInstance(Locale inLocale)
                - 매개 변수로 제공된 지역으로 통화 format 제공
            - getIntegerInstance()
                - 현재 jvm의 기본 지역으로 정수 format 제공
            - getIntegerInstance(Locale inLocale)
                - 매개 변수로 제공된 지역으로 정수 format 제공
        - DecimalFormat 클래스를 통해 좀 더 세밀한 숫자 표현이 가능하다.
    - 날짜와 시간
        - DateFormat 클래스
            - getInstance()
                - 날짜와 시간을 현재 jvm의 기본 지역 및 짧은 형식으로 생성하는 format 제공
            - getDateInstance()
                - 날짜를 기본 지역 및 기본 형식으로 생성하는 format 제공
            - getDateInstance(int style)
                - 날짜를 기본 지역 및 style에 지정된 형식으로 생성하는 format 제공
            - getDateInstance(int style, Locale aLocale)
                - 날짜를 aLocale에 지정된 지역 및 style에 지정된 형식으로 format 제공
            - getTimeInstance()
            - getTimeInstance(int style)
            - getTimeInstance(int style, Locale aLocale)
            - getDateTimeInstance()
            - getDateTimeInstance(int dateStyle, int timeStyle)
            - getDateTimeInstance(int dateStyle, int timeStyle, Locale aLocale)
    - 문자열
        - Formatter의 가장 기본적인 사용은 다음과 같다.
            - Formatter 클래스를 사용하여 문자열 생성
            - String 클래스의 format() 메서드를 사용
        - Formatter의 매개 변수 선정에는 3가지 방식이 존재한다.
            1. 절대적인 위치 사용
                1. 매개 변수의 절대적인 위치를 사용하며 그 위치는 1부터 시작한다. 0부터 시작하는 것이 아니다. 
            2. 상대적인 위치 사용
                1. 매개 변수의 상대적인 위치를 사용하며 앞에서 사용한 위치를 재활용한다는 의미로 ‘<’를 사용한다. 
            3. 순서에 따른 위치 사용
                1. 매개 변수의 나열된 순서를 별도의 위치를 지정하지 않고 사용한다. 

# 10. Collections 다음으로 많이 쓰이는 자바 유틸

- java.util의 유용한 클래스
    - Date, Calendar
        - Date 클래스는 자바 1.0때부터 존재했으나, Calendar 클래스는 자바 1.1버전부터 등장하였다.
    - Collections
        - 기본적으로 대부분의 Collections 클래스들은 쓰레드에 안전하게 구현되어 있지 않은데, synchronized로 시작하는 메서드를 사용하면 쓰레드에 안전한 클래스가 된다.
    - Arrays
        - 배열을 쉽게 처리할 수 있도록 도우는 클래스이다.
    - StringTokenizer
        - 어떤 문자열이 일정한 기호로 분리되어 있을 때 적합한 클래스이다.
    - Properties
        - 속성 파일의 설정을 관리하는 클래스
    - Random
        - 난수 생성을 위한 클래스이다.
    - Formatter

# 11. 자바의 ThreadLocal

- ThreadLocal에 저장된 값은 해당 쓰레드에서 고유하게 사용할 수 있다.
- ThreadLocal 클래스 변수는 private static final로 선언한다.
- ThreadLocal 클래스에 선언되어 있는 메서드는 set, get, remove, initalValue가 있다.
- 사용이 끝난 후에는 remove() 메서드를 호출해주는 습관을 가져야만 한다.

# 12. 자바의 volatile

- 해당 예약어는 변수 선언 시에만 사용된다.
- 쓰레드에 선언된 인스턴스 변수를 선언할 일이 있을 때, 이처럼 valatile 로 선언하면 해당 변수 값이 바뀌면 같은 객체에 있는 변수는 모든 쓰레드가 같은 값을 바라보게 된다.
