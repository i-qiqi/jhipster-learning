# AccessController.doPrivileged()
# ServiceLoader
- [Java SPI - ServiceLoader 使用简介 java 优雅地获取接口实现](https://blog.csdn.net/ryo1060732496/article/details/80472013)
- [ServiceLoader : JAVA SPI 机制](https://blog.csdn.net/conquer0715/article/details/50728458)
- [ServiceLoader实现原理](https://blog.csdn.net/is_zhoufeng/article/details/50722440)
- [ServiceLoader使用](https://www.jianshu.com/p/7601ba434ff4)
- [SPI(Service Provider Interface)机制](https://www.cnblogs.com/wade-luffy/p/8578812.html)

# ClassLoader
## 类加载器 :
  - 根加载器 `Bootstrap ClassLoader` : 主要加载核心类库，%JRE_HOME%/lib下的rt.jar, resources.jar, charsets.jar和class等。
 ```bash
 # 启动jvm时指定-Xbootclasspath和路径改变根加载器的加载目录，追加
 java -XBootclasspath/a:path
 ```
  - 扩展加载器`Extension ClassLoader` : 加载%JRE_HOME%\lib\ext下的jar包和class文件
  ```bash
  # 选定指定的目录
  java -D java.exr.dirs=...
  ```
  - `Appclass ClassLoader` : 加载当前应用的classpath下的所有类

## 加载顺序
- System property `sun.boot.class.path` :
```bash
# outputs
/usr/lib/jvm/java-8-oracle/jre/lib/resources.jar
/usr/lib/jvm/java-8-oracle/jre/lib/rt.jar
/usr/lib/jvm/java-8-oracle/jre/lib/sunrsasign.jar
/usr/lib/jvm/java-8-oracle/jre/lib/jsse.jar
/usr/lib/jvm/java-8-oracle/jre/lib/jce.jar
/usr/lib/jvm/java-8-oracle/jre/lib/charsets.jar
/usr/lib/jvm/java-8-oracle/jre/lib/jfr.jar
/usr/lib/jvm/java-8-oracle/jre/classes
```
- System property `java.ext.dirs` :
```bash
# outputs :
/usr/lib/jvm/java-8-oracle/jre/lib/ext
/usr/java/packages/lib/ext
```
- System property `java.class.path`
```bash
/usr/lib/jvm/java-8-oracle/jre/lib/charsets.jar
/usr/lib/jvm/java-8-oracle/jre/lib/deploy.jar
/usr/lib/jvm/java-8-oracle/jre/lib/ext/cldrdata.jar
/usr/lib/jvm/java-8-oracle/jre/lib/ext/dnsns.jar
/usr/lib/jvm/java-8-oracle/jre/lib/ext/jaccess.jar
/usr/lib/jvm/java-8-oracle/jre/lib/ext/jfxrt.jar
/usr/lib/jvm/java-8-oracle/jre/lib/ext/localedata.jar
/usr/lib/jvm/java-8-oracle/jre/lib/ext/nashorn.jar
/usr/lib/jvm/java-8-oracle/jre/lib/ext/sunec.jar
/usr/lib/jvm/java-8-oracle/jre/lib/ext/sunjce_provider.jar
/usr/lib/jvm/java-8-oracle/jre/lib/ext/sunpkcs11.jar
/usr/lib/jvm/java-8-oracle/jre/lib/ext/zipfs.jar
/usr/lib/jvm/java-8-oracle/jre/lib/javaws.jar
/usr/lib/jvm/java-8-oracle/jre/lib/jce.jar
/usr/lib/jvm/java-8-oracle/jre/lib/jfr.jar
/usr/lib/jvm/java-8-oracle/jre/lib/jfxswt.jar
/usr/lib/jvm/java-8-oracle/jre/lib/jsse.jar
/usr/lib/jvm/java-8-oracle/jre/lib/management-agent.jar
/usr/lib/jvm/java-8-oracle/jre/lib/plugin.jar
/usr/lib/jvm/java-8-oracle/jre/lib/resources.jar
/usr/lib/jvm/java-8-oracle/jre/lib/rt.jar
/home/bqzhu/Desktop/workspace/java8-programming-examples/target/classes
```

## 双亲委托机制

## 线程上下文类加载器`Context ClassLoader`
- 只是一个概念
- Context ClassLoader 默认是AppClassLoader,可以被重新设置成自定义的ClassLoader

## Reference
- [深入分析Java ClassLoader原理](https://blog.csdn.net/xyang81/article/details/7292380)
- [一看你就懂，超详细java中的ClassLoader详解](https://blog.csdn.net/briblue/article/details/54973413)
