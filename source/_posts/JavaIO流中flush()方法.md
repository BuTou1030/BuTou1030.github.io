---
title: JavaIO流中flush()方法
copyright: true
date: 2021-03-28 16:34:41
toc: true
tags: [后端,JAVA]
categories: [后端,JAVA]
---

# JavaIO流中flush()方法

<!-- more -->

flush()方法将输入流和输出流中的缓冲进行刷新，使缓冲区中的元素即时做输入和输出，而不必等缓冲区满

```
一般主要用在IO中，即清空缓冲区数据，就是说你用读写流的时候，其实数据是先被读到了内存中，然后用数据写到文件中，当你数据读完的时候不代表你的数据已经写完了，因为还有一部分有可能会留在内存这个缓冲区中。这时候如果你调用了 close()方法关闭了读写流，那么这部分数据就会丢失，所以应该在关闭读写流之前先flush()，先清空数据。
```

 java的io流相当于一个数据流通的管道，这里面存在一个默认的数据缓冲区，大小是8k。当我们在进行io操作的时候，数据会经过这个缓冲区，然后保存到硬盘文件或其它存储设备文件中。如果保存过程中的数据少于8k之后,那么这时，它就有可能把少于8k的这部分数据缓存在缓冲区中，而不写进存储设备里面，因此，我们调用当前io流的flush()方法，清空当前缓冲区，即把数据完整的存储到文件中。

有人会问使用这种类的时候，难道必须使用 flush() 方法吗，当然不是喽？？！！有两种情况下可以不用调用 flush 方法。

（1）、写入的数据不小于8KB。

如下示例代码，byte 大小改为 8KB：

import java.io.BufferedOutputStream; 
import java.io.File; 
import java.io.FileOutputStream; 

public class Test { 	
    public static void main(String[] args) throws Exception { 	
        File file = new File("text.txt"); 		
        if (!file.exists()) { 	
            file.createNewFile(); 	
        } 		
        FileOutputStream fos = new FileOutputStream(file); 		
        BufferedOutputStream bos = new BufferedOutputStream(fos); 		
        byte[] b = new byte[1024*8]; 	
        bos.write(b); 		
        //bos.flush(); 
    }
} 
执行代码，会产生 8KB 大小的文本文件。

（2）、修改默认缓冲区大小

如下示例代码，修改一下构造 BufferedOutputStream 的方法，设置默认缓冲区大小为 1024。

File file = new File("text4.txt");
if (!file.exists()) {
    file.createNewFile();
}
FileOutputStream fos = new FileOutputStream(file);
BufferedOutputStream bos = new BufferedOutputStream(fos, 1024);
byte[] b = new byte[1024];
bos.write(b);
//bos.flush();
执行代码，会产生 1KB 大小的文本文件。

这里提醒一下，如果你的文件读写没有达到预期目的，十之八九是因为你没有调用 flush() 或者 close() 方法。

另外，字符流类大多数都实现了 flush() 或者 close() 方法，只不过，它们调用的是 StreamEncoder 类的该方法。该类位于 sun.nio.cs 包下面，其源码在我们JDK中是没有的。

可以点击 StreamEncoder.java 查看源码。

flush 与 Writer
该类 Writer 是一个抽象类，声明如下：

public abstract class Writer implements Appendable, Closeable, Flushable
Writer 类的 flush() 方法是一个抽象方法，其子类一般都实现了该方法。

所以，一般使用字符流之后需要调用一下 flush() 或者 close() 方法。

abstract public void flush() throws IOException;
细节请看JDK的API，或者Java的源码以及上面的 StreamEncoder 类源码。

今天就说到这里吧，本文主要借助Java IO中字节流与字符流的 flush() 方法，来说明学编程语言看源码和思考是很重要的。

总之，不管你使用哪种流（字符、字节、具有缓冲的流）技术，不妨调用一下 flush() 或者 close() 方法，防止数据无法写到输出流中。
————————————————
版权声明：本文为CSDN博主「veryitman」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/veryitman/article/details/6460726

### 输出流的close()和flush的区别

close()方法被调用前，会自动flush

close()关闭流对象，一旦关了，流对象就不能再用了

flush方法调用后，仅是把文件刷新到缓冲区，并不是把流关了，即调用完后还可以接着调用流