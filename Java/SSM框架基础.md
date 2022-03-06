<center>
    <h1>
        SSM框架基础
    </h1>
</center>

## 1. Spring

### 1.1 Spring基础概述

Spring是分层的Java SE/EE应用full-stack 轻量级开源框架，以IoC（Inverse Of Control：反转控制）和AOP（Aspect Oriented Programming：面向切面编程）为内核。

提供了展现层SpringMVC和持久层Spring JDBCTemplate以及业务层事务管理等众多的企业级应用技术，还能整合开源世界众多著名的第三方框架和类库，逐渐成为使用最多的Java EE 企业应用开源框架。

**Spring的优势**

1. 方便解耦，简化开发
   - 通过Spring 提供的IoC容器，可以将对象间的依赖关系交由Spring 进行控制，避免硬编码所造成的过度耦合。
   - 用户也不必再为单例模式类、属性文件解析等这些很底层的需求编写代码，可以更专注于上层的应用。
2. AOP编程的支持
   - 通过Spring的AOP 功能，方便进行面向切面编程，许多不容易用传统OOP 实现的功能可以通过AOP 轻松实现。
3. 声明式事务的支持
   - 可以将我们从单调烦闷的事务管理代码中解脱出来，通过声明式方式灵活的进行事务管理，提高开发效率和质量。
4. 方便程序的测试
   - 可以用非容器依赖的编程方式进行几乎所有的测试工作，测试不再是昂贵的操作，而是随手可做的事情。
5. 方便集成各种优秀框架
   - Spring对各种优秀框架（Struts、Hibernate、Hessian、Quartz等）的支持。
6. 降低JavaEE API的使用难度
   - Spring对JavaEEAPI（如JDBC、JavaMail、远程调用等）进行了薄薄的封装层，使这些API 的使用难度大为降低。
7. Java源码是经典学习范例
   - Spring的源代码设计精妙、结构清晰、匠心独用，处处体现着大师对Java 设计模式灵活运用以及对Java技术的高深
     造诣。它的源代码无意是Java 技术的最佳实践的范例。

**Spring程序开发步骤**

1. 导入Spring开发的基本包坐标
2. 编写Dao接口和实现类
3. 创建Spring核心配置文件
4. 在Spring配置文件中配置UserDaoImpl
5. 使用Spring的API获得Bean实例

### 1.2 Spring配置文件

**Bean标签的基本配置**

用于配置对象交由Spring来创建。

默认情况下它调用的是类中的无参构造函数，如果没有无参构造函数则不能创建成功。

基本属性

- id：Bean实例在Spring容器中的唯一标识
- class：Bean的全限定名称

**Bean标签范围配置**

scope：指对象的作用范围，取值如下表：

|    取值范围    |                             说明                             |
| :------------: | :----------------------------------------------------------: |
|   singleton    |                        默认值，单例的                        |
|   prototype    |                            多例的                            |
|    request     |  WEB项目中，Spring创建一个Bean对象，将对象存入到request域中  |
|    session     |  WEB项目中，Spring创建一个Bean对象，将对象存入到session域中  |
| global session | WEB项目中，应用在Portlet环境，如果没有Portlet环境，那么global session相当于session |

1.当scope的取值为singleton时

- Bean的实例化个数：1个
- Bean的实例化时机：当Spring核心文件被加载时，实例化配置Bean实例
- Bean的生命周期
  - 对象创建：当应用加载，创建容器时，对象就被创建了
  - 对象运行：只要容器在，对象一直活着
  - 对象销毁：当应用卸载，销毁容器时，对象就被销毁了

2.当scope的取值为prototype时

- Bean的实例化个数：多个
- Bean的实例化时机：当调用getBean()方法时实例化Bean
- Bean的生命周期
  - 对象创建：当使用对象时，创建新的对象实例
  - 对象运行：只要对象在使用中，就一直活着
  - 对象销毁：当对象长时间不用时，被Java 的垃圾回收器回收了

**Bean生命周期配置**

init-method：指定类中的初始化方法名称

destroy-method：指定类中销毁方法名称

**Bean实例化三种方式**

无参构造方法实例化

- 它会根据默认无参构造方法来创建类对象，如果bean中没有默认无参构造函数，将会创建失败

```XML
<bean id="userDao" class="com.itahu.dao.impl.UserDaoImpl"/>
```

工厂静态方法实例化

- 工厂的静态方法返回Bean实例

```Java
public class StaticFactory {
    public static UserDao getUserDao() {
        return new UserDaoImpl();
    }
}
```

```XML
<bean id="userDao" class="com.itahu.factory.StaticFactory" factory-method="getUserDao"></bean>
```

工厂实例方法实例化

- 工厂的非静态方法返回Bean实例

```Java
public class DynamicFactory {
    public UserDao getUserDao() {
        return new UserDaoImpl();
    }
}
```

```XML
<bean id="factory" class="com.itahu.factory.DynamicFactory"></bean>
<bean id="userDao" factory-bean="factory" factory-method="getUserDao"></bean>
```

**Bean的依赖注入分析**

因为UserService和UserDao都在Spring容器中，而最终程序直接使用的是UserService，所以可以在Spring容器中，将UserDao设置到UserService内部。

**Bean的依赖注入概念**

依赖注入(Dependency Injection)：它是Spring 框架核心IOC 的具体实现。

在编写程序时，通过控制反转，把对象的创建交给了Spring，但是代码中不可能出现没有依赖的情况。

IOC 解耦只是降低他们的依赖关系，但不会消除。例如：业务层仍会调用持久层的方法。

那这种业务层和持久层的依赖关系，在使用Spring 之后，就让Spring 来维护了。

简单的说，就是坐等框架把持久层对象传入业务层，而不用我们自己去获取。

**Bean的依赖注入方式**

将UserDao注入到UserService内部的方法

1.构造方法

创建有参构造

```Java
public class UserServiceImpl implements UserService {
    private UserDao userDao;

    public UserServiceImpl() {
    }

    public UserServiceImpl(UserDao userDao) {
        this.userDao = userDao;
    }
    
    public void save() {
        userDao.save();
    }
}
```

配置Spring容器调用有参构造时进行注入

```XML
<bean id="userService" class="com.itahu.service.impl.UserServiceImpl">
    <constructor-arg name="userDao" ref="userDao"></constructor-arg>
</bean>
```

2.set方法

在UserServiceImpl中添加setUserDao方法

```Java
public class UserServiceImpl implements UserService {
    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    public void save() {
        userDao.save();
    }
}
```

配置Spring容器调用set方法进行注入

```XML
<bean id="userDao" class="com.itahu.dao.impl.UserDaoImpl"></bean>

<bean id="userService" class="com.itahu.service.impl.UserServiceImpl">
    <property name="userDao" ref="userDao"></property>
</bean>
```

P命名空间注入本质也是set方法注入，但比起上述的set方法注入更加方便，主要体现在配置文件中，如下：
首先，需要引入P命名空间：

```XML
xmlns:p="http://www.springframework.org/schema/p"
```

其次，需要修改注入方式

```XML
<bean id="userService" class="com.itahu.service.impl.UserServiceImpl" p:userDao-ref="userDao"/>
```

**Bean的依赖注入的数据类型**

上面的操作，都是注入的引用Bean，除了对象的引用可以注入，普通数据类型，集合等都可以在容器中进行注入。

注入数据的三种数据类型

- 普通数据类型
- 引用数据类型
- 集合数据类型

**引入其他配置文件（分模块开发）**

实际开发中，Spring的配置内容非常多，这就导致Spring配置很繁杂且体积很大，所以，可以将部分配置拆解到其他配置文件中，而在Spring主配置文件通过import标签进行加载。

```XML
<import resource="applicationContext-xxx.xml"/>
```

### 1.3 Spring相关API

**ApplicationContext的继承体系**

applicationContext：接口类型，代表应用上下文，可以通过其实例获得Spring容器中的Bean对象。

**ApplicationContext的实现类**

1. ClassPathXmlApplicationContext
   - 它是从类的根路径下加载配置文件推荐使用这种。
2. FileSystemXmlApplicationContext
   - 它是从磁盘路径上加载配置文件，配置文件可以在磁盘的任意位置。
3. AnnotationConfigApplicationContext
   - 当使用注解配置容器对象时，需要使用此类来创建spring 容器。它用来读取注解。

**getBean()方法使用**

```Java
public Object getBean(String name) throws BeansException {
    assertBeanFactoryActive();
    return getBeanFactory().getBean(name);
}

public <T> T getBean(Class<T> requiredType) throws BeansException {
    assertBeanFactoryActive();
    return getBeanFactory().getBean(requiredType);
}
```

其中，当参数的数据类型是字符串时，表示根据Bean的id从容器中获得Bean实例，返回是Object，需要强转。
当参数的数据类型是Class类型时，表示根据类型从容器中匹配Bean实例，当容器中相同类型的Bean有多个时，则此方法会报错。

```Java
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
UserService userService1 = (UserService) applicationContext.getBean("userService");
UserService userService2 = applicationContext.getBean(UserService.class);
```

### 1.4 Spring配置数据源

**数据源(连接池)的作用**

- 数据源(连接池)是提高程序性能而出现的
- 事先实例化数据源，初始化部分连接资源
- 使用连接资源时从数据源中获取
- 使用完毕后将连接资源归还给数据源

常见的数据源(连接池)：DBCP、C3P0、BoneCP、Druid等。

**数据源的开发步骤**

1. 导入数据源的坐标和数据库驱动坐标
2. 创建数据源对象
3. 设置数据源的基本连接数据
4. 使用数据源获取连接资源和归还连接资源

**Spring配置数据源**

可以将DataSource的创建权交由Spring容器去完成

- ataSource有无参构造方法，而Spring默认就是通过无参构造方法实例化对象的
- DataSource要想使用需要通过set方法设置数据库连接信息，而Spring可以通过set方法进行字符串注入

```XML
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
    <property name="driverClass" value="com.mysql.jdbc.Driver"></property>
    <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/test"></property>
    <property name="user" value="root"></property>
    <property name="password" value="root"></property>
</bean>
```

**抽取jdbc配置文件**

applicationContext.xml加载jdbc.properties配置文件获得连接信息。

首先，需要引入context命名空间和约束路径：

- 命名空间：xmlns:context="http://www.springframework.org/schema/context"
- 约束路径：http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd

```XML
<context:property-placeholder location="classpath:jdbc.properties"/>
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
    <property name="driverClass" value="${jdbc.driver}"></property>
    <property name="jdbcUrl" value="${jdbc.url}"></property>
    <property name="user" value="${jdbc.username}"></property>
    <property name="password" value="${jdbc.password}"></property>
</bean>
```

Spring容器加载properties文件

```XML
<context:property-placeholder location="xx.properties"/>
<property name="" value="${key}"/>
```

### 1.5 Spring注解开发

**Spring原始注解**

Spring是轻代码而重配置的框架，配置比较繁重，影响开发效率，所以注解开发是一种趋势，注解代替xml配置文件可以简化配置，提高开发效率。

Spring原始注解主要是替代\<Bean>的配置

|      注解      |                      说明                      |
| :------------: | :--------------------------------------------: |
|   @Component   |            使用在类上用于实例化Bean            |
|  @Controller   |         使用在web层类上用于实例化Bean          |
|    @Service    |       使用在service层类上用于实例化Bean        |
|  @Repository   |         使用在dao层类上用于实例化Bean          |
|   @Autowired   |        使用在字段上用于根据类型依赖注入        |
|   @Qualifier   | 结合@Autowired一起使用用于根据名称进行依赖注入 |
|   @Resource    | 相当于@Autowired+@Qualifier，按照名称进行注入  |
|     @Value     |                  注入普通属性                  |
|     @Scope     |               标注Bean的作用范围               |
| @PostConstruct |    使用在方法上标注该方法是Bean的初始化方法    |
|  @PreDestroy   |     使用在方法上标注该方法是Bean的销毁方法     |

注意：使用注解进行开发时，需要在applicationContext.xml中配置组件扫描，作用是指定哪个包及其子包下的Bean需要进行扫描以便识别使用注解配置的类、字段和方法。

```XML
<!--配置组件扫描-->
<context:component-scan base-package="com.itahu"/>
```

**Spring新注解**

使用上面的注解还不能全部替代xml配置文件，还需要使用注解替代的配置如下：

- 非自定义的Bean的配置：\<bean>
- 加载properties文件的配置：\<context:property-placeholder>
- 组件扫描的配置：\<context:component-scan>
- 引入其他文件：\<import>

|      注解       |                             说明                             |
| :-------------: | :----------------------------------------------------------: |
| @Configuration  | 用于指定当前类是一个Spring配置类，当创建容器时会从该类上加载注解 |
| @ComponentScan  | 用于指定Spring在初始化容器时要扫描的包。<br/>作用和在Spring的xml配置文件中的<br/><context:component-scan base-package="com.itheima"/>一样 |
|      @Bean      |     使用在方法上，标注将该方法的返回值存储到Spring容器中     |
| @PropertySource |               用于加载.properties文件中的配置                |
|     @Import     |                      用于导入其他配置类                      |

### 1.6 Spring集成Junit与Web

**Spring集成Junit**

在测试类中，每个测试方法都有以下两行代码：

```Java
ApplicationContext ac = newClassPathXmlApplicationContext("bean.xml");
IAccountService as = ac.getBean("accountService",IAccountService.class);
```

这两行代码的作用是获取容器，如果不写的话，直接会提示空指针异常。所以又不能轻易删掉。

解决思路

- 让SpringJunit负责创建Spring容器，但是需要将配置文件的名称告诉它
- 将需要进行测试Bean直接在测试类中进行注入

Spring集成Junit步骤

