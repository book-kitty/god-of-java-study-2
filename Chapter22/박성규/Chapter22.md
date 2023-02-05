# ❓22 java.lang 다음으로 많이쓰이는 컬렉션 - Part1 (List)
   
Collection 인터페이스를 구현하는 대표적인 3개의 자료구조에는 List , Set , Queue 가 있다.<br>
배열과 같이 순서가 있는 목록형을 나타내는 대표 인터페이스는 List이다.<br>
ArrayList라는 클래스의 생성자 중 매개변수가 없는 기본 생성자를 사용하면 기본적으로 10 개의 저장공간을 가진다.<br>
만약 ArrayList 클래스의 저장 공간 개수를 처음부터 지정하려면 어떤 생성자를 사용하면 되나요? ArrayList(int 공간개수);<br>
ArrayList 객체를 생성할 때 제네릭을 사용하는 이유는 컴파일 시 타입을 잘못 지정한 부분을 거럴낼 수 있기 때문이다.<br>
ArrayList에 데이터를 담는 메소드 두가지의 이름은 add(), addAll()이다.<br>
Collection 인터페이스를 구현한 클래스의 객체에서 사용할 수 있는 for 루프의 구조는 아래와 같다. <br>
List<String> list = new ArrayList<>(); for(String data:list) { System.out.println(data); }<br>
Collection 인터페이스를 구현한 클래스의 객체에 저장된 데이터의 갯수를 확인하는 메소드 이름은 size() 이다.<br>
ArrayList에서 특정 위치에 있는 데이터를 확인하는 메소드는 get()이다.<br>
ArrayList에서 특정 위치에 있는 데이터를 삭제하는 메소드는 remove()이다.<br>
java.util 패키지에 있는 Stack 이라는 클래스는 List 인터페이스를 구현하고 Vector 클래스를 상속한다.<br>
Stack 클래스에서 데이터를 담는 메소드는 push()이다.<br>
