---
title: JavaRandom类的简单使用
copyright: true
date: 2021-03-28 16:34:41
toc: true
tags: [后端,JAVA]
categories: [后端,JAVA]
---

# JavaRandom类的简单使用

<!-- more -->

## 一.Random类的概念

Random，即随机数。用于产生随机数的类。

## 二.Random类的使用步骤

```java
//第一步：导包
import java.util.Random;

public class RandomDemo {
	public static void main(String[] args) {
        //第二步：创建Random类的对象
		Random r = new Random();
        for(int x = 1; x <= 10; x++) {
            //第三步：获取随机数
            int number = r.nextInt(10); //获取int类型随机数，值为0-9
            System.out.println("number：" + number);
        }
    }
}
```

