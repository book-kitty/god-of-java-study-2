# ❓33장 그럼 데이터를 저장하려면 어떻게 해야 하는데요?
JDBC<br>
Java Database Connectivity<br>
자바언어와 DB를 연결해주는 통로와 같은 것.<br>
자바를 이용한 DB접속과 SQL문장의 실행, 그리고 실행 결과로 얻어진 데이터의 핸들링을 제공하는 방법과 절차에 관한 규약.<br>
자바 프로그램내에서 SQL문을 실행하기 위한 자바 API.<br>
SQL과 프로그래밍 언어의 통합 접근 중 한 형태<br>

Statement<br>
쿼리문을 수행할 때마다 SQL 실행단계 1~3 단계를 거침<br>
SQL 문을 수행하는 과정에서 매번 컴파일을 하기 때문에 성능상 이슈 발생<br>
실행되는 SQL문을 확인 가능<br>

Prepared Statement<br>
컴파일이 미리 되어있기 때문에 Statement에 비해 좋은 성능<br>
특수문자를 자동으로 파싱해주기 때문에 SQL injection 같은 공격을 막을 수 있음<br>
"?" 부분에만 변화를 주어 쿼리문을 수행하므로 실행되는 SQL문을 파악하기 어려움<br>

Statement와 PreparedStatement의 아주 큰 차이는 바로 캐시 사용여부이다.<br>
Statement를 사용하면 매번 쿼리를 수행할 때마다 계속적으로 단계를 거치면서 수행하지만 PreparedStatement는 처음 한 번만 세 단계를 거친 후 캐시에 담아 재사용을 한다. <br>
만약 동일한 쿼리를 반복적으로 수행한다면 PrepardStatement가 DB에 훨씬 적은 부하를 주며, 성능도 좋다.<br>
