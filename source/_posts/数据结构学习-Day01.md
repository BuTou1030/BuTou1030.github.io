---
title: 数据结构学习 Day01
copyright: true
date: 2020-09-22 15:27:56
toc: true
tags: [课程学习,数据结构]
categories: [课程学习,数据结构]
---
## 一、顺序栈
<!-- more -->
### 1.顺序栈定义

```c
typedef struct {
	ElemType *elem; // 存储空间的基址
	int top; // 栈顶元素的下一个位置,简称栈顶位标
	int size; // 当前分配的存储容量
	int increment; // 扩容时,增加的存储容量
} SqStack; // 顺序栈
```

### 2.顺序栈的常用接口

```c
Status InitStack_Sq(SqStack &S, int size, int inc) // 顺序栈初始化
Status DestroyStack_Sq(SqStack &S) // 销毁
void ClearStack_Sq(SqStack &S) // 清空
Status StackEmpty_Sq(SqStack S) // 判空
Status Push_Sq(SqStack &S, ElemType e) // 入栈操作
Status Pop_Sq(SqStack &S, ElemType &e) // 出栈操作
Status GetTop_Sq(SqStack S, ElemType &e) // 取栈顶元素
```

### 3.接口实现

#### (1)顺序栈初始化

```c
Status InitStack_Sq(SqStack &S, int size, int inc) {
	S.elem = (ElemType *)malloc(size * sizeof(ElemType));
	S.top = 0; // 置S为空栈
	S.size = size; // 初始容量值
	S.increment = inc; // 初始增量值
	return OK;
}
```

#### (2)销毁

```c
Status DestroyStack_Sq(SqStack &S) {
    if(S.elem) {
        free(S.elem); // 释放空间
        S.elem = NULL;
        S.top = 0;
        S.size = 0;
        return OK;
    }
}
```

#### (3)清空

```c
void ClearStack_Sq(SqStack &S) {
    if(s.elem) {
        S.top = 0;
    }
    return OK;
}
```

#### (4)判空

```c
Status StackEmpty_Sq(SqStack S) {
    if(S.top == 0) {
        return TRUE;
    }else {
        return FALSE;
    }
}

```

#### (5)入栈操作

```c
Status Push_Sq(SqStack &S, ElemType e) { // 元素e压入栈S
	ElemType *newbase;
	if(S.top >= S.size) { // 若栈顶位标已达到所分配的容量，则栈满，扩容
		newbase = (ElemType*)realloc(S.elem, (S.size + S.increment) * sizeof(ElemType));
		if(NULL == newbase) return OVERFLOW;
		S.elem = newbase;
		S.size += S.increment;
	}
	S.elem[S.top ++] = e; // e入栈,并将S.top加1
	return OK;
}
```

#### (6)出栈操作

```c
Status Pop_Sq(SqStack &S, ElemType &e) {
	ElemType temp;
	if(S.top == 0) {
		return ERROR;
	}
	S.top --;
	e = S.elem[S.top];
	return OK;
}
```

#### (7)取栈顶元素

```c
Status GetTop_Sq(SqStack S, ElemType &e) {
    if(S.top == 0) {
        return ERROR;
    }
	e = S.elem[S.top - 1];
	return OK;
}
```

---
## 参考书籍
《数据结构》-高等教育出版社