1. 导入spring集成Junit的坐标
2. 使用@Runwith注解替换原来的运行期
3. 使用@ContextConfiguration指定配置文件或配置类
4. 使用@Autowired注入需要测试的对象
5. 创建测试方法进行测试

```Java
import com.itahu.config.SpringConfiguration;
import com.itahu.service.UserService;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

import javax.sql.DataSource;
import java.sql.Connection;
import java.sql.SQLException;

@RunWith(SpringJUnit4ClassRunner.class)
//@ContextConfiguration("classpath:applicationContext.xml")
@ContextConfiguration(classes = {SpringConfiguration.class})
public class SpringJunitTest {
    @Autowired
    private UserService userService;

    @Autowired
    private DataSource dataSource;

    @Test
    public void test1() throws SQLException {
        userService.save();
        Connection connection = dataSource.getConnection();
        System.out.println(connection);
    }
}
```

**Spring集成web环境**

==ApplicationContext应用上下文获取方式==

应用上下文对象是通过new ClasspathXmlApplicationContext(spring配置文件) 方式获取的，但是每次从容器中获得Bean时都要编写new ClasspathXmlApplicationContext(spring配置文件)，这样的弊端是配置文件加载多次，应用上下文对象创建多次。

在Web项目中，可以使用ServletContextListener监听Web应用的启动，我们可以在Web应用启动时，就加载Spring的配置文件，创建应用上下文对象ApplicationContext，在将其存储到最大的域servletContext域中，这样就可以在任意位置从域中获得应用上下文ApplicationContext对象了。

==Spring提供获取应用上下文的工具==

Spring提供了一个监听器ContextLoaderListener就是对上述功能的封装，该监听器内部加载Spring配置文件，创建应用上下文对象，并存储到ServletContext域中，提供了一个客户端工具WebApplicationContextUtils供使用者获得应用上下文对象。

所以我们需要做的只有两件事：

1. 在web.xml中配置ContextLoaderListener监听器(导入spring-web坐标)
2. 使用WebApplicationContextUtils获得应用上下文对象ApplicationContext

==导入Spring集成web的坐标==

```XML
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-web</artifactId>
  <version>5.0.5.RELEASE</version>
</dependency>
```

==配置ContextLoaderListener监听器==

```XML
<!--全局参数-->
<context-param>
  <param-name>contextConfigLocation</param-name>
  <param-value>classpath:applicationContext.xml</param-value>
</context-param>
<!--Spring的监听器-->
<listener>
  <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
```

==通过工具获得应用上下文对象==

```Java
ApplicationContext app = WebApplicationContextUtils.getWebApplicationContext(servletContext);
UserService userService = app.getBean(UserService.class);
```

==Spring集成web环境步骤==

1. 配置ContextLoaderListener监听器
2. 使用WebApplicationContextUtils获得应用上下文

## 2. SpringMVC

### 2.1 SpringMVC概述

SpringMVC是一种基于Java 的实现MVC 设计模型的请求驱动类型的轻量级Web 框架，属于SpringFrameWork的后续产品，已经融合在Spring Web Flow 中。

SpringMVC已经成为目前最主流的MVC框架之一，并且随着Spring3.0 的发布，全面超越Struts2，成为最优秀的MVC 框架。它通过一套注解，让一个简单的Java 类成为处理请求的控制器，而无须实现任何接口。同时它还支持RESTful编程风格的请求。

**SpringMVC快速入门**

需求：客户端发起请求，服务器端接收请求，执行逻辑并进行视图跳转。

开发步骤：

1. 导入SpringMVC相关坐标
2. 配置SpringMVC核心控制器DispathcerServlet
3. 创建Controller类和视图页面
4. 使用注解配置Controller类中业务方法的映射地址
5. 配置SpringMVC核心文件spring-mvc.xml
6. 客户端发起请求测试

在web.xml配置SpringMVC的核心控制器

```XML
<!--配置SpringMVC的前端控制器-->
<servlet>
  <servlet-name>DispatcherServlet</servlet-name>
  <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  <init-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:spring-mvc.xml</param-value>
  </init-param>
  <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
  <servlet-name>DispatcherServlet</servlet-name>
  <url-pattern>/</url-pattern>
</servlet-mapping>
```

创建Controller和业务方法并注解

```Java
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class UserController {
    @RequestMapping("/quick")
    public String save() {
        System.out.println("Controller save running......");
        return "success.jsp";
    }
}
```

创建spring-mvc.xml

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <!--Controller的组件扫描-->
    <context:component-scan base-package="com.itahu.controller"/>
</beans>
```

### 2.2 SpringMVC组件解析

**SpringMVC的执行流程**

1. 用户发送请求至前端控制器DispatcherServlet。
2. DispatcherServlet收到请求调用HandlerMapping处理器映射器。
3. 处理器映射器找到具体的处理器(可以根据xml配置、注解进行查找)，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet。
4. DispatcherServlet调用HandlerAdapter处理器适配器。
5. HandlerAdapter经过适配调用具体的处理器(Controller，也叫后端控制器)。
6. Controller执行完成返回ModelAndView。
7. HandlerAdapter将controller执行结果ModelAndView返回给DispatcherServlet。
8. DispatcherServlet将ModelAndView传给ViewReslover视图解析器。
9. ViewReslover解析后返回具体View。
10. DispatcherServlet根据View进行渲染视图（即将模型数据填充至视图中）。DispatcherServlet响应用户。

**SpringMVC组件解析**

1.前端控制器：DispatcherServlet

- 用户请求到达前端控制器，它就相当于MVC 模式中的C，DispatcherServlet是整个流程控制的中心，由它调用其它组件处理用户的请求，DispatcherServlet的存在降低了组件之间的耦合性。

2.处理器映射器：HandlerMapping

- HandlerMapping负责根据用户请求找到Handler 即处理器，SpringMVC提供了不同的映射器实现不同的映射方式，例如：配置文件方式，实现接口方式，注解方式等。

3.处理器适配器：HandlerAdapter

- 通过HandlerAdapter对处理器进行执行，这是适配器模式的应用，通过扩展适配器可以对更多类型的处理器进行执行。

4.处理器：Handler

- 它就是我们开发中要编写的具体业务控制器。由DispatcherServlet把用户请求转发到Handler。由Handler 对具体的用户请求进行处理。

5.视图解析器：View Resolver

- View Resolver 负责将处理结果生成View 视图，View Resolver 首先根据逻辑视图名解析成物理视图名，即具体的页面地址，再生成View 视图对象，最后对View 进行渲染将处理结果通过页面展示给用户。

6.视图：View

- SpringMVC框架提供了很多的View 视图类型的支持，包括：jstlView、freemarkerView、pdfView等。最常用的视图就是jsp。一般情况下需要通过页面标签或页面模版技术将模型数据通过页面展示给用户，需要由程序员根据业务需求开发具体的页面。

**SpringMVC注解解析**

@RequestMapping

作用：用于建立请求URL 和处理请求方法之间的对应关系

位置：

- 类上，请求URL 的第一级访问目录。此处不写的话，就相当于应用的根目录
- 方法上，请求URL 的第二级访问目录，与类上的使用@ReqquestMapping标注的一级目录一起组成访问虚拟路径

属性：

- value：用于指定请求的URL。它和path属性的作用是一样的
- method：用于指定请求的方式
- params：用于指定限制请求参数的条件。它支持简单的表达式。要求请求参数的key和value必须和配置的一模一样

例子：

- params= {"accountName"}，表示请求参数必须有accountName
- params= {"moeny!100"}，表示请求参数中money不能是100

组件扫描

- SpringMVC基于Spring容器，所以在进行SpringMVC操作时，需要将Controller存储到Spring容器中，如果使用@Controller注解标注的话，就需要使用\<context:component-scanbase-package=“com.itheima.controller"/>进行组件扫描。

**视图解析器**

SpringMVC有默认组件配置，默认组件都是DispatcherServlet.properties配置文件中配置的，该配置文件地址org/springframework/web/servlet/DispatcherServlet.properties，该文件中配置了默认的视图解析器，如下：

```Properties
org.springframework.web.servlet.ViewResolver=org.springframework.web.servlet.view.InternalResourceViewResolver
```

翻看该解析器源码，可以看到该解析器的默认设置，如下：

```Java
REDIRECT_URL_PREFIX = "redirect:" --重定向前缀
FORWARD_URL_PREFIX = "forward:" --转发前缀（默认值）
prefix = ""; --视图名称前缀
suffix = ""; --视图名称后缀
```

可以通过属性注入的方式在spring-mvc.xml中修改视图的的前后缀

```XML
<!--配置内部资源视图解析器-->
<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/jsp/"></property>
    <property name="suffix" value=".jsp"></property>
</bean>
```

### 2.3 SpringMVC的数据响应

**SpringMVC的数据响应方式**

1. 页面跳转
   - 直接返回字符串
   - 通过ModelAndView对象返回
2. 回写数据
   - 直接返回字符串
   - 返回对象或集合

**页面跳转**

返回字符串形式

- 直接返回字符串：此种方式会将返回的字符串与视图解析器的前后缀拼接后跳转。

返回ModelAndView对象

```Java
@RequestMapping(value = "/quick2",method = RequestMethod.GET)
public ModelAndView save2() {
    /*
        Model：模型 作用是封装数据
        View： 视图 作用是展示数据
    */
    ModelAndView modelAndView = new ModelAndView();
    //设置模型数据
    modelAndView.addObject("username","Mark");
    //设置视图名称
    modelAndView.setViewName("success");
    return modelAndView;
}

@RequestMapping(value = "/quick3",method = RequestMethod.GET)
public ModelAndView save3(ModelAndView modelAndView) {
    modelAndView.addObject("username","Welcome Mark");
    modelAndView.setViewName("success");
    return modelAndView;
}

@RequestMapping(value = "/quick4",method = RequestMethod.GET)
public String save4(Model model) {
    model.addAttribute("username","你好世界，哈哈哈");
    return "success";
}
```

向request域存储数据

通过SpringMVC框架注入的request对象setAttribute()方法设置

```Java
@RequestMapping(value = "/quick5",method = RequestMethod.GET)
public String save5(HttpServletRequest request) {
    request.setAttribute("username","你好世界");
    return "success";
}
```

**回写数据**

直接返回字符串

Web基础阶段，客户端访问服务器端，如果想直接回写字符串作为响应体返回的话，只需要使用response.getWriter().print(“hello world”) 即可，那么在Controller中想直接回写字符串该怎样呢？

1.通过SpringMVC框架注入的response对象，使用response.getWriter().print(“hello world”) 回写数据，此时不需要视图跳转，业务方法返回值为void。

```Java
@RequestMapping(value = "/quick6")
public void save6(HttpServletResponse response) throws IOException {
    response.getWriter().print("Hello World");
}
```

2.将需要回写的字符串直接返回，但此时需要通过@ResponseBody注解告知SpringMVC框架，方法返回的字符串不是跳转是直接在http响应体中返回。

```Java
@RequestMapping(value = "/quick7")
@ResponseBody //告知SpringMVC框架不进行视图跳转，直接进行数据响应
public String save7() {
    return "Hello Mark";
}
```

在异步项目中，客户端与服务器端往往要进行json格式字符串交互，此时我们可以手动拼接json字符串返回。

```Java
@RequestMapping(value = "/quick8")
@ResponseBody
public String save8() {
    return "{\"username\":\"zhangsan\",\"age\":18}";
}
```

上述方式手动拼接json格式字符串的方式很麻烦，开发中往往要将复杂的java对象转换成json格式的字符串，我们可以使用web阶段学习过的json转换工具jackson进行转换，导入jackson坐标。

```XML
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-core</artifactId>
  <version>2.9.0</version>
</dependency>
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
  <version>2.9.0</version>
</dependency>
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-annotations</artifactId>
  <version>2.9.0</version>
</dependency>
```

通过jackson转换json格式字符串，回写字符串。

```Java
@RequestMapping(value = "/quick9")
@ResponseBody
public String save9() throws Exception {
    User user = new User();
    user.setUsername("lisi");
    user.setAge(30);
    //使用json的转换工具将对象转换成json格式字符串再返回
    ObjectMapper objectMapper = new ObjectMapper();
    String json = objectMapper.writeValueAsString(user);
    return json;
}
```

返回对象或集合

通过SpringMVC帮助我们对对象或集合进行json字符串的转换并回写，为处理器适配器配置消息转换参数，指定使用jackson进行对象或集合的转换，因此需要在spring-mvc.xml中进行如下配置：

```XML
<!--配置处理器映射器-->
<bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter">
    <property name="messageConverters">
        <list>
            <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter"></bean>
        </list>
    </property>
</bean>
```

```Java
@RequestMapping(value = "/quick10")
@ResponseBody
public User save10() throws Exception {
    User user = new User();
    user.setUsername("lisi");
    user.setAge(28);
    return user;
}
```

在方法上添加@ResponseBody就可以返回json格式的字符串，但是这样配置比较麻烦，配置的代码比较多，因此，我们可以使用mvc的注解驱动代替上述配置。

```XML
<!--mvc的注解驱动-->
<mvc:annotation-driven/>
```

在SpringMVC的各个组件中，处理器映射器、处理器适配器、视图解析器称为SpringMVC的三大组件。

使用\<mvc:annotation-driven>自动加载RequestMappingHandlerMapping（处理映射器）和RequestMappingHandlerAdapter（处理适配器），可用在Spring-mvc.xml配置文件中使用\<mvc:annotation-driven>替代注解处理器和适配器的配置。

同时使用\<mvc:annotation-driven>默认底层就会集成jackson进行对象或集合的json格式字符串的转换。

### 2.4 SpringMVC的请求

**获取请求参数**

客户端请求参数的格式是：name=value&name=value......

服务器端要获得请求的参数，有时还需要进行数据的封装，SpringMVC可以接收如下类型的参数：

- 基本类型数据
- POJO类型数据
- 数组类型数据
- 集合类型数据

**获得基本类型参数**

Controller中的业务方法的参数名称要与请求参数的name一致，参数值会自动映射匹配。

```URL
http://localhost:8080/user/quick11?username=zhangsan&age=18
```

```Java
@RequestMapping(value = "/quick11")
@ResponseBody
public void save11(String username, int age) throws Exception {
    System.out.println(username);
    System.out.println(age);
}
```

**获得POJO类型参数**

Controller中的业务方法的POJO参数的属性名与请求参数的name一致，参数值会自动映射匹配。

```URL
http://localhost:8080/user/quick12?username=zhangsan&age=19
```

```Java
public class User {
    private String username;
    private int age;
	getter/setter...
}

