# resultType
resultType은 SQL 쿼리의 결과를 지정된 클래스의 인스턴스로 직접 매핑합니다. 이 타입은 각 컬럼 값을 해당 클래스의 프로퍼티나 필드에 자동으로 할당합니다. 클래스는 일반적인 POJO(Plain Old Java Object)이며, 컬럼 이름과 클래스의 프로퍼티 이름이 일치해야 합니다.


```xml

<select id="selectUser" resultType="com.example.User">
    SELECT id, name, email FROM users
</select>
```
여기서 com.example.User 클래스는 id, name, email 프로퍼티를 가져야 하며, 이는 데이터베이스의 users 테이블의 컬럼 이름과 일치해야 합니다.

# resultMap
resultMap은 더 복잡한 매핑을 정의할 수 있는 기능을 제공합니다. resultMap을 사용하면 컬럼과 클래스 프로퍼티 사이의 매핑, 복합 타입의 매핑, 컬렉션과 같은 복잡한 구조의 매핑을 세밀하게 정의할 수 있습니다.

예를 들어, 사용자가 여러 주소를 가지고 있고 이를 매핑하고 싶다면 resultMap을 사용하여 다음과 같이 정의할 수 있습니다.

```xml
    <resultMap type="Board" id="boardMap">
        <result column="id" property="id"/>		<!--property : getter setter의 메서드명 이다. 변수명 아님! -->
		<result column="writer" property="writer"/>
		<result column="title" property="title"/>
		<result column="content" property="content"/> 
		<result column="reg_date" property="regDate"/>
	</resultMap>
	
	<!-- 전체 게시글 조회 -->
	<select id="selectAll" resultMap="boardMap">
		SELECT id, content, writer, title, view_cnt, date_format(reg_date, '%y-%m-%d') AS reg_date FROM board;
	</select>
	
	<!-- 상세 게시글 조회 -->
	<select id="selectOne" resultMap="boardMap" parameterType="int">	<!-- 인자가 하나일 때 parameterType="int"로 하면 알아서 들어온다 -->
		SELECT * FROM board
		WHERE id = #{id};
	</select>
```

혹은

```xml
<resultMap id="userResultMap" type="com.example.User">
    <id property="id" column="user_id"/>
    <result property="name" column="user_name"/>
    <collection property="addresses" ofType="com.example.Address">
        <id property="id" column="address_id"/>
        <result property="street" column="street_name"/>
        <!-- 여기에 더 많은 주소 필드 매핑 -->
    </collection>
</resultMap>

<select id="selectUser" resultMap="userResultMap">
    SELECT u.id AS user_id, u.name AS user_name,
           a.id AS address_id, a.street AS street_name
    FROM users u
    LEFT JOIN addresses a ON u.id = a.user_id
</select>
```

이처럼 resultMap을 사용하면 결과의 구조를 자세히 정의하고, 다대일 또는 일대다 관계와 같은 복잡한 SQL 쿼리 결과도 적절히 처리할 수 있습니다.

resultMap을 통해서 sql database의 컬럼명과 java 필드 명이 다를 때에도 매핑을 시켜줄 수 있습니다.
