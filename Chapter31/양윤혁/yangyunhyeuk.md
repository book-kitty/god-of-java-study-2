# [chapter 31]

> 정리
> 

## 자바 7에서 추가된 것은?

- jdk 7에서 추가된 클래스 중 Fork/Join 과 관련된 클래스가 있다.
    - Fork : 작업을 여러 개로 나눔을 의미
    - Join : 여러 개로 나눠 작업한 결과를 모음을 의미
- 허나 jdk 7에서 추가된 Fork/Join 작업은 Work Stealing이란 개념이 포함되어 있다.
    - Work Stealing : 작업을 위해 대기하고 있는 상태의, 할 일이 없는 Dequeue가 바쁜 Dequeue에 대기하고 있는 일을 가져가서 해주는 것을 의미한다.
- Fork/Join의 경우 CPU가 많이 있는 장비에서 계산 위주의 작업을 빠르게 해야 하는 경우에 매우 유용하게 사용되곤 한다.

```jsx
package forkJoin;

import java.util.concurrent.RecursiveTask;

public class GetSum extends RecursiveTask<Long> {
    long from, to;

    public GetSum(long from, long to) {
        this.from = from;
        this.to = to;
    }

    @Override
    protected Long compute() {
        // 작업의 단위가 충분히 작을 경우를 확인하는 값을 찾기 위한 세팅
        long gap = to - from;

        try {
            Thread.sleep(1000);
        } catch (Exception e) {
            e.printStackTrace();
        }

        log("From" + from + " To=" + to);

        // 작은 작업의 단위일 경우 다음 로직 수행
        if (gap <= 3) {
            long tempSum = 0;

            for (long loop = from; loop <= to; loop++) {
                tempSum += loop;
            }
            log("Return !!" + from + "~" + to + "=" + tempSum);
            return tempSum;
        }

        // 작업을 반으로 쪼개어 2개의 작업으로 나눠 수행
        long middle = (from + to) / 2;
        GetSum sumPre = new GetSum(from, middle);
        log("Pre     From=" + from + "   TO" + middle);
        sumPre.fork();
        GetSum sumPost = new GetSum(middle + 1, to);
        log("Post     From=" + (middle + 1) + "   TO" + to);
        return sumPost.compute() + sumPre.join();

    }

    public void log(String message) {
        String threadName = Thread.currentThread().getName();
        System.out.println("[" + threadName + "]" + message);
    }
}
```

```jsx
package forkJoin;

import java.util.concurrent.ForkJoinPool;

public class ForkJoinSample {

    static final ForkJoinPool mainPool = new ForkJoinPool();

    public static void main(String[] args) {
        ForkJoinSample sample = new ForkJoinSample();
        sample.calculate();
    }

    public void calculate() {
        long from = 0;
        long to = 10;

        GetSum sum = new GetSum(from, to);
        Long result = mainPool.invoke(sum);
        System.out.println("Fork Join : Total sum of " + from + "~" + to + "=" + result);
    }
}
```

---

