---
title: springboot-mybatis
date: 2020-06-09 21:34:26
tags: [springboot, mybatis]
cover: http://t9.baidu.com/it/u=427372821,944655008&fm=193
---

### annotations
- `@Mapper` add to mapper, use `@MapperScan(“com.a”, “com.b”)` in `Application.class` instead
- maybe need use `@Repository` to avoid error when `@Autowired`.

### xml
#### like
- concat(concat('%',#{username}),'%')
- add `%` in param
- use `bind` label
```xml
<select id="selectPersons" resultType="person" parameterType="person">
  <bind name="pattern" value="'%' + _parameter.username + '%'" />
  select id,sex,age,username,password 
  from person
  where username LIKE #{pattern}
</select>
```