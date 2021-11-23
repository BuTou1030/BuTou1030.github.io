---
title: Java常用工具_IO流
copyright: true
date: 2021-03-03 19:14:41
toc: true
tags: [后端,JAVA]
categories: [后端,JAVA]
---

## 一.什么是IO流

<!-- more -->

### 1.IO流的基本概念

对于任何程序设计语言而言，输入输出(Input/Output)系统都是非常核心的功能。程序运行需要数据，数据的获取往往需要跟外部系统进行通信，外部系统可能是文件、数据库、其他程序、网络、IO设备等等。外部系统比较复杂多变，那么我们有必要通过某种手段进行抽象、屏蔽外部的差异，从而实现更加便捷的编程。

 java.io包为我们提供了相关的API，实现了对所有外部系统的输入输出操作
————————————————
版权声明：本文为CSDN博主「兰知行」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_43698400/article/details/97022253

流是一个抽象、动态的概念，是一连串连续动态的数据集合。

对于输入流而言，数据源就像水箱，流(stream)就像水管中流动着的水流，程序就是我们最终的用户。我们通过流(A Stream)将数据源(Source)中的数据(information)输送到程序(Program)中。

对于输出流而言，目标数据源就是目的地(dest)，我们通过流(A Stream)将程序(Program)中的数据(information)输送到目的数据源(dest)中。
————————————————
版权声明：本文为CSDN博主「兰知行」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_43698400/article/details/97022253

### 2.IO流体系

按流的方向分类：

1. 输入流：数据流向是数据源到程序(以InputStream、Reader结尾的流)。

2. 输出流：数据流向是程序到目的地(以OutPutStream、Writer结尾的流)。

按处理的数据单元分类：

1. 字节流：以字节为单位获取数据，命名上以Stream结尾的流一般是字节流，如FileInputStream、FileOutputStream。

2. 字符流：以字符为单位获取数据，命名上以Reader/Writer结尾的流一般是字符流，如FileReader、FileWriter。

按处理对象不同分类

1. 节点流：可以直接从数据源或目的地读写数据，如FileInputStream、FileReader、DataInputStream等。

2.  处理流：不直接连接到数据源或目的地，是”处理流的流”。通过对其他流的处理提高程序的性能，如BufferedInputStream、BufferedReader等。处理流也叫包装流。

节点流处于IO操作的第一线，所有操作必须通过它们进行;处理流可以对节点流进行包装，提高性能或提高程序的灵活性。
————————————————
版权声明：本文为CSDN博主「兰知行」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_43698400/article/details/97022253

### 3.IO流操作的异常

#### (1)什么是异常

即非正常情况，通俗的说，异常就是程序出现的错误

#### (2) 异常体系

异常(Throwable)分为Exception和Error.

异常(Exception)

​	合理的应用程序可能需要捕获的问题

​	举例：NullPointerException

错误(Error)

​	合理的应用程序不应该试图捕获的问题

​	举例：StackOverFlowError

#### (3)怎么处理异常

JVM默认的异常处理方式：在控制台打印错误信息，并终止程序

开发中的异常处理方式

方式一：try...catch(finally):捕获，自己处理

```java
public class Test {
    pulic static void main(String[] args) {
        try {
			   //尝试执行的代码
                int a = 10 / 10;
                System.out.println("a：" + a);
                return;
            } catch(Exception e) {
                //出现可能的异常之后的处理代码
                System.out.println("被除数不能为0!!!");
                return;
            } finally {
                //一定会执行的代码，如关闭资源
                System.out.println("看看我执行了吗?");
            }
            //细节：即使try或者catch中有return,finally里边的代码也会执行
    }
}
```

方式二：抛出，交给调用者处理，throws

特点：执行结束后，程序不再继续执行

```java
//方案一
public class Test {
    public static void main(String[] args) throws Exception {
       //show()方法已经跑出来一个异常，main方法继续接着抛出异常,会抛给JVM
        show();
        System.out.println("看看我执行了吗");
    }
    
    //定义一个方法
    public static void show() throws Exception {
        int a = 10 / 0;
        System.out.println("a：" + a);
    }
    
}
//方案二
public class Test {
    public static void main(String[] args) {
       //采用try...catch处理
       try {
           show();
       }catch(Exception e) {
           System.out.println("代码出问题了!!!");
       }
       System.out.println("看看我执行了吗?");
    }
    
    //定义一个方法
    public static void show() throws Exception {
        int a = 10 / 0;
        System.out.println("a：" + a);
    }
    
}
    
    
    
   
```







## 二.IO流的使用

### 1.File类 (java.io.File)

(1)概述：一个File对象代表磁盘上的某个文件或文件夹，通俗地讲，File用来操作文件（夹）的路径,

