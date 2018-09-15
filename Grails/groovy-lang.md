# Groovy

## Groovy基础
### Groovy beans
  - 自动生成访问器方法
  - JavaBeans（包括GroovyBeans）的简化访问方式
  - 事情处理器的简化注册？？？

### Gstrings
字符串能出现在单引号或者双引号中，在双引号的字符串中允许使用占位符，占位符在需要的时候将自动解析，这是一个GString类型
### Regex expression
  - `=~` : find operator

### 一切事物皆对象，数字也是

### 容器类型——list/map/ranges
- `list` :
```python
def roman = ['', 'I', 'II', 'III', 'IV', 'V', 'VI', 'VII']
```
- `map` :
```python
def http = [
100 : 'CONTINUE',
200 : 'OK',
400 : 'BAD REQUEST' ]
```
- `range` : range的概念有一个直观的
感觉——一个有效的开始点和一个结束点
```ruby
def x = 1..10
assert x.contains(5)
assert x.contains(15) == false
assert x.size() == 10
assert x.from == 1
assert x.to == 10
assert x.reverse() == 10..1
```

### 代码块：闭包(*Closure*)
> <font color="HotPink">在面向对象语言，方法对象模式（ Method-Object pattern）通常用来模拟一个行为：为一个目的定义一个独立的方法接口，这个接口的实例能够传递一组参数给方法，然后
调用这个接口方法;
>
>java使用匿名内部类来达到这种效果，但是语法是难以理解的，并且他们的意
义被限制在调用方法的内部，和访问调用方法的内部变量。 groovy允许将闭包简明的内联在代码中，清晰而强大，实际上提升方法对象模式到语言顶级类的位置</font>