@RequestMapping(value = "/quick12")
@ResponseBody
public void save12(User user) throws Exception {
    System.out.println(user);
}
```

**获得数组类型参数**

Controller中的业务方法数组名称与请求参数的name一致，参数值会自动映射匹配。

```URL
http://localhost:8080/user/quick13?strs=aaa&strs=bbb&strs=ccc
```

```Java
@RequestMapping(value = "/quick13")
@ResponseBody
public void save13(String[] strs) throws Exception {
    System.out.println(Arrays.asList(strs));
}
```

**获得集合类型参数**

获得集合参数时，要将集合参数包装到一个POJO中才可以。

```JSP
<form action="${pageContext.request.contextPath}/user/quick14" method="post">
    <%--表明是第一个User对象的username age--%>
    <input type="text" name="userList[0].username"><br>
    <input type="text" name="userList[0].age"><br>
    <input type="text" name="userList[1].username"><br>
    <input type="text" name="userList[1].age"><br>
    <input type="submit" value="提交">
</form>
```

```Java
import java.util.List;

public class Vo {
    private List<User> userList;

    public List<User> getUserList() {
        return userList;
    }

    public void setUserList(List<User> userList) {
        this.userList = userList;
    }

    @Override
    public String toString() {
        return "Vo{" +
                "userList=" + userList +
                '}';
    }
}
```

```Java
@RequestMapping(value = "/quick14")
@ResponseBody
public void save14(Vo vo) throws Exception {
    System.out.println(vo);
}
```

当使用ajax提交时，可以指定contentType为json形式，那么在方法参数位置使用@RequestBody可以直接接收集合数据而无需使用POJO进行包装。

```JSP
<script src="${pageContext.request.contextPath}/js/jquery-3.3.1.js"></script>
<script>
    var userList = new Array();
    userList.push({username:"zhangsan",age:18});
    userList.push({username:"lisi",age:28});

    $.ajax({
        type:"POST",
        url:"${pageContext.request.contextPath}/user/quick15",
        data:JSON.stringify(userList),
        contentType:"application/json;charset=utf-8"
    });
</script>
```

```Java
@RequestMapping(value = "/quick15")
@ResponseBody
public void save15(@RequestBody List<User> userList) throws Exception {
    System.out.println(userList);
}
```

注意：通过谷歌开发者工具抓包发现，没有加载到jquery文件，原因是SpringMVC的前端控制器DispatcherServlet的url-pattern配置的是/,代表对所有的资源都进行过滤操作，我们可以通过以下两种方式指定放行静态资源：

- 在spring-mvc.xml配置文件中指定放行的资源

  \<mvc:resourcesmapping="/js/**" location="/js/"/>

- 使用\<mvc:default-servlet-handler/>标签

**请求数据乱码问题**

当post请求时，数据会出现乱码，我们可以设置一个过滤器来进行编码的过滤。

```XML
<!--配置全局过滤的filter-->
<filter>
  <filter-name>CharacterEncodingFilter</filter-name>
  <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
  <init-param>
    <param-name>encoding</param-name>
    <param-value>UTF-8</param-value>
  </init-param>
</filter>
<filter-mapping>
  <filter-name>CharacterEncodingFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
```

**参数绑定注解@requestParam**

当请求的参数名称与Controller的业务方法参数名称不一致时，就需要通过@RequestParam注解显示的绑定。

```JSP
<form action="${pageContext.request.contextPath}/quick16" method="post">
    <input type="text" name="name"><br>
    <input type="submit" value="提交"><br>
</form>
```

```Java
@RequestMapping(value = "/quick16")
@ResponseBody
public void save16(@RequestParam("name") String username) {
    System.out.println(username);
}
```

注解@RequestParam的其他参数

- value：与请求参数名称
- required：此在指定的请求参数是否必须包括，默认是true，提交时如果没有此参数则报错
- defaultValue：当没有指定请求参数时，则使用指定的默认值赋值

```Java
@RequestMapping(value = "/quick16")
@ResponseBody
public void save16(@RequestParam(value = "name",required = false,defaultValue = "Mark") String username) {
    System.out.println(username);
}
```

**获得Restful风格的参数**

Restful是一种软件架构风格、设计风格，而不是标准，只是提供了一组设计原则和约束条件。主要用于客户端和服务器交互类的软件，基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存机制等。

Restful风格的请求是使用“url+请求方式”表示一次请求目的的，HTTP 协议里面四个表示操作方式的动词如下：

- GET：用于获取资源
- POST：用于新建资源
- PUT：用于更新资源
- DELETE：用于删除资源

例如：

- /user/1 GET ：得到id = 1 的user
- /user/1 DELETE：删除id = 1 的user
- /user/1 PUT：更新id = 1 的user
- /user POST：新增user

上述url地址/user/1中的1就是要获得的请求参数，在SpringMVC中可以使用占位符进行参数绑定。地址/user/1可以写成/user/{id}，占位符{id}对应的就是1的值。在业务方法中我们可以使用@PathVariable注解进行占位符的匹配获取工作。

```URL
http://localhost:8080/user/quick17/zhangsan
```

```Java
@RequestMapping(value = "/quick17/{username}")
@ResponseBody
public void save17(@PathVariable("username") String username) {
    System.out.println(username);
}
```

**自定义类型转换器**

SpringMVC默认已经提供了一些常用的类型转换器，例如客户端提交的字符串转换成int型进行参数设置。

但是不是所有的数据类型都提供了转换器，没有提供的就需要自定义转换器，例如：日期类型的数据就需要自定义转换器。

自定义类型转换器的开发步骤

1. 定义转换器类实现Converter接口
2. 在配置文件中声明转换器
3. 在\<annotation-driven>中引用转换器

```Java
import org.springframework.core.convert.converter.Converter;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class DateConverter implements Converter<String, Date> {
    @Override
    public Date convert(String dateStr) {
        //将日期字符串转换成日期对象返回
        SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd");
        Date date = null;
        try {
            date = format.parse(dateStr);
        } catch (ParseException e) {
            e.printStackTrace();
        }
        return date;
    }
}
```

```XML
<!--声明转换器-->
<bean id="conversionService" class="org.springframework.context.support.ConversionServiceFactoryBean">
    <property name="converters">
        <list>
            <bean class="com.itahu.converter.DateConverter"></bean>
        </list>
    </property>
</bean>
```

```XML
<!--mvc的注解驱动-->
<mvc:annotation-driven conversion-service="conversionService"/>
```

**获得Servlet相关API**

SpringMVC支持使用原始ServletAPI对象作为控制器方法的参数进行注入，常用的对象如下：

- HttpServletRequest
- HttpServletResponse
- HttpSession

```Java
@RequestMapping(value = "/quick19")
@ResponseBody
public void save19(HttpServletRequest request, HttpServletResponse response, HttpSession session) {
    System.out.println(request);
    System.out.println(response);
    System.out.println(session);
}
```

**获得请求头**

1.@RequestHeader

使用@RequestHeader可以获得请求头信息，相当于web阶段学习的request.getHeader(name)

@RequestHeader注解的属性如下：

- value：请求头的名称
- required：是否必须携带此请求头

```Java
@RequestMapping(value = "/quick20")
@ResponseBody
public void save20(@RequestHeader(value = "User-Agent",required = false) String user_agent) {
    System.out.println(user_agent);
}
```

2.@CookieValue

使用@CookieValue可以获得指定Cookie的值

@CookieValue注解的属性如下：

- value：指定cookie的名称
- required：是否必须携带此cookie

```Java
@RequestMapping(value = "/quick21")
@ResponseBody
public void save21(@CookieValue("JSESSIONID") String jsessionId) {
    System.out.println(jsessionId);
}
```

**文件上传**

文件上传客户端三要素

- 表单项type=“file”
- 表单的提交方式是post
- 表单的enctype属性是多部分表单形式，及enctype=“multipart/form-data”

```JSP
<form action="${pageContext.request.contextPath}/user/quick22" method="post" enctype="multipart/form-data">
    名称<input type="text" name="username"><br>
    文件<input type="file" name="upload"><br>
    <input type="submit" value="上传">
</form>
```

文件上传原理

- 当form表单修改为多部分表单时，request.getParameter()将失效。
- enctype=“application/x-www-form-urlencoded”时，form表单的正文内容格式是：key=value&key=value&key=value
- 当form表单的enctype取值为Mutilpart/form-data时，请求正文内容就变成多部分形式。

单文件上传步骤

1. 导入fileupload和io坐标
2. 配置文件上传解析器
3. 编写文件上传代码

```XML
<dependency>
  <groupId>commons-fileupload</groupId>
  <artifactId>commons-fileupload</artifactId>
  <version>1.3.1</version>
</dependency>
<dependency>
  <groupId>commons-io</groupId>
  <artifactId>commons-io</artifactId>
  <version>2.3</version>
</dependency>
```

```XML
<!--配置文件上传解析器-->
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
    <property name="defaultEncoding" value="UTF-8"/>
    <property name="maxUploadSize" value="500000"/>
</bean>
```

```Java
@RequestMapping(value = "/quick22")
@ResponseBody
public void save22(String username, MultipartFile upload) throws IOException {
    System.out.println(username);
    //获得上传文件名称
    String originalFilename = upload.getOriginalFilename();
    upload.transferTo(new File("F:\\Upload\\" + originalFilename));
}
```

多文件上传实现

多文件上传，只需要将页面修改为多个文件上传项，将方法参数MultipartFile类型修改为MultipartFile[]即可

```JSP
<form action="${pageContext.request.contextPath}/user/quick22" method="post" enctype="multipart/form-data">
    名称<input type="text" name="username"><br>
    文件<input type="file" name="upload"><br>
    文件<input type="file" name="upload"><br>
    <input type="submit" value="上传">
</form>
```

```Java
@RequestMapping(value = "/quick22")
@ResponseBody
public void save22(String username, MultipartFile[] upload) throws IOException {
    System.out.println(username);
    //获得上传文件名称
    for (MultipartFile file : upload) {
        String originalFilename = file.getOriginalFilename();
        file.transferTo(new File("F:\\Upload\\" + originalFilename));
    }
}
```

## 3. JdbcTemplate

### 3.1 Spring JdbcTemplate基本使用

**JdbcTemplate概述**

它是spring框架中提供的一个对象，是对原始繁琐的JdbcAPI对象的简单封装。spring框架为我们提供了很多的操作模板类。例如：操作关系型数据的JdbcTemplate和HibernateTemplate，操作nosql数据库的RedisTemplate，操作消息队列的JmsTemplate等等。

**JdbcTemplate开发步骤**

1.导入spring-jdbc和spring-tx坐标

2.创建数据库表和实体

3.创建JdbcTemplate对象

4.执行数据库操作

```XML
<!--导入spring的jdbc坐标-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
<!--导入spring的tx坐标-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-tx</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
```

```Java
public class Account {
    private String name;
    private double money;
	//省略get和set方法
}
```

```Java
@Test
//测试JdbcTemplate开发步骤
public void test1() throws PropertyVetoException {
    //创建数据源对象
    ComboPooledDataSource dataSource = new ComboPooledDataSource();
    dataSource.setDriverClass("com.mysql.jdbc.Driver");
    dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/test");
    dataSource.setUser("root");
    dataSource.setPassword("root");
    JdbcTemplate jdbcTemplate = new JdbcTemplate();
    //设置数据源对象，知道数据库在哪
    jdbcTemplate.setDataSource(dataSource);
    //执行操作
    int row = jdbcTemplate.update("insert into account values(?,?)", "Tom", 5000);
    System.out.println(row);
}
```

**Spring产生JdbcTemplate对象**

我们可以将JdbcTemplate的创建权交给Spring，将数据源DataSource的创建权也交给Spring，在Spring容器内部将数据源DataSource注入到JdbcTemplate模版对象中，配置如下：

```XML
<!--配置数据源对象-->
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
    <property name="driverClass" value="com.mysql.jdbc.Driver"/>
    <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/test"/>
    <property name="user" value="root"/>
    <property name="password" value="root"/>
</bean>
<!--jdbc模板对象-->
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
    <property name="dataSource" ref="dataSource"/>
</bean>
```

从容器中获得JdbcTemplate进行添加操作

```Java
@Test
//测试Spring产生jdbcTemplate对象
public void test2() {
    ApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
    JdbcTemplate jdbcTemplate = app.getBean(JdbcTemplate.class);
    int row = jdbcTemplate.update("insert into account values(?,?)", "zhangsan", 2888);
    System.out.println(row);
}
```

使用jdbc.properties文件改善使用JdbcTemplate在applicationContext.xml中的配置

```XML
<!--加载jdbc.properties-->
<context:property-placeholder location="classpath:jdbc.properties"/>
<!--配置数据源对象-->
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
    <property name="driverClass" value="${jdbc.driver}"/>
    <property name="jdbcUrl" value="${jdbc.url}"/>
    <property name="user" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>
