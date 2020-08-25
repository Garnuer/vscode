## 第二周-第三周：Spring   SpringMVC Mybatis(12h)

​    我们一般说 Spring 框架指的都是 Spring Framework，它是很多模块的集合，使用这些模块可以很方便地协助我们进行开发。这些模块是：核心容器、数据访问/集成,、Web、AOP（面向切面编程）、工具、消息和测试模块。比如：Core Container 中的 Core 组件是Spring 所有组件的核心，Beans 组件和 Context 组件是实现IOC和依赖注入的基础，AOP组件用来实现面向切面编程。

![](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20200721111624746.png)

- [Core technologies](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/core.html): dependency injection, events, resources, i18n, validation, data binding, type conversion, SpEL, AOP.
- [Testing](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/testing.html): mock objects, TestContext framework, Spring MVC Test, `WebTestClient`.
- [Data Access](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/data-access.html): transactions, DAO support, JDBC, ORM, Marshalling XML.
- [Spring MVC](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html) and [Spring WebFlux](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html) web frameworks.
- [Integration](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/integration.html): remoting, JMS, JCA, JMX, email, tasks, scheduling, cache.
- [Languages](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/languages.html): Kotlin, Groovy, dynamic languages.

## 1.2谈谈对SpringIoc  aop的理解。

#### IoC

​     IoC（Inverse of Control:控制反转）是一种**设计思想**，就是 **将原本在程序中手动创建对象的控制权，交由Spring框架来管理。** IoC 在其他语言中也有应用，并非 Spring 特有。 **IoC 容器是 Spring 用来实现 IoC 的载体， IoC 容器实际上就是个Map（key，value）,Map 中存放的是各种对象。**

​    将对象之间的相互依赖关系交给 IoC 容器来管理，并由 IoC 容器完成对象的注入。这样可以很大程度上简化应用的开发，把应用从复杂的依赖关系中解放出来。 **IoC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的。** 在实际项目中一个 Service 类可能有几百甚至上千个类作为它的底层，假如我们需要实例化这个 Service，你可能要每次都要搞清这个 Service 所有底层类的构造函数，这可能会把人逼疯。如果利用 IoC 的话，你只需要配置好，然后在需要的地方引用就行了，这大大增加了项目的可维护性且降低了开发难度。

![image-20200721144704977](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20200721144704977.png)

![image-20200721145851703](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20200721145851703.png)

1. ApplicationContext 继承了 ListableBeanFactory，这个 Listable 的意思就是，通过这个接口，我们可以获取多个 Bean，大家看源码会发现，最顶层 BeanFactory 接口的方法都是获取单个 Bean 的。
2. ApplicationContext 继承了 HierarchicalBeanFactory，Hierarchical 单词本身已经能说明问题了，也就是说我们可以在应用中起多个 BeanFactory，然后可以将各个 BeanFactory 设置为父子关系。
3. AutowireCapableBeanFactory 这个名字中的 Autowire 大家都非常熟悉，它就是用来自动装配 Bean 用的，但是仔细看上图，ApplicationContext 并没有继承它，不过不用担心，不使用继承，不代表不可以使用组合，如果你看到 ApplicationContext 接口定义中的最后一个方法 getAutowireCapableBeanFactory() 就知道了。
4. ConfigurableListableBeanFactory 也是一个特殊的接口，看图，特殊之处在于它继承了第二层所有的三个接口，而 ApplicationContext 没有。这点之后会用到。
5. 请先不用花时间在其他的接口和类上，先理解我说的这几点就可以了。

然后，请读者打开编辑器，翻一下 BeanFactory、ListableBeanFactory、HierarchicalBeanFactory、AutowireCapableBeanFactory、ApplicationContext 这几个接口的代码，大概看一下各个接口中的方法，大家心里要有底，限于篇幅，我就不贴代码介绍了。

## 1.3Spring AOP 和 AspectJ AOP 有什么区别？

**Spring AOP 属于运行时增强，而 AspectJ 是编译时增强。** Spring AOP 基于代理(Proxying)，而 AspectJ 基于字节码操作(Bytecode Manipulation)。

Spring AOP 已经集成了 AspectJ ，AspectJ 应该算的上是 Java 生态系统中最完整的 AOP 框架了。AspectJ 相比于 Spring AOP 功能更加强大，但是 Spring AOP 相对来说更简单，

