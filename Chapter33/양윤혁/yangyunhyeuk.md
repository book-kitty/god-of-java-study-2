# [chapter 33]

> 정리
> 

- 자바 8에서는 추가되거나 변경된 것이 너무 많다. 그 중 중요한 것들은 다음과 같다.
    - 람다 표현식
        - 기본 람다 표현식은 3 부분으로 구성된다.
            
            
            | 매개변수 목록 | 화살표 토큰 | 처리식 |
            | --- | --- | --- |
            | (int x, int y) | → | x + y |
        - 메서드가 하나만 존재하는 인터페이스는 @FunctionalInterface로 선언할 수 있으며, 이 인터페이스는 람다식으로 표현할 수 있다.
        - (매개 변수 목록) → 처리식으로 람다를 표현하며, 처리식이 한 줄 이상일 때에는 처리식을 중괄호로 묶을 수 있다.
    - Functional 인터페이스
        - 자바 8에서 제공하는 주요 Functional 인터페이스는 java.util.function 패키지에 다음과 같이 있다.
            - Predicate
                - 두개의 객체를 비교할 때 사용하고 boolean을 리턴하는 test 메서드를 필두로 and, negate, or이라는 default 메서드가 구현되어 있으며 isEqual 이란 static 메서드도 존재한다.
            - Supplier
                - 유일하게 get 메서드가 있으며 리턴값으로 generic으로 선언된 타입을 리턴한다.
            - Consumer
                - accept란 매개변수를 하나 갖는 메서드가 존재하며, 리턴값이 없다. 그래서 출력할 때처럼 작업을 수행하고 결과를 받을 일이 없을 때 사용한다. 이외에도 andThen이란 default 메서드가 구현되어 있는데, 순차적인 작업을 할 때 유용하다.
            - Function
                - apply라는 하나의 매개 변수를 갖는 메서드가 있으며, 리턴값도 존재한다. 해당 인터페이스는 Functional<T,R>로 정의되어, 앞에 있는 T는 입력 타입, 뒤에 있는 R은 리턴 타입을 의미한다. 즉, 변환을 할 필요가 있을 때 이 인터페이스를 사용한다.
            - UnaryOperator
                - apply라는 하나의 매개 변수를 갖는 메서드가 있으며 리턴값도 존재한다. 단, 한 가지 타입에 대해 결과도 같은 타입일 경우 사용한다.
            - BinaryOperator
                - apply라는 2개의 매개 변수를 갖는 메서드가 있으며 리턴값도 존재하며 단 한가지 타입에 대해 결과도 같은 타입일 때 사용한다.
    - Stream
        - 자바 8에서는 스트림이 추가되었다.
            - 스트림은 연속된 정보를 처리하는 데 사용한다.
            
            ```jsx
            list.stream().filter(x -> x>10).count();
            ```
            
            - 스트림 생성(stream()) : 컬렉션의 목록을 스트림 객체로 변환한다. 여기서 스트림 객체는 [java.util.stream](http://java.util.stream) 패키지의 Stream 인터페이스를 말한다. 이 stream 메서드는 당연히 Collection 인터페이스에 선언되어 있다.
            - 중개 연산(filter) : 생성된 스트림 객체를 사용하여 중개 연산 부분에서 처리한다. 하지만 이 부분에서는 아무런 결과를 리턴하지 못하기에 중개 연산이라 불리운다.
                - 중개 연산은 있어도, 없어도 상관없다. 0개 이상 존재할 수 있다.
            - 종단 연산(count()) : 마지막으로 중개 연산에서 작업된 내용을 바탕으로 결과를 리턴해준다.
            - stream을 보다 빠르게 처리하려면 parallelStream을 사용하면 되나, 이는 병렬로 처리하기에 CPU도 많이 사용하고 몇 개의 쓰레드로 처리할지 보장이 안되어 일반적 웹 프로그래밍엔 stream을 사용하자
        - 더블 콜론도 자바 8에서 추가되었다.
            - 더블 콜론은 메서드 참조라고도 불리우며 메서드 참조의 종류는 4가지 이다.
                - static 메서드 참조
                - 특정 객체의 인스턴스 메서드 참조
                - 특정 유형의 임의의 객체에 대한 인스턴스 메서드 참조
                - 생성자 참조
            
            ```jsx
            forEach(System.out::println)
            ```
            
        - 중개 연산의 메서드 중 map()은 스트림에서 처리하는 값들을 중간에 변경할 수 있다.
            
            ```jsx
            List<StudentDTO> studentList = new ArrayList<>();
            studentList.add(new StudentDTO("홍길동",11,22,33));
            studentList.add(new StudentDTO("임꺽정",44,55,66));
            studentList.add(new StudentDTO("김철수",77,88,99));
            
            List<String> nameList = studentList.stream()
            			.map(student -> student.getName()).collect(Collectors.toList());
            ```
            
        - 중개 연산의 메서드 중 filter()는 스트림 내에서 필요한 데이터를 걸러서 처리할 때 사용한다.
            
            ```jsx
            studentList.stream()
            		.filter(student -> student.getScore() > scoreCutLine)
            		.forEach(student -> Sout(student.getNaeme()));
            ```
            
        
        ## Stream
        
        - 스트림 생성 -중간 연산 - 종단 연산으로 구분된다.
            - 스트림 생성 시에는 stream 메서드를 호출하면 Stream 타입을 리턴한다.
            - 중간 연산은 데이터를 가공할 때 사용되며 연산 결과로 Stream 타입을 리턴한다. 따라서 여러 개의 중간 연산을 연결할 수 있다.
            - 종단 연산은 스트림 처리를 마무리하기 위해서 사용되며 숫자값을 리턴하거나 목록형 데이터를 리턴한다.
                - 중간 연산
                    - filter()
                    - map() / mapToInt() / mapToLong() / mapToDouble()
                    - flatMap() / flatMapToInt() / flatMapToLong() / flatMapToDouble()
                    - distinct()
                    - sorted()
                    - peek()
                    - limit()
                    - skip()
                - 종단 연산
                    - forEach() / forEachOrdered()
                    - toArray()
                    - reduce()
                    - collect()
                    - min() / max() / count()
                    - anyMatch() / allMatch() / noneMatch()
                    - findFirst() / findAny()
    - Optional 클래스
    - 인터페이스의 기본 메서드 (Default Method)
    - 날짜 관련 클래스들 추가
    - 병렬 배열 정렬
    - String Joiner 추가
