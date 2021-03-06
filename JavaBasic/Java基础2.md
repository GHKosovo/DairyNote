### 第一天

1. jvm是什么，其实我一点都不知道，但是现在我知道了，他处理字节码，让java编译后的字节码可以在不同的平台上运行，让平台无关性，正所谓一处编译，到处运行
2. mysql的优化：日志慢查询，其实就是让日志记录量少点；重构数据库；换引擎；用索引；
3. tomcat是什么，其实就是处理servlet/jsp的容器，而平常接触的spring等就是通过servlet这个出入口来执行网页任务的，发送请求/响应请求。
4. 何为多线程？多线程的最大特征是将一个进程进行继续拆分，简单理解就是：如果在WEB开发过程中，Tomcat是一个进程，那么在Tomcat里面会把每一个连接上它的用户作为一个线程存在
5. 对象序列化：用于存储和传输

### 第二天

1. JDK：Java Runtime Environment，Java开发工具包，提供了Java的开发环境和运行环境（JRE）。包含了编译Java源文件的编译器Javac，还有调试和分析的工具。JDK一般都包含有JRE，所以JDK是用于开发的。

2. JRE：Java Runtime Environment，Java运行环境，包含Java虚拟机及一些基础类库，如果只是运行JAVA程序，则只需要JRE，而不用JDK。

3. JVM：Java Virtual Machine，Java虚拟机，提供执行字节码文件的能力

   所以，如果只是运行Java程序，只需要安装JRE即可。

   另外注意，JVM是实现Java跨平台的核心，但JVM本身并不是跨平台的，不同的平台装有不同的JVM，它们能够将相同的.class文件，解释成不同平台所需要的字节码（机器码）；

4. ==和equals的区别

   #### == （比较的是值）

   比较基本的数据类型，比较的是数值；

   而比较引用类型：比较引用指向的值（地址）

   #### equals

   **默认比较也是地址，因为这个方法的最初定义在Object上，默认的实现就是比较地址**

   自定义的类，如果需要比较的是内容，那么就要学String，重写equals方法

6. final修饰类，表示类不可变，不可继承

   比如，String，不可变性

   final修饰方法，表示该方法不可重写

   比如模板方法，可以固定我们的算法

   final修饰变量，这个变量就是常量

   注意：

   修饰的是基本数据类型，这个值本身不能修改

   **修饰的是引用类型，引用的指向不能修改**

   **比如下面的代码是可以的**

   ```text
   final Student student = new Student(1,"Andy");
   student.setAge(18);//注意，这个是可以的！
   ```

7. jvm为每个线程创建一个栈，而这个栈是独享的，用于存放该线程**执行的方法们的信息。**StringBuilder一般都写在方法中，所以一般StringBuilder是线程安全的。

7. Integer&int（缓存&自动装箱和拆箱）：引用类型跟引用类型相比较，看边界（自动装箱）；如果是引用类型跟数值比较，看数值（自动拆箱）

   反编译：Interger.valueof(126);

   

11. List和Set的不同

    - List（有序，可重复）
    - Set（无序，不可重复）
    
    [参考链接](https://www.jianshu.com/p/6f0da4dfcb09)
    
13. 如何在双向链表插入新节点

14. HashSet的储存原理

    其实HashSet的底层原理采用的是HashMap

18. io流的分类和选择

    1.如何看是输入流还是输出流？以java程序为主体，而操作的文件为客体，那么从文件中读取就是输入流；从java程序输出就是输出流；

    2.根据传输单位：字节流，字符流

    3.传输数据是一个个来还是一个个来？一批就用-缓冲区（本质是数组）

    IO流的4大基类：InputStream,OutputStream,Reader,Writer

    字节流----一般用于二进制文件；字符流-----一般用域文本文件

19. serialVersionUID的作用是什么？

    当执行序列化的时候，会把对象写到磁盘中，会根据当前这个类的结构生成一个版本号ID，当反序列化的时候，程序会比较磁盘中的序列化版本号ID跟当前的类结构生成的版本号是否一致，如果一致则反序列化成功，否则失败。

    加上版本号，有助于当我们的类结构发生变化，依然可以把之前已经序列化的对象反序列化成功。

20. Java的异常体系

    ![image-20201201230951109](C:\Users\llj\AppData\Roaming\Typora\typora-user-images\image-20201201230951109.png)

    Error是虚拟机内部错误（虽然是我们无法解决的重大错误，但是一般是人为造成的）

    > 栈内存溢出错误：StackOverflowError(递归，递归层次太多或递归没有结束)
    > 堆内存溢出错误：OutOfMemoryError(堆创建了很多对象)

    Exception是我们编写的程序错误

    > RuntimeException：也称为LogicException
    > 为什么编译器不会要求你去try catch处理？
    > 本质是逻辑错误，比如空指针异常，这种问题是编程逻辑不严谨造成的（也就是程序员的代码出了问题）
    > 应该通过完善我们的代码编程逻辑，来解决问题

    非RuntimeException：

    > 编译器会要求我们try catch或者throws处理
    > 本质是客观因素造成的问题，比如FileNotFoundException
    > 写了一个程序，自动阅卷，需要读取答案的路径（用户录入），用户可能录入是一个错误的路径，所以我们要提前预案，写好发生异常之后的处理方式，这也是java程序健壮性的一种体现（也就是说你操作的时候可能没问题，但是换个人来可能就有问题，为了排除问题的发生，就得预防它的错误，捕获它）

21. ”static”关键字是什么意思？Java中是否可以覆盖(override)一个private或者是static的方法

static表明一个成员量或者是方法可以在没有实例化对象的情况下被访问，**故在static环境下也无法访问非static变量**；static的方法不能被覆盖，因为方法覆盖发生是基于运行时动态绑定，而static方法则是编译时静态绑定。static方法跟类的任何实例都不相关，所以概念上不适用。

java中也不可以覆盖private的方法，因为private修饰的变量和方法只能在当前类中使用，如果是其他的类继承当前类是不能访问到private变量或方法的，当然也不能覆盖。



