# Introduction


Java® 编程语言是一种通用、并发、基于类的面向对象编程语言。它的设计目标是使许多程序员能够轻松掌握并熟练使用这门语言。Java 编程语言与 C 和 C++ 有一定关系，但其组织方式有很大不同，许多 C 和 C++ 中的特性被省略，同时吸收了其他语言的一些思想。Java 被设计为一种生产语言，而非研究语言，因此，Java 的设计避免了包含未经验证的新特性。

Java 编程语言是强类型且静态类型的。本规范清晰地区分了编译时错误（可以并且必须在编译时检测到）与运行时错误（在程序执行时发生）。编译时通常包括将程序转换为与平台无关的字节码表示。运行时活动包括加载和链接执行程序所需的类、可选的机器代码生成、程序的动态优化以及程序的实际执行。

Java 编程语言是一种相对高级的语言，因为语言本身并不直接暴露机器表示的细节。它内置了自动存储管理，通常采用垃圾回收机制，以避免像 C 语言中的 free 或 C++ 中的 delete 这类手动内存管理可能带来的安全问题。高性能的垃圾回收实现可以通过设定暂停时间来支持系统编程和实时应用。语言本身不包含任何不安全的结构，比如没有进行边界检查的数组访问，因为这些不安全的结构会导致程序表现出不可预期的行为。

Java 编程语言通常会被编译成字节码指令集，并采用《Java 虚拟机规范，Java SE 23 版》中定义的二进制格式。


第4章 介绍了类型、值和变量。
第5章 介绍了类型转换和数值提升。
第6章 介绍了声明和命名，以及如何确定名称的含义（即某个名称指代的声明）。
第7章 介绍了程序的结构，程序被组织为包。
第8章 介绍了类。
第9章 介绍了接口。
第10章 介绍了数组。
第11章 介绍了异常，它们是不可恢复的，并且与语言语义和并发机制完全集成。
第12章 介绍了程序执行过程中发生的活动。
第13章 介绍了二进制兼容性
第14章 介绍了代码块和语句
第15章 介绍了表达式。
第16章 介绍了语言确保局部变量在使用之前已被明确赋值的精确方式。
第17章 介绍了线程和锁的语义
第18章 介绍了多种类型推导算法
第19章 介绍了语言的语法文法。

大部分示例程序都可以直接执行，并且与下面的形式相似：
```
class Test {
    public static void main(String[] args) {
        for (int i = 0; i < args.length; i++)
            System.out.print(i == 0 ? args[i] : " " + args[i]);
        System.out.println();
    }
}
```


# Classes
类声明定义了一个新类，并描述了它的实现方式
- 顶级类
- 嵌套类
   - 成员类
   - 局部类
   - 匿名类
- 内部类
- 枚举类
- 记录类

类的修饰符与继承
类体的成员