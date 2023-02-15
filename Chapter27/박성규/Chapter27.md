# ❓27장 Serializable과 NIO도 살펴 봅시다
   
java.io.Serializable을 import 하는 이유는 생성한 객체를 파일로 저장할 일이 있을수도 있고, 저장한 객체를 읽을 일이 생길수도 있고 객체를 다른서버로 보낼 때도 있고, 다른서버로 보내 생성한 객체를 받을 일도 생길 수 있기 때문에 Serializable 인터페이스를 구현하기 하여 직렬화 역직렬화 하기위해서 이다.<br>
java.io.Serializable의 serialVersionUID 를 지정하는 이유는 객체의 버전을 명시하여 객체가 같은지 다른지 확인할 수 있도록 하기 위해서 이다.<br>
자바에서 객체를 파일로 읽거나 쓸 때 사용하는 Stream 클래스 이름은 FileInputStream FileOutputStream 이다.<br>
transient 예약어의 용도는 직렬화 대상에서 제외 하기 위함이다.<br>
NIO가 생긴 이유는 채널과 버퍼를 사용하여 스트림 기반 I/O의 속도를 개선하기 위해서 이다.<br>
NIO에서 Channel의 용도는 데이터를 중간에 처리하기 위함이다.<br>
NIO에서 Buffer의 용도는 데이터를 담는 역할이다.<br>
NIO에서 Buffer의 상태를 확인하기 위한 메소드들에는 capacity() limit() position() 가 있다.<br>
NIO에서 Buffer의 position을 변경하기 위한 메소드들에는 flip() mark() reset() rewind() remaining() hasRemaining() clear()가 있다.<br>
