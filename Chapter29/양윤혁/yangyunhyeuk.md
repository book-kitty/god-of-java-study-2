

> 정리
> 

> 타입과 관련된 예약어
> 

| 타입 | 설명 |
| --- | --- |
| byte | 8비트 정수형 |
| short | 16비트 정수형 |
| int | 32비트 정수형 |
| long | 64비트 정수형 |
| float | 32비트 소수형 |
| double | 64비트 소수형 |
| char | 0~65,535 범위의 정수형 |
| boolean | 참, 거짓 타입 |

> 클래스, 메서드, 변수 선언, 객체 생성과 관련된 예약어
> 

| 타입 | 설명 |
| --- | --- |
| package | 클래스의 패키지를 선언할 때 사용 |
| import | 다른 패키지에 있는 클래스, 요소들 사용 |
| interface | 인터페이스 선언 |
| abstract | 추상 클래스 선언 |
| class | 클래스 선언 |
| enum | enum 선언 |
| implements | 인터페이스 구현 시 사용 가능 |
| extends | 클래스 확장 시 사용 가능 |
| private | 같은 클래스 내 접근 가능 |
| protected | 같은 패키지 내, 상속받은 경우 접근 가능 |
| public | 누구나 접근 가능 |
| final | 변수에 사용 시 : 값 불변
클래스에 사용 시 : 확장 불가 |
| synchronized | 동시 접근 제어자 |
| void | 메서드 반환값이 없음을 선언 |
| static | 하나의 인스턴스만 허용하고자 할 때 사용 |
| return | 메서드를 종료하고 값을 반환할 때 사용 |
| assert | 검증을 위한 로직 선언 |
| native | 다른 언어로 구현된 것을 선언 |
| new | 새로운 객체를 생성 |
| null | 참조되고 있는 객체가 없다는 것을 선언 |
| strictfp | strict 소수값 제어자 |
| super | 상위 클래스 참조 |
| this | 현재 객체에 대한 참조를 명시적으로 나타낼 때 사용 |
| transient | Serializable 할 때 저장되거나 전송되지 않는 객체를 선언 |
| volatile | 하나의 변수를 여러 쓰레드가 참조할 때 모두 동일한 값을 바라보도록 할 때 사용 |
| instanceof | 객체의 타입을 확인할 때 사용 |
|  |  |

> 조건 및 반복문과 관련 있는 예약어
> 

| 타입 | 설명 |
| --- | --- |
| if | 데이터 조건 확인 시 사용, if 문은 참, 거짓을 제어하는 boolean 타입 |
| else | if 조건 외 해당될 때 사용 |
| switch | 정수형 및 문자열(자바7 이후)의 값에 따른 분기에 사용 |
| case | switch 문 내 변수값에 따른 작업을 선언 |
| default | switch 문 내 case 조건에 부합되는 값이 없을 때 사용 |
| for | 조건에 따른 반복을 변수에 따라 제어할 때 사용 |
| do | 한 번은 최소 수행하고자 할 때 사용 |
| while | 조건에 따른 반복만 수행하고자 할 때 사용 |
| continue | 반복 작업 시 조건 확인문으로 이동 시 사용 |
| break | 반복 작업 종료 시 사용 |

> 예외 처리와 관련된 예약어
> 

| 타입 | 설명 |
| --- | --- |
| try | 예외 발생 가능한 코드 범위 선언 |
| catch | try 문으로 묶은 범위 내 예외 발생 시 처리 방법 선언 |
| finally | try-catch 수행 후 반드시 실행해야 하는 작업 선언 |
| throw | 예외를 발생시키거나 호출한 클래스로 넘길 때 사용 |
| throws | 예외를 던질 수도 있다는 것을 선언할 때 사용 |

---

## 제네릭

- 형 변환 시에 발생할 수 있는 문제들을 사전에 없애기 위한 것
- 컴파일 시점에 발생할 수 있는 문제들을 발견

- 제네릭 타입 이름 명명 규칙
    - E : 요소, 자바 컬렉션에서 주로 사용
    - K : 키
    - V : 값
    - N : 숫자
    - T : 타입
    - S,U,V : 두 번째, 세 번째, 네 번째에 선언되는 타입

- wildcard 타입
    - 메서드 선언 시 제네릭 타입 제한을 해소하기 위해 사용 “<?>”
    - 해당 타입을 정확히 모르기에 Object로 받는다.

---

## 쓰레드

- Runnable 인터페이스나 Thread 클래스를 직/간접적으로 구현한 클래스만 쓰레드로 처리 가능
- 쓰레드 선언 시 public void run() 메서드를 필수로 선언
- 쓰레드 시작을 위해 쓰레드 객체의 start() 메서드를 호출하면 선언되어 있는 run() 메서드 실행
- Daemon으로 선언된 쓰레드는 다른 쓰레드가 종료될 시 자동 종료
- 쓰레드를 실행한 메서드에서 쓰레드가 종료될 때까지 대기하려면 join() 메서드를 사용
- wait() : 쓰레드 대기상태, notify(), notifyAll() : 쓰레드 깨움
- 수행 중인 쓰레드 종료를 위해선 interrupt() 사용
    - join(), sleep(), wait() 메서드 호출된 상태서 종료됨
