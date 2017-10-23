# Spring 4 学习笔记

# I.Spring 框架概述

## 1.开启 Spring 之旅
## 2 Spring 框架概述

### 2.1 依赖注入和控制反转


### 2.2 模块
Spring 框架的各个特性被组织成20个模块。这些模块被分成：

- 核心容器：Core container
- 数据访问：Data Access
- Web
- 切面编程：AOP
- Instrumentation
- 消息：Messaging
- 测试：Test

![Spring 框架总览](http://spring.cndocs.ml/images/spring-overview.png)

#### 2.2.1 核心容器
核心容器包含四个：

- `spring-core`：core 和 beans 提供了整个框架的基础部分，包括 IoC（控制反转） 和 DI（依赖注入）
- `spring-beans`：
- `spring-context`：建立在前两者基础之上，提供框架式访问对象的方式，类似于 JNDI 注册。[扩展阅读：JNDI 是什么？](http://blog.csdn.net/zhaosg198312/article/details/3979435)
- `spring-expression`：提供一种强大的在运行时查询操作对象的表达式语言。是 JSP2.1 中 unified expression 的扩展。

#### 2.2.2 AOP 和 Instrumentation
- `spring-AOP`：就不说了
- `spring-aspects`：集成了 AspectJ（定义了AOP实现的语法，它有一个专门的编译器用来生成遵守Java字节编码规范的Class文件。）[扩展阅读：AspectJ](http://www.jianshu.com/p/27b997677149)
- `spring-instrument`：提供了类 instrumentation 支持和使用在某些应用服务器上的类加载器实现。[扩展阅读：java instrument 是什么？可改写类文件](http://jiangbo.me/blog/2012/02/21/java-lang-instrument/)

#### 2.2.3 Messaging
- `spring-messaging`：包含了 Spring Integration 的高度抽象。

#### 2.2.4 Data Access

- `spring-jdbc：JDBC抽象层，消除冗长的JDB编码和解析数据库提供商特定错误代码。
- `spring-tx`：编程和声明式事务管理。
- `spring-orm`：为流行的对象关系映射API提供集成层，包括：Mybatis、Hibernate 等，使用 spring-orm 模块可以将这些 O/R 映射框架与 Spring 提供的其他功能结合使用，例如前面提到的事务。
- `spring-oxm`：提供 Object/XML 映射的实现，如 JAXB、Castor、XMLBeans、JiBX 和 XStream
- `spring-jms`：生成和消费消息的功能。

#### 2.2.5 Web
- `spring-web`：基本的面向 Web 的集成功能，如：多部分文件上传，Servlet监听器，面向 Web 的应用程序上下文初始化 IoC容器。等
- `spring-webmvc`：（也称为 Web-Servlet模块）包含用于Web应用程序的Spring MVC实现。
- `spring-websocket`：
- `spring-webmvc-portlet`：（Web-Porlet模块）提供了在 Porlet环境中使用的MVC实现。

#### 2.2.6 Test
- `spring-test`：支持 JUnit 或 TestNG 对Spring组件进行单元测试和集成测试。 它提供了 Spring ApplicationContext 的一致加载和这些上下文的缓存。还提供可用于孤立测试代码的模拟对象。

### 2.3 使用场景
- [扩展阅读：Spring循环依赖检查算法分析（其实就是有向图的深度遍历算法）](http://jingzhongwen.iteye.com/blog/2208921)
- [扩展阅读：跟我学Spring3（3.2）:DI之循环依赖](http://jinnianshilongnian.iteye.com/blog/1415278)

#### 2.3.1 依赖管理和命名约定
如果出现jar 冲突等问题，可以使用 `spring-framework-bom`，确保所有依赖（直接和传递）都是相同的版本。如下：

	<dependencyManagement>
	    <dependencies>
	        <dependency>
	            <groupId>org.springframework</groupId>
	            <artifactId>spring-framework-bom</artifactId>
	            <version>4.1.3.RELEASE</version>
	            <type>pom</type>
	            <scope>import</scope>
	        </dependency>
	    </dependencies>
	</dependencyManagement>

#### 2.3.2 Logging
- `commons-logging`：它具有运行时发现算法，可以在类路径中找其他日志框架，并使用它认为合适的记录框架。如果没有可用的，则使用 JDK 自带的。

##### 不使用 commons-logging
两种方式关闭：
- 排除 `spring-core` 模块的依赖关系
- 用一个空的jar库替换 commons-logging 依赖。

	<dependencies>
	    <dependency>
	        <groupId>org.springframework</groupId>
	        <artifactId>spring-core</artifactId>
	        <version>4.1.3.RELEASE</version>
	        <exclusions>
	            <exclusion>
	                <groupId>commons-logging</groupId>
	                <artifactId>commons-logging</artifactId>
	            </exclusion>
	        </exclusions>
	    </dependency>
	</dependencies>

##### 使用 SLF4J
后期使用时在做搜索。

##### 使用 Log4J

# II.Spring 4.x的新功能
## 3.Spring 4.0 增强和新功能
完全支持 java 8。

### 3.1 改进的入门体验
- [spring.io](https://spring.io/) 提供了一系列的入门指南。

### 3.2 移除过时的包和方法
### 3.3 Java 8
支持 Java 8 的一些特性。最低兼容 java6
### 3.4 Java EE 6和7
### 3.5 Groovy DSL 定义 Bean
### 3.6 核心容器改进

### 3.7 常规 Web 改进
### 3.8 WebSocket、SockJS 和 STOMP 消息、
### 3.9 测试改进

## 4.Spring 4.1 增强和新功能
### 4.1 JMS 改进
### 4.2 Caching（缓存）改进

### 4.3 Web 改进
### 4.4 WEbSocket STOMP消息改进
### 4.5 测试改进

# Part III.核心技术
## 5.IoC 容器
### 5.4 依赖注入
- IoC（控制反转）：创建调用者的工作不再有调用者来完成，因此被称为控制反转。
- DI（依赖注入）：创建被调用者实例的工作通常由Spring容器来完成，然后注入调用者，因此也称为依赖注入。

#### 5.4.1 依赖注入

##### 依赖解决步骤
- 描述所有 bean 的 `ApplicationContext`创建并根据配置初始化。XML 配置或注解等。
- 每个 bean 的依赖将以属性，构造器参数或者静态工厂方法等形式出现，当这些 bean 被创建时，这些依赖会提供给该 bean。
- 每个属性或者构造器参数可以是实际的值，也可以是容器中的另一个引用。
- 每个指定的属性或构造器参数必须能够被转换成特定格式或构造参数所需的类型。

Spring 容器创建的时候会检查每个 bean 的配置。除了单例类型的 bean 和 被设为非懒加载的 bean 会在容器创建时创建，其他 bean 只在需要时被创建。

>**`循环依赖`**
>
>A类需要注入B类的实例，并且B类有需要注入A类的实例，如果A和B互相依赖的话，Spring IoC 容器在运行时会检测到这个循环依赖，并且抛出一个 BeanCurrentlyInCreationException 异常
>
>**`遇到问题：Spring 是如何检测出循环依赖的？`**
>
>简单的说，如果 A依赖B，B依赖C、D，C依赖A，在创建A时，需要创建B，此时A加入“当前创建Bean池”（ThreadLocal 对应的 Set 集合），尚未创建完成的对象，都加入这个集合，创建完成后，从该集合删除，如果已经加入了，还需要再次加入，则表明有环。
>源码地址：org.springframework.beans.factory.support.AbstractBeanFactory
>beforePrototypeCreation、afterPrototypeCreation、isPrototypeCurrentlyInCreation方法
>
>- [**`扩展阅读：Spring 循环依赖检查算法`**](http://jingzhongwen.iteye.com/blog/2208921)
>- [**`扩展阅读：有向图的深度优先搜索 DFS`**](http://www.cnblogs.com/skywang12345/p/3711483.html)


#### 5.4.4 延迟初始化bean
`ApplicationCOntext` 启动时默认初始化所有的 singleton bean。
初始化的好处：配置或运行环境的错误会被立刻发现，否则可能要花好几个小时甚至几天。

#### 5.4.5 自动装配协作者
对于有相互协作关系的bean，Spring 容器可以自动装配。通过
- byName：根据属性名自动装配。
- byType：从容器中寻找指定类型的bean。如果存在多个该类型的bean，将抛出异常。如果没找到同类型的，则不会装配？
- constructor：寻找与构造器参数类型一致的bean，找不到就会抛异常。
- no：（默认）不进行自动装配

#### 5.4.6 方法注入

>**`遇到问题：不同（作用域）生命周期 bean 的装配`**
>
>单例类型bean A依赖于另一个非单例(prototype)类型 bean B，对于 A来说，容器只会创建一次，这样就没法在需要的时候每次让容器为 bean A 提供一个新的 bean B 实例。
>
>解决方案：
>
>- （推荐）使用lookup-method，原理是使用 cglib 生成 B 的一个子类，然后把这个子类对象给 A。**[扩展阅读：Spring 方法注入lookup-method](http://rooock.iteye.com/blog/338847)**
>- （不推荐，容器每次都要重新加载一次）放弃控制反转，用 ApplicationContextAware 来获取bean。如下例子：
>

	// a class that uses a stateful Command-style class to perform some processing
	package fiona.apple;
	
	// Spring-API imports
	import org.springframework.beans.BeansException;
	import org.springframework.context.ApplicationContext;
	import org.springframework.context.ApplicationContextAware;
	
	public class CommandManager implements ApplicationContextAware {
	
	    private ApplicationContext applicationContext;
	
	    public Object process(Map commandState) {
	        // grab a new instance of the appropriate Command
	        Command command = createCommand();
	        // set the state on the (hopefully brand new) Command instance
	        command.setState(commandState);
	        return command.execute();
	    }
	
	    protected Command createCommand() {
	        // notice the Spring API dependency!
	        return this.applicationContext.getBean("command", Command.class);
	    }
	
	    public void setApplicationContext(
	            ApplicationContext applicationContext) throws BeansException {
	        this.applicationContext = applicationContext;
	    }
	}

##### Lookup 方法注入
解决不同作用域 bean 互相依赖的问题，参见上一小节。

##### 自定义方法的替代方案
用bean的一个方法替换另一个方法：`replaced-method` 元素。

### 5.5 Bean 作用域
- singleton：（默认）Spring IoC 容器中每个一个 bean 只对应一个实例。
- prototype：一个 bean 多个实例
- request：一个 bean 定义作用于 HTTP `request` 生命周期
- session：一个 bean 定义作用于 HTTP `session` 生命周期。
- global session：一个 bean 定义作用于全局的 HTTP `session` 生命周期。
- application：一个 bean 定义作用于整个 `ServletContext` 生命周期。

>**`遇到问题：request、session、global session 等作用域如何实现的？`**
>
>`DispatcherServlet`、`RequestContextListener`和`RequestContextFilter` 都是把每个 http 请求对象绑定到处理线程`Thread`上，这样请求、回话和全局回话作用域bean就可以沿着调用链继续往下走了。

### 5.6 定制 bean 特性

#### 5.6.1 声明周期回调
##### 组合生命周期机制
一个 bean 的 
**初始化方法** 调用顺序如下：
- `@PostConstruct` 元注释
- `InitializingBean` 的 `afterPropertiesSet()` 定义
- 自定义 `init()` 方法
**析构方法** 调用顺序：
- `@PreDestroy` 元注释
- `DisposableBean` 的 `destroy()` 定义
- 自定义 `destroy()` 方法

#### 5.6.3 其他 Aware 接口
- ApplicationContextAware：声明 ApplicationContext
- ServletContextAware：目前 ServletContext 容器运行. 仅在一个web-aware Spring中有效 ApplicationContext

### 5.7 Bean 定义的继承
讲述 ChildBeanDefinition 表示 bean 的子类，并且 parent 的方式来定义父类子类的关系。子类会继承父类的所有属性，但会覆盖自己定义的属性。

### 5.8 容器拓展点

- `BeanPostProcessor`：Spring IoC 容器实例化一个 bean 后，才会进行回调。**待确定**：作用范围是每一个容器？

### 5.9 基于注释的容器配置
- `<context:annotation-config/>` 只能在同一 application context 中寻找。

### 5.10 Classpath scanning 



















































## 分享内容

### Spring 容器启动流程
整体流程，以及细节。

- 扫描
- BeanDefinition：内容、依赖关系如何存储
- 实例化单例 bean
- 自动装配：byName、byType

### 循环依赖如何检测
参见：5.4.1 














