这点非常重要，是路径！

(2)构造方法：

​	File(String pathname)			根据给定的字符串路径创建其对应的File对象.

​	File(String parent, String child)			根据给定的字符串形式的父目录和子文件（夹）名创建File对象.

​	File(File parent, String child)			根据给定的父目录对象和子文件（夹）名创建File对象.

 (3)成员方法：

​	  创建功能：如果不存在就创建，返回true，否则不创建，返回false

​		  createNewFile();			创建文件

​		  mkdir();			创建单级目录

​		  mkdirs();			创建目录（包括多级和单级，因此常用mkdirs()）

​	  判断功能：

​		  isDirectory();			判断File对象是否为目录

​		  isFile();			判断File对象是否为文件

​		  exists();			判断File对象是否存在

​     创建功能和判断功能的使用举例

```java
public class Test {
    public static void main(String[] args) throws Exception {
        //因为后续给出的路径的存在未知，因此为了方便可以使用throws抛出错误
        
        //方式一
        File file1 = new File("D:/abc/1.txt");
        System.out.println("file1：" + file1);
        
        //方式二
        File file2 = new File("D:/abc/", "1.txt");
        System.out.println("file2：" + file2);
        
        //方式三
        File file3 = new File("D:/abc/");
        File file4 = new File(file3, "1.txt");
        System.out.println("file4：" + file4);
        System.out.println("----------------------------");
        System.out.println("创建功能");
        
        //需求：在d:盘下创建2.txt文件
        File file5 = new File("d:/2.txt");
        boolean flag1 = file5.createNewFile();
        System.out.println("flag1：" + flag1);
        
        //需求：在d:盘下创建a文件夹
        File file6 = new File("d:/a");
        boolean flag2 = file6.mkdir();
        System.out.println("flag2：" + flag2);
        
        //需求：在d:盘下创建a/b/c文件夹
        File file7 = new File("d:/a/b/c");
        boolean flag3 = file7.mkdirs();
        System.out.println("flag3：" + flag3);
        System.out.println("---------------------------");
        
        System.out.println("测试判断功能");
        File file8 = new File("d:/2.txt");
        System.out.println("测试file8是否为文件夹：" + file8.isDirectory());
        System.out.println("测试file8是否为文件：" + file8.isFile());
        System.out.println("测试file8是否存在：" + file8.exists());
        
    }
}
```

​	获取功能：

​		getAbsolutePath();			获取文件（夹）绝对路径

​		getPath();			获取文件（夹）的相对路径

​		getName();			获取文件（夹）名

​		list();			获取指定目录下所有文件（夹）名称数组

​		listFiles();			获取指定目录下所有文件（夹）File数组

​	获取功能的使用举例

```java
public static Test {
    public static void main(String[] args) {
        File file1 = new File("lib/1.txt");
        
        //获取file1的绝对路径
    	String path1 = file1.getAbsolutePath();
        System.out.println("path1：" + path1);
        
        //获取file1的相对路径
        String path2 = file1.getPath();
        System.out.println("path2：" + path2);
        
        //获取文件名
        String fileName = file1.getName();
        System.out.println("fileName：" + fileName);
        
        //获取目录下所有文件（夹）名称数组
        File file2 = new File("lib");
        String[] names = file2.list();
        for (String name : names) {
            System.out.println(name);
        }
        
        //获取lib文件夹下所有的文件（夹）的File对象数组File[]
        File[] files = file2.listFiles();
        for (File file : files) {
            System.out.println(file);
            //可以对获取到File对象进行操作
            System.out.println("是文件吗：" + file.isFile());
            System.out.println("是文件夹吗：" + file.isDirectory());
        }
        
    }
}
```



### 2.字符流

#### (1)字符流读取数据

​	Reader类中的方法

​		int read();			读一个字符，返回该字符对应的ASCII码值，读不到返回-1

​		FileReader类的构造方法：

​			public FileReader(String pathname)			根据传入的字符串形式的路径，获取字符输入流对象

​	FileReader读取数据--一次一个字符举例

```java
public class ReaderDemo {
    public static void main(String[] args) throws IOException {
		//1.创建字符输入流对象.
        Reader reader = new FileReader("lib/1.txt");
       
        //2.定义变量，用来接收读取到的字符
        int ch;
        while((ch = reader.read()) != -1) { //3.利用循环读取数据，直到返回-1
            System.out.println(ch);
        }
        
        //4.释放资源
        reader.close();
    }
}
```

​	Reader类中的方法：

​		int read(char[] chs);			一次读一个字符数组，将读取到的内容存入数组中，并返回读取到的有效字符数，读不到返回-1