如果我们的切面比较少，那么两者性能差异不大。但是，当切面太多的话，最好选择 AspectJ ，它比Spring AOP 快很多。

## Spring MVC的工作原理：

![image-20200721165958670](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20200721165958670.png)



## Spring Ioc介绍和反射注解讲解

  依赖注入的原理是反射(核心)和注入。

​     反射的标准概念：java的反射机制是在运行状态中，对于任意一个类，都能够这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；这种动态获取信息以及动态调用对象方法的功能称为Java语言的反射机制。

  注解：是代码的标签，标签需要人去解读。

## Spring Ioc的自定义实现

## Spring Ioc的基本实现

## Spring的bean的作用域：

   singleton : spring的默认作用域，容器里拥有唯一的bean实例

  prototype: 针对每一个bean请求，容器都会创建一个Bean实例

  request ：会为每一http请求创建一个bean实例

 session ：会为每个session 创建一个bean实例

  globalSession：会为每个全局Http Session创建一个Bean实例，该作用域仅对Protlet有效

  

## Spring Ioc 的注解讲解

作业：利用Spring ioc ，完成service层对dao层的依赖注入。

## Spring Ioc xml配置方式

Resource 中配置spring.xml

采用配置的形式。

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="org.example.Service,org.example.Dao"></context:component-scan>

    <bean id="UserDao" class="org.example.Dao.UserDao"></bean>

    <bean id="UserService" class="org.example.Service.UserService">
        <property name="userDao" ref="UserDao"></property>

    </bean>
</beans>
```

```java
加入依赖    
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.2.3.RELEASE</version>
    </dependency>
        		
    DAO层
        package org.example.Dao;

    public class UserDao implements IUserDao{

    public String getName(){
        return "zhangsan";
    }
}

DAO接口：
    package org.example.Dao;

    public interface IUserDao {

        String getName();
    }


 Service层
     package org.example.Service;

   import org.example.Dao.IUserDao;
   import org.example.Dao.UserDao;

   public class UserService {

    private IUserDao userDao ;

    public void setUserDao(IUserDao userDao) {
        this.userDao = userDao;
    }

    public void queryName(){
        String name = userDao.getName();
        System.out.println(name);
    }
}


        
```

```java
TEST:测试类
package org.example;

import org.example.Service.UserService;
import org.junit.Test;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class SpringTest {

    @Test
    public void testCasel(){
        ClassPathXmlApplicationContext context=new ClassPathXmlApplicationContext("Spring.xml");
        UserService userService = context.getBean(UserService.class);
        userService.queryName();
    }
}

```



## Spring aop 之静态代理

  AOP为Aspect Oriented Programming的缩写，意为：[面向切面编程]，利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的[耦合度](https://baike.baidu.com/item/耦合度/2603938)降低，提高程序的可重用性，同时提高了开发的效率。

 代理和厂家具有相同的行为 （代理提供的东西是厂家的，厂家的东西是自己生产的）

## Spring aop之动态代理

```java
package org.example.dynamic;


import org.example.Icomputer;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;

//实现动态代理的核心代码

public class DynamicProxy implements InvocationHandler {

    /**
     * 提供电脑的许可证（动态代理，代理的对象必须实现Icomputer方法）
     *
     */
    private Icomputer computer;

    /**
     * 传入进来参数的是工厂
     * @param computer
     */
    public DynamicProxy(Icomputer computer) {
        this.computer = computer;
    }

    /**
     * 执行代理的方法
     * @param proxy  当前代理本身
     * @param method 需要被代理的工厂方法
     * @param args  工厂方法的参数
     * @return
     * @throws Throwable
     */
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("提供分期付款");
        Object invoke=method.invoke(computer,args);
        System.out.println("提供分期服务");
        return invoke;
    }
}
```



```java
Test
       ClassLoader classLoader = buy.class.getClassLoader();
        //获取工厂实现的所有接口
        Class<?>[] interfaces = ComputerFactory.class.getInterfaces();
        Icomputer icomputer = new ComputerFactory();
        DynamicProxy dynamicProxy = new DynamicProxy(icomputer);

        /**
         * 参数1:类加载器
         * 参数2：当前被代理的工厂所实现的所有接口
         * 参数3：动态代理对象本身
         */
       Icomputer proxyInstance = (Icomputer) Proxy.newProxyInstance(classLoader,interfaces,dynamicProxy);
       String computer = proxyInstance.provideComputer();
        System.out.println(computer);
    }
}
```



## Spring aop之注解配置方式(annotation)

  

```java
/**
 * 统一的协议
 */
