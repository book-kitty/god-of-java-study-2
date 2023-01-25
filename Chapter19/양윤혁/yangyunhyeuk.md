

> 정리
> 

- JDK : Java Development Kit (자바 개발 통합 도구)
- JRE : Java Runtime Environment (자바를 실행할 수 있는 환경의 집합)

- JDK의 경우 자바 프로그램을 개발하고 실행할 수 있는 환경을 제공하는 반면 
JRE의 경우 자바 프로그램을 실행하는 환경만 제공하는 차이를 갖는다.

### 자바의 버전별 차이

- JDK 1.0
    - 가장 최조의 버전이다.

- JDK 1.1
    - AWT의 이벤트 모델의 확장 및 변경
        - AWT(Abstract Window Toolkit)는 자바를 이용하여 UI를 구성할 때 사용되는 기술이다.
    - 내부 클래스 추가
    - JavaBeans, JDBC, RMI 등 추가
        - JavaBeans : 자바에서 제공하는 컴포넌트 모델 중 하나이다.
        - JDBC : 자바에서 DB에 데이터를 담기 위한 API이다.
        - RMI : Remot Method Invocation의 약자로 JVM에 있는 메서드를 호출하는 것이 아니라 원격 JVM에 있는 메서드를 호출하기 위한 기술을 의미한다.

- JDK 1.2
    - strictfp 예약어 추가
    - 자바에서 GUI를 제공하기 위한 swing이 코어 라이브러리에 추가
    - JIT이란 컴파일러가 Sun JVM에 처음 추가
    - 자바 플러그인 추가
    - CORBA란 기술과 데이터를 주고 받기 위한 IDK 추가
    - 컬렉션 프레임워크 추가

- JDK 1.3
    - HotSpot JVM 추가
    - CORBA와의 호환성을 위해 RMI 수정
    - 자바에서 사운드를 처리하기 위한 JavaSound 라이브러리 추가
    - JNDI가 코어 라이브러리에 추가
    - 자바의 디버깅을 보다 쉽게 하기 위한 JPDA 추가
    - Synthetic 프록시 클래스 추가

- JDK 1.4
    - assert 예약어 추가
    - Perl 언어의 정규 표현식을 따르는 정규 표현식 추가
    - IPv6 지원 시작
    - NIO라는 non-blocking 추가
    - 각종 로그를 처리하기 위한 logging API 추가
    - JPEG나 PNG 등의 이미지를 읽고 쓰기 위한 image I/O API 추가
    - 통합 XML 파서와 JAXP라는 XSLT 프로세서 추가
    - JCE, JSSE, JAAS와 같은 통합 보안 및 cryptography extentions 추가
    - Java Web Start 추가
    - 각종 설정 값들을 저장하고 읽는데 사용되는 Preference API(java.util.prefs) 추가

- JDK 1.5
    - 제네릭 추가
    - 어노테이션이라 불리우는 메타데이터 기능 추가
    - autoboxing, unboxing 추가
    - enum 타입 추가
    - 매개 변수의 개수를 가변적으로 선언할 수 있는 varargs 추가
    - static import 추가
    - 향상된 for문 추가
    - 쓰레드 처리를 돕는 concurrent 패키지 추가
    - 스트림이나 버퍼로 들어오는 데이터의 분석을 보다 간편하게 할 수 있는 Scanner 클래스 추가

- JDK 1.6
    - 스크립팅 언어가 JVM 위에서 수행 가능하게 됨
    - 각종 코어 기능의 성능 개선
    - Compiler API가 추가되어 프로그램에서 자바 컴파일러 실행이 가능

- JDK 1.7
    - 제네릭 클래스 초기화 시 “<>”로 타입 인터페이스 지정 가능
    - switch문에서 String 사용 가능

