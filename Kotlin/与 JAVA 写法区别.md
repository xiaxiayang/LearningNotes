> 笔记内容来自 hencoder 的 https://kaixue.io/kotlin-basic-2/

###  constructor

构造函数
- Java 中构造器和类同名，Kotlin 中使用 `constructor` 表示。
- Kotlin 中构造器没有 public 修饰，因为默认可见性就是公开的

### init

Kotlin 的 init 代码块和 Java 一样，都在实例化时执行，并且执行顺序都在构造器之前。

- Java 用 {} 表示 init 代码块  
- Kotlin 用 init 关键字

### final

| 语言 | 关键字 |是否是默认值|
| ------ | ------ | ------ |
|  Java | final  | 非默认 |
| Kotlin | val  | 默认。这样设计的原因是保证了参数不会被修改|

### object
 object 不是类，像 class 一样在 Kotlin 中属于关键字,意思是对象。

 用 object 修饰的对象中的变量和函数都是静态的
 ```
 object Sample {
    val name = "A name"
}
```
上述代码含义，创建一个类，并创建一个这个类的对象。

在代码中如果要使用这个对象，直接通过它的类名就可以访问：
`Sample.name`

1、用 object 可以实现单例模式,且线程安全
```
// 👇 class 替换成了 object
object A {
    val number: Int = 1
    fun method() {
        println("A.method()")
    }
}   
```

2、用 object 创建匿名类
```
val listener = object: ViewPager.SimpleOnPageChangeListener() {
    override fun onPageSelected(position: Int) {
        // override
    }
}
```

### companion object
companion 可以理解为伴随、伴生，表示修饰的对象和外部类绑定。

Java 静态变量和方法的等价写法：companion object 变量和函数
```
class A {
    companion object {
        var c: Int = 0
    }
}
```
直接调用 `A.c`

### top-level property / function 声明
把属性和函数的声明不写在 class 里面。

这样写的属性和函数，不属于任何 class，而是直接属于 package。
```
package com.hencoder.plus
​
// 👇 属于 package，不在 class/object 内
fun topLevelFuncion() {
}
```
调用的时候:
```
import com.hencoder.plus.topLevelFunction // 👈 直接 import 函数
​
topLevelFunction()
```

在实际使用中，在 object、companion object 和 top-level 中该选择哪一个?
- 如果想写工具类的功能，直接创建文件，写 top-level「顶层」函数。
- 如果需要继承别的类或者实现接口，就用 object 或 companion object。

### 常量
Kotlin 中只有基本类型和 String 类型可以声明成常量。

| 语言 | 关键字 |示例|
| ------ | ------ | ------ |
  |  Java |  static final  | public static final int CONST_NUMBER = 1; |
| Kotlin | const   | const val CONST_SECOND_NUMBER = 2|

### 集合
| 语言 | 类型 |含义|
| ------ | ------ | ------ |
  |  Java/Kotlin |  List  | 以固定顺序存储一组元素，元素可以重复 |
  |  Java/Kotlin |  Set  | 存储一组互不相等的元素，通常没有固定顺序 |
  |  Java/Kotlin |  Map  | 存储 键-值 对的数据集合，键互不相等，但不同的键可以对应相同的值 |

  List 集合的创建
  - Java
  ```
  List<String> strList = new ArrayList<>();
strList.add("a");
strList.add("b");
strList.add("c"); // 👈 添加元素繁琐
  ```
  - Kotlin
  ```
  val strList = listOf("a", "b", "c")

  ```


  Set 集合的创建

  - Java
  ```
  Set<String> strSet = new HashSet<>();
strSet.add("a");
strSet.add("b");
strSet.add("c");
  ```

- Kotlin
```
val strSet = setOf("a", "b", "c")
```

Map 集合的创建

- Java
```
Map<String, Integer> map = new HashMap<>();
map.put("key1", 1);
map.put("key2", 2);
map.put("key3", 3);
map.put("key4", 3);
```
- Kotlin
```
val map = mapOf("key1" to 1, "key2" to 2, "key3" to 3, "key4" to 3)
```

mapOf 的每个参数表示一个键值对，to 表示将「键」和「值」关联

### 可变集合/不可变集合
Kotlin 中不可变（只读）集合：集合的 size 不可变、集合中的元素值不可变


| 类型| 是否可变 | 函数 |转换为可变|转换为可变的备注|
| ------ | ------ | ------ | ------ | ------ |
|  List| 不可变| listOf() | toMutableList()|返回的是一个新建的集合|
|  List|  可变  | mutableListOf() |--|--|
|  Set| 不可变| setOf() | toMutableSet()|返回的是一个新建的集合|
|  Set|  可变  | mutableSetOf() |--|--|
|  Map| 不可变| mapOf() | toMutableMap()|返回的是一个新建的集合|
|  Map|  可变  | mutableMapOf() |--|--|

有 `mutable` 前缀的函数创建的是可变的集合，没有 `mutbale` 前缀的创建的是不可变的集合(可以通过 `toMutable*()` 变成可变集合，但生成的是一个新的集合)。

### 可见性修饰符

| 修饰符|描述 |
| ------ | ------ |
|  public| 公开，可见性最大，哪里都可以引用|
|  private|  私有，可见性最小，根据声明位置不同可分为类中可见和文件中可见  |
|  protected| 私有，可见性最小，根据声明位置不同可分为类中可见和文件中可见|
|  internal|  内部，仅对 module 内可见  |