<!--jdbc模板对象-->
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
    <property name="dataSource" ref="dataSource"/>
</bean>
```

**JdbcTemplate的常用操作**

修改、删除、查询等操作测试

```Java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class JdbcTemplateCRUDTest {
    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Test
    public void testUpdate() {
        jdbcTemplate.update("update account set money=? where name=?",10000,"Tom");
    }

    @Test
    public void testDelete() {
        jdbcTemplate.update("delete from account where name=?","Tom");
    }

    @Test
    public void testQueryAll() {
        List<Account> accountList = jdbcTemplate.query("select * from account", new BeanPropertyRowMapper<Account>(Account.class));
        System.out.println(accountList);
    }

    @Test
    public void testQueryOne() {
        Account account = jdbcTemplate.queryForObject("select * from account where name=?", new BeanPropertyRowMapper<Account>(Account.class), "tom");
        System.out.println(account);
    }

    @Test
    public void testQueryCount() {
        Long count = jdbcTemplate.queryForObject("select count(*) from account", Long.class);
        System.out.println(count);
    }
}
```

### 3.2 Spring练习

**Spring环境搭建步骤**

- 创建工程（Project&Module）
- 导入静态页面（jsp页面）
- 导入需要坐标（pom.xml）
- 创建包结构（controller、service、dao、domain、utils）
- 导入数据库脚本
- 创建POJO类
- 创建配置文件（applicationContext.xml、spring-mvc.xml、jdbc.properties、log4j.properties、web.xml）

### 3.3 SpringMVC拦截器

**拦截器（interceptor）的作用**

Spring MVC 的拦截器类似于Servlet 开发中的过滤器Filter，用于对处理器进行预处理和后处理。

将拦截器按一定的顺序联结成一条链，这条链称为拦截器链（Interceptor Chain）。在访问被拦截的方法或字段时，拦截器链中的拦截器就会按其之前定义的顺序被调用。拦截器也是AOP思想的具体实现。

**拦截器和过滤器区别**

|   区别   |                      过滤器(Filter)                      |                     拦截器(Interceptor)                      |
| :------: | :------------------------------------------------------: | :----------------------------------------------------------: |
| 使用范围 |  是servlet 规范中的一部分，任何Java Web 工程都可以使用   | 是SpringMVC 框架自己的，只有使用了SpringMVC 框架的工程才能用 |
| 拦截范围 | 在url-pattern 中配置了/*之后，可以对所有要访问的资源拦截 | 在\<mvc:mappingpath=“”/>中配置了/**之后，也可以多所有资源进行拦截，但是可以通过\<mvc:exclude-mappingpath=“”/>标签排除不需要拦截的资源 |

**拦截器快速入门**

自定义拦截器步骤

1. 创建拦截器类实现HandlerInterceptor接口
2. 配置拦截器
3. 测试拦截器的拦截效果

```Java
public class MyInterceptor1 implements HandlerInterceptor {
    //在目标方法执行之前 执行
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("preHandle......");
        return true;
    }

    //在目标方法执行之后 视图对象返回之前执行
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("postHandle......");
    }

    //在流程都执行完毕之后 执行
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("afterCompletion......");
    }
}
```

```XML
<!--配置拦截器-->
<mvc:interceptors>
    <mvc:interceptor>
        <!--对哪些资源执行拦截操作-->
        <mvc:mapping path="/**"/>
        <bean class="com.itahu.interceptor.MyInterceptor1"/>
    </mvc:interceptor>
</mvc:interceptors>
```

```Java
@Controller
public class TargetController {
    @RequestMapping("/target")
    public ModelAndView show() {
        System.out.println("目标资源执行......");
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.addObject("name","Mark");
        modelAndView.setViewName("index.jsp");
        return modelAndView;
    }
}
```

**拦截器方法说明**

|      方法名       |                             说明                             |
| :---------------: | :----------------------------------------------------------: |
|    preHandle()    | 方法将在请求处理之前进行调用，该方法的返回值是布尔值Boolean类型的，当它返回为false 时，表示请求结束，后续的Interceptor 和Controller 都不会再执行；当返回值为true 时就会继续调用下一个Interceptor 的preHandle方法 |
|   postHandle()    | 该方法是在当前请求进行处理之后被调用，前提是preHandle方法的返回值为true 时才能被调用，且它会在DispatcherServlet进行视图返回渲染之前被调用，所以我们可以在这个方法中对Controller 处理之后的ModelAndView对象进行操作 |
| afterCompletion() | 该方法将在整个请求结束之后，也就是在DispatcherServlet渲染了对应的视图之后执行，前提是preHandle方法的返回值为true 时才能被调用 |

### 3.4 SpringMVC异常处理

**异常处理的思路**

系统中异常包括两类：预期异常和运行时异常RuntimeException，前者通过捕获异常从而获取异常信息，后者主要通过规范代码开发、测试等手段减少运行时异常的发生。

系统的Dao、Service、Controller出现都通过throws Exception向上抛出，最后由SpringMVC前端控制器交由异常处理器进行异常处理。

**异常处理两种方式**

- 使用SpringMVC提供的简单异常处理器SimpleMappingExceptionResolver
- 实现Spring的异常处理接口HandlerExceptionResolver自定义自己的异常处理器

**简单异常处理器SimpleMappingExceptionResolver**

SpringMVC已经定义好了该类型转换器，在使用时可以根据项目情况进行相应异常与视图的映射配置

```XML
<!--配置异常处理器-->
<bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
    <property name="defaultErrorView" value="error"/>
    <property name="exceptionMappings">
        <map>
            <entry key="java.lang.ClassCastException" value="error1"/>
            <entry key="com.itahu.exception.MyException" value="error2"/>
        </map>
    </property>
</bean>
```

**自定义异常处理步骤**

1. 创建异常处理器类实现HandlerExceptionResolver
2. 配置异常处理器
3. 编写异常页面
4. 测试异常跳转

```Java
public class MyExceptionResolver implements HandlerExceptionResolver {
    /*
        参数Exception：异常对象
        返回值ModelAndView：跳转到错误视图信息
    */
    public ModelAndView resolveException(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) {
        ModelAndView modelAndView = new ModelAndView();
        if (e instanceof MyException) {
            modelAndView.addObject("info","自定义异常");
        } else if (e instanceof ClassCastException) {
            modelAndView.addObject("info","类转换异常");
        }
        modelAndView.setViewName("error");
        return modelAndView;
    }
}
```

```XML
<!--自定义异常处理器-->
<bean class="com.itheima.resolver.MyExceptionResolver"/>
```

## 4. 面向切面编程AOP

### 4.1 Spring的AOP简介

AOP 为Aspect Oriented Programming 的缩写，意思为面向切面编程，是通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。

AOP是OOP 的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

**AOP 的作用及其优势**

- 作用：在程序运行期间，在不修改源码的情况下对方法进行功能增强
- 优势：减少重复代码，提高开发效率，并且便于维护

**AOP 的底层实现**

实际上，AOP 的底层是通过Spring 提供的的动态代理技术实现的。在运行期间，Spring通过动态代理技术动态的生成代理对象，代理对象方法执行时进行增强功能的介入，在去调用目标对象的方法，从而完成功能的增强。

**AOP 的动态代理技术**

常用的动态代理技术

- JDK代理：基于接口的动态代理技术
- cglib代理：基于父类的动态代理技术

**JDK的动态代理**

1.目标类接口

```Java
public interface TargetInterface {
    public void save();
}
```

2.目标类

```Java
public class Target implements TargetInterface {
    @Override
    public void save() {
        System.out.println("save running......");
    }
}
```

3.增强类

```Java
public class Advice {
    public void before() {
        System.out.println("前置增强...");
    }

    public void afterReturning() {
        System.out.println("后置增强...");
    }
}
```

4.动态代理代码

```Java
public class ProxyTest {
    public static void main(String[] args) {
        //目标对象
        final Target target = new Target();
        //增强对象
        final Advice advice = new Advice();
        //返回值就是动态生成的代理对象
        TargetInterface proxy = (TargetInterface) Proxy.newProxyInstance(
                target.getClass().getClassLoader(), //目标对象类加载器
                target.getClass().getInterfaces(), //目标对象相同的接口字节码对象数组
                new InvocationHandler() {
                    //调用代理对象的任何方法，实质执行的都是invoke方法
                    @Override
                    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                        advice.before(); //前置增强
                        Object invoke = method.invoke(target, args); //执行目标方法
                        advice.afterReturning(); //后置增强
                        return invoke;
                    }
                }
        );
        //调用代理对象的方法
        proxy.save();
    }
}
```

**cglib的动态代理**

1.目标类

```Java
public class Target {
    public void save() {
        System.out.println("save running......");
    }
}
```

2.增强类

```Java
public class Advice {
    public void before() {
        System.out.println("前置增强...");
    }

    public void afterReturning() {
        System.out.println("后置增强...");
    }
}
```

3.动态代理代码

```Java
public class ProxyTest {
    public static void main(String[] args) {
        //目标对象
        final Target target = new Target();
        //增强对象
        final Advice advice = new Advice();
        //返回值就是动态生成的代理对象，基于cglib
        //1、创建增强器
        Enhancer enhancer = new Enhancer();
        //2、设置父类(目标)
        enhancer.setSuperclass(Target.class);
        //3、设置回调
        enhancer.setCallback(new MethodInterceptor() {
            @Override
            public Object intercept(Object proxy, Method method, Object[] args, MethodProxy methodProxy) throws Throwable {
                advice.before(); //执行前置
                Object invoke = method.invoke(target, args); //执行目标
                advice.afterReturning(); //执行后置
                return invoke;
            }
        });
        //4、创建代理对象
        Target proxy = (Target) enhancer.create();
        //调用代理对象的方法
        proxy.save();
    }
}
```

**AOP 相关概念**

Spring 的AOP实现底层就是对上面的动态代理的代码进行了封装，封装后我们只需要对需要关注的部分进行代码编写，并通过配置的方式完成指定目标的方法增强。

在正式讲解AOP 的操作之前，我们必须理解AOP 的相关术语，常用的术语如下：

- Target(目标对象)：代理的目标对象
- Proxy (代理)：一个类被AOP 织入增强后，就产生一个结果代理类
- Joinpoint(连接点)：所谓连接点是指那些被拦截到的点。在spring中，这些点指的是方法，因为spring只支持方法类型的连接点
- Pointcut(切入点)：所谓切入点是指我们要对哪些Joinpoint进行拦截的定义
- Advice(通知/ 增强)：所谓通知是指拦截到Joinpoint之后所要做的事情就是通知
- Aspect(切面)：是切入点和通知(引介)的结合
- Weaving(织入)：是指把增强应用到目标对象来创建新的代理对象的过程。spring采用动态代理织入，而AspectJ采用编译期织入和类装载期织入

**AOP开发明确的事项**

1.需要编写的内容

- 编写核心业务代码(目标类的目标方法)
- 编写切面类，切面类中有通知(增强功能方法)
- 在配置文件中，配置织入关系，即将哪些通知与哪些连接点进行结合

2.AOP技术实现的内容

Spring 框架监控切入点方法的执行。一旦监控到切入点方法被运行，使用代理机制，动态创建目标对象的代理对象，根据通知类别，在代理对象的对应位置，将通知对应的功能织入，完成完整的代码逻辑运行。

3.AOP底层使用哪种代理方式

在Spring中，框架会根据目标类是否实现了接口来决定采用哪种动态代理的方式。

### 4.2 XML方式实现AOP

**快速入门**

1. 导入AOP相关坐标
2. 创建目标接口和目标类(内部有切点)
3. 创建切面类(内部有增强方法)
4. 将目标类和切面类的对象创建权交给spring
5. 在applicationContext.xml中配置织入关系
6. 测试代码

```XML
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-context</artifactId>
  <version>5.0.5.RELEASE</version>
</dependency>
<dependency>
  <groupId>org.aspectj</groupId>
  <artifactId>aspectjweaver</artifactId>
  <version>1.8.4</version>
</dependency>
```

```Java
public interface TargetInterface {
    public void save();
}
```

```Java
public class Target implements TargetInterface {
    @Override
    public void save() {
        System.out.println("save running......");
    }
}
```

```Java
public class MyAspect {
    public void before() {
        System.out.println("前置增强......");
    }
}
```

```XML
<!--目标对象-->
<bean id="target" class="com.itahu.aop.Target"></bean>
<!--切面对象-->
<bean id="myAspect" class="com.itahu.aop.MyAspect"></bean>
<!--配置织入：告诉Spring框架哪些方法(切点)需要进行哪些增强(前置、后置...)-->
<aop:config>
    <!--声明切面-->
    <aop:aspect ref="myAspect">
        <!--切面，切点+通知-->
        <aop:before method="before" pointcut="execution(public void com.itahu.aop.Target.save())"></aop:before>
    </aop:aspect>
