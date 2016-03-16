---
layout: post
title: Java调用外部命令使用waitFor()方法阻塞或锁死
categories: Java
description: 解决线程锁死
keywords: waitFor(),调用外部命令,阻塞，锁死
---

　　在 Linux 下调用外部命令(Shell命令)，或者可执行的二进制文件， Java 中依赖 Process 和 Runtime 两个类,查看官方API可以知道 Process 抽象类中通过 ProcessBuilder.start() 和 Runtime.exec 两个方法来创建本地进程的。

　　在官方API中值得注意的是：创建的子进程是没有他们自己的 terminal 或者 console 的。所有标准的 I/O 都会重定向到父进程，并且通过方法　getOutStream(), getInputStream(), 和 getErrorStram(),　分别获得标准输出，输入和错误流。**由于 JVM 提供标准输入和输出流的缓冲区大小是十分有限，很快的读入或者输出流将会导致进程阻塞或者锁死**。

　　我在调用外部命令的时候就遇到了这种情况，第一次调用的命令输出很少，循环执行命令，使用 waitFor() 让线程等待，直到上一个线程结束了再执行下一个命令，很成功的执行完了所有的命令。然而我再次调用一个不同的二进制可执行文件时候，由于输出很多，使用　waitFor()　时候，执行第一次就一直假死在那，不在继续执行后面的代码块了，最终发现问题就出在　API　中提到的**导致进程阻塞或者锁死**这一步。

### waitFor()阻塞或锁死解决办法
 
* 办法就是再调用两个线程分别输出标准输出流和标准错误流，这样就可以解决标准输出和错误流缓冲区限制而导致的阻塞和锁死状态了。

###　解决线程阻塞或锁死的类

```java
class RunThread extends Thread
{
    InputStream is;
    String type;
    
    RunThread(InputStream is, String printType)
    {
        this.is = is;
        this.printType = printType;
    }
    
    public void run()
    {
        try
        {
            InputStreamReader isr = new InputStreamReader(is);
            BufferedReader br = new BufferedReader(isr);
            String line=null;
            while ( (line = br.readLine()) != null)
                System.out.println(PrintType + ">" + line);
            } catch (IOException ioe)
              {
                ioe.printStackTrace();
              }
    }
}
```

###执行外部命令的主函数

*  主函数用Runtime.getRuntime().exec()来调用外部命令

```java

public class Runpro {
    public void main(String arg[]){ 
        try {
            System.out.println("cmd start");
            Process p = Runtime.getRuntime().exec("pwd");  //调用Linux的相关命令  
            new RunThread(p.getInputStream(), "INFO").start(); 
            new RunThread(p.getErrorStream(),"ERR").start();
            int value = p.waitFor();
            if(value == 0)
        	System.out.println("complete");
            else
        	System.out.println("failuer");
        } catch (IOException e) {
            e.printStackTrace();
        }
       }
    }
    
```

### 参考资料

* [JAVA API Process](http://docs.oracle.com/javase/8/docs/api/)
* [ JAVA 进程 waitFor() 阻塞总结](http://www.linuxidc.com/Linux/2011-11/47493.htm)
* [ JAVA 调用其他程序时候 waitFor() 阻塞](http://www.cnblogs.com/yejg1212/archive/2013/06/02/3114242.html)