public interface IFactory {

    String provideProduct();

}

                import org.springframework.stereotype.Component;

                @Component
                public class ComputerFactory implements IFactory{
                    @Override
                    public String provideProduct() {
                        System.out.println("---------");
                        return "电脑";
                    }
                }

/**
 * 代理
 * 切面Aspect
 */
@Component
@Aspect  //定义切面
public class ComputerProxy {

    //配置切入点的位置
    @Before("execution(public String org.example.ComputerFactory.provideProduct())")
    public void before(){
        System.out.println("提供分期付款");
    }

    @After("execution(public String org.example.ComputerFactory.provideProduct())")
    public  void after(){
        System.out.println("提供售后维修");
    }
}

                        import org.springframework.context.annotation.ComponentScan;
                        import org.springframework.context.annotation.Configuration;
                        import org.springframework.context.annotation.EnableAspectJAutoProxy;
                        @Configuration
                        @EnableAspectJAutoProxy
                        @ComponentScan("org.example")
                        public class Configration {
                        }


public class Buyer {
    public static void main(String[] args) {
     //  IFactory computerFactory  = new ComputerFactory();
      // String s = computerFactory.provideProduct();
       // System.out.println(s);
        ApplicationContext context =  new AnnotationConfigApplicationContext(Configration.class);
        //getBean(ComputerFactory.class)为啥不行
        IFactory bean = context.getBean(IFactory.class);
        String s = bean.provideProduct();
        System.out.println(s);
    }
}
```



## Spring aop 之xml配置方式和aop 完成日志记录

```xml
<!--配置aop>
    <aop:config>
      <aop:aspect id = "aspect" ref="computerAspect">
<aop:pointcut id ="" expression="" >
   <aop:before method="" pointcut-ref="" >
   <aop:after method="after" pointcut-ref="">
</aop:config>
```





## PO VO DAO DTO的关系



## Spring mvc 基本配置

在web.xml中配置 DispatcherServlet

  

```java
/**
 * 使用这个注解的类类似一个Servlet，功能更强大
 */
@Controller//相当于Component
public class UserController {

    @RequestMapping("/login")
    public ModelAndView login(){
        System.out.println("这是登录");
        ModelAndView modelAndView = new ModelAndView();
        //指定跳转的页面
        modelAndView.setViewName("index.jsp");
        return modelAndView;
    } 
}



  <servlet>
    <servlet-name>spring</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>spring</servlet-name>
    <!--/拦截除jsp之外的/*拦截所有-->
    <url-pattern>/</url-pattern>
    </servlet-mapping>
  
  配置spring-servlet.xml
    <context:component-scan base-package="WebController" />
    <!--//采用注解的方式来配置mvc-->
    <!-- Spring能识别mvc注解-->
    <mvc:annotation-driven/>
  
```



## Spring mvc 参数传递

 参数传递的几种方式（见代码）

```java
 //get和post只是地址栏的显示
    @RequestMapping("/login")
//传递参数的几种形式
    public ModelAndView login(@RequestParam("user_name") String username, String password){
        System.out.println(username+":"+password);
        ModelAndView modelAndView = new ModelAndView();
        //指定跳转的页面
        modelAndView.setViewName("index.jsp");
        return modelAndView;
    }


@RequestMapping("/login2")
    public ModelAndView login(){
        ModelAndView modelAndView = new ModelAndView();
        //参数传递的方式
        modelAndView.addObject("name","lisi");
        //指定跳转的页面
        modelAndView.setViewName("index.jsp");
        return modelAndView;
    }

    //jsp页面接收参数的方式，在这个过程中需要增加依赖
    /*  
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>servlet-api</artifactId>
      <version>2.5</version>
    </dependency> 
   */    
       
    <%@page isELIgnored="false" %>
    <html>
    <body>
    <h2>Hello World!</h2>
    <h1> name=<%=request.getAttribute("name")%></h1>
    <h1>name= ${name}</h1>


