# Spectre 编程语言

这是 `Spectre` 编程语言得主仓库，主要包含编译器、文档和开发计划。

`Spectre` **幽灵**是这款编程语言的暂定名，来源于《共产党宣言》的第一句话：「一个**幽灵**，共产主义的**幽灵**，在欧洲游荡」。

这款语言应该具备以下特性：

* 编译型语言。
* 代码跨平台。
* 支持面向对象的程序设计。
* 支持反射。
* 具备异常。
* 空安全。
* 所有权和生命周期。

## 走马观花

下面**可能**是用 `Spectre` 编写的 Hello World 程序：

```spectre
fun main(args: Array<String>) = println("Hello World!")
```

## 特性

我们正在设计 `Spectre` 语言的草案，下面是一些以往编程语言中令人着迷的特性，我们正在考虑将哪些特性添加进 `Spectre` 中。

### 空安全

`Type?` 是一个可以指向 `null` 的指针，而 `Type` 是不允许指向 `null` 的指针。

```spectre
// 下面的语句定义一个可以为 `null` 的整型数字
val i1: Int? = null

// 下面的代码将会编译错误，因为使用 `null` 初始化不可为 `null` 的类型
val i2: Int = null
```

### 类型条件

运用 `Type{condition}` 可以声明一个满足某条件的类型。例如，`Int{!=0}` 是一个取值非 `0` 的整型数字。

```spectre
// 下面的代码将会编译错误，因为 `int` 不能为 `0`
val int: Int{? != 0} = 0
```

这些条件未必是编译期能验证的条件。例如，`spectre.lang.List` 中有一个方法 `get`：

```spectre
operator fun get(index: Int{? >= 0 && ? < length}) = data[index]
```

`size` 属性不一定是编译时能确定的，但依旧可以写入类型条件。编译器如果不确定，将会在合适的时候插入断言。