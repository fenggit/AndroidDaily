# Kotlin - 高级用法

## 一、操作符

Kotlin 函数的对象创建的三种方式：

* 双引号
* 匿名函数 
* Lambda表达式

### 双引号（::）

双引号（::）：**函数引用**，表示把一个方法当做一个参数，传递到另一个方法中进行使用，就是引用一个方法。

**场景一：计算 （ 2 + 3 ）\* 5**

```text
fun main() {
    
    // 方法一：
    val a1 = add(2, 3)
    val a2 = mul(a1, 5)
    println("cal : ${mul(add(2, 3), 5)}")

    // 方法二：
    println("cal : ${mul((::add)(2, 3), 5)}")

}

/**
 * 加法
 */
fun add(a: Int, b: Int) = a + b

/**
 * 乘法
 */
fun mul(a: Int, b: Int) = a * b
```

 **Kotlin 函数并不能传递，传递的是对象，匿名函数和Lambda表达式其实都是对象**

```text
// 函数赋值，表示函数类型的对象，这个对象具有invoke方法，
// 可以把这个当做对象一样使用.
// 指向对象的引用，这个对象复制了原函数的功能，但它并不是原函数
val a = ::add        // a 是对象，add不是对象
a(1, 2)              // 调用函数
a.invoke(1, 2)       // 等价于上面
(::add).invoke(1, 2) // 等价于上面
(::add)(1, 2)        // 等价于上面

val c = a            // 验证是对象
```

 **场景二：将int数字转成字符串**

**匿名函数的写法**

```text
// 匿名函数，注意：kotlin的匿名函数是对象
// Kotlin 函数并不能传递，传递的是对象，匿名函数和Lambda表达式其实都是对象
val c0 = fun(p: Int): String {
    return p.toString()
}
println(c0(1))
```

 **Lambda 表达式的写法**

> { 参数1: 类型, 参数2: 类型 -&gt; 表达式 }

```text
// Lambda表达式的写法，返回值不用写return
val c1: (Int) -> String = {
    it.toString()
}

println(c1(1))

// Lambda 表达式的写法，和上面的结果一样
val c2 = { p: Int ->
    p.toString()
}
println(c2(1))
```

### 高阶函数

```text
//  高阶函数，传递函数的参数
//  其中：
//    （Int）是指传递一个int类型参数
//     String:返回值类型
fun t1(a: (Int) -> String): String {
    return a(1)
}
```

```text
// 无参数无返回类型
() -> Unit
```

 



## 二、函数

### Main函数的写法

```text
fun main(args: Array<String>) {

}

or

fun main() {

}

```

Java 👈  = 👉 Kotlin

![](../.gitbook/assets/image%20%2819%29.png)

### 可变参数vararg

vararg 关键字：主要用于无法确定传递多少个参数

**场景一：传递任意一组数字，计算所有数字的总和**

```text
fun main() {
    println(add(1, 2, 3, 4, 5, 6))
}


fun add(vararg arr: Int): Int {
    var count = 0
    for (value in arr) {
        count += value
    }
    return count
}
```

![](../.gitbook/assets/image%20%2818%29.png)

### 接口冗余问题



