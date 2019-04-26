---
title: mybatis_sql片段
date: 2018-12-04 15:15:36
tags: mybatis
---

# Mybatis sql 片段使用

## 1、在 mybatis 中通过使用 SQL 片段可以提高代码的重用性，如下情景：

1. 创建动态 SQL

```sql
<sql id="sql_count">select count(*)</sql>
```

2. 使用代码

```sql
<select id="selectListCountByParam" parameterType="map" resultType="String">
　　<include refid="sql_count"/> from table_name
</select>
```

3. 解析

> 在使用 sql 片段时使用 include 标签通过 sql 片段的 id 进行引用，sql 片段的 ID 在当前空间必须为唯一的。当然，sql 片段中也可以写其他的内容，只要符合语法规范都是可以的。如下：

```sql
<sql id="sql_where">
　　<trim prefix="WHERE" prefixoverride="AND | OR">
　　　　<if test="id != null">AND id=#{id}</if>
　　　　　　<if test="name != null and name.length()>0">AND name=#{name}</if>
　　　　　　<if test="gender != null and gender.length()>0">AND gender=#{gender}</if>
　　</trim>
</sql>
<select id="updateByKey" parameterType="Map" resultType="List">
　　　select * from user <include refid="sql_where">
</select>　　　　
```