​		FileReader读取数据--一次一个字符数组举例

```java
public class ReaderDemo2 {
    public static void main(String[] args) throws IOException {
        //1.创建字符输入流对象
        Reader reader = new FileReader("lib/1.txt");
        
        //2.定义字符数组
        char[] chs = new char[3];
        //定义一个变量，记录读到的有效字符数.
        int len;
        while((len = reader.read(chs)) != -1) {
            /*
            	chs：表示要操作的数组.
            	0：表示起始索引.
            	len：表示要操作字符的个数.
            */
            String s = new String(chs, 0, len);
            /*
            	使用案例：abcdefg
            	第一次循环输出：abc
            	第二次循环输出：def
            	第三次循环输出：g
            */
            System.out.println(s);
        }
        
        //3.释放资源
        reader.close();
    }
}
```

#### (2)字符流写数据

​	Write类中的方法：

​		void write(int ch);			一次写一个字符

​		void write(char[] chs, int index, int len);			一次写一个指定的字符数组

​		void write(String str);			一次写一个字符串

​	FileWriter类的构造方法：

​		public FileWrite(String pathname)			根据传入的字符串形式的路径，获取字符输出流对象

​	FileWriter写数据举例

```java
public class WriterDemo {
    public static void main(String[] args) throws IOException {
        //1.创建字符输出流对象
        Writer writer = new FileWriter("lib/1.txt");
        
        //2.写数据
        //一次写一个字符
        writer.write('a');
        //一次写一个指定的字符数组
        char[] chs = {'你', '好', '世', '界'};
        writer.write(chs, 0, 4);
       	//一次写一个字符串
        writer.write("HelloWorld");
        
        //3.释放资源
        writer.close();
    }
}
```

#### (4)字符流拷贝文件

FileReader 和 FileWriter 举例 -- 一次复制一个字符

```java
public class CopyFile1 {
    public staic void main(String[] args) throws IOException {
        //将1.txt文件中的内容复制到2.txt
        /*
        	IO流拷贝文件6步：
        	1.创建字符输入流对象，关联数据源文件.
        	2.创建字符输出流对象，关联目的地文件.
        	3.定义变量，记录读取到的内容.
        	4.循环读取，只要条件满足就一直读，并将读取到的内容赋值给变量.
        	5.将读取到的数据写入到目的地文件中.
        	6.释放资源.
        */
        
        //1.
        FileReader fr = new FileReader("lib/1.txt");
        
        //2.
        FileWriter fw = new FileWriter("lib/2.txt");
        
        //若文件不存在会自动创建
        
        //3.
        int len;
        
        //4.
        while((len =  fr.read()) != -1) {
            //5.
            fw.write(len);
        }
        
        //6.
        fr.close();
        fw.close();
    }
}
```

FileReader 和 FileWriter 举例 -- 一次复制一个字符数组

```java
public class CopyFile2 {
    public static void main(String[] args) throws IOException {
        /*
        	IO流核心6步
        		1.创建字符输入流对象，关联数据源文件
        		2.创建字符输出流对象，关联目的地文件
        		3.创建变量，用来记录读取到的数据
        		4.通过循环进行读取，并将读取到的有效字符数赋值给变量
        		5.将读取到的数据写入到目的地文件中
        		6.释放资源
        */
        
        //1.
        FileReader fr = new FileReader("lib/1.txt");
        
        //2.
        FileWriter fw = new FileWriter("lib/2.txt");
        
        //3.
        char[] chs = new char[1024];
        int len;
        
        //4.
        while((len = fr.read(chs)) != -1) {
            //5.
            fw.write(chs, 0, len);
        }
        
        //6.
        fr.close();
        fw.close();
    }
}
```

#### (5)字符缓冲流用法

​	分类：

​		BufferReader：字符缓冲输入流（也叫高效字符输入流）

​			构造方法：

​				public BufferReader(Reader reader);

​		BufferWriter：字符缓冲输出流（也叫高效字符输出流）

​	特点：

​		字符缓冲流自带有缓冲区，大小为8192字符，即16KB

​	BufferedReader和BufferedWriter使用举例--一次复制一个字符

```java
public class CopyFile1 {
    public static void main(String[] args) throws IOException {
        //1.创建字符缓冲输入流对象，关联数据源文件
        BufferedReader br = new BufferedReader(new FileReader("lib/1.txt"));
        
        //2.创建字符缓冲输出流对象，关联目的地文件
        BufferedWriter bw = new BufferedWriter(new FileWriter("lib/2.txt"));
        
        //3.定义变量，记录读取到的数据
        int len;
        
        //4.循环读，只要条件满足就读取，并赋值给变量
        while((len = br.read()) != -1) {
            //5.将读取到的数据写入目的地文件中
            bw.write(len);
        }
        
        //6.释放资源
        br.close();
        bw.close();
    }
}
```

