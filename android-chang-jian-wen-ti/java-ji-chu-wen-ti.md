# Java 基础

## 多态的原理

多态：一个引用变量到底会指向哪个类的实例，该引用变量发出的方法调用到底是哪个类中实现的方法，编译器是不确定的，必须在由程序运行期间才能决定。

原理：在JVM运行时区域，类相关的信息存放在**方法区，**在这些信息中有一个叫**方法表的区域，**该表包含有该类型所定义的所有方法的信息和指向这些方法实际代码的指针。

## 进程和线程的区别？

进程：可以理解为一个应用程序的执行过程，一旦运行，至少有一个进程。每个进程都有自己的地址空间，多任务的时候，一个进程显然不够，所以有了多线程。

线程：程序执行的最小单位。

> Android可以通过process设置多进程。

## 接口和抽象类的区别？

接口和抽象类都是提取对象的共性，声明抽象方法。面向对象重点在于复用抽象层，而不是复用具体代码。

相同点：

* 不可以直接实例化
* jdk 1.8之后，接口可以有实现方法，抽象类一直都支持

不同点：

* 通过接口 **implements** 去实现，抽象类通过 **extends** 继承去实现
* jdk 1.8之前接口只可以声明，不可以实现，抽象类是可以实现方法
* 接口成员变量默认为 public static final，必须赋初值，不能被修改

用法：**最常见的是缺省适配模式，声明用接口，同时给出一个抽象类，实现接口，这样业务既可以选择继承抽象类，也可以选择实现接口。**

## 静态属性和静态方法能被继承吗？

父类的静态属性和方法可以被子类继承

## 静态方法又是否能被重写呢？

不可以重写。

原因：

静态方法和属性是属于类的，调用的时候直接通过类名.方法名完成对，不需要继承机制及可以调用。如果子类里面定义了静态方法和属性，那么这时候父类的静态方法或属性称之为"隐藏"。如果你想要调用父类的静态方法和属性，直接通过父类名.方法或变量名完成，至于是否继承一说，子类是有继承静态方法和属性，但是跟实例方法和属性不太一样，存在"隐藏"的这种情况。

**总结：当父类引用指向子类对象，只会调用父类的静态方法，此行为并不具有多态性！所以子类重写父类的静态方法，并没有实际意义。**



