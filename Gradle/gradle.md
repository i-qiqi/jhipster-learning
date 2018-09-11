#v Gradle
>  [读懂gradle语法](https://help.gradle.org)
>
> [Gradle user guide](http://blog.didispace.com/books/GradleUserGuide/)
>
> [阿拉神农](https://www.jianshu.com/p/6dc2074480b8)

## Groovy
### Groovy中bean的概念
- Groovy为每一个字段都会自动生成getter和setter，并且我们可以通过像访问字段本身一样调用getter和setter
### 闭包的Delegatej机制
> [Groovy闭包](https://blog.csdn.net/u014099894/article/details/51118703)

- `闭包` ： A closure in Groovy is an open, anonymous, block of code that can take arguments, return a value and be assigned to a variable.（Groovy中的闭包是一段 开放的、匿名的代码)。
  -  `this`： 包所在的最近的类 .class
  - `owner` : 定义闭包的宿主，不仅仅是类，还可能是一个闭包
  -  `delegate` : 代理
- `闭包的Delegation` : The ability to change the delegate or change the delegation strategy of closures make it possible to design beautiful domain specific languages (DSLs) in Groovy.(Groovy中的闭包具有能够改变代理或代理策略的这种能力，使得我们能够使用它设计出很优美的DSL语言。）
###
