---
title: Eshop网上商城项目
copyright: true
date: 2021-03-23 15:50:57
toc: true
tags: [后端,JAVA]
categories: [后端,JAVA]
---

# EShop网上商城项目

<!-- more -->

## 一.项目定位

JavaSE第一阶段的综合案例

### 1)核心基础

### 2)面向对象

### 3)常用API

### 4)集合

### 5)IO流

### 6)反射

## 二.项目目标

1.熟练应用JavaSE第一阶段的基础知识

2.【重点】具备一定的分析问题的能力

3.【重点】具备一定的解决问题的能力

4.能够使用JSON技术进行数据的存储和解析

5.能够使用JUnit5进行单元测试

6.能够使用IDEA的Debug工具调试代码

7.能够自定义注释并用反射技术解析和使用

熟练应用基础知识 + 两项重要能力 + 四项新技术点

## 三.内容安排

### Java程序开发

#### 先设计

##### 需求分析

业务模块：商品模块 ---> 购物车模块 ---> 订单模块

​		系统模块：登录模块				日志模块

##### 概要设计

运行流程，功能分配，数据存取

接口设计，出错处理，日志设计

#### 再编码

##### 先底层框架代码

登录模块，日志模块

##### 再上层业务逻辑

商品模块，购物车模块，订单模块

## 四.学习方法

### 1.吃透需求

### 2.梳理步骤

### 3.代码实现

### 4.调试错误

## 五.需求分析

### 1.项目需求：

使用控制台作为用户交互界面，实现用户进入购物网站后从首页到最终下单支付的流程中一系列动作

### 2.需求分析的目标：

分析出要开发的系统的模块，及每个模块下的功能

### 3.购物网站举例：

https://www.jd.com/

### 4.本系统操作流程：

