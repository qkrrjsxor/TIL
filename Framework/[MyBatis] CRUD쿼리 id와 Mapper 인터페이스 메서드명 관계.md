### CRUD 쿼리의 id 속성과 Mapper 인터페이스의 메서드명
MyBatis에서는 Mapper XML 파일에 정의된 <insert>, <select>, <update>, <delete> 요소의 id 속성과 Mapper 인터페이스의 메서드 이름을 일치시켜야 합니다.
이렇게 일치시키는 이유는 MyBatis가 id 속성 값을 사용하여 XML 파일에 정의된 SQL 쿼리와 인터페이스의 메서드를 매핑하기 때문입니다.

**Ex)**
다음과 같이 
```xml
<mapper namespace="com.example.mapper.UserMapper">
    <select id="selectUserById" resultType="com.example.domain.User" parameterType="String">
        SELECT * FROM users WHERE id = #{id}
    </select>
</mapper>

```

```java
package com.example.mapper;

public interface UserMapper {
    User selectUserById(int id);
}

```