- synchronized
    - 해당 예약어는 하나의 쓰레드만 해당 메서드를 수행할 수 있어, thread safe
    - synchronized 블록 생성 시 동일한 객체를 공유하는 블록은 하나의 쓰레드에서만 수행 가능
    

---

## 자바의 자료구조와 Collection

- [Collection] 순서가 있는 List
    - 각 데이터에 대한 위치가 있다.
    - 위치에 있는 데이터를 꺼내거나 지우고, 원하는 위치에 데이터를 저장하는 작업 가능
    - 특정 데이터의 중복을 허용한다.
- [Collection] 순서가 중요하지 않은 Set
    - 데이터를 목록 형태로 담아둔다.
    - 데이터의 위치는 정해져 있지 않으며, 중복된 데이터는 허용치 않는다.
    - contains() 메서드를 통해 데이터 포함 여부 확인에 유용하다.
- [Collection] 먼저 들어온 값이 먼저 나가는 Queue
    - 데이터가 들어온 순서대로 빠르게 처리할 때 유용하다.
- 키-값 형태의 Map
    - key는 중복을 허용치 않으나, value는 상관없다.
    - 부모 interface가 존재하지 않는다.

- [Collection]
    - List, Set, Queue 타입 구현의 모체가 되는 인터페이스
    - Iterable 인터페이스 확장
    - 데이터를 담는 add(), addAll() 메서드 존재
    - 데이터를 확인하는 contains(), containsAll(), isEmpty(), equals(), size() 메서드 존재
    - 데이터를 삭제하는 clear(), remove(), removeAll() 메서드 존재
    

---

## IO 관련 클래스

- IO : 파일이나 네트워크로 데이터를 읽고 쓰는 것을 칭한다.

- IO의 기본은 Stream
    - 자바 프로그램에서 데이터를 읽을 때에는 InputStream을 사용한다.
    - 자바 프로그램에서 밖으로 데이터를 쓸 때에는 OutputStream을 사용한다.
    - char 기반의 데이터 처리 시, Reader, Writer를 사용한다.

- InputStream, Reader
    - 주요 메서드
        - read() : 스트림 내용 읽기
        - close() : 스트림 닫기
    - InputStream의 주요 자식 클래스
        - FileInputStream : 바이트 기반의 파일을 읽을 때 사용
        - ObjectInputStream : 저장되어 있는 객체를 읽을 때 사용
        - FilterInputStream : 기타 여러 형태의 스트림을 처리하는 클래스의 부모가 되는 클래스

- OutputStream, Writer
    - 주요 메서드
        - write() : 스트림에 내용 쓰기
        - flush() : 강제로 쓰기
        - close() : 스트림 닫기
    - OutputStream의 주요 자식 클래스
        - FileOutputStream : 바이트 기반의 파일을 쓸 때 사용
        - ObjectOutputStream : 저장되어 있는 객체를 쓸 때 사용
        - FilterOutputStream : 기타 여러 형태의 스트림을 처리하는 클래스의 부모가 되는 클래스
        

- File 클래스
    - 파일 및 경로를 관리하는 클래스
    - 기본 기능
        - exist() : 존재 여부 확인
        - isFile(), isDirectory() : 파일인지 경로인지 확인
        - isHidden() : 숨겨진 파일 및 경로 확인
        - lastModified() : 마지막 수정 시간 확인
        - delete() : 파일 및 경로 삭제
    - 파일인 경우
        - renameTo() : 파일 이름 변경
        - createNewFile() : 파일 생성
        - canRead(), canWrite(), canExecute():  읽기, 쓰기, 실행 가능 여부 확인
    - 경로인 경우
        - list(), listFiles() : 파일 목록 확인
        - mkdir(), mkdirs() : 경로 생성

- Serializable
    - 객체를 다른 서버로 전송하거나, 파일에 쓰고 읽기 위해 사용하는 인터페이스
    - static final long serialVersionUID : 객체에 대한 serial 버전 값 지정

- transient
    - Serializable로 선언한 객체 내에 전송하거나 저장하지 않은 변수를 선언할 때 사용
    - 변수 선언 시 해당 예약어 지정

- NIO
    - 보다 빠른 IO 처리를 위해 추가된 패키지
    - Channel, Buffer 기반으로 데이터 처리

---

## 네트워크 관련 클래스

- TCP 처리를 위한 Socket
    - Socket 클래스는 데이터를 전달하고 받기 위해 사용하는 클래스
    - ServerSocket 클래스를 통해 데이터를 수신하며, Socket 객체를 통해 데이터를 받아 처리한다.
    - 서버 시작 여부 및 데이터 송수신 가능 여부를 판단하여 처리하는 신뢰성 통신이다.
    
- UDP 처리를 위한 Datagram
    - DatagramPacket 클래스를 데이터를 전달하고 받기 위해 사용하는 클래스
    - DatagramSocket 클래스는 데이터 수신 시 사용하는 클래스로, 데이터를 받아서 처리하는 클래스는 DatagramPacket이다.
    - 서버 시작 여부 및 데이터 송수신 가능 여부와 상관없이 데이터를 전송하는 비신뢰성 통신이다.