```ruby
# syntex structure : closure in braces.
{ [parameter...]->statement}
```
- [`Java内部类`](https://www.cnblogs.com/dolphin0520/p/3811445.html) ：成员内部类、局部内部类、匿名内部类和静态内部类
  - [`匿名内部类`](http://www.cnblogs.com/chenssy/p/3390871.html)：
    - 使用匿名内部类时，我们必须是继承一个类或者实现一个接口，但是两者不可兼得，同时也只能继承一个类或者实现一个接口;
    - 匿名内部类中是不能定义构造函数的;
    - 匿名内部类中不能存在任何的静态成员变量和静态方法;
    - 匿名内部类为局部内部类，所以局部内部类的所有限制同样对匿名内部类生效;
    - 匿名内部类不能是抽象的，它必须要实现继承的类或者实现的接口的所有抽象方法;
    - 当所在的方法的形参需要被内部类里面使用时，该形参必须为final。
- 闭包有一组可选的参数列表，通过`->`表示列表的结束;
- 闭包是 groovy 提供的进行`透明回调`的一种方式;
- 控制逻辑和每次迭代处理的逻辑分开;
- 处理资源的时候使用闭包；
  - 一般的 java 解决方法：`使用内部类`
  - 另外一种方式：`使用模板方法模式`
- 声明闭包：
```ruby
# 简单的声明
log = ‘’
(1..10).each{ log += it }
# 赋值的方式
def printer = {line -> println line }
# 方法的返回值
def Closure getPrinter() {
  return { line -> println line }
}
# 引用一个方法作为闭包 / 重用已有的声明:一个方法
# groovy 让你重用你已经在方法中存在的代码，但是作为一个闭包，引用一个方法作为闭包是使用reference.&操作符， reference 是闭包调用时使用的对象实例
def c = reference.&someMethod
```

- 使用闭包
- 闭包方法

  类[groovy.lang.Closure](http://docs.groovy-lang.org/latest/html/api/groovy/lang/Closure.html)是一个Java普通类
  - 参数类型：`getParameterTypes`
  - 怎样使用闭包实现`curry`？[know more](https://www.ibm.com/developerworks/cn/java/j-pg08235/)

    curry 的基本思想是一个多个参数的函数， 传递较少的参数给函数来固定一些值，一个典型的例子是选择一些数 n 并且传递给函数与后面传递的单个参数进行相加。Curry 最强大的地方是当闭包的参数是闭包本身的时候，这通常在函数式编程时使用到。
 - 分类 ： `isCase`
 - 克隆 ： `asWriter`
- 闭包的范围 [know more](http://www.paulgraham.com/icad.html)

  对于闭包来说，闭包的花括号就像 new 关键字一样，这后面是闭包和方法的根本差别，方法在类产生的时候就被构建，而且只会构建一次，闭包对象在运行的时候被构建，并且相同的代码也有可能被构建多次。
  - 什么样的本地变量可以被访问？
    - `引用原始上下文`：花括号显示了闭包声明的时间，不是执行的时间。 在闭包的声明期间， 闭包可以对本地变量 x 进行读和写操作
  - this（当前对象）引用到的是什么？
    - this 引用时有个特例，在闭包中，你正确的猜想 this 将引用到
当前对象，这是闭包对象本身，在另一方面，使用 this.reference 和直接使用 reference 来处
理本地引用是没有区别的
  - 什么属性和方法是可以访问的？
    -  his 引用到闭包，而不是声明闭包的对象，在这里，闭包有点糊弄人，它们将所有的方法调用代理给delegate对象， delegate 缺省是声明闭包的对象（也就是 owner） 通过一个名称为 owner 的变量可以获取到声明闭包的对象，这样保证了闭包在它的上下文中运行。
- 从闭包返回结果
  - 闭包最后一个表达式执行的结果， 并且这个结果被返回，这叫做结束返回（ end return），在最后的语句前面的return关键字是可选的。
  - 使用return关键字从闭包的任何地方返回
    - 在闭包体外面，任何出现return的地方都会导致离开当前方法，当在闭包体内出现return
语句时，这仅仅结束闭包的当前计算，这是更加有限的，例如，当使用List.each时，从闭包的提前返回不会引起从each方法的提前返回——闭包仍旧会在list的下一个元素出现时被调
用。

### 结构控制
- groovy中的结构控制简单的如if-else， while， switch和try-catch-finally，这与java的结构控制是一样的
- 在条件中， null被处理成false， not-null被处理成true， for循环有一个for(i in x){body}的标记， x可以是任何对象， groovy知道怎样迭代它
```java
//在一行的if语句
if (false) assert false
//null表示false
if (null){
assert false
}
else{
assert true
}
//典型的while
def i = 0
while (i < 10) {
i++
}
assert i == 10
//迭代一个range
def clinks = 0
for (remainingGuests in 0..9) {
clinks += remainingGuests
}
assert clinks == (10*9)/2
//迭代一个列表
def list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
for (j in list) {
assert j == list[j]
}
//以闭包为参数的each方法
list.each() { item ->
assert item == list[item]
}
//典型的switch
switch(3) {
case 1 : assert false; break
case 3 : assert true; break
default: assert false
}
```

## 在 java 环境中运行 groovy

### 在JVM中运行groovy类
- `Precompiled mode` : `groovyc`编译所有的*.groovy为java的*.class文件，把这些*.class文件放在java类路径中，通过`java类加载器`来加载这些类；
```bash
Code.groovy——>Code.class——>Loded Class
```
- `Direct mode` : `groovy的类加载器`在运行时直接加载*.groovy文件并且生成对象，在
这种方式下，没有生成任何*.class， 但是生成了一个java.lang.Class对象的实例；
```bash
Code.class——>Loded Class
```

### GDK:groovy 类库
> Groovy的类库是JDK类库的扩展， groovy类库提供了一些新的类（例如，简化数据库访问和XML处理的类），也为已经存在的java类增加了功能，这些附加的功能就是GDK，为java类在兼容性、功能性和可表达性方面提供了重要的优势；

`我的类就是你的类`：每一个groovy对象都是一个java对象实例，在运行时他们都指向同一个对象

### groovy 的生命周期
- Groovy的语法是`面向行`的，但是执行groovy代码确不是这样的，不像别的脚本语言，groovy代码不是一行一行的解释执行的。相反， groovy代码被完整的转换，通过转换器产生一个java类，产生的这个类是groovy和java之间的粘合剂。产生的groovy类的格式与java字节码的格式是一样的
- `Groovy是动态的` : 使动态语言如此强大的原因是在表面上看来在运行时修改类的能力