</aop:config>
```

```Java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class AopTest {
    @Autowired
    private TargetInterface target;

    @Test
    public void test1() {
        target.save();
    }
}
```

**XML配置AOP详解**

1.切点表达式的写法

表达式语法：

```XML
execution([修饰符] 返回值类型 包名.类名.方法名(参数))
```

- 访问修饰符可以省略
- 返回值类型、包名、类名、方法名可以使用星号*代表任意
- 包名与类名之间一个点. 代表当前包下的类，两个点.. 表示当前包及其子包下的类
- 参数列表可以使用两个点.. 表示任意个数，任意类型的参数列表

例如：

```XML
execution(public void com.itheima.aop.Target.method())
execution(void com.itheima.aop.Target.*(..))
execution(* com.itheima.aop.*.*(..))
execution(* com.itheima.aop..*.*(..))
execution(* *..*.*(..))
```

2.通知的类型

通知的配置语法：

```XML
<aop:通知类型 method=“切面类中方法名” pointcut=“切点表达式"></aop:通知类型>
```

|     名称     |          标签          |                             说明                             |
| :----------: | :--------------------: | :----------------------------------------------------------: |
|   前置通知   |     \<aop:before>      |     用于配置前置通知。指定增强的方法在切入点方法之前执行     |
|   后置通知   | \<aop:after-returning> |     用于配置后置通知。指定增强的方法在切入点方法之后执行     |
|   环绕通知   |     \<aop:around>      | 用于配置环绕通知。指定增强的方法在切入点方法之前和之后都执行 |
| 异常抛出通知 |    \<aop:throwing>     |     用于配置异常抛出通知。指定增强的方法在出现异常时执行     |
|   最终通知   |      \<aop:after>      |     用于配置最终通知。无论增强方式执行是否有异常都会执行     |

3.切点表达式的抽取

当多个增强的切点表达式相同时，可以将切点表达式进行抽取，在增强中使用pointcut-ref属性代替pointcut 属性来引用抽取后的切点表达式。

```XML
<!--目标对象-->
<bean id="target" class="com.itahu.aop.Target"></bean>
<!--切面对象-->
<bean id="myAspect" class="com.itahu.aop.MyAspect"></bean>
<!--配置织入：告诉Spring框架哪些方法(切点)需要进行哪些增强(前置、后置...)-->
<aop:config>
    <!--声明切面-->
    <aop:aspect ref="myAspect">
        <!--抽取切点表达式-->
        <aop:pointcut id="myPointcut" expression="execution(* com.itahu.aop.*.*(..))"/>
        <aop:around method="around" pointcut-ref="myPointcut"/>
        <aop:after method="after" pointcut-ref="myPointcut"/>
    </aop:aspect>
</aop:config>
```

### 4.3 注解方式实现AOP

**快速入门**

基于注解的aop开发步骤：

1. 创建目标接口和目标类(内部有切点)
2. 创建切面类(内部有增强方法)
3. 将目标类和切面类的对象创建权交给spring
4. 在切面类中使用注解配置织入关系
5. 在配置文件中开启组件扫描和AOP的自动代理
6. 测试

```Java
public interface TargetInterface {
    public void save();
}
```

```Java
@Component("target")
public class Target implements TargetInterface {
    @Override
    public void save() {
        System.out.println("save running......");
    }
}
```

```Java
@Component("myAspect")
@Aspect //标注当前MyAsPect是一个切面类
public class MyAspect {
    //配置前置通知
    @Before("execution(* com.itahu.anno.*.*(..))")
    public void before() {
        System.out.println("前置增强......");
    }

    public void afterReturning() {
        System.out.println("后置增强......");
    }

    //Proceeding JoinPoint：正在执行的连接点==切点
    public Object around(ProceedingJoinPoint pjp) throws Throwable {
        System.out.println("环绕前增强...");
        //切点方法
        Object proceed = pjp.proceed();
        System.out.println("环绕后增强...");
        return proceed;
    }

    public void afterThrowing() {
        System.out.println("异常抛出增强......");
    }

    public void after() {
        System.out.println("最终增强......");
    }
}
```

```XML
<!--组件扫描-->
<context:component-scan base-package="com.itahu.anno"/>

<!--aop自动代理-->
<aop:aspectj-autoproxy/>
```

```Java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext-anno.xml")
public class AnnoTest {
    @Autowired
    private TargetInterface target;

    @Test
    public void test1() {
        target.save();
    }
}
```

**注解配置AOP详解**

1.注解通知的类型

通知的配置语法：@通知注解(“切点表达式")

|     名称     |      注解       |                             说明                             |
| :----------: | :-------------: | :----------------------------------------------------------: |
|   前置通知   |     @Before     |     用于配置前置通知。指定增强的方法在切入点方法之前执行     |
|   后置通知   | @AfterReturning |     用于配置后置通知。指定增强的方法在切入点方法之后执行     |
|   环绕通知   |     @Around     | 用于配置环绕通知。指定增强的方法在切入点方法之前和之后都执行 |
| 异常抛出通知 | @AfterThrowing  |     用于配置异常抛出通知。指定增强的方法在出现异常时执行     |
|   最终通知   |     @After      |     用于配置最终通知。无论增强方式执行是否有异常都会执行     |

2.切点表达式的抽取

同xml配置aop一样，我们可以将切点表达式抽取。抽取方式是在切面内定义方法，在该方法上使用@Pointcut注解定义切点表达式，然后在在增强注解中进行引用。

```Java
@Component("myAspect")
@Aspect //标注当前MyAsPect是一个切面类
public class MyAspect {
    //配置前置通知
    //@Before("execution(* com.itahu.anno.*.*(..))")
    public void before() {
        System.out.println("前置增强......");
    }

    public void afterReturning() {
        System.out.println("后置增强......");
    }

    //Proceeding JoinPoint：正在执行的连接点==切点
    @Around("pointcut()")
    public Object around(ProceedingJoinPoint pjp) throws Throwable {
        System.out.println("环绕前增强...");
        //切点方法
        Object proceed = pjp.proceed();
        System.out.println("环绕后增强...");
        return proceed;
    }

    public void afterThrowing() {
        System.out.println("异常抛出增强......");
    }

    @After("MyAspect.pointcut()")
    public void after() {
        System.out.println("最终增强......");
    }

    //定义切点表达式
    @Pointcut("execution(* com.itahu.anno.*.*(..))")
    public void pointcut() {}
}
```

## 5. Spring的事务控制

### 5.1 编程式事务控制相关对象

**PlatformTransactionManager**

PlatformTransactionManager接口是spring的事务管理器，它里面提供了我们常用的操作事务的方法。

|                             方法                             |        说明        |
| :----------------------------------------------------------: | :----------------: |
| TransactionStatus getTransaction(TransactionDefination defination) | 获取事务的状态信息 |
|            void commit(TransactionStatus status)             |      提交事务      |
|           void rollback(TransactionStatus status)            |      回滚事务      |

注意：PlatformTransactionManager是接口类型，不同的Dao层技术则有不同的实现类，例如：Dao层技术是jdbc或mybatis时：org.springframework.jdbc.datasource.DataSourceTransactionManager
Dao层技术是hibernate时：org.springframework.orm.hibernate5.HibernateTransactionManager

**TransactionDefinition**

TransactionDefinition是事务的定义信息对象，里面有如下方法：

|             方法             |        说明        |
| :--------------------------: | :----------------: |
|   int getIsolationLevel()    | 获得事务的隔离级别 |
| int getPropogationBehavior() | 获得事务的传播行为 |
|       int getTimeout()       |    获得超时时间    |
|     boolean isReadOnly()     |      是否只读      |

1.事务隔离级别

设置隔离级别，可以解决事务并发产生的问题，如脏读、不可重复读和虚读。

- ISOLATION_DEFAULT
- ISOLATION_READ_UNCOMMITTED
- ISOLATION_READ_COMMITTED
- ISOLATION_REPEATABLE_READ
- ISOLATION_SERIALIZABLE

2.事务传播行为

- REQUIRED：如果当前没有事务，就新建一个事务，如果已经存在一个事务中，加入到这个事务中。一般的选择（默认值）
- SUPPORTS：支持当前事务，如果当前没有事务，就以非事务方式执行（没有事务）
- MANDATORY：使用当前的事务，如果当前没有事务，就抛出异常
- REQUERS_NEW：新建事务，如果当前在事务中，把当前事务挂起
- NOT_SUPPORTED：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起
- NEVER：以非事务方式运行，如果当前存在事务，抛出异常
- NESTED：如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则执行REQUIRED 类似的操作
- 超时时间：默认值是-1，没有超时限制。如果有，以秒为单位进行设置
- 是否只读：建议查询时设置为只读

**TransactionStatus**

TransactionStatus接口提供的是事务具体的运行状态，方法介绍如下。

|            方法            |      说明      |
| :------------------------: | :------------: |
|   boolean hasSavepoint()   | 是否存储回滚点 |
|   boolean isCompleted()    |  事务是否完成  |
| boolean isNewTransaction() |  是否是新事务  |
|  boolean isRollbackOnly()  |  事务是否回滚  |

### 5.2 基于XML的声明式事务控制

**什么是声明式事务控制**

Spring的声明式事务顾名思义就是采用声明的方式来处理事务。这里所说的声明，就是指在配置文件中声明，用在Spring 配置文件中声明式的处理事务来代替代码式的处理事务。

**声明式事务处理的作用**

- 事务管理不侵入开发的组件。具体来说，业务逻辑对象就不会意识到正在事务管理之中，事实上也应该如此，因为事务管理是属于系统层面的服务，而不是业务逻辑的一部分，如果想要改变事务管理策划的话，也只需要在定义文件中重新配置即可
- 在不需要事务管理的时候，只要在设定文件上修改一下，即可移去事务管理服务，无需改变代码重新编译，这样维护起来极其方便

注意：Spring声明式事务控制底层就是AOP。

**声明式事务控制的实现**

声明式事务控制明确事项

- 谁是切点
- 谁是通知
- 谁是切面

```XML
<!--目标对象 内部的方法就是切点-->
<bean id="accountService" class="com.itheima.service.impl.AccountServiceImpl">
    <property name="accountDao" ref="accountDao"/>
</bean>

<!--配置平台事务管理器-->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <property name="dataSource" ref="dataSource"/>
</bean>

<!--通知 事务的增强-->
<tx:advice id="txAdvice" transaction-manager="transactionManager">
    <!--设置事务的属性信息的-->
    <tx:attributes>
        <tx:method name="*"/>
    </tx:attributes>
</tx:advice>

<!--配置事务的aop织入-->
<aop:config>
    <aop:advisor advice-ref="txAdvice" pointcut="execution(* com.itheima.service.impl.*.*(..))"></aop:advisor>
</aop:config>
```

**切点方法的事务参数的配置**

```XML
<!--通知 事务的增强-->
<tx:advice id="txAdvice" transaction-manager="transactionManager">
    <!--设置事务的属性信息的-->
    <tx:attributes>
        <tx:method name="transfer" isolation="REPEATABLE_READ" propagation="REQUIRED" read-only="false"/>
        <tx:method name="save" isolation="REPEATABLE_READ" propagation="REQUIRED" read-only="false"/>
        <tx:method name="findAll" isolation="REPEATABLE_READ" propagation="REQUIRED" read-only="true"/>
        <tx:method name="update*" isolation="REPEATABLE_READ" propagation="REQUIRED" read-only="false"/>
        <tx:method name="*"/>
    </tx:attributes>
</tx:advice>
```

其中，\<tx:method> 代表切点方法的事务参数的配置，例如：

<tx:method name="transfer" isolation="REPEATABLE_READ" propagation="REQUIRED" timeout="-1" read-only="false"/>

- name：切点方法名称
- isolation：事务的隔离级别
- propogation：事务的传播行为
- timeout：超时时间
- read-only：是否只读

**声明式事务控制的配置要点**

- 平台事务管理器配置
- 事务通知的配置
- 事务aop织入的配置

### 5.3 基于注解的声明式事务控制

**使用注解配置声明式事务控制**

1.编写AccoutDao

```Java
@Repository("accoutDao")
public class AccountDaoImpl implements AccountDao {
    @Autowired
    private JdbcTemplate jdbcTemplate;

    public void out(String outMan, double money) {
        jdbcTemplate.update("update account set money=money-? where name=?",money,outMan);
    }

    public void in(String inMan, double money) {
        jdbcTemplate.update("update account set money=money+? where name=?",money,inMan);
    }
}
```

2.编写AccoutService

```Java
@Service("accountService")
@Transactional(isolation = Isolation.REPEATABLE_READ)
public class AccountServiceImpl implements AccountService {

    @Autowired
    private AccountDao accountDao;

    @Transactional(isolation = Isolation.READ_COMMITTED,propagation = Propagation.REQUIRED)
    public void transfer(String outMan, String inMan, double money) {
        accountDao.out(outMan,money);
        int i = 1/0;
        accountDao.in(inMan,money);
    }
}
```

3.编写applicationContext.xml配置文件

```XML
<!--之前省略datsSource、jdbcTemplate、平台事务管理器的配置-->
<!--组件扫描-->
<context:component-scan base-package="com.itheima"/>
<!--事务的注解驱动-->
<tx:annotation-driven transaction-manager="transactionManager"/>
```

**注解配置声明式事务控制解析**

- 使用@Transactional在需要进行事务控制的类或是方法上修饰，注解可用的属性同xml 配置方式，例如隔离级别、传播行为等。
- 注解使用在类上，那么该类下的所有方法都使用同一套注解参数配置。
- 使用在方法上，不同的方法可以采用不同的事务参数配置。
- Xml配置文件中要开启事务的注解驱动\<tx:annotation-driven/>

## 6. MyBatis入门操作

### 6.1 Mybatis简介

**原始jdbc操作的分析**

原始jdbc开发存在的问题

- 数据库连接创建、释放频繁造成系统资源浪费从而影响系统性能
- sql语句在代码中硬编码，造成代码不易维护，实际应用sql变化的可能较大，sql变动需要改变java代码
- 查询操作时，需要手动将结果集中的数据手动封装到实体中。插入操作时，需要手动将实体的数据设置到sql语句的占位符位置

应对上述问题给出的解决方案

- 使用数据库连接池初始化连接资源
- 将sql语句抽取到xml配置文件中
- 使用反射、内省等底层技术，自动将实体与表进行属性与字段的自动映射

**什么是Mybatis**

- mybatis是一个优秀的基于java的持久层框架，它内部封装了jdbc，使开发者只需要关注sql语句本身，而不需要花费精力去处理加载驱动、创建连接、创建statement等繁杂的过程。
- mybatis通过xml或注解的方式将要执行的各种statement配置起来，并通过java对象和statement中sql的动态参数进行映射生成最终执行的sql语句。
- 最后mybatis框架执行sql并将结果映射为java对象并返回。采用ORM思想解决了实体和数据库映射的问题，对jdbc进行了封装，屏蔽了jdbcapi底层访问细节，使我们不用与jdbcapi打交道，就可以完成对数据库的持久化操作。

### 6.2 Mybatis的快速入门

**MyBatis开发步骤**

1. 添加MyBatis的坐标
2. 创建user数据表
3. 编写User实体类
4. 编写映射文件UserMapper.xml
5. 编写核心文件SqlMapConfig.xml
6. 编写测试类

导入MyBatis的坐标和其他相关坐标

```XML
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.32</version>
</dependency>
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.4.6</version>
</dependency>
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

