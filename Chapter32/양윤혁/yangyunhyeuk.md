# [chapter 32]

> 정리
> 

- 자바 8에서는 추가되거나 변경된 것이 너무 많다. 그 중 중요한 것들은 다음과 같다.
    - 람다 표현식
    - Functional 인터페이스
    - Stream
    - Optional 클래스
        - null 처리를 보다 간편하게 하기 위해 만들어졌다.
        - 자칫 잘못하면 발생할 NPE 문제를 보다 간편하게 처리하기 위해 사용된다.
        
        ```jsx
        public void createOptionalObjects() {
                // 만약 데이터가 없는 Optional 객체 생성
                Optional<String> emptyString = Optional.empty();
                String common = null;
                // 만약 null이 추가될 수 있는 상황
                Optional<String> nullableString = Optional.ofNullable(common);
                common = "common";
                // 반드시 데이터가 들어갈 수 있는 상황 
                Optional<String> commonString = Optional.of(common);
            }
        ```
        
    - 인터페이스의 기본 메서드 (Default Method)
        - 하위호환성때문에 만들어졌다.
        - 키워드 default를 사용하여 생성 가능하다.
    - 날짜 관련 클래스들 추가
        - java.time 패키지 추가
            
            
            | 내용 | 버전 | 패키지 | 설명 |
            | --- | --- | --- | --- |
            | 값 유지 | 예전 버전 | java.util.Date
            java.util.Calander | Date 클래스는 날짜 계산이 불가능하다. 
            Calander 클래스는 불변 객체가 아니라 연산 시 객체 자체가 변경된다. |
            | 값 유지 | 자바 8 | java.time.ZoneDateTime
            java.time.LocalDate | ZoneDateTime과 localDate 등은 불변 객체이다. 
            모든 클래스가 연산용의 메서드를 갖고 있으며, 연산 시 새로운 불변 객체를 돌려준다. 
            Thread Safe하다. |
            | 변경 | 예전 버전 | java.text.SimpleDateFormat | Thread Unsafe하고 느리다. |
            | 변경 | 자바 8 | java.time.format.DateTimeFormatter | Thread Safe하고 빠르다. |
            | 시간대 | 예전 버전 | java.util.TimeZone | “Asian/Seoul”이나 “+09:00”같은 정보를 갖는다.  |
            | 시간대 | 자바 8 | java.time.ZoneId
            java.time.ZoneOffset | ZoneId : “Asian/Seoul”
            ZoneOffset : “+09:00”
            위와 같은 정보를 갖는다. |
            | 속성 관련 | 예전 버전 | java.util.Calander | 해당 클래스 내 속성들은 정수값을 갖는다.  |
            | 속성 관련 | 자바 8 |  | 해당 클래스 내 속성들은 enum 타입을 갖는다.  |
    - 병렬 배열 정렬
        - parallelSort란 정렬 메서드가 제공되며, 자바 7에서 소개된 Fork-Join 프레임웤이 내부적으로 사용된다.
        - 다음과 같이 사용된다.
        
        ```jsx
        int[] intValues = new int[10];
        Arrays.paralleSort(intValues);
        ```
        
        - sort() : 단일 쓰레드로 수행된다.
        - parallelSort() : 필요에 따라 여러 개의 쓰레드로 나뉘어 작업이 수행된다. 그렇기에 더 많은 CPU를 사용하나, 처리 속도는 더 빠르다.
    - String Joiner 추가
      - 그저 순차적으로 나열된 문자열을 예쁘게 처리하기 위한 클래스이다.

      ```jsx
              String[] stringArray = new String[]{"gray", "green", "red", "yellow"};

              // StringJoiner joiner = new StringJoiner(",");
              // 출력 결과
              // gray,green,red,yellow

              // StringJoiner joiner = new StringJoiner(",","(",")");
              // 출력 결과
              // (gray,green,red,yellow)

              for (String string : stringArray) {
                  joiner.add(string);
              }
              System.out.println(joiner);
      ```