```



## Spring mvc 数据传递和页面跳转

（页面跳转种引入视图解析器，具体见代码）



```java
 <!--视图解析的配置 -->
    <!-- -->
    <bean id="ViewResovler" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
        
        
 //重定向redirect:
 // Binder
 //  @InitBinder 注解的用法
```



## Spring mvc 静态资源处理

```
<!-- spring用来处理静态资源无法访问的配置  也是静态资源交给DefaultServlet来处理-->
<!-- mvc:default-servlet-handler/-->

<!--处理静态资源无法访问的配置 -->
<!--Mapping 昵称 -->
<!--location 具体的静态资源路径-->
<!--所有以file开头的静态资源路径，全部会映射到localhost所配置的物理路径下查找 -->
```

## Spring mvc 的拦截器

  类似servlet中的filter，但是同Filter还是有很大区别

  1.创建拦截器的类实现HandleInterceptor接口

 2.在spring的配置文档中配置拦截器如下（忘掉的概率很大，用的很少）

 

```java
/**
 * 创建拦截器，需要实现Handler
 */
public class Loginintercaptor implements HandlerInterceptor {
    /**
     * 请求执行前
     * @param request
     * @param response
     * @param handler
     * @return
     * @throws Exception
     */
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("执行前");
        return true;//如果这个地方是false就需要去spring-servlet.xml里面去配置不拦截什么类型的文件。
    }

    /**
     * 请求完成（代表方法执行完毕）
     * @param request
     * @param response
     * @param handler
     * @param modelAndView
     * @throws Exception
     */
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("执行中");
    }

    /**
     * 请求结束（给用户响应也执行完毕）
     * @param request
     * @param response
     * @param handler
     * @param ex
     * @throws Exception
     */
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("执行结束");
    }
}
```

```jsp
<body>
 <form action="<%=request.getContextPath()%>/upload" method="post" enctype="multipart/form-data">
     <input type="file" name="file"><br/>
     <input type="submit" value="上传">
 </form>
</body>
```

```java
<mvc:interceptors>
        <mvc:interceptor>
            <!-- 拦截的地址-->
             <mvc:mapping path="/**"/>
            <!-- 不拦截的地址-->
            <mvc:exclude-mapping path="/file/**"/>
            <!--具体执行拦截的类 -->
            <bean class="interceptor.Loginintercaptor"></bean>
        </mvc:interceptor>
    </mvc:interceptors>
