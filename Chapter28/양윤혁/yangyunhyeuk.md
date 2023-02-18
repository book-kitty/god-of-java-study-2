

> 정리
> 

### 사용자들이 바로 옆에 있는 장비와 데이터를 주고 받는 작업을 네트워킹이라고 하는데, 이러한 네트워킹은 다음과 같은 레이어로 구분되어 있다. (실제론 이것보다 훨씬 복잡하나, 간소화시켰다.)

![3](https://user-images.githubusercontent.com/56379649/218321985-8ccdc3c9-0335-4d0c-8eb0-cc176b2b22c9.png)

- 만약 자바로 TCP 통신을 하는 경우엔 애플리케이션 레이어에서 프로그래밍만 하면 트랜스포트 레이어에서 처리는 자바에서 다 알아서 처리해준다.

---

### TCP 통신은 가장 대표적인 통신 방법이다.

- TCP 통신은 연결 기반 프로토콜이라고 불리운다.
- 상대방이 데이터를 제대로 전달받았는지 보장할 수 있는 통신 방법이다.
- 허나, UDP(User Datagram Protocol)는 데이터를 제대로 받았는지에 대한 보장을 못받는
- 그럼 왜 신뢰성없는 UDP가 존재하며, 이를 사용하는 것일까
    - TCP 통신은 신뢰성을 보장하다보니, 부분적으로 처리되는 절차가 매우 복잡하게 되어 있어, UDP보다 비싸고 느리다는 특징이 있다.
    - 그리고 이 세상의 모든 데이터는 꼭 전송이 보장되리라는 법이 없기에, 데이터가 유실되도 치명적이지 않은 시스템들에는 TCP가 필수적이기 않다.

---

## 포트

- 포트는 IP 내에 프로세스 구분을 위해 사용하는 번호를 의미한다.
- 포트의 숫자는 IP 주소가 가리키는 PC에 접속할 수 있는 통로(채널)를 의미한다.
- 이미 사용 중인 포트는 중복하여 사용할 수 없다.
- 16비트로 구성된 포트는 65,535까지 사용할 수 있다.
- 0~1023포트는 용도가 정해져있는 포트로 사용하는 것이 제한되어 있다.

---

## Socket

- TCP 통신을 자바에서 수행하려면 Socket 클래스를 사용하면 된다.
    - Socket 클래스는 데이터를 보내는 쪽(클라이언트)에서 객체를 생성하여 사용한다.
    - 데이터를 받는 쪽(서버)에서 클라이언트 요청을 받으면 요청에 대한 Socket 객체를 생성하여 데이터를 처리한다.
    - 즉, Socket 클래스는 서버, 클라이언트 간 원격에 있는 장비와의 연결 상태를 보관하고 있다.
    

---

# TCP 통신 예제

## Server

```jsx
package socket;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.ServerSocket;
import java.net.Socket;

public class SocketServerSample {
    public static void main(String[] args) {
        SocketServerSample sample = new SocketServerSample();
        sample.startServer();
    }

    public void startServer() {
        ServerSocket server = null;
        Socket client = null;

        try {
            // 포트번호 9999로 서버 소켓 객체 생성
            server = new ServerSocket(9999);

            while (true) {
                System.out.println("Server:Waiting for Request");

                // 다른 원격 호출을 대기하는 상태,
                // 연결이 완료되면 소켓 객체를 리턴하여 client 변수에 담긴다.
                client = server.accept();
                System.out.println("Server:accept");

                // 데이터를 받기 위해 해당 메서드를 호출하여 데이터 저장
                InputStream stream = client.getInputStream();
                BufferedReader in = new BufferedReader(new InputStreamReader(stream));
                String data = null;
                StringBuilder receivedData = new StringBuilder();
                while ((data = in.readLine()) != null) {
                    receivedData.append(data);
                }
                System.out.println("Received Data : " + receivedData);
                in.close();
                stream.close();
                client.close();

                // 소켓 통신을 통해 넘어오는 데이터가 EXIT이면 더 이상 대기하지 않고 프로그램 종료
                if (receivedData != null && "EXIT".equals(receivedData.toString())) {
                    System.out.println("STOP Socket Server");
                    break;
                }
                System.out.println("=======================");
            }

        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (server != null) {
                try {

                    // 모든 데이터 처리가 끝난 후 소켓 사용 종료
                    server.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }

}
```

## Client

```jsx
package socket;

import java.io.BufferedOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.net.Socket;
import java.util.Date;

public class SocketClientSample {
    public static void main(String[] args) {
        SocketClientSample sample = new SocketClientSample();
        sample.sendSocketSample();
    }

    public void sendSocketSample() {
        for (int loop = 0; loop < 3; loop++) {
            sendSocketData("I liked Java at " + new Date());
        }
    }

    public void sendSocketData(String data) {
        Socket socket = null;

        try {
            System.out.println("Client : connecting");

            // 서버 쪽에서 지정한 포트넘버와 싱크를 맞춰준다.
            socket = new Socket("127.0.0.1", 9999);
            System.out.println("Client:Connect status : " + socket.isConnected());

            Thread.sleep(1000);

            // 데이터를 서버에 전달하기 위해 객체 생성
            OutputStream stream = socket.getOutputStream();
            BufferedOutputStream out = new BufferedOutputStream(stream);

            byte[] bytes = data.getBytes();
            out.write(bytes);
            System.out.println("Client : Sent data" + out);
            out.close();

        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        } finally {
            if (socket != null) {
                try {
                    // 데이터를 전달한 후 소켓 연결을 닫는다.
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }
}
```

---

# UDP 통신 예제

## Server

```jsx
package socket;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.SocketException;

public class DatagramServerSample {
    public static void main(String[] args) {

        DatagramServerSample sample = new DatagramServerSample();
        sample.startServer();
    }

    public void startServer() {
        DatagramSocket server = null;

        try {
            // 데이터그램 소켓 객체를 port 넘버 지정 후 생성
            server = new DatagramSocket(9999);

            int bufferLength = 256;
            byte[] buffer = new byte[bufferLength];

            // 데이터를 받기 위한 패킷 객체를 byte 배열과 크기로 지정하여 생성
            DatagramPacket packet = new DatagramPacket(buffer, bufferLength);
            while (true) {
                System.out.println("Server:Waiting for Request");

                // 데이터를 받기 위해 대기하다가, 데이터가 넘어오면 패킷 객체에 데이터를 담는다.
                server.receive(packet);

                // 전송받은 데이터 크기 확인
                int dataLength = packet.getLength();
                System.out.println("Server Received : " + dataLength);

                // byte 배열로 되어 있는 데이터를 String 문자열로 변경
                String data = new String(packet.getData(), 0, dataLength);
                System.out.println("Received data : " + data);

                if (data.equals("EXIT")) {
                    System.out.println("Stop DatagramServer");
                    break;
                }
                System.out.println("======================");
            }
        } catch (SocketException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (server != null) {
                // 모든 처리가 끝나면 소켓 객체 종료
                server.close();
            }
        }

    }
}
```

## Client

```jsx
package socket;

import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;

public class DatagramClientSample {
    public static void main(String[] args) {
        DatagramClientSample sample = new DatagramClientSample();
        sample.sendDatagramSample();
    }

    public void sendDatagramSample() {
        for (int loop = 0; loop < 3; loop++) {
            sendDatagramData("");
        }
    }

    public void sendDatagramData(String data) {
        try {
            // 매개 변수없이 객체 생성 가능
            DatagramSocket client = new DatagramSocket();

            // 데이터를 받을 서버의 IP 설정
            InetAddress address = InetAddress.getByName("127.0.0.1");
            byte[] buffer = data.getBytes();

            // 전송하기 위한 DatagramPacket 패킷 생성
            DatagramPacket packet = new DatagramPacket(buffer, 0, buffer.length, address, 9999);

            // 데이터 전송
            client.send(packet);
            System.out.println("client sent data");

            // 소켓 연결 종료
            client.close();
            Thread.sleep(1000);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

---

- UDP
    - 서버에서 데이터를 받을 준비가 되어 있지 않더라도 클라이언트 측에서 아무런 오류를 내지 않고 그냥 수행된다. (비신뢰성)
- TCP
    - 서버에 접속하지 못할 경우 다음과 같은 에러를 발생시킨다. (신뢰성)
        - java.net.ConnectException: Connection refused: connect
