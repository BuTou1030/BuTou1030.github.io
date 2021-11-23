---
title: Java常用工具_IO流
copyright: true
date: 2021-03-30 19:19:41
toc: true
tags: [后端,JAVA]
categories: [后端,JAVA]
---

# JavaIO流中的RandomAccessFile

<!-- more -->

## 一.RandomAccessFile简介

​	这是一个很有价值的访问文件的类，**它既可以读文件，又可以写文件**，同时，RandomAccessFile支持“随机访问”的方式，**还可以访问文件的任何地方**，所以RandomAccessFile有更高的灵活性。

​	RandomAccessFile同时实现了DataInput和DataOutput接口，所以它同时具有各种readxxx()和writexxx()方法。

​	由于RandomAccess可以自由访问文件的任意位置，**所以如果需要访问文件的部分内容，而不是把文件从头读到尾，使用RandomAccessFile将是更好的选择。**

​	RandomAccessFile还支持文件指针（file pointer）的概念，用于指示当前的读写位置，当最初打开文件时，文件指针指向文件的开始位置，除了由read/write方法可以隐式地移动指针外，RandomAccessFile类提供了一些进行显式指针操作的方法。因此RandomAccessFile可以不从文件开始的地方输出，可以向已存在的文件后追加内容。**如果程序需要向已存在的文件后追加内容，则应该使用RandomAccessFile。**

​	RandomAccessFile的方法虽然多，**但它有一个最大的局限，就是只能读写文件，不能读写其他IO节点。**

​	**RandomAccessFile的一个重要使用场景就是网络请求中的多线程下载及断点续传。**

## 二.RandomAccessFile中的方法

### 1.RandomAccessFile的构造方法

```java
RandomAccessFile(File file, String mode)

RandomAccessFile(String name, String mode)
```

RandomAccessFile类有两个构造函数，其实这两个构造函数基本相同，只不过是指定文件的形式不同——一个需要使用String参数来指定文件名，一个使用File参数来指定文件本身。由于文件名与系统相关，所以用File类实例表示文件名可能更好。除此之外，创建RandomAccessFile对象时还需要指定一个mode参数，该参数指定RandomAccesFile的访问模式，一共有4种模式。

```java
r:	以只读方式打开。调用结果对象的任何write方法都将导致抛出IOException。
rw:	打开以便读取和写入。如果该文件不存在，则将尝试创建该文件。
rws: 打开以便读取和写入。相对于"rw", "rws"还要求对"文件的内容"或"元数据"的每个更新都同步写入到基础存储设备。
rwd: 打开以便读取和写入。相对于"rw"，"rwd"还要求对"文件的内容"的每个更新都同步写入到基础存储设备。
```

Rws模式的s即是synchronously同步的意思...

默认情形下(rw模式下),是使用buffer的,只有cache满的或者使用RandomAccessFile.close()关闭流的时候儿才真正的写到文件...

这个会有两个问题:

1.调试麻烦的...------------------使用write方法修改byte的时候儿,只修改到个内存,还没到个文件,闪的调试麻烦的,不能使用notepad++工具立即看见修改效果..

2.当系统halt的时候儿,不能写到文件...安全性稍微差点儿....

 Rwd模式跟个rws基础的一样..不过,只对“文件的内容”同步更新到磁盘...不对metadata同步更新..

这个模式间于 rw 跟个 rws 中间....

### 2.RandomAccessFile的常用方法

```java
public long length()		 返回文件的长度
public void seek(long pos)	  移动文件指针到指定的位置
public long getFilePointer()  返回文件指针的当前位置
public int skipByte(int n)	  使文件指针向前移动指定的n个字节
```



## 三.RandomAccessFile的使用

**当RandomAccessFile向指定文件中插入内容时，将会覆盖掉原有内容。如果不想覆盖掉，则需要将原有内容先读取出来，然后先把插入内容插入后再把原有内容追加到插入内容后。**

**插入步骤：**

**1）创建临时文件，保存被插入文件的插入点后面的内容。**

附加：使用File 的 createTempFile() 方法存储文件原有内容 
该方法有两种调用方式： 

在默认临时文件目录中创建一个空文件，使用给定前缀和后缀生成其名称。 

createTempFile(String prefix, String suffix)；
方法默认的保存路径为：C:\Documents and Settings\Administrator\Local Settings\Temp 。

在指定目录中创建一个新的空文件，使用给定的前缀和后缀字符串生成其名称。 createTempFile(String prefix, String suffix, File directory)；

createTempFile() 方法，在指定的目录下创建一个temp文件，directory 类型为File ，如果路径不存在，则创建失败。

3.删除方法

  //立即删除文件
   file.delete();
 //在JVM退出时删除文件
   file.deleteOnExit();
总结：临时文件能够使用默认路径，可以避免存在创建文件是因为路径错误导致创建文件失败的问题。 如果需求中需要创建一个临时文件，这个临时文件可能作为存储使用，但在程序运行结束后需要删除文件，可以使用deleteOnExit方法

**2）再重新定位到插入点，将需要插入的内容添加到文件后面，**

**3）最后将临时文件的内容添加到文件后面，**

```java
public class RandomDemo {
    public static void insert(String fileName, long pos, String insertContent) throws IOException {
        // 创建临时文件，设置为JVM退出后删除
        File tmp = File.createTempFile("tmp", null);
        tmp.deleteOnExit();
        
        // 创建RandomAccessFile对象，模式设为rw
        RandomAccessFile raf = new RandomAccessFile(fileName, "rw");
        // 使用临时文件保存插入点后的数据
        FileOutputStream out = new FileOutputStream(tmp);
        FileInputStream in = new FileInputStream(tmp);
        // 移动文件记录指针
        raf.seek(pos);
        
        //------------下面代码将插入点后的内容读入临时文件中保存--------
        byte[] buff = new byte[64];
        // 用于保存实际读取的字节数
        int hasRead = 0;
        
        // 使用循环方式读取插入点后的数据
        while((hasRead=raf.read(buff)) != -1) {
            // 将读取到数据写入临时文件
            out.write(buff, 0, hasread);
        }
        
        //-------------下面代码用于插入内容
        // 把文件记录指针重新定位到pos位置
        raf.seek(pos);
        // 追加需要插入的内容
        raf.write(insertContent.getBytes());
        // 追加临时文件中的内容
        while((hasRead=in.read(buff)) > 0) {
            raf.write(buff, 0, hasRead);
        }
    }
}
public static void main(String[] args) throws IOException {
    insert("G:/iotest/FileApartAndMerge/Insert.txt", 5, "I am a insert");
}
```





---



参考：
1.版权声明：本文为CSDN博主「sunlggggg」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/sunlggggg/article/details/53035466
2.[Ruheng](https://www.jianshu.com/u/0fa6f5d09040)：https://www.jianshu.com/p/360e37539266

3.Java技术及其应用第2版（清华大学出版社）

4.版权声明：本文为CSDN博主「巴黎没有欧莱雅你也不值得被拥有」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/lp15203883326/article/details/83783433

5.版权声明：本文为CSDN博主「Zero-place」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_41877184/article/details/86434490