- JDK 1.8
    - 오라클 인수 이후 첫 번째 버전으로 Oracle JDK, Open JDK로 나뉜다.
    - 람다 표현식 사용 가능
    - 람다의 축약형인 특정 메서드만을 호출하는 메서드 레퍼런스 사용 가능
        - System.out::println
    - Optional이라는 구조체에서 Null 처리해주는 ofNullable 메서드를 통해 NPE 처리 용이
    - Clock, ZoneId, LocalDate 등의 날짜, 시간 API 제공
    
    ---
    
    ### JIT 컴파일러
    
    JIT이란 Just In Time의 약자로 “동적 변환”이라는 의미를 갖는다. 
    
    이것을 만든 이유는 프로그램 실행을 보다 빠르게 하기 위해서이다. 
    
    명칭은 컴파일러나, 실행 시에 적용되는 기술이다. 
    
    변환 작업은 인터프리터에 의해서 지속적으로 수행되나, 
    
    필요한 코드의 정보는 캐시에 담아두었다가 재사용한다. 
    
    javac라는 명령어는 자바 파일을 어떤 OS에서라도 수행될 수 있게 
    
    바이트 코드라는 파일로 만드는 것 뿐이며, 
    
    컴퓨터가 알아들을 수 있는 기계어로 바꾸기 위해선 
    
    다시 변환 작업이 필요한데, 이 작업을 JIT 컴파일러에서 한다고 보면 된다. 
    
    - 자바 프로그램이 수행되는 절차는 다음 그림과 같다.
    
    ![Untitled](https://user-images.githubusercontent.com/56379649/214615962-71383c86-a4ce-43cb-9752-52d13d4bda52.png)
    
    ---
    
    JDK 1.3부터 공식적으로 HotSpot JVM이 제공된다. 
    
    자바에서는 “HotSpot 클라이언트 컴파일러”, “HotSpot 서버 컴파일러” 두 가지 컴파일러를 제공한다. 
    
    CPU 코어가 하나 뿐인 사용자를 위해 만들어진것이 HotSpot 클라이언트 컴파일러이다. 
    
    코어가 많은 장비에서 애플리케이션을 돌리기 위해 만들어 진것이 HotSpot 서버 컴파일러이다. 
    
    오라클에서 만든 JVM의 경우 다음의 경우에 해당되면 서버 컴파일러를 선택한다. 
    
    - 2개 이상의 물리적 프로세서
    - 2GB 이상의 물리적 메모리

참고로 Window의 경우 Default로 클라이언트 컴파일러가 사용된다. 

---

일반적으로 사용되는 GC는 가비지 컬렉션을 의미한다.

- 쓰레기를 청소하는 작업이 수행되면 “가비지 컬렉션이 수행되었다.”가 그 예이다.

JVM 내에서 메모리 관리를 해주는 것을 “가비지 컬렉터”라고 부른다. 

java 1.7 버전 부터는 G1이라는 가비지 컬렉터를 제외한 나머지 JVM은 힙 공간에 객체를 관리한다. 

- 자바에서 메모리가 살아가는 과정은 다음과 같다.
    1. Eden 영역에서 객체가 생성된다. 
    2. Eden 영역이 꽉차면 살아있는 개체만 Survivor 영역으로 복사되고, 다시 Eden 영역을 채운다. 
    3. Survivor 영역이 꽉 차게 되면 다른 Survivor 영역으로 객체가 복사된다. 이 때 Eden 영역에 있는 객체들 중 살아있는 객체들도 다른 Survivor 영역으로 간다. 즉, Survivor 영역의 둘 중 하나는 반드시 비어있어야만 한다. 
- 지금까지 설명한 부분은 마이너 GC(영 GC)라고 부르며, 
여기서 GC는 가비지 컬렉터가 아닌 가비지 컬렉션이다.
- 그러다가 오래 살아있는 개체들은 Old 영역으로 이동하다가 Old 영역이 꽉차면 GC가 발생하는데 이것을 메이저 GC(풀 GC)라고 부른다.
- 일반적으로 영 GC가 풀 GC보다 더 작은 공간이 할당되고 객체들을 처리하는 방식도 달라, 영 GC가 더 빠르다.
