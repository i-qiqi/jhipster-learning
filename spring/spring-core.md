# Spring
### DefaultListableBeanFactory
## 注册BeanDefinition
> <font color="red">DoLoadBeanDefinitions</font>

- ### 获取对XML文件模式的验证模式
  - DTD vs XSD 区别
- ### 加载XML文件，并得到对应的Document
- ### 根据返回的Document注册Bean信息

## 加载Bean
> <font color="red">DoGetBean</font>

- ### 转换对应的beanName
  -  去除FactoryBean的修饰符
  - 取指定alias所表示的最终的beanName
- ### 尝试从缓存中加载单例
  - 单例缓存
  - `singletonFactories`
  - Spring创建bean的原则:不等bean创建完成就把创建bean的`ObjectFactory`曝光到缓存中，一旦下一个bean的创建依赖上一个bean的时候则直接使用ObjectFactory


  ## 资料搜集
  - [`田小波源码分析`](https://www.tianxiaobo.com/2018/05/30/Spring-IOC-%E5%AE%B9%E5%99%A8%E6%BA%90%E7%A0%81%E5%88%86%E6%9E%90%E7%B3%BB%E5%88%97%E6%96%87%E7%AB%A0%E5%AF%BC%E8%AF%BB/)
  - [`黄忆华tiny-spring`](https://www.zybuluo.com/dugu9sword/note/382745)
  - [`Spring揭秘`](https://www.dropbox.com/s/93b7vkukf27t5q5/spring%E6%8F%AD%E7%A7%98.pdf?dl=0)
  - [`Spring源码深度分析`](https://www.dropbox.com/s/xot5ipi6hkmco09/Spring-deep.pdf?dl=0)