![](https://z3.ax1x.com/2021/03/23/67tuSx.png)



### 5.功能模块（普通用户/商家）：

注：商家模块标记红![微信图片_20210311105518](https://z3.ax1x.com/2021/03/23/67teYR.png)



## 六.概要设计

对要开发的系统功能进行设计，包括以下方面：

### 1.运行流程：

[![67tmf1.png](https://z3.ax1x.com/2021/03/23/67tmf1.png)](https://imgtu.com/i/67tmf1)



### 2.功能分配：

#### 1）客户端(Client)

Client			客户端页面的顶层父类

UserClient		用户（登录/注册）操作页面

GoodsClient			商品操作页面

CartClient			购物车操作页面

OrderClient			订单操作页面

![微信图片_20210311105526](https://z3.ax1x.com/2021/03/23/67tZk9.png)



#### 2）服务端

BaseAction			控制器基类（Controller）

​	UserAction			用户控制器类

​	GoodsAction			商品控制器类

​	CartAction			购物车控制器类

​	OrderAction			订单控制器类

Service			服务层

DAO			数据访问层（Data Access Object）

![微信图片_20210311105529](https://z3.ax1x.com/2021/03/23/67tETJ.png)



#### 3）数据库

TXT文件

JSON格式存储

IO流读写

### 3.接口设计：

#### 1）Service层的接口：可能向多个模块提供服务

​	BaseService			服务层的顶层接口，所有模块的服务层接口的父接口

​	UserService			用户模块的接口，处理所有与用户数据相关的业务逻辑

​	GoodsService		 商品模块的接口，处理所有与商品数据相关的业务逻辑

​	CartService			 购物车模块的接口，处理所有与购物车数据相关的业务逻辑

​	OrderService		  订单模块的接口，处理所有与订单数据相关的业务逻辑



![微信图片_20210311105533](https://z3.ax1x.com/2021/03/23/67tKl6.png)



#### 2）DAO层的接口：可能向多个服务层提供数据

​	BaseDAO				数据访问层的顶层接口，所有模块的数据访问层接口的父接口

​	UserDAO				用户模块的接口，处理所有与用户相关的数据

​	GoodsDAO			 商品模块的接口，处理所有与商品相关的数据

​	CartDAO				 购物车模块的接口，处理所有与购物车相关的数据

​	OrderDAO			  订单模块的接口，处理所有与订单相关的数据



![微信图片_20210311105537](https://z3.ax1x.com/2021/03/23/67tM6K.png)



#### 3）数据库的接口：可能操作不同的数据库

​	IDataAccess		   定义数据的基本操作

#### 4）日志模块的接口：支持控制台打印和写入本地文件

​	ISysLog				  定义日志的基本操作

### 4.数据结构：

#### 1）实体类：描述现实事物的类

​	Entity					  实体类，所有子模块的实体类的父类

​		id						数据的唯一标识，String

​		createTime		 数据的创建时间，String

​		deleteTime		 数据的删除时间，String

​		isDel				  数据的删除状态，String，0已删除，1正常，默认1

​	User					  用户模块的实体类，用于描述用户的基本信息

​	Goods				  商品模块的实体类，用于描述商品的基本信息

​	Cart					  购物车模块的实体类，用于描述购物车的基本信息

​	Order				   订单模块的实体类，用于描述订单的基本信息



![微信图片_20210311105541](https://z3.ax1x.com/2021/03/23/67tQOO.png)



#### 2）数据文件：和每个实体类是一一对应的

​	User					 db_user.txt

​	Goods				  db_goods.txt

​	Cart					  db_cart.txt

​	Order				    db_order.txt

### 5.出错处理：顶层调用者处理异常，其他抛出

​	Action					在控制器中捕获异常

​	Service				  服务层的所有异常全部抛出

​	DAO					  数据访问层的所有异常全部抛出

![微信图片_20210311105544](https://z3.ax1x.com/2021/03/23/67t1mD.png)



### 6.日志设计：支持控制台打印和写入本地文件

​	ISysLog				 日志模块接口

​		info					普通信息

​		warn				  警告信息

​		error				  错误信息

​	ConsoleLog		 实现类，打印日志信息到控制台
​	TxtLog				 实现类，打印日志信息到txt文件



### 7.小结



![微信图片_20210311105551](https://z3.ax1x.com/2021/03/23/67t8TH.md.png)



## 七.开发前的准备工作

### 1.项目模块和分包

#### 1）创建项目Eshop，并添加如下模块

​	user			用户模块

​	log			  日志模块

​	goods		 商品模块

​	cart			 购物车模块

​	order		  订单模块

​	client		  客户端模块

​	common	公共模块，存放所有顶层父类，接口，公共bean，工具类等

#### 2）各模块下的包：

​	cn.butou.eshop.user

​	cn.butou.eshop.log

​	cn.butou.eshop.goods

​	cn.butou.eshop.cart

​	cn.butou.eshop.order

​	cn.butou.eshop.client

​	cn.butou.eshop.common

### 2.公共模块的基类和顶层接口

#### 1）common模块下的基类和接口

​	cn.butou.eshop.common.action.BaseAction

```java
/**
	Action，控制器类的基类
	1.封装请求数据
	2.校验权限
	3.调用服务层（Service）处理业务逻辑
	4.日志的记录
	5.返回消息到客户端
*/
public class BaseAction {}
```



​	cn.butou.eshop.common.service.BaseService

```java
/**
	服务层，所有模块服务层的顶层接口
	1.调用DAO层获取数据
	2.处理业务逻辑
	3.把处理结果返回给Action
*/
public interface BaseService {}
```



​	cn.butou.eshop.common.dao.BaseDAO

```java
/**
	数据访问层，所有模块数据访问层的顶层接口
	1.获取数据
	2.把数据返回给服务层（Service）
*/
public interface BaseDAO {}
```



​	cn.butou.eshop.common.dao.IDataAccess

```java
/**
	访问数据库（文件）
	返回结果给DAO
*/
public interface IDataAccess {}
```



​	cn.butou.eshop.common.entity.Entity

```java
/**
	实体类
	所有模块实体类的父类
	职责，封装数据
*/
public class Entity {
    /* 数据唯一标识 */
    private String id;

    /* 创建时间 */
    private String createTime;

    /* 删除时间 */
    private String deleteTime;

    /* 删除状态 0已删除，1正常，默认值1 */
    private String isDel = "1";

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getCreateTime() {
        return createTime;
    }

    public void setCreateTime(String createTime) {
        this.createTime = createTime;
    }

    public String getDeleteTime() {
        return deleteTime;
    }

    public void setDeleteTime(String deleteTime) {
        this.deleteTime = deleteTime;
    }

    public String getIsDel() {
        return isDel;
    }

    public void setIsDel(String isDel) {
        this.isDel = isDel;
    }
}
```



#### 2）client模块下的基类

​	cn.itcast.eshop.client.Client

```java
/** 
	客户端顶层父类
	处理公共的用户操作
*/
public class Client {}
```

### 3.数据交换格式-JSON技术简介

#### 1）JSON的概念

JSON（JavaScript Object Notation）是一种使用文本存储和表示数据的格式

#### 2）JSON格式数据的表现形式

{}：对象

[]：数组

对象的数据表示为键值对

数据之间用逗号隔开

#### 3）JSON支持的数据类型（任意组合）

数值：整数对应int，浮点数对应double

boolean：布尔型，true，false

字符串：如"JoJo"

null：Java中的null

array：数组[]

object：对象{}

### 4.JSONUtil工具类封装（使用了fastjson中的部分方法）

注：fastjson中的方法通过JSON.的方式调用

#### 1）把对象转为JSON格式的字符串

​	public static String enity2JSON(Object entity)

```java
/**
     * 把对象转换成JSON格式的字符串
     * @param entity 指定对象
     * @return 返回JSON格式的字符串
     */
    public static String entity2JSON(Object entity) {
        return JSON.toJSONString(entity);
    }
```



#### 2）把实体对象列表转换成JSON字符串

​	public static String entityList2JSON(List<?> entityList)

```java
/**
     * 把实体对象列表转换成JSON字符串
     * @param entityList 指定实体对象列表
     * @return 返回JSON格式的字符串
     */
    public static String entityList2JSON(List<?> entityList) {
        return entity2JSON(entityList);
    }
```



#### 3）将JSON字符串转换成指定类型对象

​	public static <T> T JSON2Entity(String json, Class<T> clazz)

```java
/**
     * 把JSON字符串转换成指定类型的对象
     *
     * 定义了泛型<T> T 的方法叫做泛型方法
     * T 泛型
     * @param json 要转换的数据
     * @param clazz 指定的类型Class对象
     * @return 返回泛型
     */
public static <T> T JSON2Entity(String json, Class<T> clazz) {
        return JSON.parseObject(json, clazz);
}
```



​	public static Object JSON2Entity(String json, Class<?> clazz)

```java
/**
     * 把JSON字符串转换成指定类型的对象
     *
     * ? 泛型的通配符，代表的是未知的任意类型，或者说是Object
     * @param json 要转换的数据
     * @param clazz 指定的类型Class对象
     * @return 返回Object对象
     */
    public static Object JSON2Entity(String json, Class<?> clazz) {
        Object obj = JSON.parseObject(json, clazz); 
        return obj; //返回的只是一个obj对象，而不是指定的类型，需要用泛型方法改进
    }
```



#### 4）将JSON数组转换成指定类型对象列表

​	public static <T> List<T> JSONArray2List(String json, Class<T> clazz)

```java
 /**
     * 将JSON数组转换成指定类型的对象列表
     *
     * @param json 数据
     * @param clazz 指定的类型Class对象
     * @param <T> 指定的类型
     * @return 对象列表
     */
public static <T> List<T> JSONArray2List(String json, class<T> clazz) {
    return JSON.parseArray(json, clazz);
}
```



​	public static List<?> JSONArray2List(String json, Class<?> clazz)

## 八.用户管理

### 1.用户管理模块主要功能

#### 1）用户登录

输入用户名，密码，并根据用户名，密码获取用户，若该用户存在，则登录成功，否则登录失败

#### 2）用户注册

提示用户输入用户信息和个人基本信息，封装成用户对象，向数据库添加一条数据

![微信图片_20210311192039](https://z3.ax1x.com/2021/03/23/67t30e.png)



#### 3）用户实体类

username，password，role，（NORMAL，ADMIN）

#### 4）Person实体类

name，sex，phone，address

![微信图片_20210311193035](https://z3.ax1x.com/2021/03/23/67tJkd.png)

### 2.登录功能分析

![微信图片_20210311195148](https://z3.ax1x.com/2021/03/23/67ttfI.png)

### 3.客户端登录界面

#### 1）分析步骤

1.使用控制台提示用户输入用户名，密码

2.向服务器发送请求，并接收返回消息字符串，使用setter方法把数据传递给Action，调用Action的登录功能

3.解析消息字符串，提示用户信息

4.页面跳转：使用字符串常量作为跳转标记

成功：返回上一次操作的页面

失败：返回登录页面

注：登录不用判断权限，因为所有用户（普通用户，商家）都可以登录

```java
package cn.butou.eshop.client;

import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.user.action.UserAction;

import java.util.Scanner;

/**
 * 用户操作界面
 * 所有和用户操作相关的内容，都放到这个类里
 */
public class UserClient extends Client {
    /**
     * 用户登录操作界面
     * 1.使用控制台提示用户输入用户名，密码
     * 2.向服务器发送请求，并接收返回消息字符串
     * 使用setter方法把数据传递给Action
     * 调用Action的登录功能
     * 3.解析消息字符串，提示用户信息
     * 4.页面跳转，使用字符串常量作为跳转标记
     * 成功，返回上一次操作的页面
     * 失败，返回登录页面
     * @return
     */
    public String showLogin() {
        // 1.使用控制台提示用户输入用户名，密码
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入用户名：");
        String username = sc.nextLine();
        System.out.println("请输入密码：");
        String password = sc.nextLine();
        
        // 2.向服务器发送请求，并接收返回消息字符串
        UserAction userAction = UserAction();
        // 2.1 使用setter方法把数据传递给Action
        userAction.setUsername(username);
        userAction.setPassword(password);
        // 2.2 调用Action的登录功能
        String result = userAction.login();
        
        // 3.解析消息字符串，提示用户消息
        Msg msg = JSONUtil.JSON2Entity(result, Msg.class);
        if(msg.getType().equals(Msg.SUCCESS)) { // 登录成功
            System.out.println("登录成功！");
            return HISTORY;
        } else {
            System.out.println("登录失败");
            return LOGIN;
        }
    }
}
```

```java
package cn.butou.eshop.client;

/**
* 客户端顶层父类
* 处理公共的用户操作
*/
public class Client {
    
    /** 全局 用户操作 登录 */
    public static final String LOGIN = "L";
    /** 全局 用户操作 上一次操作记录 */
    public static final String HISTORY = "I";
    /** 全局 用户操作 首页 */
    public static final String INDEX = "I";
    
    public static void main(String[] args) {
        Client c = new Client();
        c.start();
    }
    
    public void start() {
        UserClient userClient = new UserClient();
        String result = userClient.showLogin();
        
        if(result.equals(INDEX)) { // 首页
            System.out.println("这里是首页");
        } else if(result.equals(LOGIN)) { // 登录页面
            System.out.println("这里是登录页面");
        } else if(result.equals(HISTORY)) { // 上一次操作页面
            System.out.println("这里是历史页面");
        } else {
            System.out.println("出错了。");
        }
    }
}
```

```java
package cn.butou.eshop.user.action;

import cn.butou.eshop.common.action.BaseAction

/**
* 用户控制器类
* 处理所有用户的后台操作，并返回JSON格式的字符串消息
*/
public class UserAction extends BaseAction {
    /** 用户名 */
    private String username;
    /** 密码 */
    private String password;
    
    /**
    * 用户登录功能
    * @return
    */
    public String login() {
        return "";
    }
    
    public String getUsername() {
        return username;
    }
    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```

```java
package cn.butou.eshop.common.entity;

/**
* 消息封装类
*/
public class Msg {
    /** 消息类型，成功 */
    public static final String SUCCESS = "SUCCESS";
    /** 消息类型，失败 */
    public static final String FAIL = "FAIL";
    
    // 消息类型，成功SUCCESS，失败，FAIL
    private String type;
    // 消息内容
    private String msg;
    
    public String getType() {
        return type;
    }
    
     public void setType(String type) {
        this.type = type;
    }

    public String getMsg() {
        return msg;
    }

    public void setMsg(String msg) {
        this.msg = msg;
    }
}
```

### 4.服务端登录 - Controller层的实现

#### 1）分析步骤

1.封装数据到User对象

2.调用UserService处理逻辑

​	User login(User user) throws Exception;

3.异常处理

4.根据服务层返回结果生成消息

​	消息实体类Msg

5.记录日志（待开发）

6.响应消息到客户端

```java
package cn.butou.eshop.user.action;

import cn.butou.eshop.common.action.BaseAction;
import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.user.entity.User;
import cn.butou.eshop.user.service.UserService;
import cn.butou.eshop.user.service.impl.UserServiceImpl;

/**
 * 用户控制器类
 * 处理所有用户的后台操作，并返回JSON格式的字符串消息
 */
public class UserAction extends BaseAction {
    // 用户名
    private String username;
    // 密码
    private String password;
    
    /**
    * 用户登录功能
    * 1.封装数据到User对象
    * 2.调用UserService处理逻辑
    *	User login(User user) throws Exception;
    * 3.异常处理
    * 4.根据服务层返回结果生成消息
    * 5.记录日志
    * 6.响应消息到客户端
    * @return
    */
    public String login() {
        Msg msg = new Msg();
        try {
            // 1.封装数据到User对象
            User user = new User();
            user.setUsername(username);
            user.setPassword(password);
            
            // 2.调用UserService处理逻辑
            //	User login(User user) throws Exception;
            UserService userService = new UserService();
            user = userService.login(user);
            
            // 3.异常处理
            
            // 4.根据服务层返回结果生成消息
            //		消息实体类Msg
            if(user != null) {
                msg.setType(Msg.SUCCESS); // 登录成功
                msg.setMsg("登录成功");
                // TODO 5.记录日志（待开发）
            } else {
                msg.setType(Msg.FAIL); // 登录失败
                msg.setMsg("用户名或密码不正确");
            }
            return JSONUtil.entity2JSON(msg);
        } catch(Exception e) {
            e.printStackTrace();
            msg.setType(Msg.FAIL); // 登录失败
            msg.setMsg("服务器异常");
            return JSONUtil.entity2JSON(msg);
        }
    }
}
```

```java
// 6.响应消息到客户端
package cn.butou.eshop.client;

import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.user.action.UserAction;

import java.util.Scanner;

public class UserClient extends Client {
    /**
    * 用户登录操作界面
    * 1.使用控制台提示用户输入用户名，密码
    * 2.向服务器发送请求，并接收返回消息字符串
    * 使用setter方法把数据传递给Action
    * 调用Action的登录功能
    * 3.解析消息字符串，提示用户信息
    * 4.页面跳转，使用字符串常量作为跳转标记
    * 成功，返回上一次操作的页面
    * 失败，返回登录页面
    * @return
    */
    public String showLogin() {
        // 1.使用控制台提示用户输入用户名，密码
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入用户名：");
        String username = sc.nextLine();
        System.out.println("请输入密码：");
        String password = sc.nextLine();
        
        // 2.向服务器发送请求，并接收返回消息字符串
        UserAction userAction = new UserAction();
        // 2.1 使用setter方法把数据传递给Action
        userAction.setUsername(username);
        userAction.setPassword(password);
        // 2.2 调用Action的登录功能
        String result = UserAction.login();
        
        // 3.解析消息字符串，提示用户消息
        Msg msg = JSONUtil.JSON2Entity(result, Msg.class);
        if(msg.getType().equals(Msg.SUCCESS)) { // 登录成功
            System.out.println(msg.getMsg()); // 打印获取到的消息
            return HISTORY;
        } else { // 登录失败
            System.out.println(msg.getMsg()); // 打印获取到的消息
            return LOGIN;
        }
    }
}
```



```java
package cn.butou.eshop.user.entity;

/**
* 用户模块的实体类，用于描述用户的基本信息
*
*/
public class User extends Person {
    /** 用户名 */
    private String username;
    /** 密码 */
    private String password;
    /** 角色 */
    private String role = "NORMAL";
    
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```

```java
package cn.butou.eshop.user.entity;

import cn.butou.eshop.common.entity.Entity;

/**
* 人类，User的父类
*/
public class Person extends Entity {
}
```

```java
package cn.butou.eshop.user.service;

import cn.butou.eshop.user.entity.User;

// 用户模块的接口，处理所有与用户数据相关的业务逻辑
public interface UserService {
    /**
    * 服务端登录
    * @param user 根据输入的User对象进行逻辑处理
    * @return 返回一个User对象
    * @throws Exception 抛出异常交给UserAction处理
    */
    User login(User user) throws Exception;
}
```

```java
package cn.butou.eshop.user.service.impl;

import cn.butou.eshop.user.entity.User;
import cn.butou.eshop.user.service.UserService;

/**
* UserService接口的实现类
*/
public class UserServiceImpl implements UserService {
    @Override
    public User login(User user) throws Exception {
        return null;
    }
}
```

### 5.服务端登录 - Service层的实现

#### 1）分析步骤

1.调用UserDAO获取用户列表数据

​	List<User> getEntityList() throws Exception;

2.遍历用户列表，逐个与给定用户对象的用户名，密码进行匹配

3.匹配成功则返回该用户对象，失败返回null

```java
package cn.butou.eshop.user.service.impl;

import cn.butou.eshop.user.dao.UserDAO;
import cn.butou.eshop.user.dao.impl.UserDAOImpl;
import cn.butou.eshop.user.entity.User;
import cn.butou.eshop.user.service.UserService;

import java.util.List;

/**
* UserService接口的实现类
*/
public class UserServiceImpl implements UserService {
    //将要调用的UserDAO接口定义为私有成员变量
    private UserDAO userDAO;
    
    /**
     * 用户登录，根据用户名，密码获取用户对象
     * 1.调用UserDAO获取用户列表数据
     * List<User> getEntityList() throws Exception;
     * 2.遍历用户列表，逐个与给定用户对象的用户名，密码进行匹配
     * 3.匹配成功则返回该用户对象，失败返回null
     * @param User 封装了用户名，密码的实体对象
     * @return 返回User对象，或者当用户名/密码错误时返回null
     * @throws Exception
     */
    @Override
    public User login(User user) throws Exception {
        // 1.调用UserDAO获取用户列表数据
        userDAO = new UserDAOimpl();
        List<User> userList = userDAO.getEntityList();
        
        // 2.遍历用户列表，逐个与给定用户对象的用户名，密码进行匹配
        if(userList != null) {
            for (User u : userList) {
                if(u.getUsername().equals(user.getUsername())
                  		&& u.getPassword().equals(user.getPassword())) {
                    return u; // 3.匹配成功则返回该用户对象
                }
            }
        }
        return null; // 失败返回null;
    }
    
}
```

```java
package cn.butou.eshop.user.dao
    
import cn.butou.eshop.common.dao.BaseDAO;
import cn.butou.eshop.user.entity.User;

import java.util.List;

/**
 * 用户模块的接口，处理所有与用户相关的数据
 */
public interface UserDAO extends BaseDAO {
    List<User> getEntityList() throws Exception;
}
```

```java
package cn.butou.eshop.user.dao.impl;
import cn.butou.eshop.user.dao.UserDAO;
import cn.butou.eshop.user.entity.User;

import java.util.List;

/**
 * UserDAO接口的实现类
 */
public class UserDAOImpl implements UserDAO {
    @Override
    public List<User> getEntityList() throws Exception {
        return null;
    }
}
```



#### 2）注意事项

实际生产环境中，使用操作数据库的语言（SQL）将用户名，密码作为条件进行查询，本系统不支持此操作

### 6.服务端登录 - DAO层的实现

#### 1）分析步骤

1.创建IDataAccess子类TXTDataAccess的对象

​	IDataAccess dataAccess = new TXTDataAccess();

2.调用该对象的方法获取所有用户数据并返回

​	List<User> userList = dataAccess.getList(User.class);

```java
package cn.butou.eshop.user.dao.impl;

import cn.butou.eshop.common.dao.BaseDAO;
import cn.butou.eshop.common.dao.impl.BaseDAOImpl;
import cn.butou.eshop.user.dao.UserDAO;
import cn.butou.eshop.user.entity.User;

import java.util.List;

/**
 * UserDAO接口的实现类
 */
public class UserDAOImpl extends BaseDAOImpl implements UserDAO {
    /**
     * 调用IDataAccess获取数据并返回
     * 1.创建IDataAccess子类TXTDataAccess的对象
     *		IDataAccess dataAccess = new TXTDataAccess();
     * 2.调用该对象的方法获取所有用户数据并返回
     *		List<User> userList = dataAccess.getList(User.class);
     * @return 返回用户列表
     * @throws Exception
     */
    @Override
    public List<User> getEntityList() throws Exception {
        // 2.调用该对象的方法获取所有用户数据并返回
        return dataAccess.getList(User.class);
    }
}
```

```java
package cn.butou.eshop.common.dao.impl;

import cn.butou.eshop.common.dao.BaseDAO;
import cn.butou.eshop.common.dao.IDataAccess;

/**
* BaseDAO接口的实现类
*/
public class BaseDAOImpl implements BaseDAO {
    // 1.创建IDataAccess子类TXTDataAccess的对象
    protected IDataAccess dataAccess = new TXTDataAccess();
}
```

```java
package cn.butou.eshop.common.dao;

import java.util.List;

/**
* 访问数据库（文件）
* 返回结果给DAO
*/
public interface IDataAccess {
    // List<User> getList(Class<User> clazz) throws Exception;
    <T> List<T> getList(Class<T> clazz) throws Exception;
}
```

```java
package cn.butou.eshop.common.dao.impl;

import cn.butou.eshop.common.dao.IDataAccess;
import cn.butou.eshop.common.util.JSONUtil;

import java.io.File;
import java.util.List;

/**
* IDataAccess的实现类
*/
public class TXTDataAccess implements IDataAccess {
    /**
     * 获取数据列表
     * 1.根据实体类的字节码文件对象获取类名
     * 2.根据类名获取用户数据文件名
     * 3.合成数据文件路径
     * 4.使用文件操作工具类读取文件中的字符串数据
     * 5.将字符串数据转换成List<User>对象并返回
     * @param clazz
     * @param <T>
     * @return
     * @throws Exception
     */
    @Override
    public <T> List<T> getList(Class<T> clazz) throws Exception {
        // 1.根据实体类的字节码文件对象获取类名
        String userName = clazz.getSimpleName().toLowerCase(); // User --> user
        // 2.根据类名获取用户数据文件名
        String dataFileName = "db_" + userName + ".txt"; // db_user.txt
        // 3.合成数据文件路径
        String dataFilePath = "db/" + dataFileName; // db/db_user.txt
        // 4.使用文件操作工具类读取文件中的字符串数据
        String dataJson = FileUtil.readByBuffered(dataFilePath);
        // 5.将字符串数据转换成List<User>对象并返回
        return JSONUtil.JSONArray2List(dataJson, clazz);
    }
}
```



#### 2）getList()方法定义分析

作用：获取全部数据

返回值：List<User> 用户对象列表

参数：Class<User> (JSON转换需要)

#### 3）getList()方法实现步骤

根据实体类的字节码文件对象获取类名

根据类名获取用户数据文件名

合成数据文件路径

使用文件操作工具类读取文件中的字符串数据

将字符串数据转换成List<User>对象并返回

#### 4）文件操作工具类FileUtil的实现

```java
package cn.butou.eshop.common.util;

import java.io.*;

/**
 * 文件工具类
 */
public class FileUtil {
    /**
     * 字节缓冲流拷贝文件
     * @param file
     * @param destDir
     * @throws IOException
     */
    public static void copyFileByStream(File file, String destDir) throws IOException {
        if(file != null) {
            File dir = new File(destDir); //目标目录
            if(!dir.exists()) {
                dir.mkdirs(); // 创建目录
            }
            if(file.isFile()) {
                String fileName = file.getName(); // 文件名
                File dest = new File(dir, filename); // 目标文件对象
                BufferedInputStream bis = new BufferedInputStream(new FileInputStream(file));
                BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(dest));
                
                int len = 0;
                byte[] bs = new byte[2048];
                while((len = bis.read(bs)) != -1) {
                    bos.write(bs, 0, len);
                    // 因为len可能小于2048字节即2KB
                    bos.flush(); //清空缓冲区数据
                }
                bos.close();
                bis.close();
            } else if(file.isDirectory()) { // 在目标位置创建目录
                File dest = new File(dir, file.getName());
                dest.mkdir();
            }
        }
    }
    
    /**
     * 使用字符缓冲流对象读取文件内容并转成字符串返回
     * @param filePath
     * @return
     * @throws IOException
     */
    public static String readByBuffered(String filePath) throws IOException {
        StringBuilder sb = new StringBuilder();
        // 使用ClassLoader加载资源，路径从src下开始：db/db_user.txt
        // FileUtil.class.getClassLoader() --> common/src/
        // FileUtil.class.getClassLoader().getResource(db/db_user.txt) --> common/src/db/db_user.txt的URL对象
        filePath = FileUtil.class.getClassLoader().getResource(filePath).getFile();
        
        File file = new File(filePath);
        if(file.exists()) {
            BufferedReader br = new BufferedReader(new FileReader(file));
            String str = br.readLine(); // 按行读取
            while(str != null) {
                sb.append(str);
                str = br.readLine();
            }
            br.close();
            return sb.toString();
        }
        return null;
    }
    
    /**
     * 将字符串数据写入指定文件。写入时会先清空原文件内容
     * @param data 要写入的数据
     * @param destFilePath 文件路径 + 文件名
     * @throws IOException
     */
    public static void writeByBuffered(String data, String destFilePath) throws IOException {
        File destFile = new File(destFilePath);
        if(!destFile.exists()) {
            File parent = destFile.getParentFile();
            if(!parent.exists()) parent.mkdirs();
            destFile.createNewFile();
        }
        
        BufferedWriter bw = new BufferedWriter(new FileWriter(destFile));
        bw.write(data);
        bw.close();
    }
}
```



### 7.客户端注册界面

### 8.服务端注册 - Controller层的实现

### 9.服务端注册 - Service层的实现

### 10.服务端注册 - DAO层的实现



## 九.日志管理

### 1.日志的概念

记录系统操作或消息的数据文件，具有处理历史数据，诊断问题等作用

![微信图片_20210315213913](https://z3.ax1x.com/2021/03/23/67tYtA.md.png)

#### 1）常见日志级别（level）

info			普通信息

warn		  警告信息

error		  错误信息

#### 2）实体类Log

String msg： 日志内容

String level： 日志级别

String time：  日志发生时间

### 2.ISysLog接口定义

#### 1）级别常量

```java
public static final String INFO = "INFO";
public static final String WARN = "WARN";
public static final String ERROR = "ERROR";
```

#### 2）方法定义

```java
void info(String msg)
void warn(String msg)
void error(String msg)
```

### 2.日志 - ConsoleLog实现

```java
package cn.butou.eshop.log.dao;

/**
 * 日志模块接口
 */
public interface ISysLog {
    /** 日志级别 普通消息 */
    public static final String INFO = "INFO";
    /** 日志级别 警告消息 */
    public static final String WARN = "WARN";
    /** 日志级别 错误消息 */
    public static final String ERROR = "ERROR";
    
    void info(String msg);
    
    void warn(String msg);
    
    void error(String msg);
}
```

```java
package cn.butou.eshop.log.dao.impl;

import cn.butou.eshop.log.dao.ISysLog;
import cn.butou.eshop.log.entity.Log;

import java.text.SimpleDateFormat;
import java.util.Date;

/**
 * 日志实现类
 * 在控制台打印日志信息
 * 
 * 步骤：
 * 	1.封装日志对象
 *	2.打印日志数据到控制台
 */
public class ConsoleLog implements ISysLog {
    SimpleDateFormat sdf = new SimpleDateFormat("h:mm a");
    
    @Override
    public void info(String msg) {
        // 1.封装日志对象
        String log = new Log(msg, INFO, sdf.format(new Date()));
        // 2.打印日志数据到控制台
        System.out.println(log);
    }
    
    @Override
    public void warn(String msg) {
        // 1.封装日志对象
        String log = new Log(msg, WARN, sdf.format(new Date()));
        // 2.打印日志数据到控制台
        System.out.println(log);
    }
    
    @Override
    public void warn(String msg) {
        // 1.封装日志对象
        String log = new Log(msg, WARN, sdf.format(new Date()));
        // 2.打印日志数据到控制台
        System.out.println(log);
    }
    
    @Override
    public void error(String msg) {
        // 1.封装日志对象
        String log = new Log(msg, ERROR, sdf.format(new Date()));
        // 2.打印日志数据到控制台
        System.out.println(log);
    }
}
```

```java
package cn.butou.eshop.log.entity;

/**
* 日志实体类
*/
public class Log {
    // 日志内容
    private String msg;
    
    // 日志级别
    private String level;
    
    // 日志发生时间
    private String time;
    
    public Log() {}
    
    /**
     * 构造方法封装日志数据
     * @param msg 日志内容
     * @param level 日志级别
     * @param time 日志发生时间
     */
    public Log(String msg, String level, String time) {
        this.msg = msg;
        this.level = level;
        this.time = time;
    }
    
    public String getMsg() {
        return msg;
    }

    public void setMsg(String msg) {
        this.msg = msg;
    }

    public String getLevel() {
        return level;
    }

    public void setLevel(String level) {
        this.level = level;
    }

    public String getTime() {
        return time;
    }

    public void setTime(String time) {
        this.time = time;
    }
    
    @Override
    public String toString() {
        // [时间] 级别：消息内容
        return "[" + time + "]" + level + "：" + msg;
    }
}
```

```java
package cn.butou.eshop.user.action;

import cn.butou.eshop.common.action.BaseAction;
import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.log.dao.ISysLog;
import cn.butou.eshop.log.dao.impl.ConsoleLog;
import cn.butou.eshop.user.entity.User;
import cn.butou.eshop.user.service.UserService;
import cn.butou.eshop.user.service.impl.UserServiceImpl;

/**
 * 用户控制类
 * 处理用户所有的后台操作，并返回JSON格式的字符串消息
 */
public class UserAction extends BaseAction {
    // 用户名
    private String username;
    // 密码
    private String password;
    
    /**
     * 用户登录功能
     * 1.封装数据到User对象
     * 2.调用UserService处理逻辑
     *	User login(User user) throws Exception;
     * 3.异常处理
     * 4.根据服务层返回结果生成消息
     * 5.记录日志（待开发）
     * 6.响应消息到客户端
     * @return
     */
    public String login() {
        Msg msg = new Msg();
        try {
            // 1.封装数据到User对象
            User user = new User();
            user.setUsername(username);
            user.setPassword(password);
            
            // 2.调用UserService处理逻辑
            //	User login(User user) throws Exception;
            UserService userService = new UserServiceImpl();
            user = userService.login(user);
            
            // 3.异常处理
            
            // 4.根据服务层返回结果生成消息
            //	消息实体类Msg
            if(user != null) {
                msg.setType(Msg.SUCCESS); //登录成功
                msg.setMsg("登录成功");
                // 5.记录日志（待开发）
                log.info(username + "已登录");
            } else {
                msg.setType(Msg.FAIL); // 登录失败
                msg.setMsg("用户名或密码不正确");
            }
            return JSONUtil.entity2JSON(msg);
        } catch(Exception e) {
            e.printStackTrace();
            msg.setType(Msg.FAIL); // 登录失败
            msg.setMsg("服务器异常");
            return JSONUtil.entity2JSON(msg);
        }
    }
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```

```java
package cn.butou.eshop.common.action;

import cn.butou.eshop.log.dao.ISysLog;
import cn.butou.eshop.log.dao.impl.ConsoleLog;

/**
 * Action，控制器类的基类
 * 1.封装请求数据
 * 2.校验权限
 * 3.调用服务层（Service）处理业务逻辑
 * 4.日志的记录
 * 5.返回消息到客户端
 */
public class BaseAction {
    protected ISysLog log = new ConsoleLog();
}
```



### 3.日志 - TxtLog实现



## 十.商品管理

### 1.商城首页

#### 1）GoodsClient步骤分析

1.向后台发送请求，获取商品数据

2.解析响应消息字符串

3.展示商品列表

```java
package cn.butou.eshop.client;

import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.action.GoodsAction;
import cn.butou.eshop.goods.entity.Goods;
import jdk.swing.interop.SwingInterOpUtils;

import java.util.ArrayList;
import java.util.List;

/**
 * 商品操作页面
 */
public class GoodsClient extends Client {
    /**
     * 展示商品列表
     * 1.向后台发送请求，获取商品数据
     * 2.解析响应消息字符串
     * 3.展示商品列表
     */
    public void showGoodsList() {
        // 1.向后台发送请求，获取商品数据
        GoodsAction goodsAction = new GoodsAction();
        String msgJSON = goodsAction.getGoodsList();
        
        // 2.解析响应消息字符串
        Msg msg = JSONUtil.JSON2Entity(msgJSON, Msg.class);
        Object obj = msg.getObj(); // 数据就存放在obj对象里：[{}, {}, {}]
        List<?> goodsListJson = (List<?>) obj;
        
        System.out.println("【商品列表】");
        System.out.println("编号\t商品名称\t\t单价\t\t库存");
        System.out.println("--------------------------------");
        int index = 1; //编号
        for (Object o : goodsListJson) {
            // o : {...}
            String goodsJson = o.toString(); // 这就是Goods对象的json字符串
            Goods goods = JSONUtil.JSON2Entity(goodsJson, Goods.class);
            String name = goods.getName(); // 名称
            String price = goods.getPrice() + ""; // 单价
            String num = goods.getNumber() + ""; // 库存

            //3.展示商品列表
            System.out.println(index + ".\t\t" + name + "\t\t" + price + num);
            index ++;

        }
    }
}
```

```java
package cn.butou.eshop.goods.action;

import cn.butou.eshop.common.action.BaseAction;
import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;

public class GoodsAction extends BaseAction {
    /**
     * 获取商品列表
     * 1.获取所有商品的对象列表
     * 2.将商品对象列表转换成字符串并返回
     * 3.异常处理
     * 4.记录日志
     * 5.响应消息到客户端
     * @return
     */
    public String getGoodsList() {
        Msg msg = new Msg();
        // List<Goods>
        return JSONUtil.entity2JSON(msg);
    }
    
    /**
    * 获取商品详情
    * @return
    */
    public String getGoodsDetail() {
        Msg msg = new Msg();
        
        return JSONUtil.entity2JSON(msg);
    }
}
```

```java
package cn.butou.eshop.goods.entity;

import  cn.butou.eshop.common.entity.Entity;

/**
* 商品模块的实体类，用于描述商品的基本信息
*/
public class Goods extends Entity {
    /* 名称 */
    private String name;
    
    /* 单价 */
    private String price;
    
    /* 数量 */
    private int number;
    
    /* 品牌 */
    private String brand;
    
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public int getNumber() {
        return number;
    }

    public void setNumber(int number) {
        this.number = number;
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }
}
```



#### 2）GoodsAction步骤分析

1.获取所有商品的对象列表

2.将商品对象列表转换成字符串并返回

3.异常处理

4.记录日志

5.响应消息到客户端

```java
package cn.butou.eshop.goods.action;

import cn.butou.eshop.common.action.BaseAction;
import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.entity.Goods;
import cn.butou.eshop.goods.service.GoodsService;
import cn.butou.eshop.goods.service.impl.GoodsServiceImpl;

import java.util.List;

/**
* 商品控制器类
*/
public class GoodsAction extends BaseAction {
    // 商品实体对象
    private Goods goods;
    
    private GoodsService goodsService;
    
    public GoodsAction() {
        goodsService = new GoodsSerivceImpl();
    }
    
    /**
     * 1.获取所有商品的对象列表
     * 2.将商品对象列表转换成字符串并返回
     * 3.异常处理
     * 4.记录日志
     * 5.响应消息到客户端
     * @return
     */
    public String getGoodsList() {
        Msg msg = new Msg();
        // 3.异常处理
        try {
            // 1.获取所有商品的对象列表
            List<Goods> goodsList = goodsService.getGoodsList();
            
            // 2.将商品对象列表转换成字符串并返回
            msg.setObj(goodsList);
            msg.setType(Msg.SUCCESS);
            String result = JSONUtil.entity2JSON(msg);
            
            // 4.记录日志
            log.info("获取商品列表");
            
            // 5.响应消息到客户端
            return result;
        } catch (Exception e) {
            msg.setType(Msg.FAIL);
            msg.setMsg("获取商品列表失败，服务器异常");
            // 4.记录日志
            log.error("获取商品列表失败：" +  e.getMessage());
        }
        return JSONUtil.entity2JSON(msg);
    }
    
    /**
     * 获取商品详情
     * @return
     */
    public String getGoodsDetail() {
        Msg msg = new Msg();
        
        return JSONUtil.entity2JSON(msg);
    }
}
```

```java
package cn.butou.eshop.goods.service;

import cn.butou.eshop.common.service.BaseService;
import cn.butou.eshop.goods.entity.Goods;

import java.util.List;

/**
* 商品服务层
* 处理商品模块的相关业务逻辑
*/
public interface GoodsService extends BaseService {
    public List<Goods> getGoodsList() throws Exception;
    public Goods getGoodsDetail() throws Exception;
}
```

```java
package cn.butou.eshop.goods.service.impl;

import cn.butou.eshop.common.service.BaseService;
import cn.butou.eshop.common.service.impl.BaseServiceImpl;
import cn.butou.eshop.goods.dao.GoodsDAO;
import cn.butou.eshop.goods.dao.impl.GoodsDAOimpl;
import cn.butou.eshop.goods.entity.Goods;
import cn.butou.eshop.goods.service.GoodsService;

import java.util.List;

/**
* 商品服务层接口的实现类
*/
public class GoodsServiceImpl extends BaseServiceImpl implements GoodsService {
    private GoodsDAO goodsDAO;
    
    public GoodsSerivceImpl() {
        goodsDAO = new GoodsDAOimpl();
    }
    
    /**
     * 获取商品列表
     * 1.调用GoodsDAO对象的方法获取数据并返回
     * @return 商品列表
     * @throws Exception
     */
    @Override
    public List<Goods> getGoodsList() throws Exception {
        return goodsDAO.getEntityList();
    }
    
    /**
     * 1.根据商品ID获取商品对象
     * 2.若该对象存在则返回，否则返回null
     * @return Good对象，或null
     * @throws Exception
     */
    @Override
    public Goods getGoodsDetail() throws Exception {
        return null;
    }
}
```

```java
package cn.butou.eshop.goods.dao;

import cn.butou.eshop.common.dao.BaseDAO;
import cn.butou.eshop.goods.entity.Goods;

import java.util.List;

/**
* 商品模块的接口，处理所有与商品相关的数据
*/
public interface GoodsDAO extends BaseDAO {
    public List<Goods> getEntityList() throws Exception;
}
```

```java
package cn.butou.eshop.goods.dao.impl;

import cn.butou.eshop.common.dao.impl.BaseDAOImpl;
import cn.butou.eshop.goods.dao.GoodsDAO;
import cn.butou.eshop.goods.entity.Goods;

import java.util.List;

/**
* 商品模块接口实现类
*/
public class GoodsDAOimpl extends BaseDAOImpl implements GoodsDAO {
    /**
    * 调用dataAccess对象获取数据列表并返回
    * @return
    * @throws Exception
    */
    public List<Goods> getEntityList() throws Exception {
        return dataAccess.getList(Goods.class);
    }
}
```

```java
package cn.butou.eshop.client;

/**
 * 客户端顶层父类
 * 处理公共的用户操作
 */
public class Client {
    /** 全局 用户操作 登录 */
    public static final String LOGIN = "L";
    /** 全局 用户操作 上一次操作记录 */
    public static final String HISTORY = "I";
    /** 全局 用户操作 首页 */
    public static final String INDEX = "I";
    
    public static void main(String[] args) {
        Client c = new Client();
        c.start();
    }
    
    public void start() {
        GoodsClient goodsClient = new GoodsClient();
        goodsClient.showGoodsList();
        
        UserClient userClient = new UserClient();
        String result = userClient.showLogin();
        
        if(result.equals(INDEX)) { // 首页
            System.out.println("这里是首页");
        } else if(result.equals(LOGIN)) { // 登录页面
            System.out.println("这里是登录页面");
        } else if(result.equals(HISTORY)) { // 上一次操作页面
            System.out.println("这里是历史页面");
        } else {
            System.out.println("出错了。");
        }
    }
}
```

### 2.创建公共的用户操作的方法

主要功能：

1.提示用户信息和用户操作

​	请根据编号进行操作（或 L登录；E退出）：

2.接收用户的录入

​	sc.nextLine()

方法的分析：

​	方法名：	userOperate

​	返回值：	String

​	参数列表：

​		String msg;	用户信息

​		String... oprs;	用户操作

​			可变参数，本质是一个数组

```java
package cn.butou.eshop.client;

import java.util.Arrays;
import java.util.Scanner;

/**
 * 客户端顶层父类
 * 处理公共的用户操作
 */
public class Client {

    /** 全局 用户操作 登录 */
    public static final String LOGIN = "L";
    /** 全局 用户操作 上一次操作记录 */
    public static final String HISTORY = "I";
    /** 全局 用户操作 首页 */
    public static final String INDEX = "I";
    /** 全局 用户操作 退出 */
    public static final String EXIT = "E";

    // Client及其子类可用的Scanner对象，UserClient中new Scanner代码可以删去
    protected Scanner sc = new Scanner(System.in);


    public static void main(String[] args) {
        Client c = new Client();
        c.start();
    }

    public void start() {
        GoodsClient goodsClient = new GoodsClient();
        UserClient userClient = new UserClient();
        
        String result = goodsClient.index(); // 返回商品模块用户录入的公共操作

       while (true) {
            if(result.equals(INDEX)) { // 首页
                result = goodsClient.index();
            } else if(result.equals(LOGIN)) { // 登录页面
                result = userClient.showLogin();
            } else if(result.equals(HISTORY)) { // 上一次操作页面
                result = HISTORY;
            } else if(result.equals(EXIT)) { //退出
                System.exit(0);
            } else {
                System.out.println("出错了。");
            }
       }
    }

    /**
     * 需求：创建公共的用户操作的方法
     * 主要功能：
     *  1.提示用户信息和用户操作
     *      请根据编号进行操作（或 L登录；E退出）：
     *  2.接收用户的录入
     *      sc.nextLine()
     *  方法的分析：
     *      方法名：    userOperate
     *      返回值：    String
     *      参数列表：
     *          String msg; 用户信息
     *          String... oprs; 用户操作
     *              可变参数，本质是一个数组
     */
    public String userOperate(String msg, String... oprs) {
        // oprs == String[]
        String opr = Arrays.toString(oprs); // [opr1, opr2, opr3]
        opr = opr.substring(1, opr.length() - 1); // opr1, opr2, opr3
        msg = msg + "或 " + opr + "；E退出）：";
        System.out.println(msg); // 请根据编号进行操作（或 L登录；E退出）：
        return sc.nextLine().trim().toUpperCase(); // 去掉空格，转成大写
    }
}

```

```java
package cn.butou.eshop.client;

import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.action.GoodsAction;
import cn.butou.eshop.goods.entity.Goods;
import jdk.swing.interop.SwingInterOpUtils;

import java.util.ArrayList;
import java.util.List;

/**
 * 商品操作页面
 */
public class GoodsClient extends Client {
    private Goods currentGoods;
    
    /**
     * 商品页面跳转控制器：
     *	本模块的操作由此方法控制跳转
     *	其他模块的操作返回上层，由Client控制跳转
     * @return 返回公共操作
     */
    public String index() {
        showGoodsList(); // 展示商品列表
        String result = userOperate("请根据序号查看商品详情", "L登录；");
        return result;
    }
    
    /**
     * 展示商品列表
     * 1.向后台发送请求，获取商品数据
     * 2.解析响应消息字符串
     * 3.展示商品列表
     */
    public void showGoodsList() {
        // 1.向后台发送请求，获取商品数据
        GoodsAction goodsAction = new GoodsAction();
        String msgJSON = goodsAction.getGoodsList();

        // 2.解析响应消息字符串
        Msg msg = JSONUtil.JSON2Entity(msgJSON, Msg.class);
        Object obj = msg.getObj(); // 数据就存放在obj对象里：[{},{},{}]
        List<?> goodsListJson = (List<?>) obj;

        System.out.println("【商品列表】");
        System.out.println("编号\t商品名称\t\t单价\t\t库存");
        System.out.println("------------------------------");
        int index = 1; //编号
        for (Object o : goodsListJson) {
            // o : {...}
            String goodsJson = o.toString(); // {,,,}
            Goods goods = JSONUtil.JSON2Entity(goodsJson, Goods.class);
            String name = goods.getName(); // 名称
            String price = goods.getPrice() + ""; // 单价
            String num = goods.getNumber() + ""; // 库存

            //3.展示商品列表
            System.out.println(index + ".\t\t" + name + "\t\t" + price + "\t\t" + num);
            index ++;

        }
    }

    /**
     * 查看商品详情
     */
    public void showGoodsDetail() {

    }

    /**
     * TODO 添加商品
     */

    /**
     * TODO 修改库存
     */

    /**
     * TODO 修改单价
     */

    /**
     * TODO 删除商品
     */
}
```

### 3.商品详情

#### 1）思路分析

查看商品详情有两种方式

1.通过数据ID获取数据，然后进行展示（需要重新访问数据库，显然不妥）

2.在展示商品的时候，把商品列表存储起来，然后，当选择商品编号时，就把对应商品展示出来

​	Map<String, Goods> : key --> 编号，value --> Goods对象

```java
package cn.butou.eshop.client

import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.action.GoodsAction;
import cn.butou.eshop.goods.entity.Goods;
import jdk.swing.interop.SwingInterOpUtils;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

/**
 * 商品操作页面
 */
public class GoodsClient extends Client {
    private Goods currentGoods;
    
    // 使用哈希表建立编号与Goods对象之间一一对应关系
    Map<String, Goods> code2Goods = new HashMap<>();
    
    /**
     * 商品管理首页
     *
     * 商品页面跳转控制器：
     * 	本模块的操作由此方法控制跳转
     *	其他模块的操作返回上层，由Client控制跳转
     * @return 返回公共操作
     */
    public String index() {
        showGoodsList(); //展示商品列表
        String result = userOperate("请根据序号查看商品详情", "L登录；");
        Goods goods = code2Goods.get(result); // get方法返回结果为数据或null
        if(goods != null) {
            currentGoods = goods;
            showGoodsDetail();
        }
        return result;
    }
    
    /**
     * 展示商品列表
     * 1.向后台发送请求，获取商品数据
     * 2.解析响应消息字符串
     * 3.展示商品列表
     */
    public void showGoodsList() {
        // 1.向后台发送请求，获取商品数据
        GoodsAction goodsAction = new GoodsAction();
        String msgJSON = goodsAction.getGoodsList();
        
        // 2.解析响应消息字符串
        Msg msg = JSONUtil.JSON2Entity(msgJSON, Msg.class);
        Object obj = msg.getObj(); // 数据就存放在obj对象里：[{},{},{}]
        List<?> goodsListJson = (List<?>) obj;
        
        System.out.println("【商品列表】");
        System.out.println("编号\t商品名称\t\t单价\t\t库存");
        System.out.println("---------------------------------");
        int index = 1; // 编号
        for(Object o : goodsListJson) {
            // o : {...}
            String goodsJson = o.toString(); // {,,,}
            Goods goods = JSONUtil.JSON2Entitiy(goodsJson, Goods.class);
            String name = goods.getName(); // 名称
            String price = goods.getPrice() + ""; // 单价
            String num = goods.getNumber() + ""; // 库存
            
            //3.展示商品列表
            System.out.println(index + ".\t\t" + name + "\t\t" + price + "\t\t" + num);
            code2Goods.put(index + "", goods);
            index ++;
        }
    }
    
    /**
     * 查看商品详情
     * 通过数据ID获取数据，然后进行展示（需要重新访问数据库，显然不妥）
     *  or
     * 在展示商品的时候，把商品列表存储起来，然后，当选择商品编号时，就把对应商品展示出来
     *  Map<String, Goods> ： key --> 编号，value --> Goods对象
     */
     public void showGoodsDetail() {

    }

    /**
     * TODO 添加商品
     */

    /**
     * TODO 修改库存
     */

    /**
     * TODO 修改单价
     */

    /**
     * TODO 删除商品
     */
}
    
```



#### 2）代码实现

```java
package cn.butou.eshop.client;

import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.action.GoodsAction;
import cn.butou.eshop.goods.entity.Goods;
import jdk.swing.interop.SwingInterOpUtils;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

/**
 * 商品操作页面
 */
public class GoodsClient extends Client {
    private Goods currentGoods;
    
    Map<String, Goods> code2Goods =  new HashMap<>();
    
    /**
     * 商品管理首页
     *
     * 商品页面跳转控制器：
     *	本模块的操作由此方法控制跳转
     *	其他模块的操作返回上层，由Client控制跳转
     * @return 返回公共操作
     */
    public String index() {
        showGoodsList(); // 展示商品列表
        String result = userOperate("请根据序号查询商品详情", "L登录；");
    	
        while(true) {
            if(result.equals(LOGIN)) {
                return LOGIN;
            }
            if(result.equals(EXIT)) {
                return EXIT;
            }
            Goods goods = code2Goods.get(result); // get方法返回结果为数据或者null
            if(goods != null) { // 查看详情
                currentGoods = goods;
                showGoodsDetail();
                result = userOperate("提示用户进入下一步操作");
            } else {
                System.out.println("输入错误，请重新输入");
                result = userOperate("请根据序号查看商品详情", "L登录；");
            }
        }
    }
    
    /**
     * 展示商品列表
     * 1.向后台发送请求，获取商品数据
     * 2.解析响应消息字符串
     * 3.展示商品列表
     */
    public void showGoodsList() {
        // 1.向后台发送请求，获取商品数据
        GoodsAction goodsAction = new GoodsAction();
        String msgJSON = goodsAction.getGoodsList();
        
        // 2.解析响应消息字符串
        Msg msg = JSONUtil.JSON2Entity(msgJSON, Msg.class);
        Object obj = msg.getObj(); // 数据就存放在obj对象里
        List<?> goodsListJson = (List<?>) obj;
        
        System.out.println("【商品列表】");
        System.out.println("编号\t商品名称\t\t单价\t\t库存");
        System.out.println("---------------------------------");
        int index = 1; // 编号
        for (Object o : goodsListJson) {
            // o : {...}
            String goodsJson = o.toString(); // {,,,}
            Goods goods = JSONUtil.JSON2Entity(goodsJson, Goods.class);
            String name = goods.getName(); // 名称
            String price = goods.getPrice() + ""; // 单价
            String num = goods.getNumber() + ""; // 库存
            
            // 3. 展示商品列表
            System.out.println(index + ".\t\t" + name + "\t\t" + price + "\t\t" + num + "\t\t" + num);
            code2Goods.put(index + "", goods);
            index ++;
        }
    }
    
    /**
     * 查看商品详情
     * 通过数据ID获取数据，然后进行展示（需要重新访问数据库，显然不妥）
     * or
     * 在展示商品的时候，把商品列表存储起来，然后，当选择商品编号时，就把对应商品展示出来
     * 	Map<String, Goods> : key --> 编号，value --> Goods对象
     */
    public void showGoodsDetail() {
        System.out.println("【商品详情】");
        System.out.println("编号\t商品名称\t\t单价\t\t库存\t\t品牌");
        System.out.println("-------------------------------------");
        String name = currentGoods.getName(); // 名称
        String name = currentGoods.getPrice() + ""; // 单价
        String nun = currentGoods.getNumber() + ""; // 库存
        String brand = currentGoods.getBrand(); // 品牌
        
        // 3.展示商品列表
        System.out.println(1 + ".\t\t" + name + "\t\t" + price + "\t\t" + num + "\t\t" + brand);
    }
    
    /**
     * TODO 添加商品
     */
    
    /**
     * TODO 修改库存
     */
    
    /**
     * TODO 修改单价
     */
    
    /**
     * TODO 删除商品
     */
}
```



## 十一.购物车管理

### 1.添加购物车

#### 1）添加购物车实现思路：

Map<String, Integer>

​	key:		商品ID

​	value:     商品数量

```java
package cn.butou.eshop.client;

/**
 * 购物车操作页面
 */
public class CartClient extends Client {
    /**
     * 添加购物车
     *
     * 把当前正在操作的商品对象添加到购物车中
     * @return
     */
    public String addCart() {
        return null;
    }
}
```

```java
package cn.butou.eshop.cart.action;

import cn.butou.eshop.common.action.BaseAction;

import java.util.HashMap;
import java.util.Map;

/**
 * 购物车控制器类
 */
public class CartAction extends BaseAction {
    /**
     * 购物车对象
     * key：			商品ID;
     * value：		商品数量;
     */
    Map<String, Integer> cart = new HashMap<>();
    
    /**
     * 添加购物车
     *
     * 把数据存放到cart中
     * @return 返回成功或者失败的消息
     */
    public String addCart() {
        return null;
    }
}
```

```java
package cn.butou.eshop.client;

import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.action.GoodsAction;
import cn.butou.eshop.goods.entity.Goods;
import jdk.swing.interop.SwingInterOpUtils;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

/**
 * 商品操作页面
 */
public class GoodsClient extends Client {
    Map<String, Goods> code2Goods = new HashMap<>();
    
    /**
     * 商品管理首页
     *
     * 商品页面跳转控制器：
     * 	本模块的操作由此方法控制跳转
     *	其他模块的操作返回上层，由Client控制跳转
     * @return 返回公共操作
     */
    public String index() {
        showGoodsList(); // 展示商品列表
        String result = userOperate("请根据序号查看商品详情", "L登录；");
        
        while(true) {
            if(result.equals(LOGIN)) {
                return LOGIN;
            }
            if(result.equals(EXIT)) {
                return EXIT;
            }
            if(result.equals(INDEX)) {
                return INDEX;
            }
            Goods goods = code2Goods.get(result); // get方法返回结果为数据或者null
            if(goods != null) { // 查看详情
                currentGoods = goods;
                showGoodsDetail();
                result = userOperate("输入A加入购物车", "L登录；", "I首页；");
            } else if(result.equals(ADD)) { //加入购物车
                return CART;
            } else {
                System.out.println("输入错误，请重新输入");
                result = userOperate("请根据序号查看商品详情", "L登录；", "I首页；");
            }
        }
    }   
        
        /**
         * 展示商品列表
		* 1.向后台发送请求，获取商品数据
		* 2.解析响应消息字符串
		* 3.展示商品列表
		*/
        public void showGoodsList() {
            // 1.向后台发送请求，获取商品数据
            GoodsAction goodsAction = new GoodsAction();
            String msgJSON = goodsAction.getGoodsList();
            
            // 2.解析响应消息字符串
            Msg msg = JSONUtil.JSON2Entity(msgJSON, Msg.class);
            Object obj = msg.getObj(); // 数据就存放在obj对象里
            List<?> goodsListJson = (List<?>)obj;
            
            System.out.println("【商品列表】");
            System.out.println("编号\t商品名称\t\t单价\t\t库存");
            System.out.println("--------------------------------");
            int index = 1; //编号
            for(Object o : goodsListJson) {
                // o : {...}
                String goodsJson = o.toString(); // {,,,}
                Goods goods = JSONUtil.JSON2Entity(goodsJson, Goods.class);
                String name = goods.getName(); // 名称
                String price = goods.getPrice() + ""; // 单价
                String num = goods.getNumber() + ""; // 库存

                // 3.展示商品列表
                System.out.println(index + ".\t\t" + name + "\t\t" + price + "\t\t" + num + "\t\t" + brand);
                code2Goods.put(index + "", goods);
                index ++;
            }
        }
    
    /**
     * 查看商品详情
     * 通过数据ID获取数据，然后进行展示（需要重新访问数据库，显然不妥）
     * or
     * 在展示商品的时候，把商品列表存储起来，然后，当选择商品编号时，就把对应商品展示出来
     * 	Map<String, Goods> ：key --> 编号，value --> Goods对象
     */
    public void showGoodsDetail() {
        System.out.println("【商品详情】");
        System.out.println("编号\t商品名称\t\t单价\t\t库存\t\t品牌");
         System.out.println("------------------------------");
         String name = currentGoods.getName(); // 名称
         String price = currentGoods.getPrice() + ""; // 单价
         String num = currentGoods.getNumber() + ""; // 库存
         String brand = currentGoods.getBrand(); //品牌
         //3.展示商品列表
         System.out.println(1 + ".\t\t" + name + "\t\t" + price + "\t\t" + num + "\t\t" + brand);
    }
    
    /**
     * TODO 添加商品
     */

    /**
     * TODO 修改库存
     */

    /**
     * TODO 修改单价
     */

    /**
     * TODO 删除商品
     */
        
}

```

```java
package cn.butou.eshop.client;

import cn.butou.eshop.goods.entity.Goods;

import java.util.Arrays;
import java.util.Scanner;

/**
 * 客户端顶层父类
 * 处理公共的用户操作
 */
public class Client {
    /** 全局 用户操作 登录 */
    public static final String LOGIN = "L";
    /** 全局 用户操作 上一次操作记录 */
    public static final String HISTORY = "I";
    /** 全局 用户操作 首页 */
    public static final String INDEX = "I";
    /** 全局 用户操作 退出 */
    public static final String EXIT = "E";
    /** 全局 用户操作 添加 */
    public static final String ADD = "A";
    
    /** 全局 模块 购物车 */
    public static final String CART = "C";
    
    /** 当前正在操作的商品对象 */
    protected Goods currentGoods;
    
    protected Scanner sc = new Scanner(System.in);
    
    public static void main(String[] args) {
        Client c = new Client();
        c.start();
    }
    
    public void start() {
        GoodsClient goodsClient = new GoodsClient();
        UserClient userClient = new UserClient();
        
        String result = goodsClient.index(); // 返回商品模块用户录入的公共操作
        
        while(true) {
            if(result.equals(INDEX)) { // 首页
                result = goodsClient.index();
            } else if(result.equals(LOGIN)) { // 登录页面
                result = userClient.showLogin();
            } else if(result.equals(HISTORY)) { // 上一次操作页面
                result = HISTORY;
            } else if(result.equals(EXIT)) { // 退出
                System.exit(0);
            } else if(result.equals(CART)) { // 购物车模块
                // 进入购物车模块，添加商品到购物车
            } else {
                System.out.println("出错了。");
            }
        }
    }
    
    /**
     * 需求：创建公共的用户操作的方法
     * 主要功能：
     * 	1.提示用户信息和用户操作
     *		请根据编号进行操作（或 L登录；E退出）：
     *	2.接收用户的录入
     *		sc.nextLine()
     *	方法的分析：
     *		方法名：		userOperate
     *		返回值：		String
     *		参数列表：
     *			String msg;		用户信息
     *			String... oprs;  用户操作
     *				可变参数，本质是一个数组
     */
    public String userOperate(String msg, String... oprs) {
        // oprs == String[]
        String opr = Arrays.toString(oprs); // "[opr1, opr2, opr3]";
        opr = opr.substring(1, opr.lenght() - 1); // opr1, opr2, opr3;
        msg = msg + "或 " + opr + "；E退出）：";
        System.out.println(msg); // 请根据编号进行操作（或 L登录；E退出）
        return sc.nextLine().trim().toUpperCase(); // 去掉空格，转成大写
    }
}
```

#### 2）添加购物车代码实现（另外学习使用Debugged调试找出代码中的错误）

```java
package cn.butou.eshop.client;

import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.action.GoodsAction;
import cn.butou.eshop.goods.entity.Goods;
import jdk.swing.interop.SwingInterOpUtils;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

/**
 * 商品操作页面
 */
public class GoodsClient extends Client {
    Map<String, Goods> code2Goods = new HashMap<>();
    
    /**
     * 商品管理首页
     *
     * 商品页面跳转控制器：
     *	本模块的操作由此方法控制跳转
     *	其他模块的操作返回上层，由Client控制跳转
     * @return 返回公共操作
     */
    public String index() {
        showGoodsList(); // 展示商品列表
        String result = userOperate("请根据序号查看商品详情", "L登录；");
        
        while(true) {
            if(result.equals(LOGIN)) {
                return LOGIN;
            }
            if(result.equals(EXIT)) {
                return EXIT;
            }
            if(result.equals(INDEX)) {
                return INDEX;
            }
            Goods goods = code2Goods.get(result); // get方法返回结果为数据或者null
            if(goods != null) { // 查看详情
                currentGoods = goods;
                showGoodsDetail();
                result = userOperate("输入A加入购物车", "L登录；", "I首页；");
            } else if(result.equals(ADD)) { // 加入购物车
                return ADD;
            } else {
                System.out.println("输入错误，请重新输入");
                result = userOperate("请根据序号查看商品详情", "L登录；", "I首页；");
            }
        }
    }
    /**
     * 展示商品列表
     * 1.向后台发送请求，获取商品数据
     * 2.解析响应消息字符串
     * 3.展示商品列表
     */
    public void showGoodsList() {
        // 1.向后台发送请求，获取商品数据
        GoodsAction goodsAction = new GoodsAction();
        String msgJSON = goodsAction.getGoodsList();

        // 2.解析响应消息字符串
        Msg msg = JSONUtil.JSON2Entity(msgJSON, Msg.class);
        Object obj = msg.getObj(); // 数据就存放在obj对象里：[{},{},{}]
        List<?> goodsListJson = (List<?>) obj;

        System.out.println("【商品列表】");
        System.out.println("编号\t商品名称\t\t单价\t\t库存");
        System.out.println("------------------------------");
        int index = 1; //编号
        for (Object o : goodsListJson) {
            // o : {...}
            String goodsJson = o.toString(); // {,,,}
            Goods goods = JSONUtil.JSON2Entity(goodsJson, Goods.class);
            String name = goods.getName(); // 名称
            String price = goods.getPrice() + ""; // 单价
            String num = goods.getNumber() + ""; // 库存

            // 3.展示商品列表
            System.out.println(index + ".\t\t" + name + "\t\t" + price + "\t\t" + num);
            code2Goods.put(index + "", goods);
            index ++;
        }
    }

    /**
     * 查看商品详情
     * 通过数据ID获取数据，然后进行展示（需要重新访问数据库，显然不妥）
     *  or
     * 在展示商品的时候，把商品列表存储起来，然后，当选择商品编号时，就把对应商品展示出来
     *  Map<String, Goods> ： key --> 编号，value --> Goods对象
     */
     public void showGoodsDetail() {
         System.out.println("【商品详情】");
         System.out.println("编号\t商品名称\t\t单价\t\t库存\t\t品牌");
         System.out.println("------------------------------");
         String name = currentGoods.getName(); // 名称
         String price = currentGoods.getPrice() + ""; // 单价
         String num = currentGoods.getNumber() + ""; // 库存
         String brand = currentGoods.getBrand(); //品牌
         //3.展示商品列表
         System.out.println(1 + ".\t\t" + name + "\t\t" + price + "\t\t" + num + "\t\t" + brand);
     }

    /**
     * TODO 添加商品
     */

    /**
     * TODO 修改库存
     */

    /**
     * TODO 修改单价
     */

    /**
     * TODO 删除商品
     */
}
```

```java
package cn.butou.eshop.client;

import cn.butou.eshop.goods.entity.Goods;

import java.util.Arrays;
import java.util.Scanner;

/**
 * 客户端顶层父类
 * 处理公共的用户操作
 */
public class Client {
    /** 全局 用户操作 登录 */
    public static final String LOGIN = "L";
    /** 全局 用户操作 上一次操作记录 */
    public static final String HISTORY = "I";
    /** 全局 用户操作 首页 */
    public static final String INDEX = "I";
    /** 全局 用户操作 退出 */
    public static final String EXIT = "E";
    /** 全局 用户操作 添加 */
    public static final String ADD = "A";

    /** 全局 模块 购物车 */
    public static final String CART = "C";

    /** 当前正在操作的商品对象 */
    protected Goods currentGoods;

    protected Scanner sc = new Scanner(System.in);


    public static void main(String[] args) {
        Client c = new Client();
        c.start();
    }

    /**
     * Debug调试
     * 1.在可能出现问题的代码行前加上断点
     * 2.以Debug模式运行
     *  F8 --> 单步执行
     *  F7 --> 进入方法
     *  Shift + F8 --> 执行完毕方法
     *  F9 --> 执行到下一个断点
     */
    public void start() {
        GoodsClient goodsClient = new GoodsClient();
        UserClient userClient = new UserClient();
        CartClient cartClient = new CartClient();

        String result = goodsClient.index(); // 返回商品模块用户录入的公共操作

        while (true) {
            if(result.equals(INDEX)) { // 首页
                result = goodsClient.index();
            } else if(result.equals(LOGIN)) { // 登录页面
                result = userClient.showLogin();
            } else if(result.equals(HISTORY)) { // 上一次操作页面
                result = HISTORY;
            } else if(result.equals(EXIT)) { // 退出
                System.exit(0);
            } else if(result.equals(ADD)) { // 添加到购物车
                // 添加商品到购物车
                cartClient.addCart();
            } else if (result.equals(CART)) { // 去购物车
                // 进入购物车模块
                // cartClient.showCart();
            } else {
                System.out.println("出错了。");
            }
        }
    }

    /**
     * 需求：创建公共的用户操作的方法
     * 主要功能：
     *  1.提示用户信息和用户操作
     *      请根据编号进行操作（或 L登录；E退出）：
     *  2.接收用户的录入
     *      sc.nextLine()
     *  方法的分析：
     *      方法名：    userOperate
     *      返回值：    String
     *      参数列表：
     *          String msg; 用户信息
     *          String... oprs; 用户操作
     *              可变参数，本质是一个数组
     */
    public String userOperate(String msg, String... oprs) {
        // oprs == String[]
        String opr = Arrays.toString(oprs); // "[opr1, opr2, opr3]"
        opr = opr.substring(1, opr.length() - 1); // opr1, opr2, opr3
        msg = msg + "或 " + opr + "；E退出）：";
        System.out.println(msg); // 请根据编号进行操作（或 L登录；E退出）：
        return sc.nextLine().trim().toUpperCase(); // 去掉空格，转成大写
    }
}
```

```java
package cn.butou.eshop.client;

import cn.butou.eshop.cart.action.CartAction;
import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;

/**
* 购物车操作页面
*/
public class CartClient extends Client {
    CartAction cartAction = new CartAction();
    /**
     * 添加购物车
     *
     * 把当前正在操作的商品对象添加到购物车中
     * 1.把currentGoods对象发送请求到CartAction
     * 2.接收Action的响应消息
     * @return
     */
    public String addCart() {
        // 1.把currentGoods对象发送请求到CartAction
        cartAction.setGoods(currentGoods); 
        /*	注意：这里的currentGoods为cartClient这个对象自己的currentGoods属性
        	与goodsClient中的currentGoods属性不为同一个，由于之前只给了goodsClient的currentGoods赋值，
        	因此这里的currentGoods为null，cartAction里的goods也被设置为null.
        */
        // 2.接收Action的响应消息
        String msgJson = cartAction.addCart();
        Msg msg = JSONUtil.JSON2Entity(msgJson, Msg.class);
        if(msg.getType().equals(Msg.SUCCESS)) {
            System.out.println("添加购物车成功");
        } else {
            System.out.println(msg.getMsg());
        }
        
        return userOperate("请选择操作", "I继续浏览", "C购物车", "L登录");
    }
}
```

```java
package cn.butou.eshop.cart.action;

import cn.butou.eshop.common.action.BaseAction;
import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.entity.Goods;

import java.util.HashMap;
import java.util.Map;

/**
 * 购物车控制器类
 */
public class CartAction extends BaseAction {
    private Goods goods;
    
    /**
     * 购物车对象
     * key：		商品ID;
     * value：	商品数量;
     */
    Map<String, Integer> cart = new HashMap<>();
    
    /**
     * 添加购物车
     *
     * 把数据存放到cart中
     * 1.如果购物车已存在该商品，把数量 +1
     * 2.如果不存在，则放进去数字1
     * @return 返回成功或者失败的消息
     */
    public String addCart() {
        Msg msg = new Msg();
        try {
            Integer num = cart.get(goods.getId()); // 由于goods为null,这里catch到空指针异常, 直接走catch
            if(num != null && num > 0) {
                cart.put(goods.getId(), num + 1);
            } else {
                cart.put(goods.getId(), 1);
            }
            msg.setType(Msg.SUCCESS);
        } catch (Exception e) {
            msg.setType(Msg.FAIL);
            msg.setMsg("服务器异常");
        }
        return JSONUtil.entity2JSON(msg);
    }
    
    public Goods getGoods() {return goods};
    
    public void setGoods(Goods goods) {
        this.goods = goods;
    }
}
```

通过Debugged调试，发现了问题：

```
/**
 * 首先, currentGoods这个属性在父类Client中，定义为 protected currentGoods.
 * 每new一个对象，新的对象都会具有一个自己独有的currentGoods.
 *
 * GoodsClient对象goodsClient中：
 *  currentGoods 肯定是有值的
 *  这里的赋值操作，仅仅是对GoodsClient对象goodsClient的属性currentGoods赋值
 *  CartClient对象cartClient里面的属性currentGoods并没有被赋值.
 * CartClient对象cartClient中：
 *  currentGoods 没有值
 *  CartClient在创建对象的时候，currentGoods是null
 *
 * 因此，为了解决多客户端（xxxClient）要共享数据（例如这里CLient中的currentGoods）
 * 可以将Client中的currentGoods加上static修饰符，使之变成类共有的唯一变量
 * 
 * 想想可以直接用super.属性名吗，自己思考了一下，觉得如果层级多了，调用起来会很麻烦，效率也不知道如何。
 */
```

### 二.展示购物车

#### 1）展示购物车实现思路：

1.创建购物车商品实体类CartGoods

```java
package cn.butou.eshop.cart.entity;

import cn.butou.eshop.goods.entity.Goods;

/**
 * 购物车中展示商品实体类
 */
public class CartGoods extends Goods {
    // 商品数量
    private int goodsNum;
    
    public int getGoodsNum() {
        return goodsNum;
    }
    
    public void setGoodsNum(int goodsNum) {
        this.goodsNum = goodsNum;
    }
}
```

CartAction：

1.获取购物车中所有商品IDs，并转成字符串，用逗号隔开

2.通过GoodsService对象获取对应的商品列表

3.将Goods对象转成CartGoods对象

4.将CartGoods对象封装成消息响应给客户端

CartClient：

1.向后台发送请求

2.解析响应字符串

3.展示购物车列表

#### 2）代码实现：

```java
package cn.butou.eshop.cart.action;

import cn.butou.eshop.cart.entity.CartGoods;
import cn.butou.eshop.common.action.BaseAction;
import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.entity.Goods;
import cn.butou.eshop.goods.service.GoodsService;
import cn.butou.eshop.goods.service.impl.GoodsServiceImpl;

import java.util.*;

/**
 * 购物车控制器类
 */
public class CartAction extends BaseAction {
    private Goods goods;
    private GoodsService goodsService;
    
    /**
     * 购物车对象
     * key：		商品ID;
     * value：	商品数量;
     */
    Map<String, Integer> cart = new HashMap<>();
    
    public CartAction() {
        goodsService = new GoodsSeriviceImpl();
    }
    
    /**
     * 添加购物车
     *
     * 把数据存放到cart中
     * 1.如果购物车中已存在该商品，把数量 +1
     * 2.如果不存在，则放进去数字1
     * @return 返回成功或者失败的消息
     */
    public String addCart() {
        Msg msg = new Msg();
        try {
            Integer num = cart.get(goods.getId());
            if(num != null && num > 0) {
                cart.put(goods.getId(), num + 1);
            } else {
                cart.put(goods.getId(), 1);
            }
            msg.setType(Msg.SUCCESS);
        } catch (Exception e) {
            msg.setType(Msg.FAIL);
            msg.setMsg("服务器异常");
        }
        return JSONUtil.entity2JSON(msg);
    }
    
    /**
     * 展示购物车
     * 1.获取购物车所有商品IDs，并转成字符串，用逗号隔开
     * 2.通过GoodsService对象获取对应的商品列表
     * 3.将Goods对象转成CartGoods对象
     * 4.封装到Msg对象并返回
     * @return
     */
    public String showCart() {
		Msg msg = new Msg();
        try {
            // 购物车中所有商品IDs
            String ids = Arrays.toString(cart.keySet().toArray()); // [id1, id2, id3]
        	
            //GoodsService的getGoodsList(ids)方法
            List<Goods> goodsList = goodsService.getGoodsList(ids);
            List<CartGoods> cgList = cgList = new ArrayList<>();
            for(Goods g : goodsList) {
                CartGoods cg = new CartGoods();
                cg.setId(g.getId()); // id
                cg.setGoodsNum(cart.get(g.getId())); // 数量
                cg.setName(g.getName()); // 名称
                cg.setPrice(g.getPrice()); // 单价
                cgList.add(cg);
            }
            msg.setType(Msg.SUCCESS);
            msg.setObj(cgList);
        } catch (Exception e) {
            msg.setType(Msg.FAIL);
            msg.setMsg(e.getMessage());
        }
        return JSONUtil.entity2JSON(msg);
    }
    
    public Goods getGoods() {
        return goods;
    }

    public void setGoods(Goods goods) {
        this.goods = goods;
    }
}
```

```java
package cn.butou.eshop.goods.serivce;

import cn.butou.eshop.common.service.BaseService;
import cn.butou.eshop.goods.entity.Goods;

import java.util.List;

/**
 * 商品服务层
 * 处理商品模块的相关业务
 */
public interface GoodsService extends BaseService {
    public List<Goods> getGoodsList() throws Exception;
    public List<Goods> getGoodsList(String ids) throws Exception;
    public Goods getGoodsDetail() throws Exception;
}
```

```java
package cn.butou.eshop.goods.service.impl;
import cn.butou.eshop.common.service.BaseService;
import cn.butou.eshop.common.service.impl.BaseServiceImpl;
import cn.butou.eshop.goods.dao.GoodsDAO;
import cn.butou.eshop.goods.dao.impl.GoodsDAOimpl;
import cn.butou.eshop.goods.entity.Goods;
import cn.butou.eshop.goods.service.GoodsService;

import java.util.ArrayList;
import java.util.List;

/**
 * 商品服务层接口的实现类
 */
public class GoodsServiceImpl extends BaseServiceImpl implements GoodsService {
    private GoodsDAO goodsDAO;
    
    public GoodsServiceImpl(){ goodsDAO = new GoodsDAOimpl();}
    
    /**
     * 获取商品列表
     * 1.调用GoodsDAO对象的方法获取数据并返回
     * @return 商品列表
     * @throws Exception
     */
    @Override
    public List<Goods> getGoodsList() throws Exception {
        return goodsDAO.getEntityList();
    }
    
    /**
     * 根据商品ID获取商品对象列表
     * @param ids 商品id，多个用逗号隔开
     * @return 返回商品列表
     * @throws Exception
     */
    
    @Override
    public List<Goods> getGoodsList(String ids) throws Exception {
        List<Goods> goodsList = new ArrayList<>();
        List<Goods> allGoodsList = getGoodsList();
        for (Goods goods : allGoodsList) {
            String id = goods.getId();
            if(ids.contains(id)) {
                goodsList.add(goods);
            }
        }
        return goodsList;
    }
    
    /**
     * 获取商品详情
     *
     * 1.根据商品ID获取商品对象
     * 2.若该对象存在则返回，否则返回null
     * @return Goods对象，或null
     * @throws Exception
     */
    @Override
    public Goods getGoodsDetail() throws Exception {
        return null;
    }
}
```



```java
package cn.butou.eshop.client;

import cn.butou.eshop.cart.action.CartAction;
import cn.butou.eshop.cart.entity.CartGoods;
import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.entity.Goods;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

/**
 * 购物车操作页面
 */
public class CartClient extends Client {
    private String cartAmount;
    
    Map<Integer, Goods> code2Goods;
    CartAction cartAction = new CartAction();
    
    /**
     * 添加购物车
     *
     * 把当前正在操作的商品对象添加到购物车中
     * 1.把currentGoods对象发送请求到CartAction
     * 2.接收Action的响应消息
     * @return
     */
    public String addCart() {
        // 1.把currentGoods对象发送请求到CartAction
        cartAction.setGoods(currentGoods);
        // 2.接收Action的响应消息
        String msgJson = cartAction.addCart();
        Msg msg = JSONUtil.JSON2Entity(msgJson, Msg.class);
        if(msg.getType().equals(Msg.SUCCESS)) {
            System.out.println("添加购物车成功");
        } else {
            System.out.println("msg.getMsg()");
        }
        return userOperate("请选择操作", "I继续浏览", "C购物车", "L登录");
    }
    
    /**
     * 展示购物车列表
     * 1.向后台发送请求，获取商品数据
     * 2.解析响应消息字符串
     * 3.展示购物车列表
     * @return
     */
    public String showCart() {
        System.out.println("\n【我的购物车】");
        System.out.println("编号\t商品名称\t\t单价\t\t数量");
        
        // 1.向后台发送请求，获取商品数据
        String result = cartAction.showCart();
        Msg msg = JSONUtil.JSON2Entity(result, Msg.class);
        
        // 2.解析响应消息字符串
        List<?> cartGoodsList = (List<?>)msg.getObj(); // 将得到的普通对象转换为购物车商品列表(普通列表)
        int i = 1; // 序号
        double sum = 0; // 总金额
        code2Goods = new HashMap<>(); // 将展示编号和数据ID关联起来
        
        for(Object obj : cartGoodsList) {
            String json = obj.toString();
            CartGoods cartGoods = JSONUtil.JSON2Entity(json, CartGoods.class);
            int num = cartGoods.getGoodsNum(); // 商品数量
            String name = cartGoods.getName(); // 商品名称
            double price = cartGoods.getPrice(); // 商品单价
            System.out.println(i + "." + "\t" + name + "\t\t\t"
                        + price + "\t\t" + num);
            sum += price * num; //BigDecimals
            code2Goods.put(i++, cartGoods);
        }
        this.setCartAmount(sum + "");
        System.out.println("总金额：" + sum);
        
        return userOperate("请根据序号选择操作", "I去凑单", "L登录 ", "o去结算 ");
    }
    
    public String getCartAmount() {
        return cartAmount;
    }

    public void setCartAmount(String cartAmount) {
        this.cartAmount = cartAmount;
    }
}
```



## 十二.订单管理



### 1.生成订单代码

```java
package cn.butou.eshop.client;

import cn.butou.eshop.cart.action.CartAction;
import cn.butou.eshop.cart.entity.CartGoods;
import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.entity.Goods;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

/**
 * 购物车操作页面
 */
public class CartClient extends Client {
    CartAction cartAction = new CartAction();
    
    // 购物车总金额
    private String cartAmount;
    
    /** 数字编号和商品ID映射表Map（key：数字编号；value：商品ID）*/
    Map<Integer, Goods> code2Goods;
    
    public String index() {
        // 展示购物车商品列表
        String result = showCart();
        while(true) {
            if(result.equals(LOGIN)) { // 全局操作 登录
                // 直接返回上层Client
                return LOGIN;
            }
            if(result.equals(EXIT)) {
                return EXIT;
            }
            if(result.equals(INDEX)) {
                return INDEX;
            }
            if(result.equals(ORDER)) { // 去结算
                return ORDER;
            } else {
                System.out.println("输入错误，请重新输入");
                result = userOperate("请根据序列号选择操作", "I去凑单 ", "L登录 ", "o去结算 ");
            }
        }
    }
    
    /**
     * 添加购物车
     *
     * 把当前正在操作的商品对象添加到购物车中
     * 1.把currentGoods对象发送请求到CartAction
     * 2.接收Action的响应消息
     * @return
     */
    public String addCart() {
        // 1.把currenGoods对象发送请求到CartAction
        cartAction.setGoods(currentGoods);
        // 2.接收Action的响应消息
        String msgJson = cartAction.addCart();
        Msg msg = JSONUtil.JSON2Entity(msgJson, Msg.class);
        if(msg.getType().equals(Msg.SUCCESS)) {
            System.out.println("添加购物车成功");
        } else {
            System.out.println(msg.getMsg);
        }
        return userOperate("请选择操作", "I继续浏览 ", "C购物车 ", "L登录 ");
    }
    
    /**
     * 展示购物车列表
     * 1.向后台发送请求，获取商品数据
     * 2.解析响应字符串
     * 3.展示购物车列表
     * @return
     */
    public String showCart() {
        System.out.println("\n【我的购物车】");
        System.out.println("编号\t商品名称\t\t单价\t\t数量");

        // 1.向后台发送请求，获取商品数据
        String result = cartAction.showCart();
        Msg msg = JSONUtil.JSON2Entity(result, Msg.class);

        // 2.解析响应消息字符串
        List<?> cartGoodsList = (List<?>)msg.getObj(); // 将得到的普通对象转换为购物车商品列表
        int i = 1; // 序号
        double sum = 0; // 总金额
        code2Goods = new HashMap<>(); // 将展示编号和数据ID关联起来
        for (Object obj : cartGoodsList) {
                String json = obj.toString();
                CartGoods cartGoods = JSONUtil.JSON2Entity(json, CartGoods.class);
                int num = cartGoods.getGoodsNum(); // 商品数量
                String name = cartGoods.getName(); // 商品名称
                double price = cartGoods.getPrice(); // 商品单价
                System.out.println(i + "." + "\t" + name + "\t\t\t"
                        + price + "\t\t" + num);
                sum += price * num; //BigDecimal
                code2Goods.put(i++, cartGoods);
         }
            
         this.setCartAmount(sum + "");
         System.out.println("总金额：" + sum);

         return userOperate("请根据序号选择操作", "I去凑单 ", "L登录 ", "o去结算 ");
    }
    public String getCartAmount() {
          return cartAmount;
    }

    public void setCartAmount(String cartAmount) {
          this.cartAmount = cartAmount;
    }
    
    
}
```

```java
package cn.butou.eshop.client;

import cn.butou.eshop.goods.entity.Goods;

import java.text.SimpleDateFormat;
import java.util.Arrays;
import java.util.Scanner;

/**
 * 客户端顶层父类
 * 处理公共的用户操作
 */
public class Client {

    /** 全局 用户操作 登录 */
    public static final String LOGIN = "L";
    /** 全局 用户操作 上一次操作记录 */
    public static final String HISTORY = "I";
    /** 全局 用户操作 首页 */
    public static final String INDEX = "I";
    /** 全局 用户操作 退出 */
    public static final String EXIT = "E";
    /** 全局 用户操作 添加 */
    public static final String ADD = "A";

    /** 全局 用户操作 去结算（订单模块） */
    public static final String ORDER = "O";

    /** 全局 模块 购物车 */
    public static final String CART = "C";

    /** 当前正在操作的商品对象 */
    protected static Goods currentGoods;

    protected Scanner sc = new Scanner(System.in);
    protected SimpleDateFormat sdf = new SimpleDateFormat("h:mm a");

    public static void main(String[] args) {
        Client c = new Client();
        c.start();
    }

    /**
     * Debug调试
     * 1.在可能出现问题的代码行前加上断点
     * 2.以Debug模式运行
     *  F8 --> 单步执行
     *  F7 --> 进入方法
     *  Shift + F8 --> 执行完毕方法
     *  F9 --> 执行到下一个断点
     */
    public void start() {
        GoodsClient goodsClient = new GoodsClient();
        UserClient userClient = new UserClient();
        CartClient cartClient = new CartClient();
        OrderClient orderClient = new OrderClient();

        String result = goodsClient.index(); // 返回商品模块用户录入的公共操作

        while (true) {
            if(result.equals(INDEX)) { // 首页
                result = goodsClient.index();
            } else if(result.equals(LOGIN)) { // 登录页面
                result = userClient.showLogin();
            } else if(result.equals(HISTORY)) { // 上一次操作页面
                result = HISTORY;
            } else if(result.equals(EXIT)) { // 退出
                System.exit(0);
            } else if(result.equals(ADD)) { // 添加到购物车
                result = cartClient.addCart();
            } else if (result.equals(CART)) { // 去购物车
                result = cartClient.index();
            } else if (result.equals(ORDER)) { // 去结算
                result = orderClient.index();
            } else {
                System.out.println("出错了。");
            }
        }
    }

    /**
     * 需求：创建公共的用户操作的方法
     * 主要功能：
     *  1.提示用户信息和用户操作
     *      请根据编号进行操作（或 L登录；E退出）：
     *  2.接收用户的录入
     *      sc.nextLine()
     *  方法的分析：
     *      方法名：    userOperate
     *      返回值：    String
     *      参数列表：
     *          String msg; 用户信息
     *          String... oprs; 用户操作
     *              可变参数，本质是一个数组
     */
    public String userOperate(String msg, String... oprs) {
        // oprs == String[]
        String opr = Arrays.toString(oprs); // "[opr1, opr2, opr3]"
        opr = opr.substring(1, opr.length() - 1); // opr1, opr2, opr3
        msg = msg + "或 " + opr + "；E退出）：";
        System.out.println(msg); // 请根据编号进行操作（或 L登录；E退出）：
        return sc.nextLine().trim().toUpperCase(); // 去掉空格，转成大写
    }
}

```

```java
package cn.butou.eshop.client;

import cn.butou.eshop.common.entity.Entity;
import cn.butou.eshop.order.entity.Order;

import java.util.Date;

/**
 * 订单操作页面
 */
public class OrderClient extends Client{

    /* 当前操作订单对象 */
    private Order currentOrder;

    /**
     * 订单管理页面
     * 生成订单：
     *  条件：
     *      1.购物车中有数据
     *      2.已登录
     *      3.录入收货人信息
     *  结果：
     *      封装Order对象
     *      订单状态为：待支付
     *      清空购物车
     * @return
     */
    public String index() {
        // TODO 登录验证

        generateOrder();
        return userOperate("请选择操作", "p去支付");
    }

    /**
     * 生成订单
     *  1.填写订单信息
     *  2.封装成Order对象
     *  3.生成订单 --> 待支付状态
     */
    public void generateOrder() {
        CartClient cartClient = new CartClient();
        /* 填写订单信息 */
        System.out.println("----------正在生成订单----------");

        System.out.println("请输入收货人：");
        String consignee = sc.nextLine();
        System.out.println("请输入收获地址：");
        String consigneeAddress = sc.nextLine();
        System.out.println("请输入联系电话：");
        String phone = sc.nextLine();

        /* 生成订单 --> 待支付状态 */
        currentOrder = new Order();
        currentOrder.setId(Entity.getUUID()); // 订单ID
        currentOrder.setCreateTime(sdf.format(new Date())); // 订单生成日期
        currentOrder.setAmount(cartClient.getCartAmount()); // 订单总金额
        currentOrder.setGetConsigneeAddress(consigneeAddress); // 收货地址
        currentOrder.setConsignee(consignee); // 收货人
        currentOrder.setPhone(phone); // 收货人手机号
        String serialNumber = getSerialNumber();
        currentOrder.setSerialNumber(serialNumber); // 订单序列号
        currentOrder.setState(Order.WAITING_PAY); // 待支付

        System.out.println("-------------- 订单已生成 -------------\n订单号: \t" + serialNumber
                + " \n总金额：\t" + cartClient.getCartAmount() + "\n状态：\t待支付。");
    }

    /**
     * 查看订单详情
     * TODO 后台查询数据
     *      查看当前订单数据
     *      查询历史订单数据
     */
}

```

```java
package cn.butou.eshop.order.entity;

import cn.butou.eshop.common.entity.Entity;

/**
 * 订单模块的实体类，用于描述订单的基本信息
 */
public class Order extends Entity {
    /* 订单状态 待支付 */
    public static final String WAITING_PAY = "WAITING_PAY";
    /* 订单状态 代发货 */
    public static final String WAITING_SEND = "WAITING_SEND";
    /* 订单状态 待收货 */
    public static final String WAITING_RECEIVE = "WAITING_RECEIVE";
    /* 订单状态 已完成 */
    public static final String COMPLETED = "COMPLETED";
    /* 订单状态 已取消 */
    public static final String CANCELLED = "CANCELLED";

    /* 订单序列号 根据当前系统日期生成 */
    private String serialNumber;
    /* 收货人 */
    private String consignee;
    /* 收货地址 */
    private String getConsigneeAddress;
    /* 联系电话 */
    private String phone;
    /* 订单金额 */
    private String amount;
    /* 订单状态
     * 待付款：订单生成之后，立即进入待付款状态
     *      支付完成后，进入支付完成状态，之后需要商家发货
     * 待收货：商家发货之后，进入发货状态
     * 已完成：客户查收商品，进入已完成状态
     * 已取消：订单生成后，任意环节都有可能取消该订单（也可以超时后，系统自动取消）
     *
     */
    private String state;

    public String getSerialNumber() {
        return serialNumber;
    }

    public void setSerialNumber(String serialNumber) {
        this.serialNumber = serialNumber;
    }

    public String getConsignee() {
        return consignee;
    }

    public void setConsignee(String consignee) {
        this.consignee = consignee;
    }

    public String getGetConsigneeAddress() {
        return getConsigneeAddress;
    }

    public void setGetConsigneeAddress(String getConsigneeAddress) {
        this.getConsigneeAddress = getConsigneeAddress;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public String getAmount() {
        return amount;
    }

    public void setAmount(String amount) {
        this.amount = amount;
    }

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }
}

```



### 2.生成订单前验证登录

```java
package cn.butou.eshop.client;

import cn.butou.eshop.common.entity.Entity;
import cn.butou.eshop.order.entity.Order;
import cn.butou.eshop.user.action.UserAction;
import cn.butou.eshop.user.entity.User;

import java.util.Date;

/**
 * 订单操作页面
 */
public class OrderClient extends Client {
    /* 当前操作订单对象 */
    private Order currentOrder;
    
    /** 
     * 订单管理页面
     * 生成订单：
     * 	条件：
     *		1.购物车中有数据
     *		2.已登录
     *		3.录入收货人信息
     *	结果：
     *		封装Order对象
     *		订单状态为：待支付
     *		清空购物车
     * @return
     */
    public String index() {
        UserAction userAction = new UserAction();
        if(userAction.getLoginUser() != null) {
            generateOrder();
            return userOperate("请选择操作", "p去支付");
        } else {
            return LOGIN;
        }
    }
    
    /** 
     * 生成订单
     * 	1.填写订单信息
     *	2.封装成Order对象
     *	3.生成订单 --> 待支付状态
     */
    public void generateOrder() {
        CartClient cartClient = new CartClient();
        /* 填写订单信息 */
        System.out.println("---------正在生成订单----------");
        
        System.out.println("请输入收货人：")；
        String consignee = sc.nextLine();
        System.out.println("请输入收货地址：");
        String consigneeAddress = sc.nextLine();
        System.out.println("请输入联系电话：");
        String phone = sc.nextLine();
        
        /* 生成订单 --> 待支付状态 */
        currentOrder = new Order();
        currentOrder.setId(Entity.getUUID()); // 订单ID
        currentOrder.setCreateTime(sdf.formate(new Date())); // 订单生成日期
        currentOrder.setAmount(cartClient.getCartAmount()); // 订单总金额
        currentOrder.setGetConsigneeAddress(consigneeAddress); // 收货地址
        currentOrder.setConsignee(consignee); // 收货人
        currentOrder.setPhone(phone); // 收货人手机
        String serialNumber = getSerialNumber();
        currentOrder.setSerialNumber(serialNumber); // 订单序列号
        currentOrder.setState(Order.WAITING_PAY); // 待支付
        
        System.out.println("----------订单已生成----------\n订单号: \t" + serialNumber
                + " \n总金额：\t" + cartClient.getCartAmount() + "\n状态：\t待支付。");
    }
    
    /**
     * TODO 获取订单序列号
     */
    public String getSerialNumber() {
        return "TODO 获取订单序列号";
    }

    /**
     * 查看订单详情
     * TODO 后台查询数据
     *      查看当前订单数据
     *      查询历史订单数据
     */
}
```

```java
package cn.butou.eshop.user.action;

import cn.butou.eshop.common.action.BaseAction;
import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.log.dao.ISysLog;
import cn.butou.eshop.log.dao.impl.ConsoleLog;
import cn.butou.eshop.user.entity.User;
import cn.butou.eshop.user.service.UserService;
import cn.butou.eshop.user.service.impl.UserServiceImpl;

/**
 * 用户控制器类
 * 处理所有用户的后台操作，并返回JSON格式的字符串消息
 */
public class UserAction extends BaseAction {
    // 用户名
    private String username;
    // 密码
    private String password;

    /**
     * 用户登录功能
     * 1.封装数据到User对象
     * 2.调用UserService处理逻辑
     *  User login(User user) throws Exception;
     * 3.异常处理
     * 4.根据服务层返回结果生成消息
     * 5.记录日志（待开发）
     * 6.响应消息到客户端
     * @return
     */
    public String login() {
        Msg msg = new Msg();
        try {
            // 1.封装数据到User对象
            User user = new User();
            user.setUsername(username);
            user.setPassword(password);

            // 2.调用UserService处理逻辑
            //    User login(User user) throws Exception;
            UserService userService = new UserServiceImpl();
            user = userService.login(user);

            // 3.异常处理

            //4.根据服务层返回结果生成消息
            //          消息实体类Msg
            if(user != null) {
                // 把当前登录用户对象放到上下文对象中
                context.put(LOGIN_USER, user);
                msg.setType(Msg.SUCCESS); // 登录成功
                msg.setMsg("登录成功");
                // 5.记录日志（待开发）
                log.info(username + "已登录");
            } else {
                msg.setType(Msg.FAIL); // 登录失败
                msg.setMsg("用户名或密码不正确");
            }
            return JSONUtil.entity2JSON(msg);
        } catch(Exception e) {
            e.printStackTrace();
            msg.setType(Msg.FAIL); // 登录失败
            msg.setMsg("服务器异常");
            return JSONUtil.entity2JSON(msg);

        }

    }

    /**
     * 获取当前登录用户对象
     * @return 返回用户对象，或者null
     */
    public User getLoginUser(){
        Object obj = context.get(LOGIN_USER);
        if(obj != null) {
            return (User)obj;
        }
        return null;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}

```

```java
package cn.butou.eshop.common.action;

import cn.butou.eshop.log.dao.ISysLog;
import cn.butou.eshop.log.dao.impl.ConsoleLog;

import java.util.HashMap;
import java.util.Map;

/**
 * Action，控制器类的基类
 * 1.封装请求数据
 * 2.校验权限
 * 3.调用服务层（Service)处理业务逻辑
 * 4.日志的记录
 * 5.返回消息到客户端
 */
public class BaseAction {

    /** 上下文对象的key 登录用户 */
    public static final String LOGIN_USER = "LOGIN_USER";

    /** 上下文对象 用来存储所有Action类的公共的信息 */
    protected static final Map<String, Object> context = new HashMap<>();

    protected ISysLog log = new ConsoleLog();

    //TODO 日志备份TxtLog
}

```

```java
package cn.butou.eshop.client;

import cn.butou.eshop.goods.entity.Goods;

import java.text.SimpleDateFormat;
import java.util.Arrays;
import java.util.Scanner;

/**
 * 客户端顶层父类
 * 处理公共的用户操作
 */
public class Client {

    /** 全局 用户操作 登录 */
    public static final String LOGIN = "L";
    /** 全局 用户操作 上一次操作记录 */
    public static String HISTORY = "I";
    /** 全局 用户操作 首页 */
    public static final String INDEX = "I";
    /** 全局 用户操作 退出 */
    public static final String EXIT = "E";
    /** 全局 用户操作 添加 */
    public static final String ADD = "A";

    /** 全局 用户操作 去结算（订单模块） */
    public static final String ORDER = "O";

    /** 全局 模块 购物车 */
    public static final String CART = "C";

    /** 当前正在操作的商品对象 */
    protected static Goods currentGoods;

    /** Scanner扫描器对象，从控制台录入 */
    protected Scanner sc = new Scanner(System.in);
    /** 日期格式化对象 */
    protected SimpleDateFormat sdf = new SimpleDateFormat("h:mm a");

    /**
     * 程序入口
     * @param args
     */
    public static void main(String[] args) {
        Client c = new Client();
        c.start();
    }

    /**
     * Debug调试
     * 1.在可能出现问题的代码行前加上断点
     * 2.以Debug模式运行
     *  F8 --> 单步执行
     *  F7 --> 进入方法
     *  Shift + F8 --> 执行完毕方法
     *  F9 --> 执行到下一个断点
     */
    public void start() {
        GoodsClient goodsClient = new GoodsClient();
        UserClient userClient = new UserClient();
        CartClient cartClient = new CartClient();
        OrderClient orderClient = new OrderClient();

        String result = goodsClient.index(); // 返回商品模块用户录入的公共操作

        while (true) {
            if(result.equals(INDEX)) { // 首页
                HISTORY = INDEX;
                result = goodsClient.index();
            } else if(result.equals(LOGIN)) { // 登录页面
                result = userClient.showLogin();
            } else if(result.equals(HISTORY)) { // 上一次操作页面
                result = HISTORY;
            } else if(result.equals(EXIT)) { // 退出
                System.exit(0);
            } else if(result.equals(ADD)) { // 添加到购物车
                result = cartClient.addCart();
            } else if (result.equals(CART)) { // 去购物车
                HISTORY = CART;
                result = cartClient.index();
            } else if (result.equals(ORDER)) { // 去结算
                HISTORY = ORDER;
                result = orderClient.index();
            } else {
                System.out.println("出错了。");
            }
        }
    }

    /**
     * 需求：创建公共的用户操作的方法
     * 主要功能：
     *  1.提示用户信息和用户操作
     *      请根据编号进行操作（或 L登录；E退出）：
     *  2.接收用户的录入
     *      sc.nextLine()
     *  方法的分析：
     *      方法名：    userOperate
     *      返回值：    String
     *      参数列表：
     *          String msg; 用户信息
     *          String... oprs; 用户操作
     *              可变参数，本质是一个数组
     */
    public String userOperate(String msg, String... oprs) {
        // oprs == String[]
        String opr = Arrays.toString(oprs); // "[opr1, opr2, opr3]"
        opr = opr.substring(1, opr.length() - 1); // opr1, opr2, opr3
        msg = msg + "或 " + opr + "；E退出）：";
        System.out.println(msg); // 请根据编号进行操作（或 L登录；E退出）：
        return sc.nextLine().trim().toUpperCase(); // 去掉空格，转成大写
    }
}

```

### 3.订单支付和订单详情代码实现

```java
package cn.butou.eshop.client;

import cn.butou.eshop.common.entity.Entity;
import cn.butou.eshop.order.entity.Order;
import cn.butou.eshop.user.action.UserAction;
import cn.butou.eshop.user.entity.User;

import java.util.Date;

/**
 * 订单操作页面
 */
public class OrderClient extends Client{

    /* 当前操作订单对象 */
    private Order currentOrder;

    /** 去支付 */
    public static final String PAY = "P";
    /** 查看详情 */
    public static final String SEE_DETAIL = "SD";

    /**
     * 订单管理页面
     * 生成订单：
     *  条件：
     *      1.购物车中有数据
     *      2.已登录
     *      3.录入收货人信息
     *  结果：
     *      封装Order对象
     *      订单状态为：待支付
     *      清空购物车
     * @return
     */
    public String index() {
        UserAction userAction = new UserAction();
        if(userAction.getLoginUser() != null) {
            String result = generateOrder();
            while(true) {
                if(result.equals(PAY)) { // pay 去支付
                    result = pay();
                } else if(result.equals(SEE_DETAIL)) { // 查看订单详情
                    result = showOrder();
                } else {
                    return result;
                }
            }
        } else {
            return LOGIN;
        }

    }

    /**
     * 生成订单
     *  1.填写订单信息
     *  2.封装成Order对象
     *  3.生成订单 --> 待支付状态
     */
    public String generateOrder() {
        CartClient cartClient = new CartClient();
        /* 填写订单信息 */
        System.out.println("----------正在生成订单----------");

        System.out.println("请输入收货人：");
        String consignee = sc.nextLine();
        System.out.println("请输入收货地址：");
        String consigneeAddress = sc.nextLine();
        System.out.println("请输入联系电话：");
        String phone = sc.nextLine();

        /* 生成订单 --> 待支付状态 */
        currentOrder = new Order();
        currentOrder.setId(Entity.getUUID()); // 订单ID
        currentOrder.setCreateTime(sdf.format(new Date())); // 订单生成日期
        currentOrder.setAmount(cartClient.getCartAmount()); // 订单总金额
        currentOrder.setConsigneeAddress(consigneeAddress); // 收货地址
        currentOrder.setConsignee(consignee); // 收货人
        currentOrder.setPhone(phone); // 收货人手机号
        String serialNumber = getSerialNumber();
        currentOrder.setSerialNumber(serialNumber); // 订单序列号
        currentOrder.setState(Order.WAITING_PAY); // 待支付

        System.out.println("-------------- 订单已生成 -------------\n订单号: \t" + serialNumber
                + " \n总金额：\t" + cartClient.getCartAmount() + "\n状态：\t待支付。");
        return userOperate("请选择操作", "P去支付", "SD查看订单详情 ", "I回首页");
    }

    /**
     * 订单支付
     * 1.在控制台录入一个数值，若该数值大于等于订单总金额，则支付成功，否则余额不足
     * @return
     */
    public String pay() { // PAY
        String opr = userOperate("请输入支付金额", "SD查看订单详情 ", "I回首页；");
        while(true) {
            try {
                Double num = Double.parseDouble(opr); // 将金额转成double类型
                Double sum = Double.parseDouble(currentOrder.getAmount());
                if(num >= sum) {
                    System.out.println("支付成功！");
                    currentOrder.setState(Order.WAITING_SEND); // 待发货
                    return userOperate("请选择操作",  "SD查看订单详情 ", "I回首页 ");
                } else {
                    System.out.println("余额不足，请重新支付。");
                    opr = userOperate("请输入支付金额");
                }
            } catch(Exception e) {
                return opr; // 未知操作，返回上层
            }
        }
    }

    /**
     * 获取订单序列号，根据当前系统日期生成
     * @return
     */
    public String getSerialNumber() {
        String serialNumber = new Date().getTime() + "";
        int cartHash = this.hashCode();
        return serialNumber + cartHash;
    }

    /**
     * 查看订单详情
     * 1.展示订单信息
     *      将订单中商品展示出来
     * 2.根据订单状态，显示正确的描述信息
     * @return
     */
    public String showOrder() {
        System.out.println("【我的订单】");
        System.out.println("----------------------------------------------");
        String createTime = currentOrder.getCreateTime();
        String amount = currentOrder.getAmount();
        String consigneeAddress = currentOrder.getConsigneeAddress();
        String consignee = currentOrder.getConsignee();
        String phone = currentOrder.getPhone();
        String serialNumber = currentOrder.getSerialNumber();
        String state = currentOrder.getState(); // 订单状态

        System.out.println("订单号：" + serialNumber + "\t\t下单时间：" + createTime
                + "\t\t总金额：" + amount + "\t\t状态："+ getStateDescribtion(state));
        // TODO other infos of order

        String oprs = "I回首页 ";
        if(state.equals(Order.WAITING_PAY)) { // 如果订单未支付，则提供支付功能
            oprs += " P去支付 ";
        }

        return userOperate("请选择操作", oprs);
    }

    /**
     * 根据订单状态常量，获取对应的描述
     * @param state 订单状态常量
     * @return
     */
    public String getStateDescribtion(String state) {
        switch(state) {
            case Order.CANCELLED:
                return "已取消";
            case Order.COMPLETED:
                return "已完成";
            case Order.WAITING_PAY:
                return "待支付";
            case Order.WAITING_RECEIVE:
                return "待收货";
            case Order.WAITING_SEND:
                return "待发货";
            default:
                return "";
        }
    }
}
```

# 遇到的问题

1.第一次跑起项目时，FileUtil中使用ClassLoader获取文件getfile总是报null错误，一直以为是使用方法不对，或者填的路径格式有误，尝试了各种方法，Debugged确实找不到文件路径db/db_goods.txt，最后去了编译后的out目录中一看，整个db文件夹都不在编译后的文件夹中，重新删除src中的db文件夹再创建后问题解决了。

2.HISTORY操作问题，原来添加了跳转HISTORY的条件，跑起来发现会死循环，应把HISTORY跳转删除

```java
package cn.butou.eshop.client;

import cn.butou.eshop.goods.entity.Goods;

import java.text.SimpleDateFormat;
import java.util.Arrays;
import java.util.Scanner;

/**
 * 客户端顶层父类
 * 处理公共的用户操作
 */
public class Client {

    /** 全局 用户操作 登录 */
    public static final String LOGIN = "L";
    /** 全局 用户操作 上一次操作记录 */
    public static String HISTORY = "I";
    /** 全局 用户操作 首页 */
    public static final String INDEX = "I";
    /** 全局 用户操作 退出 */
    public static final String EXIT = "E";
    /** 全局 用户操作 添加 */
    public static final String ADD = "A";

    /** 全局 用户操作 去结算（订单模块） */
    public static final String ORDER = "O";

    /** 全局 模块 购物车 */
    public static final String CART = "C";

    /** 当前正在操作的商品对象 */
    protected static Goods currentGoods;

    /** Scanner扫描器对象，从控制台录入 */
    protected Scanner sc = new Scanner(System.in);
    /** 日期格式化对象 */
    protected SimpleDateFormat sdf = new SimpleDateFormat("h:mm a");

    /**
     * 程序入口
     * @param args
     */
    public static void main(String[] args) {
        Client c = new Client();
        c.start();
    }

    /**
     * Debug调试
     * 1.在可能出现问题的代码行前加上断点
     * 2.以Debug模式运行
     *  F8 --> 单步执行
     *  F7 --> 进入方法
     *  Shift + F8 --> 执行完毕方法
     *  F9 --> 执行到下一个断点
     */
    public void start() {
        GoodsClient goodsClient = new GoodsClient();
        UserClient userClient = new UserClient();
        CartClient cartClient = new CartClient();
        OrderClient orderClient = new OrderClient();

        String result = goodsClient.index(); // 返回商品模块用户录入的公共操作

        while (true) {
            if(result.equals(INDEX)) { // 首页
                HISTORY = INDEX;
                result = goodsClient.index();
            } else if(result.equals(LOGIN)) { // 登录页面
                result = userClient.showLogin();
            } else if(result.equals(EXIT)) { // 退出
                System.exit(0);
            } else if(result.equals(ADD)) { // 添加到购物车
                result = cartClient.addCart();
            } else if (result.equals(CART)) { // 去购物车
                HISTORY = CART;
                result = cartClient.index();
            } else if (result.equals(ORDER)) { // 去结算
                HISTORY = ORDER;
                result = orderClient.index();
            } else {
                System.out.println("出错了。");
            }
        }
    }

    /**
     * 需求：创建公共的用户操作的方法
     * 主要功能：
     *  1.提示用户信息和用户操作
     *      请根据编号进行操作（或 L登录；E退出）：
     *  2.接收用户的录入
     *      sc.nextLine()
     *  方法的分析：
     *      方法名：    userOperate
     *      返回值：    String
     *      参数列表：
     *          String msg; 用户信息
     *          String... oprs; 用户操作
     *              可变参数，本质是一个数组
     */
    public String userOperate(String msg, String... oprs) {
        // oprs == String[]
        String opr = Arrays.toString(oprs); // "[opr1, opr2, opr3]"
        opr = opr.substring(1, opr.length() - 1); // opr1, opr2, opr3
        msg = msg + "或 " + opr + "；E退出）：";
        System.out.println(msg); // 请根据编号进行操作（或 L登录；E退出）：
        return sc.nextLine().trim().toUpperCase(); // 去掉空格，转成大写
    }
}
```

3.界面格式修改

```java
package cn.butou.eshop.client;

import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.action.GoodsAction;
import cn.butou.eshop.goods.entity.Goods;
import jdk.swing.interop.SwingInterOpUtils;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

/**
 * 商品操作页面
 */
public class GoodsClient extends Client {
    Map<String, Goods> code2Goods = new HashMap<>();

    /**
     * 商品管理首页
     *
     * 商品页面跳转控制器：
     *  本模块的操作由此方法控制跳转
     *  其他模块的操作返回上层，由Client控制跳转
     * @return 返回公共操作
     */
    public String index() {
        showGoodsList(); // 展示商品列表
        String result = userOperate("请根据序号查看商品详情", "L登录；");

        while(true) {
            if(result.equals(LOGIN)) {
                return LOGIN;
            }
            if(result.equals(EXIT)) {
                return EXIT;
            }
            if(result.equals(INDEX)) {
                return INDEX;
            }
            Goods goods = code2Goods.get(result); // get方法返回结果为数据或者null
            if(goods != null) { // 查看详情
                currentGoods = goods;
                showGoodsDetail();
                result = userOperate("输入A加入购物车", "L登录 ", "I首页 ");
            } else if(result.equals(ADD)) { // 加入购物车
                return ADD;
            } else {
                System.out.println("输入错误，请重新输入");
                result = userOperate("请根据序号查看商品详情", "L登录 ", "I首页 ");
            }
        }
    }

    /**
     * 展示商品列表
     * 1.向后台发送请求，获取商品数据
     * 2.解析响应消息字符串
     * 3.展示商品列表
     */
    public void showGoodsList() {
        // 1.向后台发送请求，获取商品数据
        GoodsAction goodsAction = new GoodsAction();
        String msgJSON = goodsAction.getGoodsList();

        // 2.解析响应消息字符串
        Msg msg = JSONUtil.JSON2Entity(msgJSON, Msg.class);
        Object obj = msg.getObj(); // 数据就存放在obj对象里：[{},{},{}]
        List<?> goodsListJson = (List<?>) obj;

        System.out.println("【商品列表】");
        System.out.println("编号\t商品名称\t\t单价\t\t库存");
        System.out.println("------------------------------");
        int index = 1; //编号
        for (Object o : goodsListJson) {
            // o : {...}
            String goodsJson = o.toString(); // {,,,}
            Goods goods = JSONUtil.JSON2Entity(goodsJson, Goods.class);
            String name = goods.getName(); // 名称
            String price = goods.getPrice() + ""; // 单价
            String num = goods.getNumber() + ""; // 库存

            // 3.展示商品列表
            System.out.println(index + ".\t\t" + name + "\t\t" + price + "\t\t" + num);
            code2Goods.put(index + "", goods);
            index ++;
        }
    }

    /**
     * 查看商品详情
     * 通过数据ID获取数据，然后进行展示（需要重新访问数据库，显然不妥）
     *  or
     * 在展示商品的时候，把商品列表存储起来，然后，当选择商品编号时，就把对应商品展示出来
     *  Map<String, Goods> ： key --> 编号，value --> Goods对象
     */
     public void showGoodsDetail() {
         System.out.println("【商品详情】");
         System.out.println("编号\t商品名称\t\t单价\t\t库存\t\t品牌");
         System.out.println("------------------------------");
         String name = currentGoods.getName(); // 名称
         String price = currentGoods.getPrice() + ""; // 单价
         String num = currentGoods.getNumber() + ""; // 库存
         String brand = currentGoods.getBrand(); //品牌
         //3.展示商品列表
         System.out.println(1 + ".\t\t" + name + "\t\t" + price + "\t\t" + num + "\t\t" + brand);
     }

    /**
     * TODO 添加商品
     */

    /**
     * TODO 修改库存
     */

    /**
     * TODO 修改单价
     */

    /**
     * TODO 删除商品
     */
}
```

4.所有CartClient共用cartAmount，因此设置为static

```java
package cn.butou.eshop.client;

import cn.butou.eshop.cart.action.CartAction;
import cn.butou.eshop.cart.entity.CartGoods;
import cn.butou.eshop.common.entity.Msg;
import cn.butou.eshop.common.util.JSONUtil;
import cn.butou.eshop.goods.entity.Goods;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

/**
 * 购物车操作页面
 */
public class CartClient extends Client {
    CartAction cartAction = new CartAction();

    // 购物车总金额
    private static String cartAmount;

    /** 数字编号和商品ID映射表Map（key：数字编号；value：商品ID）*/
    Map<Integer, Goods> code2Goods;

    public String index() {
        // 展示购物车商品列表
        String result = showCart();
        while (true) {
            if (result.equals(LOGIN)) { // 全局操作 登录
                // 直接返回上层Client
                return LOGIN;
            }
            if (result.equals(EXIT)) {
                return EXIT;
            }
            if (result.equals(INDEX)) {
                return INDEX;
            }

            if (result.equals(ORDER)) { // 去结算
                return ORDER;
            } else {
                System.out.println("输入错误，请重新输入");
                result = userOperate("请根据序列号选择操作", "I去凑单 ", "L登录 ", "o去结算 ");
            }
        }
    }

        /**
         * 添加购物车
         *
         * 把当前正在操作的商品对象添加到购物车中
         * 1.把currentGoods对象发送请求到CartAction
         * 2.接收Action的响应消息
         * @return
         */
        public String addCart() {
            // 1.把currentGoods对象发送请求到CartAction
            cartAction.setGoods(currentGoods);
            // 2.接收Action的响应消息
            String msgJson = cartAction.addCart();
            Msg msg = JSONUtil.JSON2Entity(msgJson, Msg.class);
            if(msg.getType().equals(Msg.SUCCESS)) {
                System.out.println("添加购物车成功");
            } else {
                System.out.println(msg.getMsg());
            }

            return userOperate("请选择操作", "I继续浏览", "C购物车", "L登录");
        }

        /**
         * GoodsClient：
         *  currentGoods 肯定是有值的
         *  这里的赋值操作，仅仅是对GoodsClient对象goodsClient的属性currentGoods赋值
         *  CartClient对象cartClient里面的属性currentGoods并没有被赋值.
         * CartClient：
         *  currentGoods 没有值
         *  CartClient在创建对象的时候，currentGoods是null
         *
         *  解决方案：
         *      currentGoods 用static修饰
         *      两个对象GoodsClient和CartClient共享同一个currentGoods对象
         */

        /**
         * 展示购物车列表
         * 1.向后台发送请求，获取商品数据
         * 2.解析响应消息字符串
         * 3.展示购物车列表
         * @return
         */
        public String showCart() {
            System.out.println("\n【我的购物车】");
            System.out.println("编号\t商品名称\t\t单价\t\t数量");

            // 1.向后台发送请求，获取商品数据
            String result = cartAction.showCart();
            Msg msg = JSONUtil.JSON2Entity(result, Msg.class);

            // 2.解析响应消息字符串
            List<?> cartGoodsList = (List<?>)msg.getObj(); // 将得到的普通对象转换为购物车商品列表
            int i = 1; // 序号
            double sum = 0; // 总金额
            code2Goods = new HashMap<>(); // 将展示编号和数据ID关联起来

            for (Object obj : cartGoodsList) {
                String json = obj.toString();
                CartGoods cartGoods = JSONUtil.JSON2Entity(json, CartGoods.class);
                int num = cartGoods.getGoodsNum(); // 商品数量
                String name = cartGoods.getName(); // 商品名称
                double price = cartGoods.getPrice(); // 商品单价
                System.out.println(i + "." + "\t" + name + "\t\t\t"
                        + price + "\t\t" + num);
                sum += price * num; //BigDecimal
                code2Goods.put(i++, cartGoods);
            }
            this.setCartAmount(sum + "");
            System.out.println("总金额：" + sum);

            return userOperate("请根据序号选择操作", "I去凑单 ", "L登录 ", "o去结算 ");
        }

        public String getCartAmount() {
            return cartAmount;
        }

        public void setCartAmount(String cartAmount) {
            this.cartAmount = cartAmount;
        }
}
```

5.出错了之后也要加System.exit(0)，否则死循环

```java
package cn.butou.eshop.client;

import cn.butou.eshop.goods.entity.Goods;

import java.text.SimpleDateFormat;
import java.util.Arrays;
import java.util.Scanner;

/**
 * 客户端顶层父类
 * 处理公共的用户操作
 */
public class Client {

    /** 全局 用户操作 登录 */
    public static final String LOGIN = "L";
    /** 全局 用户操作 上一次操作记录 */
    public static String HISTORY = "I";
    /** 全局 用户操作 首页 */
    public static final String INDEX = "I";
    /** 全局 用户操作 退出 */
    public static final String EXIT = "E";
    /** 全局 用户操作 添加 */
    public static final String ADD = "A";

    /** 全局 用户操作 去结算（订单模块） */
    public static final String ORDER = "O";

    /** 全局 模块 购物车 */
    public static final String CART = "C";

    /** 当前正在操作的商品对象 */
    protected static Goods currentGoods;

    /** Scanner扫描器对象，从控制台录入 */
    protected Scanner sc = new Scanner(System.in);
    /** 日期格式化对象 */
    protected SimpleDateFormat sdf = new SimpleDateFormat("h:mm a");

    /**
     * 程序入口
     * @param args
     */
    public static void main(String[] args) {
        Client c = new Client();
        c.start();
    }

    /**
     * Debug调试
     * 1.在可能出现问题的代码行前加上断点
     * 2.以Debug模式运行
     *  F8 --> 单步执行
     *  F7 --> 进入方法
     *  Shift + F8 --> 执行完毕方法
     *  F9 --> 执行到下一个断点
     */
    public void start() {
        GoodsClient goodsClient = new GoodsClient();
        UserClient userClient = new UserClient();
        CartClient cartClient = new CartClient();
        OrderClient orderClient = new OrderClient();

        String result = goodsClient.index(); // 返回商品模块用户录入的公共操作

        while (true) {
            if(result.equals(INDEX)) { // 首页
                HISTORY = INDEX;
                result = goodsClient.index();
            } else if(result.equals(LOGIN)) { // 登录页面
                result = userClient.showLogin();
            } else if(result.equals(EXIT)) { // 退出
                System.exit(0);
            } else if(result.equals(ADD)) { // 添加到购物车
                result = cartClient.addCart();
            } else if (result.equals(CART)) { // 去购物车
                HISTORY = CART;
                result = cartClient.index();
            } else if (result.equals(ORDER)) { // 去结算
                HISTORY = ORDER;
                result = orderClient.index();
            } else {
                System.out.println("出错了。");
                System.exit(0);
            }
        }
    }

    /**
     * 需求：创建公共的用户操作的方法
     * 主要功能：
     *  1.提示用户信息和用户操作
     *      请根据编号进行操作（或 L登录；E退出）：
     *  2.接收用户的录入
     *      sc.nextLine()
     *  方法的分析：
     *      方法名：    userOperate
     *      返回值：    String
     *      参数列表：
     *          String msg; 用户信息
     *          String... oprs; 用户操作
     *              可变参数，本质是一个数组
     */
    public String userOperate(String msg, String... oprs) {
        // oprs == String[]
        String opr = Arrays.toString(oprs); // "[opr1, opr2, opr3]"
        opr = opr.substring(1, opr.length() - 1); // opr1, opr2, opr3
        msg = msg + "或 " + opr + "；E退出）：";
        System.out.println(msg); // 请根据编号进行操作（或 L登录；E退出）：
        return sc.nextLine().trim().toUpperCase(); // 去掉空格，转成大写
    }
}
```

参考资料：黑马传智博学谷Java零基础编程