- 자바의 NIO는 New I/O의 약자로 JDK 1.4부터 제공되었다.
    - NIO는 보다 빠르게 읽고 쓰는데 주안점을 두고 각종 API를 제공한다.
    - 어떻게 보면 NIO2는 NIO와 이름만 비슷하나, NIO2에서는 [java.io](http://java.io) 패키지의 File 클래스에 미흡한 부분을 보완하는 내용이 매우 많이 포함되어 있다.

- JDK 6까지 사용된 File 클래스의 단점
    - 심볼릭 링크, 속성, 파일의 권한 등에 대한 기능이 없다.
    - 파일을 삭제하는 delete 메서드는 실패 시 아무런 예외가 없고 boolean 타입의 결과만 제공해준다.
    - 파일이 변경되었는지 확인하는 방법은 lastModified 메서드에서 제공해주는 long 타입의 결과로 이전 시간과 비교하는 수 밖에 없었으며 해당 메서드가 호출되면 연계되어 호출되는 클래스가 다수 존재하여 성능 상 이슈가 존재

- NIO2에서 File 클래스를 대체하는 클래스들을 알아보자
    - Paths
        - 해당 클래스에서 제공하는 static한 get 메서드는 Path라는 인터페이스 객체를 얻을 수 있는데, 이 때 파일과 경로에 대한 정보를 확인할 수 있다.
    - Files
        - 기존 File 클래스에서 제공되던 클래스의 단점들을 보완한 클래스이다.
        - 매우 많은 메서드들을 제공하며 Path 객체를 사용하여 파일을 통제하는데 유용하게 사용된다.
    - FileSystems
        - 현재 사용 중인 파일 시스템에 대한 정보를 처리하는 데 필요한 메서드를 제공한다.
        - Paths와 마찬가지로 해당 클래스에서 제공되는 static한 getDefault 메서드를 사용하면 현재 사용 중인 기본 파일 시스템에 대한 정보를 갖는 FileSystem이라는 인터페이스의 객체를 얻을 수 있다.
    - FileStore
        - 파일을 저장하는 디바이스, 파티션, 볼륨 등에 대한 정보들을 확인하는 데 필요한 메서드를 제공한다.
        

---

- Files 클래스는 기존 File 클래스에서 제공되는 기능보다 더 많은 기능을 제공한다.
    - 복사 및 이동
        - copy(), move()
    - 파일, 디렉토리 등 생성
        - createDirectories(), createDirectory(), createFile(), createLink(), createSymbolicLink(), createTempDirectory(), createTempFile()
    - 삭제
        - delete(), deleteIfExists()
    - 읽기와 쓰기
        - readAllBytes(), readAllLines(), readAttributes(), readSymbolicLink(), write()
            - readAllLines() 메서드는 List<String>으로 받는다.
    - Stream 및 객체 생성
        - newBufferdReader(), newBufferdWriter(), newByteChannel, newDirectoryStream(), newInputStream(), newOutputStream()
    - 각종 확인
        - get으로 시작하는 메서드와 is로 시작하는 메서드들로 파일의 상태를 확인
        

---

- 파일이 변경되었는지 확인하는 WatchService 클래스도 추가되었다.
    - File 클래스에서 제공하는 lastModified 메서드를 통해 파일이 수정된 시간을 비교하는 방법이 있었으나, 해당 메서드를 주기적으로 호출해야하는 단점과 함께 내부적으로 호출되는 연계 메서드가 많아 성능적으로 비효율적이다.
    - 이러한 단점을 보완하기 위해서 자바 7부터는 WatchService 인터페이스를 제공한다.
        - 해당 인터페이스는 문지기로, 누군가 해당 디렉터리에 파일을 생성, 수정, 삭제 작업 시 주인에게 연락을 해준다. 이는 주기적으로 순찰을 돌 필요가 없이, 문제가 발생했을 시에만 알려준다는 의미이다.
        

---

- 이외에도 파일과 관련된 다른 새로운 API가 존재한다.
    - SeekableByteChannel
        - 바이트 기반의 채널을 처리하는데 사용된다.
        - 현재의 위치를 관리하고 해당 위치가 변경되는 것을 허용하도록 되어 있어, 채널을 보다 유연하게 처리하는데에 사용된다.
    - NetworkChannel 및 MulticastChannel
        - NetworkChannel : 네트워크 소켓을 처리하기 위한 채널로 네트워크 연결에 대한 바인딩, 소켓 옵션을 세팅하고 로컬 주소를 알려주는 인터페이스
        - MulticastChannel : IP 멀티캐스트를 지원하는 네트워크 채널이다. 여기서 멀티캐스트란 네트워크 주소인 IP를 그룹으로 묶고 그 그룹에 데이터를 전송하는 방식을 의미한다.
    - Asynchronous I/O
        - 비동기 처리를 의미하며 AJAX도 여기에 속한다.
        

---

- Fork/Join 이외에도 추가 및 변경된 사항
    - JDBC 4.1
        - 대표적으로 RowSetFactory와 RowSetProvider 클래스가 추가되었다.
            - jdk 1.4부터 추가된 RowSet 인터페이스를 해당 클래스를 통해 아주 쉽게 객체를 생성할 수 있다.
    - TransferQueue 추가
        - 메시지를 처리할 때 유용하게 사용할 수 있다.
        - Producer/Consumer 패턴은 특정 타입의 객체를 처리하는 쓰레드풀을 미리 만들어놓고 해당 풀이 객체들을 받으면 처리하도록 하는 구조를 의미하는데
        - 이 기능을 보다 일반화하여 SynchronousQueue의 기능을 인터페이스로 끌어올리며 좀더 일반화해서 BlockingQueue를 확장한 것이다.
    - Objects 클래스 추가
        - compare, equals, hash, hashCode, toString 등의 static한 메서드를 제공한다.
        - 해당 클래스는 매개 변수로 넘어오는 객체가 null이여도 예외를 발생시키지 않는 것이 특징이다.