BufferedReader：

​	成员方法：

​		public String readLine();			一次读取一行数据并返回读取到的内容，读不到返回null

​		public void newLine();			根据当前操作系统给出对应的换行符.

​	

BufferedReader和BufferedWriter使用举例--一次复制一个字符数组

```java
public class CopyFile2 {
    public static void main(String[] args) throws IOExpection {
        BufferedReader br = new BufferedReader(new FileReader("lib/1.txt"));
        
        BUfferedWriter bw = new BufferedWriter(new FileWriter("lib/2.txt"));
        
        String str;
        while((str = br.readLine())) {
			bw.write(str);
             bw.newLine();
        }
        
        br.close();
        bw.close();
    }
}
```





### 3.字节流

#### (1)普通字节流拷贝文件

​	FileInputStream：普通的字节输入流，用来读取数据的.

​		构造方法：

​			public FileInputStream(String pathname);

​		成员方法：

​			public int read();			一次读取一个字节，并返回读取到的内容，读不到返回-1.

​			public int read(byte[] bys);			 一次读取一个字节数组，将读取到的内容存入到数组中，并返回读取到的有效字节数，读不到返回-1.

​	FileOutputStream：普通的字节输出流，用来写数据的.

​		构造方法：

​			public FileOutputStream(String pathname);

​		成员方法：

​			public void write(int len);

​			一次写入一个字节

​			public void write(byte[] bys, int index, int len);

​			一次写入一个指定的字节数组 

​	通过普通字节流，一次读写一个字节的方式举例

```java
public class CopyFile1 {
    public static void main(String[] args) throws IOException {
        //1.创建字节输入流，关联数据源文件.
        FileInputStream fis = new FileInputStream("lib/a.jpg");
        
        //2.创建字节输出流，关联目的地文件.
        FileOutputStream fos = new FileOutputStream("lib/b.jpg");
        
        //3.定义变量，用来记录读取到的内容.
        int len;
        
        //4.循环读取，只要条件满足就一直读，并将读取到的内容赋值给变量.
        while((len = fis.read()) !=  -1) {
            //5.将读取到的内容写入到目的地文件中.
            fos.write(len);
        }
        
        //6.释放资源.
        fis.close();
        fos.close();
    }
}
```

​	通过普通字节流一次读写一个字节数组举例

```java
public class CopyFile2 {
    public static void main(String[] args) throws IOExpection {
        //1.创建字节输入流对象，关联数据源文件.
        FileInputStream fis = new FileInputStream("lib/a.jpg");
        
        //2.创建字节输出流对象，关联目的地文件.
        FileOutputStream fos = new FileOutputStream("lib/b.jpg");
        
        //3.定义变量，用来接收读取到的内容.
        byte[] bys = new byte[1024];
        //用来记录读取到的有效字节数
        int len;
        
        //4.循环读取，只要条件满足就一直读，并将读取到的内容（有效的字节数）赋值给变量.
        while((len = fis.read(bys)) != -1) {
            //5.将读取到的数据写入到目的地文件
            fos.write(bys, 0, len);
        }
        
        //6.释放资源.
        fis.close();
        fos.close();
    }
}
```

#### (2)字节缓冲流拷贝文件

​	BufferedInputStream：字节缓冲输入流（也叫高效字节输入流）

​		构造方法：

​			public BufferedInputStream(InputStream is); 

​		成员方法：

​			public int read();			一次读取一个字节，并返回读取到的内容，读不到返回-1.

​	BufferedOutputStream：字节缓冲输出流（也叫高效字节输出流）

​		构造方法：

​			public BufferedOutputStream(OutputStream os);

​		成员方法：

​			public void write(int len);			一次写入一个字节.

​	特点：

​		字节缓冲流有自己的缓冲区，大小为8192字节，即为8KB.

​	总结：

​		字节流文件还可以拷贝非纯文本文件.

​	字节缓冲流拷贝文件使用举例

```java
public class CopyFile1 {
    public static void main(String[] args) throws IOException {
        //1.创建字节输入流对象，关联数据源文件.
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream("lib/a.jpg"));
        
        //2.创建字节输出流对象，关联目的地文件.
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("lib//b.jpg"));
        
        //3.定义变量，用来记录读取到的内容
        int len;
        
        //4.循环读取，只要条件满足就一直读，然后将读取到的内容赋值给变量
        while((len = bis.read()) != -1) {
            //5.将读取到的内容写入到目的地文件中
            bos.write(len);
        }
        
        //6.释放资源.
        bis.close();
        bos.close();
    }
}
```









