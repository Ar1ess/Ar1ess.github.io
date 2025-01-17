---
layout: post
title: 'PageHelper分页工具'
subtitle: 'PageHelper + Mybatis 实现简单分页'
date: 2020-2-5
categories: 工具
tags: Java PageHelper Mybatis
---

# PageHelper 分页工具

整理一下代码

```xml
<dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper-spring-boot-starter</artifactId>
            <version>1.2.10</version>
</dependency>
```



```bash
#pageHelper参数设置
pagehelper.helper-dialect=mysql
pagehelper.reasonable=true
pagehelper.support-methods-arguments=true
pagehelper.params=count=countSql
```



```java
@GetMapping(value = "/page")
public RestData page(@RequestParam(value = "num") Integer num){
    PageHelper.startPage(num, 5);
    List<User> list = userMapper.selectAllUser();
    PageInfo<User> pageInfo = new PageInfo<>(list);
    return new RestData(pageInfo);
}		
```



```json
"total": 2,
"list": [
  {
    "systemId": 1,
    "userName": "123",
    "userPassword": "123",
    "userRole": null
  },
  {
    "systemId": 2,
    "userName": "admin",
    "userPassword": "admin",
    "userRole": null
  }
],
"pageNum": 1,
"pageSize": 5,
"size": 2,
"startRow": 1,
"endRow": 2,
"pages": 1,
"prePage": 0,
"nextPage": 0,
"isFirstPage": true,
"isLastPage": true,
"hasPreviousPage": false,
"hasNextPage": false,
"navigatePages": 8,
"navigatepageNums": [
  1
],
"navigateFirstPage": 1,
"navigateLastPage": 1
```



```java
	//当前页
    private int pageNum;
    //每页的数量
    private int pageSize;
    //当前页的数量
    private int size;
    //由于startRow和endRow不常用，这里说个具体的用法
    //可以在页面中"显示startRow到endRow 共size条数据"
    //当前页面第一个元素在数据库中的行号
    private int startRow;
    //当前页面最后一个元素在数据库中的行号
    private int endRow;
    //总记录数
    private long total;
    //总页数
    private int pages;
    //结果集
    private List<T> list;
    //前一页
    private int prePage;
    //下一页
    private int nextPage;
    //是否为第一页
    private boolean isFirstPage = false;
    //是否为最后一页
    private boolean isLastPage = false;
    //是否有前一页
    private boolean hasPreviousPage = false;
    //是否有下一页
    private boolean hasNextPage = false;
    //导航页码数
    private int navigatePages;
    //所有导航页号
    private int[] navigatepageNums;
    //导航条上的第一页
    private int navigateFirstPage;
    //导航条上的最后一页
    private int navigateLastPage;
```