创建user数据表

编写User实体

```Java
public class User {
    private int id;
    private String username;
    private String password;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}
```

编写UserMapper映射文件

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--命名空间，与下面语句的id一起组成查询的标识-->
<mapper namespace="userMapper">
    <!--resultType：查询结果对应的实体类型-->
    <select id="findAll" resultType="com.itahu.domain.User">
        select * from user
    </select>
</mapper>
```

编写MyBatis核心文件

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--数据源环境-->
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/test"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>
    </environments>
    <!--加载映射文件-->
    <mappers>
        <mapper resource="com/itahu/mapper/UserMapper.xml"></mapper>
    </mappers>
</configuration>
```

编写测试代码

```Java
public class MyBatisTest {
    @Test
    public void test1() throws IOException {
        //获得核心配置文件
        InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
        //获得session工厂对象
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
        //获得session会话对象
        SqlSession sqlSession = sqlSessionFactory.openSession();
        //执行操作 参数：namespace+id
        List<User> userList = sqlSession.selectList("userMapper.findAll");
        //打印数据
        System.out.println(userList);
        //释放资源
        sqlSession.close();
    }
}
```

### 6.3 MyBatis的增删改查操作

**MyBatis的插入数据操作**

编写UserMapper映射文件

```XML
<!--插入操作-->
<insert id="save" parameterType="com.itahu.domain.User">
    insert into user values(#{id},#{username},#{password})
</insert>
```

编写插入实体User的代码

```Java
@Test
public void test2() throws IOException {
    //模拟user对象
    User user = new User();
    user.setUsername("tom");
    user.setPassword("abc");

    //获得核心配置文件
    InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
    //获得session工厂对象
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
    //获得session会话对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //执行操作 参数：namespace+id
    sqlSession.insert("userMapper.save",user);
    //mybatis执行更新操作，提交事务
    sqlSession.commit();
    //释放资源
    sqlSession.close();
}
```

插入操作注意问题

- 插入语句使用insert标签
- 在映射文件中使用parameterType属性指定要插入的数据类型
- Sql语句中使用#{实体属性名}方式引用实体中的属性值
- 插入操作使用的API是sqlSession.insert(“命名空间.id”,实体对象);
- 插入操作涉及数据库数据变化，所以要使用sqlSession对象显示的提交事务，即sqlSession.commit()

**MyBatis的修改数据操作**

编写UserMapper映射文件

```XML
<!--修改操作-->
<update id="update" parameterType="com.itahu.domain.User">
    update user set username=#{username},password=#{password} where id=#{id}
</update>
```

编写修改实体User的代码

```Java
@Test
public void test3() throws IOException {
    //模拟user对象
    User user = new User();
    user.setId(7);
    user.setUsername("lucy");
    user.setPassword("123");

    //获得核心配置文件
    InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
    //获得session工厂对象
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
    //获得session会话对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //执行操作 参数：namespace+id
    sqlSession.update("userMapper.update",user);
    //mybatis执行更新操作，提交事务
    sqlSession.commit();
    //释放资源
    sqlSession.close();
}
```

修改操作注意问题

- 修改语句使用update标签
- 修改操作使用的API是sqlSession.update(“命名空间.id”,实体对象);

**MyBatis的删除数据操作**

编写UserMapper映射文件

```XML
<!--删除操作-->
<delete id="delete" parameterType="java.lang.Integer">
    delete from user where id=#{id}
</delete>
```

编写删除数据的代码

```Java
@Test
public void test4() throws IOException {
    //获得核心配置文件
    InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
    //获得session工厂对象
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
    //获得session会话对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //执行操作 参数：namespace+id
    sqlSession.delete("userMapper.delete",7);
    //mybatis执行更新操作，提交事务
    sqlSession.commit();
    //释放资源
    sqlSession.close();
}
```

删除操作注意问题

- 删除语句使用delete标签
- Sql语句中使用#{任意字符串}方式引用传递的单个参数
- 删除操作使用的API是sqlSession.delete(“命名空间.id”,Object);

### 6.4 MyBatis的核心配置文件概述

**MyBatis核心配置文件层级关系**

configuration配置

- properties 属性
- settings 设置
- typeAliases 类型别名
- typeHandlers 类型处理器
- objectFactory 对象工厂
- plugins 插件
- environments 环境
  - environment 环境变量
  - transactionManager 事务管理器
  - dataSource 数据源
- databaseIdProvider 数据库厂商标识
- mappers 映射器

**MyBatis常用配置解析**

1.environments标签

其中，事务管理器（transactionManager）类型有两种

- JDBC：这个配置就是直接使用了JDBC 的提交和回滚设置，它依赖于从数据源得到的连接来管理事务作用域。
- MANAGED：这个配置几乎没做什么。它从来不提交或回滚一个连接，而是让容器来管理事务的整个生命周期（比如JEE 应用服务器的上下文）。默认情况下它会关闭连接，然而一些容器并不希望这样，因此需要将closeConnection属性设置为false 来阻止它默认的关闭行为。

其中，数据源（dataSource）类型有三种

- UNPOOLED：这个数据源的实现只是每次被请求时打开和关闭连接。
- POOLED：这种数据源的实现利用“池”的概念将JDBC 连接对象组织起来。
- JNDI：这个数据源的实现是为了能在如EJB 或应用服务器这类容器中使用，容器可以集中或在外部配置数据源，然后放置一个JNDI 上下文的引用。

2.mapper标签

该标签的作用是加载映射的，加载方式有如下几种

- 使用相对于类路径的资源引用，例如：\<mapper resource="org/mybatis/builder/AuthorMapper.xml"/>
- 使用完全限定资源定位符（URL），例如：\<mapper url="file:///var/mappers/AuthorMapper.xml"/>
- 使用映射器接口实现类的完全限定类名，例如：\<mapper class="org.mybatis.builder.AuthorMapper"/>
- 将包内的映射器接口实现全部注册为映射器，例如：\<package name="org.mybatis.builder"/>

3.Properties标签

实际开发中，习惯将数据源的配置信息单独抽取成一个properties文件，该标签可以加载额外配置的properties文件

```Properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/test
jdbc.username=root
jdbc.password=root
```

```XML
<!--通过properties标签加载外部properties文件-->
<properties resource="jdbc.properties"></properties>

<!--数据源环境-->
<environments default="development">
    <environment id="development">
        <transactionManager type="JDBC"></transactionManager>
        <dataSource type="POOLED">
            <property name="driver" value="${jdbc.driver}"/>
            <property name="url" value="${jdbc.url}"/>
            <property name="username" value="${jdbc.username}"/>
            <property name="password" value="${jdbc.password}"/>
        </dataSource>
    </environment>
</environments>
```

4.typeAliases标签

类型别名是为Java 类型设置一个短的名字。

```XML
<!--自定义别名-->
<typeAliases>
    <typeAlias type="com.itahu.domain.User" alias="user"></typeAlias>
</typeAliases>
```

```XML
<!--查询操作-->
<select id="findAll" resultType="user">
    select * from user
</select>
```

mybatis框架已经为我们设置好的一些常用的类型的别名

|  别名   | 数据类型 |
| :-----: | :------: |
| string  |  String  |
|  long   |   Long   |
|   int   | Integer  |
| double  |  Double  |
| boolean | Boolean  |
|   ...   |   ...    |

### 6.5 MyBatis相应API

**SqlSession工厂构建器SqlSessionFactoryBuilder**

常用API：SqlSessionFactorybuild(InputStreaminputStream)

通过加载mybatis的核心文件的输入流的形式构建一个SqlSessionFactory对象

```Java
//获得核心配置文件
InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
//获得session工厂对象
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
```

其中，Resources工具类，这个类在org.apache.ibatis.io包中。Resources类帮助你从类路径下、文件系统或一个web URL中加载资源文件。

**SqlSession工厂对象SqlSessionFactory**

SqlSessionFactory有多个个方法创建SqlSession实例。常用的有如下两个：

|              方法               |                             解释                             |
| :-----------------------------: | :----------------------------------------------------------: |
|          openSession()          | 会默认开启一个事务，但事务不会自动提交，也就意味着需要手动提交该事务，更新操作数据才会持久化到数据库中 |
| openSession(boolean autoCommit) |  参数为是否自动提交，如果设置为true，那么不需要手动提交事务  |

**SqlSession会话对象**

SqlSession实例在MyBatis中是非常强大的一个类。在这里你会看到所有执行语句、提交或回滚事务和获取映射器实例的方法。

执行语句的方法主要有：

```Java
<T> T selectOne(String statement, Object parameter)
<E> List<E> selectList(String statement, Object parameter)
int insert(String statement, Object parameter)
int update(String statement, Object parameter)
int delete(String statement, Object parameter)
```

操作事务的方法主要有：

```Java
void commit()
void rollback()
```

### 6.6 Mybatis的Dao层实现

**传统开发方式**

编写UserDao接口

```Java
public interface UserMapper {
    public List<User> findAll() throws IOException;
}
```

编写UserDaoImpl实现

```Java
public class UserMapperImpl implements UserMapper {
    @Override
    public List<User> findAll() throws IOException {
        InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
        SqlSession sqlSession = sqlSessionFactory.openSession();
        List<User> userList = sqlSession.selectList("userMapper.findAll");
        return userList;
    }
}
```

测试传统方式

```Java
public class ServiceDemo {
    public static void main(String[] args) throws IOException {
        //创建dao层对象，当前dao层实现是手动编写的
        UserMapper userMapper = new UserMapperImpl();
        List<User> all = userMapper.findAll();
        System.out.println(all);
    }
}
```

**代理开发方式**

代理开发方式介绍

采用Mybatis的代理开发方式实现DAO 层的开发，这种方式是我们后面进入企业的主流。

Mapper 接口开发方法只需要程序员编写Mapper 接口（相当于Dao 接口），由Mybatis框架根据接口定义创建接口的动态代理对象，代理对象的方法体同上边Dao接口实现类方法。

Mapper接口开发需要遵循以下规范：

1. Mapper.xml文件中的namespace与mapper接口的全限定名相同
2. Mapper接口方法名和Mapper.xml中定义的每个statement的id相同
3. Mapper接口方法的输入参数类型和mapper.xml中定义的每个sql的parameterType的类型相同
4. Mapper接口方法的输出参数类型和mapper.xml中定义的每个sql的resultType的类型相同

```Java
public interface UserMapper {
    public List<User> findAll() throws IOException;

    public User findById(int id);
}
```

```XML
<mapper namespace="com.itahu.dao.UserMapper">
    <!--查询操作-->
    <select id="findAll" resultType="user">
        select * from user
    </select>

    <!--根据id进行查询-->
    <select id="findById" parameterType="int" resultType="user">
        select * from user where id = #{id}
    </select>
</mapper>
```

```Java
public class ServiceDemo {
    public static void main(String[] args) throws IOException {
        //创建dao层对象，当前dao层实现是手动编写的
        InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
        SqlSession sqlSession = sqlSessionFactory.openSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        List<User> all = mapper.findAll();
        System.out.println(all);

        User user = mapper.findById(1);
        System.out.println(user);
    }
}
```

### 6.7 MyBatis映射文件深入

**动态sql语句**

动态sql语句概述

Mybatis的映射文件中，前面我们的SQL 都是比较简单的，有些时候业务逻辑复杂时，我们的SQL是动态变化的，此时在前面的学习中我们的SQL 就不能满足要求了。

动态SQL之\<if>

我们根据实体类的不同取值，使用不同的SQL语句来进行查询。比如在id如果不为空时可以根据id查询，如果username不同空时还要加入用户名作为条件。这种情况在我们的多条件组合查询中经常会碰到。

```XML
<select id="findByCondition" parameterType="user" resultType="user">
    select * from user
    <where>
        <if test="id!=0">
            and id=#{id}
        </if>
        <if test="username!=null">
            and username=#{username}
        </if>
        <if test="password!=null">
            and password=#{password}
        </if>
    </where>
</select>
```

动态SQL之\<foreach>

循环执行sql的拼接操作，例如：SELECT * FROM USER WHERE id IN (1,2,5)。

```XML
<select id="findByIds" parameterType="list" resultType="user">
    select * from user
    <where>
        <foreach collection="list" open="id in(" close=")" item="id" separator=",">
            #{id}
        </foreach>
    </where>
</select>
```

foreach标签的属性含义

\<foreach>标签用于遍历集合，它的属性

- collection：代表要遍历的集合元素，注意编写时不要写#{}
- open：代表语句的开始部分
- close：代表结束部分
- item：代表遍历集合的每个元素，生成的变量名
- sperator：代表分隔符

**SQL片段抽取**

Sql中可将重复的sql提取出来，使用时用include 引用即可，最终达到sql重用的目的