```



## Spring mvc 的文件上传

```java
/**
     * 上传：接收的文件流
     *
     * MultipartFile 用来接收客户端传递文件
     *
     * 必须使用POST请求
     *
     */
    @PostMapping("/upload")
    public void upload(@RequestParam("file") MultipartFile file){
        System.out.println("上传的文件名称:"+file.getOriginalFilename());
        String filename = file.getOriginalFilename();

        InputStream inputStream=null;
        FileOutputStream fileOutputStream=null;
        //客户端进行文件上传，传递给服务器的文件流对象
        try{
            inputStream = file.getInputStream();
            fileOutputStream = new FileOutputStream("F:\\Tomcat\\apache-tomcat-9.0.37\\webapps\\file"+filename);
            int len=0;
            byte[] buffer = new byte[1024];
            while(len !=-1){
                len = inputStream.read(buffer);
                fileOutputStream.write(buffer,0,len);
                fileOutputStream.flush();
            }
        }catch (IOException e){
            e.printStackTrace();
        }finally {
            try{
                if(fileOutputStream !=null){
                    fileOutputStream.close();
                    inputStream.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

```xml
<!--Spring上传配置 -->
    <bean id="multipartResolver"
          class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <!-- one of the properties available; the maximum file size in bytes -->
        <property name="maxUploadSize" value="100000"/>
    </bean>
```

```xml
//在执行前需要将return false 改成true 。 否则就需要在web.xml里面配置不拦截文件。
```



## Mybatis -1入门（与oracle的交互）

 orm框架--优点：小巧灵活的orm框架 2.方便进行sql优化，对于性能要求高，和业务复杂的项目，mybatis更有优势。

 回忆（hibernate）：

​                              建立对象关系映射。

​                              建立核心配置文档

​                              解析

​                              sessionfactory

## Mybatis -2入门

```xml
熟悉基本配置
```



## Mybatis -多对一

表和表之前的关系。存在一个与数据库之间的交互的过程。需要将oracle数据库的落实。

## Mybatis -的日志和缓存

## Mybatis -懒加载

## Mybatis -动态SQL

## Mybatis -事物的传播性









## oracle 数据库的学习（三天）





## svn管理工具的基本命令（一天）

Subversion(SVN) 是一个开源的版本控制系統, 也就是说 Subversion 管理着随时间改变的数据。 这些数据放置在一个中央资料档案库(repository) 中。 这个档案库很像一个普通的文件服务器, 不过它会记住每一次文件的变动。 这样你就可以把档案恢复到旧的版本, 或是浏览文件的变动历史。

![image-20200727101059825](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20200727101059825.png)

## svn与idea整合

   熟悉基本的checkout   update commit delect 命令的使用。

## svn冲突解决和分支管理

  在项目中，如果出现了代码冲突如何解决？

   *一般出现冲突就是就是同一行代码不一致导致的冲突，在svn更新代码时候，会提示冲突的提示。此时解决冲突有三种方式

 *用我的代码覆盖服务器的代码，或者用服务器的代码覆盖我的代码，一般情况下，回通过手动将我的代码和服务器上的代码做合并，从而解决冲突。

分支管理：

  *必要性：在实际项目开发过程中，当版本1上线之后出现bug，需要在对于的源码上做bug修复，所以需要在版本1上线的时候，备份一份所对应的源码，以便后期版本1出现bug方便调试。

  *版本1上的bug修复完毕之后，需要将修复后的bug合并到最新的版本中，此时要用到版本合并。

## PostgreSQL

​     我们也对误操作问题进行了防范——开源了一个叫做Xlogminer的数据库工具。这是一款日志挖掘工具，因为每个数据库都会写WAL日志，这里我们就是对WAL日志进行分析，能很好地还原数据库所有操作，从而了解什么时间做哪些操作，即可针对性地还原某些误操作的内容。当然，也可以开启数据库log，但是经过测试开启log会大大降低数据库性能，而且WAL日志本身已经将操作记录下来了，所以通过分析WAL日志来还原数据库操作是一种最优的方式。

## 负载均衡（分布式架构）

  

  

## 

1.单例模式和工厂模式

  工厂模式包含工厂方法与抽象工厂。属于创建型模式 

 策略模式关注的是结果是否能够相互替换，属于行为型模式。

工厂模式主要目的是封装好创建逻辑，策略模式接收工厂创建好的对象，从而实现不同的行为。

策略模式是委派模式内部的一种实现形式，策略模式关注的是结果是否能相互替换。

2.委派模式更关注分发和调度

有可能采用if...else...条件分支语句来分发，内部也可以使用策略模式。

3.模板方法模式和策略模式

  1.都有封装算法。

## Oop

 大家都知道的（面向对象编程）封装、继承、多态、一切皆对象。

​     用程序来描述生活中一切事物（需求转换为代码实现）只知道说，不知道做。

  （面向过程 使得我们眼光专注一个点，鼠目寸光）写出来人更容易理解的设计

## Aop：

面向切面编程:找出多个bean中有一定规律的代码，开发时将其拆开，运行时再将其合并。

面向切面编程：就是面向编程规则编程，日志控制：事物开启、关闭：权限。       

## Bop：

在Aop的继承之上，面向Bean编程，java本身就是一种面向对象的编程，用一个一个的Bean来实现的，解放程序员的双手，提出代码管理的理念，Spring一切从Bean开始。



## IOC：

控制反转。通俗的讲控制权反转，创建对象的控制权反转，反转给Spring（BeanFactory），

我们只需要伸手拿（衣来伸手饭来张口，程序员哥哥解放啦）

## DI：

#### 依赖注入，依赖查找DL，Spring不仅能创建对象，能够保存对象与对象之间的关联关系，自动赋值，三种赋值方法：构造方法，set方法，直接赋值。

## SpringBoot三大特性

组建自动装配：web mvc，web flux， jdbc

嵌入式web容器：tomcat，jetty及undertow

生产准备特性：指标，健康检查，外部花配置等。