```XML
<mapper namespace="com.itahu.mapper.UserMapper">
    <!--sql语句抽取-->
    <sql id="selectUser">select * from user</sql>
    <select id="findByCondition" parameterType="user" resultType="user">
        <include refid="selectUser"></include>
        <where>
            <if test="id!=0">
                and id=#{id}
            </if>
            <if test="username!=null">
                and username=#{username}
            </if>
            <if test="password!=null">
                and password=#{password}
            </if>
        </where>
    </select>

    <select id="findByIds" parameterType="list" resultType="user">
        <include refid="selectUser"></include>
        <where>
            <foreach collection="list" open="id in(" close=")" item="id" separator=",">
                #{id}
            </foreach>
        </where>
    </select>
</mapper>
```

### 6.8 MyBatis核心配置文件深入

**typeHandlers标签**

无论是MyBatis在预处理语句（PreparedStatement）中设置一个参数时，还是从结果集中取出一个值时，都会用类型处理器将获取的值以合适的方式转换成Java 类型。下表描述了一些默认的类型处理器（截取部分）。

|     类型处理器     |         Java类型          |              JDBC类型              |
| :----------------: | :-----------------------: | :--------------------------------: |
| BooleanTypeHandler | java.lang.Boolean,boolean |        数据库兼容的BOOLEAN         |
|  ByteTypeHandler   |    java.lang.Byte,byte    |     数据库兼容的NUMERIC或BYTE      |
|  ShortTypeHandler  |   java.lang.Short,short   | 数据库兼容的NUMERIC或SHORT INTEGER |
| IntegerTypeHandler |   java.lang.Integer,int   |    数据库兼容的NUMERIC或INTEGER    |
|  LongTypeHandler   |    java.lang.Long,long    | 数据库兼容的NUMERIC或LONG INTEGER  |

你可以重写类型处理器或创建你自己的类型处理器来处理不支持的或非标准的类型。具体做法为：实现org.apache.ibatis.type.TypeHandler接口，或继承一个很便利的类org.apache.ibatis.type.BaseTypeHandler，然后可以选择性地将它映射到一个JDBC类型。例如需求：一个Java中的Date数据类型，我想将之存到数据库的时候存成一个1970年至今的毫秒数，取出来时转换成java的Date，即java的Date与数据库的varchar毫秒值之间转换。

开发步骤

1. 定义转换类继承类BaseTypeHandler\<T>
2. 覆盖4个未实现的方法，其中setNonNullParameter为java程序设置数据到数据库的回调方法，getNullableResult为查询时mysql的字符串类型转换成java的Type类型的方法
3. 在MyBatis核心配置文件中进行注册
4. 测试转换是否正确

```Java
public class DateTypeHandler extends BaseTypeHandler<Date> {
    //将Java类型转换成数据库需要的类型
    @Override
    public void setNonNullParameter(PreparedStatement preparedStatement, int i, Date date, JdbcType jdbcType) throws SQLException {
        long time = date.getTime();
        preparedStatement.setLong(i,time);
    }

    //将数据库中类型转换成Java类型
    //String参数：要转换的字段名称
    //ResultSet：查询出的结果集
    @Override
    public Date getNullableResult(ResultSet resultSet, String s) throws SQLException {
        //获得结果集中需要的数据(long)转换成Date类型返回
        long aLong = resultSet.getLong(s);
        Date date = new Date(aLong);
        return date;
    }

    //将数据库中类型转换成Java类型
    @Override
    public Date getNullableResult(ResultSet resultSet, int i) throws SQLException {
        long aLong = resultSet.getLong(i);
        Date date = new Date(aLong);
        return date;
    }

    //将数据库中类型转换成Java类型
    @Override
    public Date getNullableResult(CallableStatement callableStatement, int i) throws SQLException {
        long aLong = callableStatement.getLong(i);
        Date date = new Date(aLong);
        return date;
    }
}
```

```XML
<!--注册类型处理器-->
<typeHandlers>
    <typeHandler handler="com.itahu.handler.DateTypeHandler"></typeHandler>
</typeHandlers>
```

```Java
public class MyBatisTest {
    @Test
    public void test1() throws IOException {
        InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
        SqlSession sqlSession = sqlSessionFactory.openSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        //创建user
        User user = new User();
        user.setUsername("ceshi");
        user.setPassword("abc");
        user.setBirthday(new Date());
        //执行保存操作
        mapper.save(user);
        sqlSession.commit();
        sqlSession.close();
    }

    @Test
    public void test2() throws IOException {
        InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
        SqlSession sqlSession = sqlSessionFactory.openSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = mapper.findById(6);
        System.out.println(user);
    }
}
```

**plugins标签**

MyBatis可以使用第三方的插件来对功能进行扩展，分页助手PageHelper是将分页的复杂操作进行封装，使用简单的方式即可获得分页的相关数据。

开发步骤

1. 导入通用PageHelper的坐标
2. 在mybatis核心配置文件中配置PageHelper插件
3. 测试分页数据获取

```XML
<dependency>
  <groupId>com.github.pagehelper</groupId>
  <artifactId>pagehelper</artifactId>
  <version>3.7.5</version>
</dependency>
<dependency>
  <groupId>com.github.jsqlparser</groupId>
  <artifactId>jsqlparser</artifactId>
  <version>0.9.1</version>
</dependency>
```

```XML
<!--配置分页助手插件-->
<plugins>
    <plugin interceptor="com.github.pagehelper.PageHelper">
        <!--指定方言-->
        <property name="dialect" value="mysql"/>
    </plugin>
</plugins>
```

```Java
@Test
public void test3() throws IOException {
    InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
    SqlSession sqlSession = sqlSessionFactory.openSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);

    //设置分页相关参数 当前页 每页显示的条数
    PageHelper.startPage(2,3);

    List<User> userList = mapper.findAll();
    for (User user : userList) {
        System.out.println(user);
    }

    //获得与分页相关参数
    PageInfo<User> pageInfo = new PageInfo<User>(userList);
    System.out.println("当前页：" + pageInfo.getPageNum());
    System.out.println("每页显示条数：" + pageInfo.getPageSize());
    System.out.println("总条数：" + pageInfo.getTotal());
    System.out.println("总页数：" + pageInfo.getPages());
    System.out.println("上一页：" + pageInfo.getPrePage());
    System.out.println("下一页：" + pageInfo.getNextPage());
    System.out.println("是否是第一页：" + pageInfo.isIsFirstPage());
    System.out.println("是否是最后一页：" + pageInfo.isIsLastPage());

    sqlSession.close();
}
```

### 6.9 MyBatis的多表操作

**Mybatis多表查询**

**一对一查询**

一对一查询的模型

用户表和订单表的关系为，一个用户有多个订单，一个订单只从属于一个用户。

一对一查询的需求：查询一个订单，与此同时查询出该订单所属的用户。

一对一查询的语句

对应的sql语句：select *,o.id oid from orders o,user u where o.uid=u.id;

创建Order和User实体

创建OrderMapper接口

```Java
public interface OrderMapper {
    public List<Order> findAll();
}
```

配置OrderMapper.xml

```XML
<mapper namespace="com.itahu.mapper.OrderMapper">
    <resultMap id="orderMap" type="order">
        <!--手动指定字段与实体属性的映射关系
            column：数据表的字段名称
            property：实体的属性名称
        -->
        <id column="oid" property="id"></id>
        <result column="ordertime" property="ordertime"></result>
        <result column="total" property="total"></result>
        <result column="uid" property="user.id"></result>
        <result column="username" property="user.username"></result>
        <result column="password" property="user.password"></result>
        <result column="birthday" property="user.birthday"></result>
    </resultMap>
    <select id="findAll" resultMap="orderMap">
        SELECT *,o.`id` oid FROM orders o,USER u WHERE o.`uid`=u.`id`
    </select>
</mapper>
```

另一种配置方式

```XML
<mapper namespace="com.itahu.mapper.OrderMapper">
    <resultMap id="orderMap" type="order">
        <!--手动指定字段与实体属性的映射关系
            column：数据表的字段名称
            property：实体的属性名称
        -->
        <id column="oid" property="id"></id>
        <result column="ordertime" property="ordertime"></result>
        <result column="total" property="total"></result>
        <!--
            property：当前实体(order)中的属性名称(private User user)
            javaType：当前实体(order)中的属性的类型(User)
        -->
        <association property="user" javaType="user">
            <id column="uid" property="id"></id>
            <id column="username" property="username"></id>
            <id column="password" property="password"></id>
            <id column="birthday" property="birthday"></id>
        </association>
    </resultMap>
    <select id="findAll" resultMap="orderMap">
        SELECT *,o.`id` oid FROM orders o,USER u WHERE o.`uid`=u.`id`
    </select>
</mapper>
```

**一对多查询**

一对多查询的模型

用户表和订单表的关系为，一个用户有多个订单，一个订单只从属于一个用户。

一对多查询的需求：查询一个用户，与此同时查询出该用户具有的订单。

一对多查询的语句

对应的sql语句：select *,o.id oid from user u,orders o where u.id=o.uid;

修改User实体

创建UserMapper接口

```Java
public interface UserMapper {
    public List<User> findAll();
}
```

配置UserMapper.xml

```XML
<mapper namespace="com.itahu.mapper.UserMapper">
    <resultMap id="userMap" type="user">
        <id column="uid" property="id"></id>
        <result column="username" property="username"></result>
        <result column="password" property="password"></result>
        <result column="birthday" property="birthday"></result>
        <!--配置集合信息
            property：集合名称
            ofType：当前集合中的数据类型
        -->
        <collection property="orderList" ofType="order">
            <!--封装order的数据-->
            <id column="oid" property="id"></id>
            <result column="ordertime" property="ordertime"></result>
            <result column="total" property="total"></result>
        </collection>
    </resultMap>
    <select id="findAll" resultMap="userMap">
        SELECT *,o.`id` oid FROM USER u,orders o WHERE u.`id`=o.`uid`
    </select>
</mapper>
```

**多对多查询**

多对多查询的模型

用户表和角色表的关系为，一个用户有多个角色，一个角色被多个用户使用。

多对多查询的需求：查询用户同时查询出该用户的所有角色。

多对多查询的语句

对应的sql语句：select * from user u,sys_user_role ur,sys_role r where u.id=ur.userId and ur.roleId=r.id;

创建Role实体，修改User实体

添加UserMapper接口方法

```Java
public List<User> findUserAndRoleAll();
```

配置UserMapper.xml

```XML
<resultMap id="userRoleMap" type="user">
    <!--user的信息-->
    <id column="id" property="id"></id>
    <result column="username" property="username"></result>
    <result column="password" property="password"></result>
    <result column="birthday" property="birthday"></result>
    <!--user内部的roleList信息-->
    <collection property="roleList" ofType="role">
        <id column="roleId" property="id"></id>
        <result column="roleName" property="roleName"></result>
        <result column="roleDesc" property="roleDesc"></result>
    </collection>
</resultMap>
<select id="findUserAndRoleAll" resultMap="userRoleMap">
    SELECT * FROM USER u,sys_user_role ur,sys_role r WHERE u.`id`=ur.`userId` AND ur.`roleId`=r.`id`
</select>
```

**知识小结**

MyBatis多表配置方式

- 一对一配置：使用\<resultMap>做配置
- 一对多配置：使用\<resultMap>+\<collection>做配置
- 多对多配置：使用\<resultMap>+\<collection>做配置

### 6.10 Mybatis的注解开发

**MyBatis的常用注解**

这几年来注解开发越来越流行，Mybatis也可以使用注解开发方式，这样我们就可以减少编写Mapper映射文件了。我们先围绕一些基本的CRUD来学习，再学习复杂映射多表操作。

- @Insert：实现新增
- @Update：实现更新
- @Delete：实现删除
- @Select：实现查询
- @Result：实现结果集封装
- @Results：可以与@Result 一起使用，封装多个结果集
- @One：实现一对一结果集封装
- @Many：实现一对多结果集封装

**MyBatis的增删改查**

修改MyBatis的核心配置文件，我们使用了注解替代的映射文件，所以我们只需要加载使用了注解的Mapper接口即可

```XML
<!--加载映射关系-->
<mappers>
    <!--扫描使用注解的类-->
    <mapper class="com.itheima.mapper.UserMapper"></mapper>
</mappers>
```

或者指定扫描包含映射关系的接口所在的包也可以

```XML
<!--加载映射关系-->
<mappers>
    <!--指定接口所在的包-->
    <package name="com.itheima.mapper"></package>
</mappers>
```

**MyBatis的注解实现复杂映射开发**

实现复杂关系映射之前我们可以在映射文件中通过配置\<resultMap>来实现，使用注解开发后，我们可以使用@Results注解，@Result注解，@One注解，@Many注解组合完成复杂关系的配置。

|      注解       |                             说明                             |
| :-------------: | :----------------------------------------------------------: |
|    @Results     | 代替的是标签\<resultMap>该注解中可以使用单个@Result注解，也可以使用@Result集合。使用格式：@Results({@Result(), @Result()})或@Results(@Result()) |
|     @Resut      | 代替了\<id>标签和\<result>标签<br/>@Result中属性介绍：<br/>column：数据库的列名<br/>property：需要装配的属性名<br/>one：需要使用的@One 注解(@Result(one=@One)()))<br/>many：需要使用的@Many 注解(@Result(many=@many)())) |
| @One（一对一）  | 代替了\<assocation> 标签，是多表查询的关键，在注解中用来指定子查询返回单一对象。<br/>@One注解属性介绍：<br/>select: 指定用来多表查询的sqlmapper<br/>使用格式：@Result(column="", property="", one=@One(select="")) |
| @Many（多对一） | 代替了\<collection>标签, 是是多表查询的关键，在注解中用来指定子查询返回对象集合。<br/>使用格式：@Result(property="", column="", many=@Many(select="")) |

**一对一查询**

一对一查询的模型

用户表和订单表的关系为，一个用户有多个订单，一个订单只从属于一个用户。

一对一查询的需求：查询一个订单，与此同时查询出该订单所属的用户。

一对一查询的语句

对应的sql语句：

select * from orders;

select * from user where id=查询出订单的uid;

创建Order和User实体

创建OrderMapper接口

使用注解配置Mapper

```Java
@Select("select * from orders")
@Results({
        @Result(column = "id",property = "id"),
        @Result(column = "ordertime",property = "ordertime"),
        @Result(column = "total",property = "total"),
        @Result(
                property = "user", //要封装的属性名称
                column = "uid", //根据那个字段去查询user表的数据
                javaType = User.class, //要封装的实体类型
                //select属性 代表查询那个接口的方法获得数据
                one = @One(select = "com.itheima.mapper.UserMapper.findById")
        )
})
public List<Order> findAll();
```

```Java
@Select("select * from user where id=#{id}")
public User findById(int id);
```

```Java
@Select("select *,o.id oid from orders o,user u where o.uid=u.id")
@Results({
        @Result(column = "oid",property = "id"),
        @Result(column = "ordertime",property = "ordertime"),
        @Result(column = "total",property = "total"),
        @Result(column = "uid",property = "user.id"),
        @Result(column = "username",property = "user.username"),
        @Result(column = "password",property = "user.password")
})
public List<Order> findAll();
```

**一对多查询**

一对多查询的模型

用户表和订单表的关系为，一个用户有多个订单，一个订单只从属于一个用户。

一对多查询的需求：查询一个用户，与此同时查询出该用户具有的订单。

一对多查询的语句

对应的sql语句：

select * from user;

select * from orders where uid=查询出用户的id;

修改User实体

创建UserMapper接口

使用注解配置Mapper

```Java
@Select("select * from user")
@Results({
        @Result(id=true,column = "id",property = "id"),
        @Result(column = "username",property = "username"),
        @Result(column = "password",property = "password"),
        @Result(
                property = "orderList",
                column = "id",
                javaType = List.class,
                many = @Many(select = "com.itheima.mapper.OrderMapper.findByUid")
        )
})
public List<User> findUserAndOrderAll();
```

```Java
@Select("select * from orders where uid=#{uid}")
public List<Order> findByUid(int uid);
```

**多对多查询**

多对多查询的模型

用户表和角色表的关系为，一个用户有多个角色，一个角色被多个用户使用。

多对多查询的需求：查询用户同时查询出该用户的所有角色。

多对多查询的语句

对应的sql语句：

select * from user;

select * from role r,user_role ur where r.id=ur.role_id and ur.user_id=用户的id;

创建Role实体，修改User实体

添加UserMapper接口方法

使用注解配置Mapper

```Java
@Select("SELECT * FROM USER")
@Results({
        @Result(id = true,column = "id",property = "id"),
        @Result(column = "username",property = "username"),
        @Result(column = "password",property = "password"),
        @Result(
                property = "roleList",
                column = "id",
                javaType = List.class,
                many = @Many(select = "com.itheima.mapper.RoleMapper.findByUid")
        )
})
public List<User> findUserAndRoleAll();
```

```Java
@Select("SELECT * FROM sys_user_role ur,sys_role r WHERE ur.roleId=r.id AND ur.userId=#{uid}")
public List<Role> findByUid(int uid);
```

## 7. SSM框架整合

### 7.1 原始方式整合

1.准备工作

```SQL
create database ssm;
create table account(
    id int primary key auto_increment,
    name varchar(100),
    money double(7,2)
);
```

2.创建Maven工程

3.导入Maven坐标

```XML
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.itahu</groupId>
  <artifactId>itahu_ssm</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <name>itahu_ssm Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>
  </properties>

  <dependencies>
    <!--spring相关-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.0.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjweaver</artifactId>
      <version>1.8.7</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.0.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>5.0.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>5.0.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.0.5.RELEASE</version>
    </dependency>

    <!--servlet和jsp-->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>servlet-api</artifactId>
      <version>2.5</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.0</version>
    </dependency>

    <!--mybatis相关-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.4.5</version>
    </dependency>
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>1.3.1</version>
    </dependency>
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.6</version>
    </dependency>
    <dependency>
      <groupId>c3p0</groupId>
      <artifactId>c3p0</artifactId>
      <version>0.9.1.2</version>
    </dependency>

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
    </dependency>
    <dependency>
      <groupId>jstl</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>

  </dependencies>

  <build>
    <finalName>itahu_ssm</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>
```

4.编写实体类

```Java
package com.itahu.domain;

public class Account {
    private Integer id;
    private String name;
    private Double money;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Double getMoney() {
        return money;
    }

    public void setMoney(Double money) {
        this.money = money;
    }
}
```

5.编写Mapper接口

```Java
package com.itahu.mapper;

import com.itahu.domain.Account;
import java.util.List;

public interface AccountMapper {
    public void save(Account account);

    public List<Account> findAll();
}
```

6.编写Service接口

```Java
package com.itahu.service;

import com.itahu.domain.Account;
import java.util.List;

public interface AccountService {
    public void save(Account account);
    
    public List<Account> findAll();
}
```

7.编写Service接口实现

```Java
package com.itahu.service.impl;

import com.itahu.domain.Account;
import com.itahu.mapper.AccountMapper;
import com.itahu.service.AccountService;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.springframework.stereotype.Service;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

@Service("accountService")
public class AccountServiceImpl implements AccountService {

    @Override
    public void save(Account account) {
        try {
            InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
            SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
            SqlSession sqlSession = sqlSessionFactory.openSession();
            AccountMapper mapper = sqlSession.getMapper(AccountMapper.class);
            mapper.save(account);
            sqlSession.commit();
            sqlSession.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @Override
    public List<Account> findAll() {
        try {
            InputStream resourceAsStream = Resources.getResourceAsStream("sqlMapConfig.xml");
            SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(resourceAsStream);
            SqlSession sqlSession = sqlSessionFactory.openSession();
            AccountMapper mapper = sqlSession.getMapper(AccountMapper.class);
            List<Account> accountList = mapper.findAll();
            sqlSession.close();
            return accountList;
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

8.编写Controller

```Java
package com.itahu.controller;

import com.itahu.domain.Account;
import com.itahu.service.AccountService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.servlet.ModelAndView;

import java.util.List;

@Controller
@RequestMapping("/account")
public class AccountController {

    @Autowired
    private AccountService accountService;

    //保存
    @RequestMapping(value = "/save",produces = "text/html;charset=UTF-8")
    @ResponseBody
    public String save(Account account) {
        accountService.save(account);
        return "保存成功";
    }

    //查询
    @RequestMapping("findAll")
    public ModelAndView findAll() {
        List<Account> accountList = accountService.findAll();
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.addObject("accountList",accountList);
        modelAndView.setViewName("accountList");
        return modelAndView;
    }
}
```

9.编写添加页面

```JSP
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h1>添加账户信息表单</h1>
    <form name="accountForm" action="${pageContext.request.contextPath}/account/save" method="post">
        账户名称：<input type="text" name="name"><br>
        账户金额：<input type="text" name="money"><br>
        <input type="submit" value="保存"><br>
    </form>
</body>
</html>
```

10.编写列表页面

```JSP
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h1>展示账户数据列表</h1>
    <table border="1">
        <tr>
            <th>账户id</th>
            <th>账户名称</th>
            <th>账户金额</th>
        </tr>
        <c:forEach items="${accountList}" var="account">
            <tr>
                <td>${account.id}</td>
                <td>${account.name}</td>
                <td>${account.money}</td>
            </tr>
        </c:forEach>
    </table>
</body>
</html>
```

11.编写相应配置文件

- Spring配置文件：applicationContext.xml
- SprngMVC配置文件：spring-mvc.xml
- MyBatis映射文件：AccountMapper.xml
- MyBatis核心文件：sqlMapConfig.xml
- 数据库连接信息文件：jdbc.properties
- Web.xml文件：web.xml
- 日志文件：log4j.xml

jdbc.properties

```Properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/ssm
jdbc.username=root
jdbc.password=root
```

log4j.xml

```XML
#
# Hibernate, Relational Persistence for Idiomatic Java
#
# License: GNU Lesser General Public License (LGPL), version 2.1 or later.
# See the lgpl.txt file in the root directory or <http://www.gnu.org/licenses/lgpl-2.1.html>.
#

### direct log messages to stdout ###
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target=System.err
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n

### direct messages to file hibernate.log ###
#log4j.appender.file=org.apache.log4j.FileAppender
#log4j.appender.file.File=hibernate.log
#log4j.appender.file.layout=org.apache.log4j.PatternLayout
#log4j.appender.file.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n

### set log levels - for more verbose logging change 'info' to 'debug' ###

log4j.rootLogger=all, stdout
```

AccountMapper.xml

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itahu.mapper.AccountMapper">
    <insert id="save" parameterType="account">
        insert into account values (#{id},#{name},#{money})
    </insert>
    <select id="findAll" resultType="account">
        select * from account
    </select>
</mapper>
```

sqlMapConfig.xml

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--加载properties文件-->
    <properties resource="jdbc.properties"></properties>

    <!--定义别名-->
    <typeAliases>
        <!--<typeAlias type="com.itahu.domain.Account" alias="account"></typeAlias>-->
        <package name="com.itahu.domain"/>
    </typeAliases>

    <!--环境-->
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc.driver}"/>
                <property name="url" value="${jdbc.url}"/>
                <property name="username" value="${jdbc.username}"/>
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>

    <!--加载映射-->
    <mappers>
        <!--<mapper resource="com/itahu/mapper/AccountMapper.xml"></mapper>-->
        <package name="com.itahu.mapper"/>
    </mappers>
</configuration>
```

applicationContext.xml

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/tx
http://www.springframework.org/schema/tx/spring-tx.xsd
http://www.springframework.org/schema/aop
http://www.springframework.org/schema/aop/spring-aop.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd">

    <!--组件扫描 扫描service和mapper-->
    <context:component-scan base-package="com.itahu">
        <!--排除controller的扫描-->
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>

</beans>
```

spring-mvc.xml

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/mvc
http://www.springframework.org/schema/mvc/spring-mvc.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd">

    <!--组件扫描 主要扫描controller-->
    <context:component-scan base-package="com.itahu.controller"></context:component-scan>
    <!--配置mvc注解驱动-->
    <mvc:annotation-driven></mvc:annotation-driven>
    <!--内部资源视图解析器-->
    <bean id="resourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/pages/"></property>
        <property name="suffix" value=".jsp"></property>
    </bean>
    <!--开放静态资源访问权限-->
    <mvc:default-servlet-handler></mvc:default-servlet-handler>
</beans>
```

web.xml

```XML
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" id="WebApp_ID" version="2.5">

  <!--spring监听器-->
  <context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:applicationContext.xml</param-value>
  </context-param>
  <listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>

  <!--springmvc的前端控制器-->
  <servlet>
    <servlet-name>DispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:spring-mvc.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>DispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>

  <!--乱码过滤器-->
  <filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>

</web-app>
```

### 7.2 Spring整合MyBatis

**整合思路**

将Session工厂交给Spring容器管理，从容器中获得执行操作的Mapper实例即可。

将事务的控制交给Spring容器进行声明式事务控制。

**将SqlSessionFactory配置到Spring容器中**

**扫描Mapper，让Spring容器产生Mapper实现类**

**配置声明式事务控制**

**修改Service实现类代码**

修改后的applicationContext.xml文件

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/tx
http://www.springframework.org/schema/tx/spring-tx.xsd
http://www.springframework.org/schema/aop
http://www.springframework.org/schema/aop/spring-aop.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd">

    <!--组件扫描 扫描service和mapper-->
    <context:component-scan base-package="com.itahu">
        <!--排除controller的扫描-->
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>

    <!--加载properties文件-->
    <context:property-placeholder location="classpath:jdbc.properties"></context:property-placeholder>

    <!--配置数据源信息-->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="${jdbc.driver}"></property>
        <property name="jdbcUrl" value="${jdbc.url}"></property>
        <property name="user" value="${jdbc.username}"></property>
        <property name="password" value="${jdbc.password}"></property>
    </bean>

    <!--配置sessionFactory-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"></property>
        <!--加载MyBatis的核心文件-->
        <property name="configLocation" value="classpath:sqlMapConfig-spring.xml"></property>
    </bean>

    <!--扫描mapper所在的包，为mapper创建实现类-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.itahu.mapper"></property>
    </bean>

    <!--声明式事务控制-->
    <!--平台事务管理器-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>

    <!--配置事务增强-->
    <tx:advice id="txAdvice">
        <tx:attributes>
            <tx:method name="*"/>
        </tx:attributes>
    </tx:advice>

    <!--事务的aop织入-->
    <aop:config>
        <aop:advisor advice-ref="txAdvice" pointcut="execution(* com.itahu.service.impl.*.*(..))"></aop:advisor>
    </aop:config>

</beans>
```

修改后的sqlMapConfig.xml

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--定义别名-->
    <typeAliases>
        <!--<typeAlias type="com.itahu.domain.Account" alias="account"></typeAlias>-->
        <package name="com.itahu.domain"/>
    </typeAliases>

</configuration>
```

修改后的Service实现类代码

```Java
package com.itahu.service.impl;

import com.itahu.domain.Account;
import com.itahu.mapper.AccountMapper;
import com.itahu.service.AccountService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service("accountService")
public class AccountServiceImpl implements AccountService {

    @Autowired
    private AccountMapper accountMapper;

    @Override
    public void save(Account account) {
        accountMapper.save(account);
    }

    @Override
    public List<Account> findAll() {
        return accountMapper.findAll();
    }
}
```
