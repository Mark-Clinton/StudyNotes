<center>
    <h1>
        SpringBoot基础
    </h1>
</center>

## 1. SpringBoot基础篇

### 1.1 快速上手SpringBoot

**IDEA联网创建**

1.开发SpringBoot程序可以根据向导进行联网快速制作

2.SpringBoot程序需要基于JDK8进行制作

3.SpringBoot程序中需要使用何种功能通过勾选选择技术

4.运行SpringBoot程序通过运行Application程序入口进行快速上手SpringBoot

**SpringBoot官网创建**

1.打开SpringBoot官网，选择QuickstartYour Project

2.创建工程，并保存项目

3.解压项目，通过IDE导入项目

**阿里云网站创建**

1.选择start来源为自定义URL

2.输入阿里云start地址

3.创建项目

**手工制作版**

手工创建项目(手工导入坐标)

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.6.4</version>
    </parent>

    <groupId>com.itheima</groupId>
    <artifactId>springboot_01_04_quickstart</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

</project>
```

```Java
package com.itheima;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class);
    }
}
```

1.创建普通Maven工程

2.继承spring-boot-starter-parent

3.添加依赖spring-boot-starter-web

4.制作引导类Application

**Idea中隐藏指定文件或指定类型文件**

- Setting --> File Types --> Ignored Files and Folders
- 输入要隐藏的文件名，支持*号通配符
- 回车确认添加

**SpringBoot简介**

SpringBoot是由Pivotal团队提供的全新框架，其设计目的是用来简化Spring应用的初始搭建以及开发过程

- Spring程序缺点
  - 依赖设置繁琐
  - 配置繁琐
- SpringBoot程序优点
  - 起步依赖（简化依赖配置）
  - 自动配置（简化常用工程相关配置）
  - 辅助功能（内置服务器，……）

**入门案例解析**

**parent**

1. 开发SpringBoot程序要继承spring-boot-starter-parent
2. spring-boot-starter-parent中定义了若干个依赖管理
3. 继承parent模块可以避免多个依赖使用相同技术时出现依赖版本冲突
4. 继承parent的形式也可以采用引入依赖的形式实现效果

**注意**

starter

- SpringBoot中常见项目名称，定义了当前项目使用的所有依赖坐标，以达到减少依赖配置的目的

parent

- 所有SpringBoot项目要继承的项目，定义了若干个坐标版本号（依赖管理，而非依赖），以达到减少依赖冲突的目的
- spring-boot-starter-parent各版本间存在着诸多坐标版本不同

实际开发

- 使用任意坐标时，仅书写GAV中的G和A，V由SpringBoot提供，除非SpringBoot未提供对应版本V
- 如发生坐标错误，再指定Version（要小心版本冲突）

**starter**

1. 开发SpringBoot程序需要导入坐标时通常导入对应的starter
2. 每个不同的starter根据功能不同，通常包含多个依赖坐标
3. 使用starter可以实现快速配置的效果，达到简化配置的目的

**引导类**

启动方式

```Java
@SpringBootApplication
public class Springboot0101QuickstartApplication {

    public static void main(String[] args) {
        SpringApplication.run(Springboot0101QuickstartApplication.class, args);
    }

}
```

SpringBoot的引导类是Boot工程的执行入口，运行main方法就可以启动项目

SpringBoot工程运行后初始化Spring容器，扫描引导类所在包加载bean

总结

1. SpringBoot工程提供引导类用来启动程序
2. SpringBoot工程启动后创建并初始化Spring容器

**内嵌tomcat**

使用maven依赖管理变更起步依赖项

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
```

Jetty比Tomcat更轻量级，可扩展性更强（相较于Tomcat），谷歌应用引擎（GAE）已经全面切换为Jetty

内置服务器

- tomcat(默认)：apache出品，粉丝多，应用面广，负载了若干较重的组件
- jetty：更轻量级，负载性能远不及tomcat
- undertow：undertow，负载性能勉强跑赢tomcat

总结

1. 内嵌Tomcat服务器是SpringBoot辅助功能之一
2. 内嵌Tomcat工作原理是将Tomcat服务器作为对象运行，并将该对象交给Spring容器管理
3. 变更内嵌服务器思想是去除现有服务器，添加全新的服务器

**REST风格**

**REST简介**

REST(Representational State Transfer)，表现形式状态转换

- 传统风格资源描述形式
  - http://localhost/user/getById?id=1
  - http://localhost/user/saveUser
- REST风格描述形式
  - http://localhost/user/1
  - http://localhost/user

优点

- 隐藏资源的访问行为，无法通过地址得知对资源是何种操作
- 书写简化

按照REST风格访问资源时使用行为动作区分对资源进行了何种操作

- http://localhost/users		查询全部用户信息    GET(查询)
- http://localhost/users/1	查询指定用户信息    GET(查询)
- http://localhost/users        添加用户信息           POST(新增/保存)
- http://localhost/users        修改用户信息           PUT(修改/更新)
- http://localhost/users/1     删除用户信息          DELETE(删除)

根据REST风格对资源进行访问称为RESTful

注意事项

- 上述行为是约定方式，约定不是规范，可以打破，所以称REST风格，而不是REST规范
- 描述模块的名称通常使用复数，也就是加s的格式描述，表示此类资源，而非单个资源，例如：users、books、accounts......

**RESTful入门案例步骤**

1. 设定http请求动作(动词)
2. 设定请求参数(路径变量)

@RequestMapping

- 类型：方法注解
- 位置：SpringMVC控制器方法定义上方
- 作用：设置当前控制器方法请求访问路径
- 属性
  - value(默认)：请求访问路径
  - method：http请求动作，标准动作(GET/POST/PUT/DELETE)

@PathVariable

- 类型：形参注解
- 位置：SpringMVC控制器方法形参定义前面
- 作用：绑定路径参数与处理器方法形参间的关系，要求路径参数名与形参名一一对应

@RequestBody、@RequestParam、@PathVariable

- 区别
  - @RequestParam用于接收url地址传参或表单传参
  - @RequestBody用于接收json数据
  - @PathVariable用于接收路径参数，使用{参数名称}描述路径参数
- 应用
  - 后期开发中，发送请求参数超过1个时，以json格式为主，@RequestBody应用较广
  - 如果发送非json格式数据，选用@RequestParam接收请求参数
  - 采用RESTful进行开发，当参数数量较少时，例如1个，可以采用@PathVariable接收请求路径变量，通常用于传递id值

**RESTful快速开发**

@RestController

- 类型：类注解
- 位置：基于SpringMVC的RESTful开发控制器类定义上方
- 作用：设置当前控制器类为RESTful风格，等同于@Controller与@ResponseBody两个注解组合功能

@GetMapping、@PostMapping、@PutMapping、@DeleteMapping

- 类型：方法注解
- 位置：基于SpringMVC的RESTful开发控制器方法定义上方
- 作用：设置当前控制器方法请求访问路径与请求动作，每种对应一个请求动作，例如@GetMapping对应GET请求
- 属性
  - value(默认)：请求访问路径

### 1.2 基础配置

**快速复制模块**

1.在工作空间中复制对应工程，并修改工程名称

2.删除与Idea相关配置文件，仅保留src目录与pom.xml文件

3.修改pom.xml文件中的artifactId与新工程/模块名相同

4.删除name标签（可选）

5.保留备份工程供后期使用

**属性配置**

修改服务器端口

- SpringBoot默认配置文件application.properties，通过键值对配置对应属性

- ```Properties
  # 服务器端口配置
  server.port=80
  ```

关闭运行日志图标(banner)

```Properties
# 修改banner
spring.main.banner-mode=off
```

设置日志相关

```Properties
# 日志
logging.level.root=info
```

SpringBoot内置属性查询

- https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#appendix.application-properties
- 官方文档中参考文档第一项：Application Properties

小结

- SpringBoot中导入对应starter后，提供对应配置属性
- 书写SpringBoot配置采用关键字+提示形式书写

**3种配置文件类型**

SpringBoot提供了多种属性配置方式

- application.properties

  ```Properties
  server.port=80
  ```

- application.yml

  ```yaml
  server:
    port: 81
  ```

- application.yaml

  ```yaml
  server:
    port: 82
  ```

小结

- SpringBoot提供了3种配置文件的格式
  - properties（传统格式/默认格式）
  - yml（主流格式）
  - yaml

**配置文件加载优先级**

SpringBoot配置文件加载顺序

- application.properties > application.yml > application.yaml

常用配置文件种类：application.yml

小结

1. 配置文件间的加载优先级
   - properties（最高）
   - yml
   - yaml（最低）
2. 不同配置文件中相同配置按照加载优先级相互覆盖，不同配置文件中不同配置全部保留

**配置文件属性提示消失解决方案**

指定SpringBoot配置文件

- Setting --> Project Structure --> Facets
- 选中对应项目/工程
- Customize Spring Boot
- 选择配置文件

**YAML数据格式**

YAML(YAML Ain't Markup Language)，一种数据序列化格式。

优点

- 容易阅读
- 容易与脚本语言交互
- 以数据为核心，重数据轻格式

YAML文件扩展名

- .yml（主流）
- .yaml

YAML语法规则

- 大小写敏感
- 属性层级关系使用多行描述，每行结尾使用冒号结束
- 使用缩进表示层级关系，同层级左侧对齐，只允许使用空格（不允许使用Tab键）
- 属性值前面添加空格（属性名与属性值之间使用冒号+空格作为分隔）
- \# 表示注释
- 核心规则：==数据前面要加空格与冒号隔开==
- 数组表示方式：在属性名书写位置的下方使用减号作为数据开始符号，每行书写一个数据，减号与数据间空格分隔

**YAML数据读取**

使用@Value读取单个数据，属性名引用方式：${一级属性名.二级属性名……}

小结

- 使用@Value配合SpEL读取单个数据
- 如果数据存在多层级，依次书写层级名称即可

在配置文件中可以使用属性名引用方式引用属性

```yaml
baseDir: /usr/local/fire

center:
  dataDir: ${baseDir}/data
  tmpDir: ${baseDir}/tmp
  logDir: ${baseDir}/log
  msgDir: ${baseDir}/msgDir
```

属性值中如果出现转移字符，需要使用双引号包裹

```yaml
lesson: "Spring\tboot\nlesson"
```

小结

- 在配置文件中可以使用${属性名}方式引用属性值
- 如果属性中出现特殊字符，可以使用双引号包裹起来作为字符解析

可以使用Environment对象封装全部配置信息，使用@Autowired自动装配数据到Environment对象中。

```Java
//使用自动装配将所有的数据封装到一个对象
@Autowired
private Environment env;

@GetMapping
public String getById() {
    System.out.println("springboot is running...");
    System.out.println("country1 ==> " + country1);
    System.out.println("name1 ==> " + name1);
    System.out.println("====================");
    System.out.println(env.getProperty("server.port"));
    System.out.println(env.getProperty("user2.name"));
    return "springboot is running...";
}
```

自定义对象封装指定数据

```yaml
datasource:
  driver-class-name: com.mysql.cj.jdbc.Driver
  url: jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC
  username: root
  password: root
```

```Java
@Component
@ConfigurationProperties(prefix = "datasource")
public class DataSource {
    private String driverClassName;
    private String url;
    private String userName;
    private String password;
}
```

### 1.3 整合第三方技术

**整合JUnit**

SpringBoot整合JUnit

- 名称：@SpringBootTest
- 类型：测试类注解
- 位置：测试类定义上方
- 作用：设置JUnit加载的SpringBoot启动类
- 相关属性
  - classes：设置SpringBoot启动类

```Java
@SpringBootTest
class Springboot04JunitApplicationTests {
    //1.注入你要测试的对象
    @Autowired
    private BookDao bookDao;

    @Test
    void contextLoads() {
        //2.执行要测试的对象对应的方法
        bookDao.save();
    }

}
```

小结

1. 导入测试对应的starter
2. 测试类使用@SpringBootTest修饰
3. 使用自动装配的形式添加要测试的对象

注意

1. 测试类如果存在于引导类所在包或子包中无需指定引导类
2. 测试类如果不存在于引导类所在的包或子包中需要通过classes属性指定引导类

**整合MyBatis**

核心配置：数据库连接相关信息（连什么？连谁？什么权限）

映射配置：SQL映射（XML/注解）

整合步骤

1. 创建新模块，选择Spring初始化，并配置模块相关基础信息
2. 选择当前模块需要使用的技术集（MyBatis、MySQL）
3. 设置数据源参数

```yaml
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/test
    username: root
    password: root
```

4. 定义数据层接口与映射配置

```Java
@Mapper
public interface UserDao {
    @Select("select * from sys_user where id = #{id}")
    public User getById(Integer id);
}
```

5. 测试类中注入dao接口，测试功能

```Java
@SpringBootTest
class Springboot05MybatisApplicationTests {
    @Autowired
    private UserDao userDao;

    @Test
    void contextLoads() {
        System.out.println(userDao.getById(1));
    }

}
```

注意：SpringBoot版本低于2.4.3(不含)，Mysql驱动版本大于8.0时，需要在url连接串中配置时区。（或在MySQL数据库端配置时区解决此问题）

```yaml
jdbc:mysql://localhost:3306/test?serverTimezone=UTC
```

小结

- 勾选MyBatis技术，也就是导入MyBatis对应的starter
- 数据库连接相关信息转换成配置
- 数据库SQL映射需要添加@Mapper被容器识别到
- MySQL 8.X驱动强制要求设置时区
  - 修改url，添加serverTimezone设定
  - 修改MySQL数据库配置（略）
- 驱动类过时，提醒更换为com.mysql.cj.jdbc.Driver

**整合MyBatis-Plus**

MyBatis-Plus与MyBatis区别

- 导入坐标不同
- 数据层实现简化

整合步骤

1. 手动添加SpringBoot整合MyBatis-Plus的坐标，可以通过mvnrepository获取。（由于SpringBoot中未收录MyBatis-Plus的坐标版本，需要指定对应的Version）

```XML
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.4.3</version>
</dependency>
```

2. 定义数据层接口与映射配置，继承BaseMapper

```Java
@Mapper
public interface UserDao extends BaseMapper<User> {
}
```

3. 其他同SpringBoot整合MyBatis

小结

- 手工添加MyBatis-Plus对应的starter
- 数据层接口使用BaseMapper简化开发
- 需要使用的第三方技术无法通过勾选确定时，需要手工添加坐标

**整合Druid**

指定数据源类型

```yaml
#spring:
#  datasource:
#    driver-class-name: com.mysql.cj.jdbc.Driver
#    url: jdbc:mysql://localhost:3306/test
#    username: root
#    password: root
#    type: com.alibaba.druid.pool.DruidDataSource

# 变更Druid的配置方式
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/test
      username: root
      password: root
```

导入Druid对应的starter

```XML
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.2.6</version>
</dependency>
```

==整合任意第三方技术==

- 导入对应的starter
- 配置对应的设置或采用默认配置

小结

- 整合Druid需要导入Druid对应的starter
- 根据Druid提供的配置方式进行配置
- 整合第三方技术通用方式
  - 导入对应的starter
  - 根据提供的配置格式，配置非默认值对应的配置项

### 1.4 基于SpringBoot的SSMP整合案例

**SSMP整合案例**

案例实现方案分析

- 实体类开发————使用Lombok快速制作实体类
- Dao开发————整合MyBatisPlus，制作数据层测试类
- Service开发————基于MyBatisPlus进行增量开发，制作业务层测试类
- Controller开发————基于Restful开发，使用PostMan测试接口功能
- Controller开发————前后端开发协议制作
- 页面开发————基于VUE+ElementUI制作，前后端联调，页面数据处理，页面消息处理
  - 列表、新增、修改、删除、分页、查询
- 项目异常处理
- 按条件查询————页面功能调整、Controller修正功能、Service修正功能

**模块创建**

1.勾选SpringMVC与MySQL坐标

2.修改配置文件为yml格式

3.设置端口为80方便访问

**实体类开发**

Lombok，一个Java类库，提供了一组注解，简化POJO实体类开发

```XML
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
</dependency>
```

lombok版本由SpringBoot提供，无需指定版本

常用注解：@Data

```Java
//lombok
@Data
public class Book {
    private Integer id;
    private String type;
    private String name;
    private String description;
}
```

为当前实体类在编译期设置对应的get/set方法，toString方法，hashCode方法，equals方法等

**数据层开发**

技术实现方案

- MyBatisPlus
- Druid

1.导入MyBatisPlus与Druid对应的starter

```XML
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.4.3</version>
</dependency>

<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.2.6</version>
</dependency>
```

2.配置数据源与MyBatisPlus对应的基础配置（id生成策略使用数据库自增策略）

```yaml
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/test?serverTimezone=UTC
      username: root
      password: root
mybatis-plus:
  global-config:
    db-config:
      table-prefix: tbl_
      id-type: auto
```

3.继承BaseMapper并指定泛型

```Java
@Mapper
public interface BookDao extends BaseMapper<Book> {

}
```

4.制作测试类测试结果

```Java
@Test
void testSave() {
    Book book = new Book();
    book.setType("测试数据123");
    book.setName("测试数据123");
    book.setDescription("测试数据123");
    bookDao.insert(book);
}
```

为方便调试可以开启MyBatisPlus的日志

```yaml
mybatis-plus:
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
```

==分页功能==

1.分页操作需要设定分页对象IPage

```Java
@Test
void testGetPage() {
    IPage page = new Page(2,5);
    bookDao.selectPage(page, null);
    System.out.println(page.getCurrent());
    System.out.println(page.getSize());
    System.out.println(page.getTotal());
    System.out.println(page.getPages());
    System.out.println(page.getRecords());
}
```

2.IPage对象中封装了分页操作中的所有数据

- 数据
- 当前页码值
- 每页数据总量
- 最大页码值
- 数据总量

3.分页操作是在MyBatisPlus的常规操作基础上增强得到，内部是动态的拼写SQL语句，因此需要增强对应的功能，使用MyBatisPlus拦截器实现

```Java
@Configuration
public class MPConfig {
    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor() {
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        interceptor.addInnerInterceptor(new PaginationInnerInterceptor());
        return interceptor;
    }
}
```

==条件查询功能==

1.使用QueryWrapper对象封装查询条件，推荐使用LambdaQueryWrapper对象，所有查询操作封装成方法调用

```Java
@Test
void testGetBy() {
    QueryWrapper<Book> qw = new QueryWrapper<>();
    qw.like("name","Spring");
    bookDao.selectList(qw);
}

@Test
void testGetBy2() {
    String name = "1";
    LambdaQueryWrapper<Book> lqw = new LambdaQueryWrapper<>();
    lqw.like(name != null,Book::getName,name);
    bookDao.selectList(lqw);
}
```

2.支持动态拼写查询条件

```Java
@Test
void testGetByCondition(){
    String name = "Spring";
    IPage page = new Page(1,10);
    LambdaQueryWrapper<Book> lqw = new LambdaQueryWrapper<Book>();
    lqw.like(Strings.isNotEmpty(name),Book::getName,"Spring");
    bookDao.selectPage(page,lqw);
}
```

小结

- 使用QueryWrapper对象封装查询条件
- 推荐使用LambdaQueryWrapper对象
- 所有查询操作封装成方法调用
- 查询条件支持动态条件拼装

**业务层开发**

Service层接口定义与数据层接口定义具有较大区别，不要混用

- 数据层：selectByUserNameAndPassword(String username,String password);
- 业务层：login(String username,String password);

1.接口定义

```Java
public interface BookService {
    Boolean save(Book book);
    Boolean update(Book book);
    Boolean delete(Integer id);
    Book getById(Integer id);
    List<Book> getAll();
    IPage<Book> getPage(int currentPage,int pageSize);
}
```

2.实现类定义

```Java
@Service
public class BookServiceImpl implements BookService {
    @Autowired
    private BookDao bookDao;

    @Override
    public Boolean save(Book book) {
        return bookDao.insert(book) > 0;
    }

    @Override
    public Boolean update(Book book) {
        return bookDao.updateById(book) > 0;
    }

    @Override
    public Boolean delete(Integer id) {
        return bookDao.deleteById(id) > 0;
    }

    @Override
    public Book getById(Integer id) {
        return bookDao.selectById(id);
    }

    @Override
    public List<Book> getAll() {
        return bookDao.selectList(null);
    }

    @Override
    public IPage<Book> getPage(int currentPage, int pageSize) {
        IPage page = new Page(currentPage,pageSize);
        return bookDao.selectPage(page,null);
    }
}
```

3.测试类定义

==业务层快速开发==

快速开发方案

- 使用MyBatisPlus提供有业务层通用接口（ISerivce\<T>）与业务层通用实现类（ServiceImpl<M,T>）
- 在通用类基础上做功能重载或功能追加
- 注意重载时不要覆盖原始操作，避免原始提供的功能丢失

1.接口定义

```Java
public interface IBookService extends IService<Book> {
    boolean saveBook(Book book);

    boolean modify(Book book);

    boolean delete(Integer id);
}
```

2.实现类定义

```Java
@Service
public class BookServiceImpl extends ServiceImpl<BookDao, Book> implements IBookService {
    @Autowired
    private BookDao bookDao;

    @Override
    public boolean saveBook(Book book) {
        return bookDao.insert(book) > 0;
    }

    @Override
    public boolean modify(Book book) {
        return bookDao.updateById(book) > 0;
    }

    @Override
    public boolean delete(Integer id) {
        return bookDao.deleteById(id) > 0;
    }
}
```

3.实现类追加功能(前面接口与实现类中所写)

4.测试类定义

小结

- 使用通用接口（ISerivce\<T>）快速开发Service
- 使用通用实现类（ServiceImpl<M,T>）快速开发ServiceImpl
- 可以在通用接口基础上做功能重载或功能追加
- 注意重载时不要覆盖原始操作，避免原始提供的功能丢失

**表现层开发**

1.基于Restful进行表现层接口开发

- 新增：POST
- 删除：DELETE
- 修改：PUT
- 查询：GET

2.使用Postman测试表现层接口功能

```Java
@RestController
@RequestMapping("/books")
public class BookController {
    @Autowired
    private IBookService bookService;

    @GetMapping
    public List<Book> getAll() {
        return bookService.list();
    }

    @PostMapping
    public Boolean save(@RequestBody Book book) {
        return bookService.save(book);
    }

    @PutMapping
    public Boolean update(@RequestBody Book book) {
        return bookService.modify(book);
    }

    @DeleteMapping("{id}")
    public Boolean delete(@PathVariable Integer id) {
        return bookService.delete(id);
    }

    @GetMapping("{id}")
    public Book getById(@PathVariable Integer id) {
        return bookService.getById(id);
    }

    @GetMapping("{currentPage}/{pageSize}")
    public IPage<Book> getPage(@PathVariable int currentPage, @PathVariable int pageSize) {
        return bookService.getPage(currentPage,pageSize);
    }
}
```

3.接收参数

- 实体数据：@RequestBody
- 路径变量：@PathVariable

==表现层消息一致性处理==

1.设计表现层返回结果的模型类，用于后端与前端进行数据格式统一，也称为前后端数据协议

```Java
@Data
public class R {
    private Boolean flag;
    private Object data;

    public R() {}

    public R(Boolean flag) {
        this.flag = flag;
    }

    public R(Boolean flag,Object data) {
        this.flag = flag;
        this.data = data;
    }
}
```

2.表现层接口统一返回值类型结果

```Java
@RestController
@RequestMapping("/books")
public class BookController {
    @Autowired
    private IBookService bookService;

    @GetMapping
    public R getAll() {
        return new R(true,bookService.list());
    }

    @PostMapping
    public R save(@RequestBody Book book) {
//        R r = new R();
//        boolean flag = bookService.save(book);
//        r.setFlag(flag);
        return new R(bookService.save(book));
    }

    @PutMapping
    public R update(@RequestBody Book book) {
        return new R(bookService.modify(book));
    }

    @DeleteMapping("{id}")
    public R delete(@PathVariable Integer id) {
        return new R(bookService.delete(id));
    }

    @GetMapping("{id}")
    public R getById(@PathVariable Integer id) {
        return new R(true,bookService.getById(id));
    }

    @GetMapping("{currentPage}/{pageSize}")
    public R getPage(@PathVariable int currentPage, @PathVariable int pageSize) {
        return new R(true,bookService.getPage(currentPage,pageSize));
    }
}
```

小结

- 设计统一的返回值结果类型便于前端开发读取数据
- 返回值结果类型可以根据需求自行设定，没有固定格式
- 返回值结果模型类用于后端与前端进行数据格式统一，也称为前后端数据协议

**前后端协议联调**

- 前后端分离结构设计中页面归属前端服务器
- 单体工程中页面放置在resources目录下的static目录中（建议执行clean）

前端发送异步请求，调用后端接口

```JavaScript
getAll() {
    //发送异步请求
    axios.get("/books").then((res)=>{
        console.log(res.data);
    });
},
```

注意

- 单体项目中页面放置在resources/static目录下
- created钩子函数用于初始化页面时发起调用
- 页面使用axios发送异步请求获取数据后确认前后端是否联通

将查询数据返回到页面，利用前端数据双向绑定进行数据展示

```javaScript
getAll() {
    //发送异步请求
    axios.get("/books").then((res)=>{
        //console.log(res.data);
        this.dataList = res.data.data;
    });
},
```

**添加功能**

弹出添加窗口

```JavaScript
//弹出添加窗口
handleCreate() {
    this.dialogFormVisible = true;
    this.resetForm();
},
```

清除数据

```JavaScript
//重置表单
resetForm() {
    this.formData = {};
},
```

添加

```JavaScript
//添加
handleAdd () {
    axios.post("/books",this.formData).then((res)=>{
        //判断当前操作是否成功
        if (res.data.flag) {
            //1.关闭弹层
            this.dialogFormVisible = false;
            this.$message.success("添加成功");
        } else {
            this.$message.error("添加失败");
        }
    }).finally(()=>{
        //2.更新加载数据
        this.getAll();
    });
},
```

取消添加

```JavaScript
//取消
cancel(){
    this.dialogFormVisible = false;
    this.$message.info("当前操作取消");
},
```

注意

- 请求方式使用POST调用后台对应操作
- 添加操作结束后动态刷新页面加载数据
- 根据操作结果不同，显示对应的提示信息
- 弹出添加Div时清除表单数据

**删除功能**

删除

```JavaScript
// 删除
handleDelete(row) {
    //console.log(row);
    this.$confirm("此操作永久删除当前信息，是否继续？","提示",{type: "info"}).then(()=>{
        axios.delete("/books/"+row.id).then((res)=>{
            //判断当前操作是否成功
            if (res.data.flag) {
                this.$message.success("删除成功");
            } else {
                this.$message.error("删除失败");
            }
        }).finally(()=>{
            //2.更新加载数据
            this.getAll();
        });
    }).catch(()=>{
        this.$message.info("取消操作");
    });
},
```

注意

- 请求方式使用Delete调用后台对应操作
- 删除操作需要传递当前行数据对应的id值到后台
- 删除操作结束后动态刷新页面加载数据
- 根据操作结果不同，显示对应的提示信息
- 删除操作前弹出提示框避免误操作

**修改功能**

弹出修改窗口

```JavaScript
//弹出编辑窗口
handleUpdate(row) {
    axios.get("/books/"+row.id).then((res)=>{
        if (res.data.flag && res.data.data != null) {
            this.dialogFormVisible4Edit = true;
            this.formData = res.data.data;
        } else {
            this.$message.error("数据同步失败，自动刷新");
        }
    }).finally(()=>{
        //2.更新加载数据
        this.getAll();
    });
},
```

注意

- 加载要修改数据通过传递当前行数据对应的id值到后台查询数据
- 利用前端数据双向绑定将查询到的数据进行回显

修改

```JavaScript
//修改
handleEdit() {
    axios.put("/books",this.formData).then((res)=>{
        //判断当前操作是否成功
        if (res.data.flag) {
            //1.关闭弹层
            this.dialogFormVisible4Edit = false;
            this.$message.success("修改成功");
        } else {
            this.$message.error("修改失败");
        }
    }).finally(()=>{
        //2.更新加载数据
        this.getAll();
    });
},
```

取消添加和修改

```JavaScript
//取消
cancel(){
    this.dialogFormVisible = false;
    this.dialogFormVisible4Edit = false;
    this.$message.info("当前操作取消");
},
```

注意

- 请求方式使用PUT调用后台对应操作
- 修改操作结束后动态刷新页面加载数据（同新增）
- 根据操作结果不同，显示对应的提示信息（同新增）

**业务消息一致性处理**

对异常进行统一处理，出现异常后，返回指定信息

```Java
//作为SpringMVC的异常处理器
//@ControllerAdvice
@RestControllerAdvice
public class ProjectExceptionAdvice {
    //拦截所有的异常信息
    @ExceptionHandler(Exception.class)
    public R doException(Exception ex) {
        //记录日志
        //通知运维
        //通知开发
        ex.printStackTrace();
        return new R("服务器故障，请稍后再试！");
    }
}
```

修改表现层返回结果的模型类，封装出现异常后对应的信息

- flag：false
- Data：null
- 消息(msg)：要显示信息

```Java
@Data
public class R {
    private Boolean flag;
    private Object data;
    private String msg;

    public R() {}

    public R(Boolean flag) {
        this.flag = flag;
    }

    public R(Boolean flag,Object data) {
        this.flag = flag;
        this.data = data;
    }

    public R(Boolean flag,String msg) {
        this.flag = flag;
        this.msg = msg;
    }

    public R(String msg) {
        this.flag = false;
        this.msg = msg;
    }
}
```

页面消息处理，没有传递消息加载默认消息，传递消息后加载指定消息

```JavaScript
//添加
handleAdd () {
    axios.post("/books",this.formData).then((res)=>{
        //判断当前操作是否成功
        if (res.data.flag) {
            //1.关闭弹层
            this.dialogFormVisible = false;
            this.$message.success(res.data.msg);
        } else {
            this.$message.error(res.data.msg);
        }
    }).finally(()=>{
        //2.更新加载数据
        this.getAll();
    });
},
```

可以在表现层Controller中进行消息统一处理

```Java
    @PostMapping
    public R save(@RequestBody Book book) throws IOException {
        if (book.getName().equals("123")) throw new IOException();
        boolean flag = bookService.save(book);
        return new R(flag, flag ? "添加成功^_^" : "添加失败-_-!");
    }
```

目的：国际化

小结

- 使用注解@RestControllerAdvice定义SpringMVC异常处理器用来处理异常的
- 异常处理器必须被扫描加载，否则无法生效
- 表现层返回结果的模型类中添加消息属性用来传递消息到页面

**分页功能**

页面使用el分页组件添加分页功能

```vue
<!--分页组件-->
<div class="pagination-container">
    <el-pagination
            class="pagiantion"

            @current-change="handleCurrentChange"

            :current-page="pagination.currentPage"

            :page-size="pagination.pageSize"

            layout="total, prev, pager, next, jumper"

            :total="pagination.total">

    </el-pagination>
</div>
```

定义分页组件需要使用的数据并将数据绑定到分页组件

```JavaScript
data:{
    pagination: {//分页相关模型数据
        currentPage: 1,//当前页码
        pageSize:10,//每页显示的记录数
        total:0//总记录数
    }
},
```

替换查询全部功能为分页功能

```JavaScript
//分页查询
getAll() {
    //发送异步请求
    axios.get("/books/" + this.pagination.currentPage + "/" + this.pagination.pageSize).then((res)=>{
        this.pagination.pageSize = res.data.data.size;
        this.pagination.currentPage = res.data.data.current;
        this.pagination.total = res.data.data.total;
        this.dataList = res.data.data.records;
    });
},
```

分页页码值切换

```JavaScript
//切换页码
handleCurrentChange(currentPage) {
    //修改页码值为当前选中的页码值
    this.pagination.currentPage = currentPage;
    //执行查询
    this.getAll();
},
```

小结

- 使用el分页组件
- 定义分页组件绑定的数据模型
- 异步调用获取分页数据
- 分页数据页面回显

**删除功能维护**

对查询结果进行校验，如果当前页码值大于最大页码值，使用最大页码值作为当前页码值重新查询

```Java
@GetMapping("{currentPage}/{pageSize}")
public R getPage(@PathVariable int currentPage, @PathVariable int pageSize) {
    IPage<Book> page = bookService.getPage(currentPage, pageSize);
    //如果当前页码值大于总页码值，那么重新执行查询操作，使用最大页码值作为当前页码值
    if (currentPage > page.getPages()) {
        page = bookService.getPage((int) page.getPages(),pageSize);
    }
    return new R(true,page);
}
```

**条件查询功能**

查询条件数据封装

- 单独封装
- 与分页操作混合封装

```JavaScript
pagination: {//分页相关模型数据
    currentPage: 1,//当前页码
    pageSize:10,//每页显示的记录数
    total:0,//总记录数
    type: "",
    name: "",
    description: ""
}
```

页面数据模型绑定

```HTML
<div class="filter-container">
    <el-input placeholder="图书类别" v-model="pagination.type" style="width: 200px;" class="filter-item"></el-input>
    <el-input placeholder="图书名称" v-model="pagination.name" style="width: 200px;" class="filter-item"></el-input>
    <el-input placeholder="图书描述" v-model="pagination.description" style="width: 200px;" class="filter-item"></el-input>
    <el-button @click="getAll()" class="dalfBut">查询</el-button>
    <el-button type="primary" class="butT" @click="handleCreate()">新建</el-button>
</div>
```

组织数据成为get请求发送的数据

```JavaScript
//分页查询
getAll() {
    //组织参数，拼接url请求地址
    //console.log(this.pagination.type);
    param = "?type=" + this.pagination.type;
    param += "&name=" + this.pagination.name;
    param += "&description=" + this.pagination.description;
    console.log(param);
    //发送异步请求
    axios.get("/books/" + this.pagination.currentPage + "/" + this.pagination.pageSize + param).then((res)=>{
        this.pagination.pageSize = res.data.data.size;
        this.pagination.currentPage = res.data.data.current;
        this.pagination.total = res.data.data.total;
        this.dataList = res.data.data.records;
    });
},
```

注：条件参数组织可以通过条件判定书写的更简洁

Controller接收参数

```Java
@GetMapping("{currentPage}/{pageSize}")
public R getPage(@PathVariable int currentPage, @PathVariable int pageSize, Book book) {
    IPage<Book> page = bookService.getPage(currentPage, pageSize, book);
    //如果当前页码值大于总页码值，那么重新执行查询操作，使用最大页码值作为当前页码值
    if (currentPage > page.getPages()) {
        page = bookService.getPage((int) page.getPages(),pageSize,book);
    }
    return new R(true,page);
}
```

业务层接口功能开发

```Java
public interface IBookService extends IService<Book> {
    boolean saveBook(Book book);

    boolean modify(Book book);

    boolean delete(Integer id);

    IPage<Book> getPage(int currentPage, int pageSize);

    IPage<Book> getPage(int currentPage, int pageSize, Book book);
}
```

```Java
@Override
public IPage<Book> getPage(int currentPage, int pageSize, Book book) {
    LambdaQueryWrapper<Book> lqw = new LambdaQueryWrapper<Book>();
    lqw.like(Strings.isNotEmpty(book.getType()),Book::getType,book.getType());
    lqw.like(Strings.isNotEmpty(book.getName()),Book::getName,book.getName());
    lqw.like(Strings.isNotEmpty(book.getDescription()),Book::getDescription,book.getDescription());
    IPage page = new Page(currentPage,pageSize);
    bookDao.selectPage(page,lqw);
    return page;
}
```

Controller调用业务层分页条件查询接口

页面回显数据

注意

- 定义查询条件数据模型（当前封装到分页数据模型中）
- 异步调用分页功能并通过请求参数传递数据到后台

## 2. SpringBoot实用篇

### 2.1 运维实用篇

**打包与运行**

SpringBoot项目快速启动（Windows版）

1. 对SpringBoot项目打包（执行Maven构建指令package）

```shell
mvn package
```

2. 运行项目（执行启动指令）

```shell
java –jar springboot.jar
```

注意：jar支持命令行启动需要依赖maven插件支持，请确认打包时是否具有SpringBoot对应的maven插件。

```XML
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

小结

- SpringBoot工程可以基于java环境下独立运行jar文件启动服务
- SpringBoot工程执行mvn命令package进行打包
- 执行jar命令：java –jar 工程名.jar

Windonws端口被占用

```shell
# 查询端口
netstat -ano
# 查询指定端口
netstat -ano | findstr"端口号"
# 根据进程PID查询进程名称
tasklist | findstr"进程PID号"
# 根据PID杀死任务
taskkill /F /PID "进程PID号"
# 根据进程名称杀死任务
taskkill -f -t -im "进程名称"
```

SpringBoot项目快速启动（Linux版）

- 基于Linux（CenterOS7）
- 安装JDK，且版本不低于打包时使用的JDK版本
- 安装包保存在/usr/local/自定义目录中或$HOME下
- 其他操作参照Windows版进行
- 执行jar命令：java –jar 工程名.jar

小结

- Boot程序打包依赖SpringBoot对应的Maven插件即可打包出可执行的jar包
- 运行jar包使用jar命令进行
- Windows与Linux下执行Boot打包程序流程相同，仅需确保运行环境有效即可

**配置高级**

临时属性设置

- 带属性数启动SpringBoot

```shell
java –jar springboot.jar –-server.port=80
```

- 携带多个属性启动SpringBoot，属性间使用空格分隔

属性加载优先顺序

- 参看https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config

小结

- 使用jar命令启动SpringBoot工程时可以使用临时属性替换配置文件中的属性
- 临时属性添加方式：java –jar 工程名.jar –-属性名=值
- 多个临时属性之间使用空格分隔
- 临时属性必须是当前boot工程支持的属性，否则设置无效

临时属性设置（开发环境）

- 带属性启动SpringBoot程序，为程序添加运行属性
- 通过编程形式带参数启动SpringBoot程序，为程序添加运行参数

```Java
public static void main(String[] args) {
    String[] arg = new String[1];
    arg[0] = "--server.port=8080";
    SpringApplication.run(SSMPApplication.class, arg);
}
```

- 不携带参数启动SpringBoot程序

```Java
public static void main(String[] args) {
    SpringApplication.run(SSMPApplication.class);
}
```

- 启动SpringBoot程序时，可以选择是否使用命令行属性为SpringBoot程序传递启动属性

==配置文件分类==

SpringBoot中4级配置文件

1级：file ：config/application.yml【最高】

2级：file ：application.yml

3级：classpath：config/application.yml

4级：classpath：application.yml【最低】

作用

- 1级与2级留做系统打包后设置通用属性，1级常用于运维经理进行线上整体项目部署方案调控
- 3级与4级用于系统开发阶段设置通用属性，3级常用于项目经理进行整体项目属性调控

小结

- 配置文件分为4种
  - 项目类路径配置文件：服务于开发人员本机开发与测试
  - 项目类路径config目录中配置文件：服务于项目经理整体调控
  - 工程路径配置文件：服务于运维人员配置涉密线上环境
  - 工程路径config目录中配置文件：服务于运维经理整体调控
- 多层级配置文件间的属性采用叠加并覆盖的形式作用于程序

自定义配置文件

- 通过启动参数加载配置文件（无需书写配置文件扩展名，properties与yml文件格式均支持)

```shell
--spring.config.name=ebank
```

- 通过启动参数加载指定文件路径下的配置文件
- 通过启动参数加载指定文件路径下的配置文件时可以加载多个配置

```shell
--spring.config.location=classpath:/ebank-server.yml,classpath:/ebank.yml
```

注意：多配置文件常用于将配置进行分类，进行独立管理，或将可选配置单独制作便于上线更新维护。

自定义配置文件——重要说明

- 单服务器项目：使用自定义配置文件需求较低
- 多服务器项目：使用自定义配置文件需求较高，将所有配置放置在一个目录中，统一管理
- 基于SpringCloud技术，所有的服务器将不再设置配置文件，而是通过配置中心进行设定，动态加载配置信息

小结

- SpringBoot在开发和运行环境均支持使用临时参数修改工程配置
- SpringBoot支持4级配置文件，应用于开发与线上环境进行配置的灵活设置
- SpringBoot支持使用自定义配置文件的形式修改配置文件存储位置
- 基于微服务开发时配置文件将使用配置中心进行管理

**多环境开发**

多环境开发（YAML版）

- 启动指定环境
- 设置生产环境
- 生产环境具体参数设定
- 设置开发环境
- 开发环境具体参数设定
- 设置测试环境
- 测试环境具体参数设定

```yaml
# 应用环境
# 公共配置
spring:
  profiles:
    active: dev
---
# 设置环境
# 生产环境
spring:
  profiles: pro
server:
  port: 80

---
# 开发环境
spring:
  profiles: dev
server:
  port: 81

---
# 测试环境
spring:
  config:
    activate:
      on-profile: test
server:
  port: 82
```

小结

- 多环境开发需要设置若干种常用环境，例如开发、生产、测试环境
- yaml格式中设置多环境使用---区分环境设置边界
- 每种环境的区别在于加载的配置属性不同
- 启用某种环境时需要指定启动时使用该环境

多环境开发（YAML版）多配置文件格式

1.主启动配置文件application.yml

```yaml
spring:
  profiles:
    active: test
```

2.环境分类配置文件application-pro.yml

```yaml
server:
  port: 8080
```

3.环境分类配置文件application-dev.yml

```yaml
server:
  port: 8081
```

4.环境分类配置文件application-test.yml

```yaml
server:
  port: 8082
```

多环境开发配置文件书写技巧

- 主配置文件中设置公共配置（全局）
- 环境分类配置文件中常用于设置冲突属性（局部）

多环境开发（Properties版）多配置文件格式

1.主启动配置文件application.properties

```properties
spring.profiles.active=dev
```

2.环境分类配置文件application-pro.properties

```properties
server.port=9080
```

3.环境分类配置文件application-dev.properties

```properties
server.port=9081
```

4.环境分类配置文件application-test.properties

```properties
server.port=9082
```

注意：properties文件多环境配置仅支持多文件格式。

**多环境分组管理**

多环境开发独立配置文件书写技巧

根据功能对配置文件中的信息进行拆分，并制作成独立的配置文件，命名规则如下：

- application-devDB.yml
- application-devRedis.yml
- application-devMVC.yml

使用include属性在激活指定环境的情况下，同时对多个环境进行加载使其生效，多个环境间使用逗号分隔

```yaml
spring:
  profiles:
    active: dev
    include: devMVC,devDB
```

注意：当主环境dev与其他环境有相同属性时，主环境属性生效；其他环境中有相同属性时，最后加载的环境属性生效。

从Spring2.4版开始使用group属性替代include属性，降低了配置书写量

使用group属性定义多种主环境与子环境的包含关系

```yaml
spring:
  profiles:
    active: dev
    group:
      "dev": devMVC,devDB
      "pro": proMVC,proDB
```

小结：多环境开发使用group属性设置配置文件分组，便于线上维护管理。

**多环境开发控制**

Maven与SpringBoot多环境兼容

1.Maven中设置多环境属性

```XML
<!--设置多环境-->
<profiles>
    <profile>
        <id>env_dev</id>
        <properties>
            <profile.active>dev</profile.active>
        </properties>
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
    <profile>
        <id>env_pro</id>
        <properties>
            <profile.active>pro</profile.active>
        </properties>
    </profile>
</profiles>
```

2.SpringBoot中引用Maven属性

```yaml
spring:
  profiles:
    active: @profile.active@
    group:
      "dev": devMVC,devDB
      "pro": proMVC,proDB
```

3.执行Maven打包指令，并在生成的boot打包文件.jar文件中查看对应信息

小结

- 当Maven与SpringBoot同时对多环境进行控制时，以Mavn为主，SpringBoot使用@..@占位符读取Maven对应的配置属性值
- 基于SpringBoot读取Maven配置属性的前提下，如果在Idea下测试工程时pom.xml每次更新需要手动compile方可生效

**日志**

**日志基础操作**

日志（log）作用

- 编程期调试代码
- 运营期记录信息
  - 记录日常运营重要信息（峰值流量、平均响应时长……）
  - 记录应用报错信息（错误堆栈）
  - 记录运维过程数据（扩容、宕机、报警……）

代码中使用日志工具记录日志

1.添加日志记录操作

```Java
@RestController
@RequestMapping("/books")
public class BookController {
    // 创建记录日志的对象
    private static final Logger log = LoggerFactory.getLogger(BookController.class);

    @GetMapping
    public String getById() {
        System.out.println("springboot is running...");

        log.debug("debug...");
        log.info("info...");
        log.warn("warn...");
        log.error("error...");

        return "springboot is running...";
    }
}
```

2.设置日志输出级别(包括设置日志组，控制指定包对应的日志输出级别，也可以直接控制指定包对应的日志输出级别)

```yaml
# debug: true

logging:
  # 设置分组
  group:
    ebank: com.itheima.controller,com.itheima.service,com.itheima.dao
    iservice: com.alibaba
  level:
    root: info
    # 设置某个包的日志级别
    #com.itheima.controller: debug
    # 设置分组，对某个组设置日志级别
    ebank: warn
```

日志级别

- TRACE：运行堆栈信息，使用率低
- DEBUG：程序员调试代码使用
- INFO：记录运维过程数据
- WARN：记录运维过程报警数据
- ERROR：记录错误堆栈信息
- FATAL：灾难信息，合并计入ERROR

小结

- 日志用于记录开发调试与运维过程消息
- 日志的级别共6种，通常使用4种即可，分别是DEBUG，INFO，WARN，ERROR
- 可以通过日志组或代码包的形式进行日志显示级别的控制

优化日志对象创建代码

使用lombok提供的注解@Slf4j简化开发，减少日志对象的声明操作

```Java
@Slf4j
@RestController
@RequestMapping("/books")
public class BookController {

    @GetMapping
    public String getById() {
        System.out.println("springboot is running...");

        log.debug("debug...");
        log.info("info...");
        log.warn("warn...");
        log.error("error...");

        return "springboot is running...";
    }
}
```

**日志输出格式控制**

默认日志输出内容：时间，级别，PID，所属线程，所属类/接口名，日志信息。

- PID：进程ID，用于表明当前操作所处的进程，当多服务同时记录日志时，该值可用于协助程序员调试程序
- 所属类/接口名：当前显示信息为SpringBoot重写后的信息，名称过长时，简化包名书写为首字母，甚至直接删除

设置日志输出格式

- %d：日期
- %m：消息
- %n：换行

```yaml
logging:
  # 设置分组
  group:
    ebank: com.itheima.controller,com.itheima.service,com.itheima.dao
    iservice: com.alibaba
  level:
    root: info
    # 设置某个包的日志级别
    #com.itheima.controller: debug
    # 设置分组，对某个组设置日志级别
    ebank: warn
  # 设置日志的模板格式
  pattern:
#    console: "%d - %m %n"
    console: "%d %clr(%5p) --- [%16t] %clr(%-40.40c){cyan} : %m %n"
```

**日志文件**

设置日志文件详细配置，使日志记录到文件

```yaml
logging:
  # 设置分组
  group:
    ebank: com.itheima.controller,com.itheima.service,com.itheima.dao
    iservice: com.alibaba
  level:
    root: info
    # 设置某个包的日志级别
    #com.itheima.controller: debug
    # 设置分组，对某个组设置日志级别
    ebank: warn
  # 设置日志的模板格式
  pattern:
    #console: "%d - %m %n"
    console: "%d %clr(%5p) --- [%16t] %clr(%-40.40c){cyan} : %m %n"
  # 设置日志文件
  file:
    name: server.log
  logback:
    rollingpolicy:
      max-file-size: 4KB
      file-name-pattern: server.%d{yyyy-MM-dd}.%i.log
```

### 2.2 开发实用篇

#### 2.2.1 热部署

**手动启动热部署**

1.导入开启开发者工具依赖

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
</dependency>
```

2.激活热部署：**Ctrl** + **F9**

关于热部署

- 重启（Restart）：自定义开发代码，包含类、页面、配置文件等，加载位置restart类加载器
- 重载（ReLoad）：jar包，加载位置base类加载器

小结

- 开启开发者工具后启用热部署
- 使用构建项目操作启动热部署（Ctrl+F9）
- 热部署仅仅加载当前开发者自定义开发的资源，不加载jar资源

**自动启动热部署**

设置自动构建项目

- 勾选Settings -> Compiler -> Build project automatically

设置自动构建项目

- 2021.3.3版IDEA中，勾选Settings -> Advanced Settings -> Compiler下的Allow auto-make to start even if developed application is currently running

激活方式：Idea失去焦点5秒后启动热部署。

**热部署范围配置**

默认不触发重启的目录列表

- /META-INF/maven
- /META-INF/resources
- /resources
- /static
- /public
- /templates

自定义不参与重启排除项

```yaml
devtools:
  restart:
    # 设置不参与热部署的文件或文件夹
    exclude: static/**,public/**,config/application.yml
```

**属性加载优先顺序**

参看[https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html)

设置高优先级属性禁用热部署

```Java
public static void main(String[] args) {
    System.setProperty("spring.devtools.restart.enabled","false");
    SpringApplication.run(SSMPApplication.class, args);
}
```

#### 2.2.2 配置高级

**@ConfigurationProperties**

使用@ConfigurationProperties为第三方bean绑定属性

```Java
@Bean
@ConfigurationProperties(prefix = "datasource")
public DruidDataSource dataSource() {
    DruidDataSource ds = new DruidDataSource();
    return ds;
}
```

```yaml
datasource:
  driverClassName: com.mysql.jdbc.Driver789
```

@EnableConfigurationProperties注解可以将使用@ConfigurationProperties注解对应的类加入Spring容器

```Java
@SpringBootApplication
@EnableConfigurationProperties(ServerConfig.class)
public class Springboot13ConfigurationApplication {
    @Bean
    @ConfigurationProperties(prefix = "datasource")
    public DruidDataSource dataSource() {
        DruidDataSource ds = new DruidDataSource();
        return ds;
    }

    public static void main(String[] args) {
        ConfigurableApplicationContext ctx = SpringApplication.run(Springboot13ConfigurationApplication.class, args);
        ServerConfig bean = ctx.getBean(ServerConfig.class);
        System.out.println(bean);
        DruidDataSource ds = ctx.getBean(DruidDataSource.class);
        System.out.println(ds.getDriverClassName());
    }

}
```

```Java
//@Component
@Data
@ConfigurationProperties(prefix = "servers")
public class ServerConfig {
    private String ipAddress;
    private int port;
    private long timeout;
}
```

注意：@EnableConfigurationProperties与@Component不能同时使用。

解除使用@ConfigurationProperties注释警告

- 出现警告：Spring Boot Configuration Annotation Processor not configured
- 解决：添加依赖

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
</dependency>
```

小结：@ConfigurationProperties可以为第三方bean绑定属性。

**宽松绑定**

@ConfigurationProperties绑定属性支持属性名宽松绑定

```Java
//@Component
@Data
@ConfigurationProperties(prefix = "servers")
public class ServerConfig {
    private String ipAddress;
    private int port;
    private long timeout;
}
```

```yaml
servers:
#  ipAddress: 192.168.0.2   # 驼峰
#  ipaddress: 192.168.0.2
#  ip_address: 192.168.0.2  # underline
  ip-address: 192.168.0.2   # 烤肉串模式 0-0-0-0---------
#  IPADDRESS: 192.168.0.2
#  IP_ADDRESS: 192.168.0.2  # 常量
#  IP_ADD_R-E_SS: 192.168.0.2
  port: 2345
  timeout: -1
```

注意

- 宽松绑定不支持注解@Value引用单个属性的方式
- 绑定前缀名命名规范：仅能使用纯小写字母、数字、下划线作为合法的字符

**常用计量单位**

SpringBoot支持JDK8提供的时间与空间计量单位

```Java
//@Component
@Data
@ConfigurationProperties(prefix = "servers")
public class ServerConfig {
    private String ipAddress;
    private int port;
    private long timeout;
    @DurationUnit(ChronoUnit.HOURS)
    private Duration serverTimeOut;
    @DataSizeUnit(DataUnit.MEGABYTES)
    private DataSize dataSize;
}
```

```yaml
servers:
#  ipAddress: 192.168.0.2   # 驼峰
#  ipaddress: 192.168.0.2
#  ip_address: 192.168.0.2  # underline
  ip-address: 192.168.0.2   # 烤肉串模式 0-0-0-0---------
#  IPADDRESS: 192.168.0.2
#  IP_ADDRESS: 192.168.0.2  # 常量
#  IP_ADD_R-E_SS: 192.168.0.2
  port: 2345
  timeout: -1
  serverTimeOut: 3
  dataSize: 10MB
```

**数据校验**

开启数据校验有助于系统安全性，J2EE规范中JSR303规范定义了一组有关数据校验相关的API

1.添加JSR303规范坐标与Hibernate校验框架对应坐标

```XML
<!--1.导入JSR303规范-->
<dependency>
    <groupId>javax.validation</groupId>
    <artifactId>validation-api</artifactId>
</dependency>
<!--使用hibernate框架提供的校验器做实现类-->
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
</dependency>
```

2.对Bean开启校验功能

3.设置校验规则

```Java
//@Component
@Data
@ConfigurationProperties(prefix = "servers")
//2.开启当前bean的属性注入校验
@Validated
public class ServerConfig {
    private String ipAddress;
    //3.设置具体的规则
    @Max(value = 8888,message = "最大值不能超过8888")
    @Min(value = 202,message = "最小值不能低于202")
    private int port;
    private long timeout;
    @DurationUnit(ChronoUnit.HOURS)
    private Duration serverTimeOut;
    @DataSizeUnit(DataUnit.MEGABYTES)
    private DataSize dataSize;
}
```

**yaml语法规则**

字面值表达方式

```yaml
boolean: TRUE  						 #TRUE,true,True,FALSE,false，False均可
float: 3.14    						 #6.8523015e+5  #支持科学计数法
int: 123       						 #0b1010_0111_0100_1010_1110    #支持二进制、八进制、十六进制
null: ~        						 #使用~表示null
string: HelloWorld      			 #字符串可以直接书写
string2: "Hello World"  			 #可以使用双引号包裹特殊字符
date: 2018-02-17        			 #日期必须使用yyyy-MM-dd格式
datetime: 2018-02-17T15:02:31+08:00  #时间和日期之间使用T连接，最后使用+代表时区
```

注意：注意yaml文件中对于数字的定义支持进制书写格式，如需使用字符串请使用引号明确标注。

#### 2.2.3 测试

**加载测试专用属性**

1.在启动测试环境时可以通过properties参数设置测试环境专用的属性

2.在启动测试环境时可以通过args参数设置测试环境专用的传入参数

```Java
//properties属性可以为当前测试用例添加临时的属性配置
//@SpringBootTest(properties = {"test.prop=testValue1"})
//args属性可以为当前测试用例添加临时的命令行参数
//@SpringBootTest(args = {"--test.prop=testValue2"})
@SpringBootTest(properties = {"test.prop=testValue1"},args = {"--test.prop=testValue2"})
public class PropertiesAndArgsTest {
    @Value("${test.prop}")
    private String msg;

    @Test
    void testProperties() {
        System.out.println(msg);
    }
}
```

优势：比多环境开发中的测试环境影响范围更小，仅对当前测试类有效。

**加载测试专用配置**

使用@Import注解加载当前测试类专用的配置

```Java
@SpringBootTest
@Import({MsgConfig.class})
public class ConfigurationTest {
    @Autowired
    private String msg;

    @Test
    void testConfiguration() {
        System.out.println(msg);
    }
}
```

```Java
@Configuration
public class MsgConfig {
    @Bean
    public String msg() {
        return "bean msg";
    }
}
```

作用：加载测试范围配置应用于小范围测试环境。

**web环境模拟测试**

模拟端口

```Java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class WebTest {
    @Test
    void test() {

    }
}
```

虚拟请求测试

```Java
@Test
void testWeb(@Autowired MockMvc mvc) throws Exception {
    // http://localhost:8080/books
    // 创建虚拟请求，当前访问/books
    MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
    // 执行对应的请求
    mvc.perform(builder);
}
```

虚拟请求状态匹配

```Java
@Test
void testStatus(@Autowired MockMvc mvc) throws Exception {
    MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
    ResultActions action = mvc.perform(builder);

    // 设定预期值，与真实值进行比较，成功测试通过，失败测试失败
    // 定义本次调用的预期值
    StatusResultMatchers status = MockMvcResultMatchers.status();
    // 预计本次调用是成功的：状态200
    ResultMatcher ok = status.isOk();
    // 添加预计值到本次调用过程中进行匹配
    action.andExpect(ok);
}
```

虚拟请求响应体匹配

```Java
@Test
void testBody(@Autowired MockMvc mvc) throws Exception {
    MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
    ResultActions action = mvc.perform(builder);

    // 设定预期值，与真实值进行比较，成功测试通过，失败测试失败
    // 定义本次调用的预期值
    ContentResultMatchers content = MockMvcResultMatchers.content();
    ResultMatcher result = content.string("springboot");
    // 添加预计值到本次调用过程中进行匹配
    action.andExpect(result);
}
```

虚拟请求响应体（json）匹配

```Java
@Test
void testJson(@Autowired MockMvc mvc) throws Exception {
    MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
    ResultActions action = mvc.perform(builder);

    // 设定预期值，与真实值进行比较，成功测试通过，失败测试失败
    // 定义本次调用的预期值
    ContentResultMatchers content = MockMvcResultMatchers.content();
    ResultMatcher result = content.json("{\"id\":1,\"name\":\"springboot\",\"type\":\"springboot\",\"description\":\"springboot\"}");
    // 添加预计值到本次调用过程中进行匹配
    action.andExpect(result);
}
```

虚拟请求响应头匹配

```Java
@Test
void testContentType(@Autowired MockMvc mvc) throws Exception {
    MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
    ResultActions action = mvc.perform(builder);

    // 设定预期值，与真实值进行比较，成功测试通过，失败测试失败
    // 定义本次调用的预期值
    HeaderResultMatchers header = MockMvcResultMatchers.header();
    ResultMatcher contentType = header.string("Content-Type", "application/json");
    // 添加预计值到本次调用过程中进行匹配
    action.andExpect(contentType);
}
```

web环境模拟测试

- 设置测试端口
- 模拟测试启动
- 模拟测试匹配（各组成部分信息均可匹配）

**业务层测试事务回滚**

1.为测试用例添加事务，SpringBoot会对测试用例对应的事务提交操作进行回滚

2.如果想在测试用例中提交事务，可以通过@Rollback注解设置

```Java
@SpringBootTest
@Transactional
@Rollback(value = true)
public class DaoTest {
    @Autowired
    private BookService bookService;

    @Test
    void testSave() {
        Book book = new Book();
        book.setName("springboot3");
        book.setType("springboot3");
        book.setDescription("springboot3");

        bookService.save(book);
    }
}
```

**测试用例数据设定**

测试用例数据通常采用随机值进行测试，使用SpringBoot提供的随机数为其赋值

- ${random.int}表示随机整数
- ${random.int(10)}表示10以内的随机数
- ${random.int(10,20)}表示10到20的随机数
- 其中()可以是任意字符，例如[]，!!均可

```yaml
testcase:
  book:
    id: ${random.int}
    id2: ${random.int(10)}
    type: ${random.int(5,10)}
    name: 无敌${random.value}
    uuid: ${random.uuid}
    publishTime: ${random.long}
```

```Java
@Component
@Data
@ConfigurationProperties(prefix = "testcase.book")
public class BookCase {
    private int id;
    private int id2;
    private int type;
    private String name;
    private String uuid;
    private long publishTime;
}
```

```Java
@Autowired
private BookCase bookCase;

@Test
void testProperties() {
    System.out.println(bookCase);
}
```

#### 2.2.4 数据层解决方案

现有数据层解决方案技术选型

Druid + MyBatis-Plus + MySQL

- 数据源：DruidDataSource
- 持久化技术：MyBatis-Plus / MyBatis
- 数据库：MySQL

**数据源配置格式**

格式一

```yaml
spring:
  datasource:
	driver-class-name: com.mysql.cj.jdbc.Driver
	url: jdbc:mysql://localhost:3306/test?serverTimezone=UTC
	username: root
	password: root
```

格式二

```yaml
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/test?serverTimezone=UTC
      username: root
      password: root
```

SpringBoot提供了3种内嵌的数据源对象供开发者选择

- HikariCP：默认内置数据源对象
- Tomcat提供DataSource：HikariCP不可用的情况下，且在web环境中，将使用tomcat服务器配置的数据源对象
- Commons DBCP：Hikari不可用，tomcat数据源也不可用，将使用dbcp数据源

通用配置无法设置具体的数据源配置信息，仅提供基本的连接相关配置，如需配置，在下一级配置中设置具体设定

```yaml
spring:
  datasource:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/test?serverTimezone=UTC
      username: root
      password: root
      hikari:
        maximum-pool-size: 50
```

内置持久化解决方案——JdbcTemplate

```Java
@Test
void testJdbcTemplate(@Autowired JdbcTemplate jdbcTemplate){
    String sql = "select * from tbl_book";
    RowMapper<Book> rm = new RowMapper<Book>() {
        @Override
        public Book mapRow(ResultSet rs, int rowNum) throws SQLException {
            Book temp = new Book();
            temp.setId(rs.getInt("id"));
            temp.setName(rs.getString("name"));
            temp.setType(rs.getString("type"));
            temp.setDescription(rs.getString("description"));
            return temp;
        }
    };
    List<Book> list = jdbcTemplate.query(sql, rm);
    System.out.println(list);
}
```

需要依赖

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```

JdbcTemplate配置

```yaml
spring:
  jdbc:
	template:
	  query-timeout: -1   # 查询超时时间
	  max-rows: 500       # 最大行数
	  fetch-size: -1      # 缓存行数
```

**内嵌数据库**

SpringBoot提供了3种内嵌数据库供开发者选择，提高开发测试效率

- H2
- HSQL
- Derby

导入H2相关坐标

```XML
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

设置当前项目为web工程，并配置H2管理控制台参数

```yaml
server:
  port: 80
spring:
  h2:
    console:
      enabled: true
      path: /h2
```

访问用户名sa，默认密码123456

设置访问数据源

```yaml
server:
  port: 80
spring:
  h2:
    console:
      enabled: true
      path: /h2
  datasource:
    url: jdbc:h2:~/test
    hikari:
      driver-class-name: org.h2.Driver
      username: sa
      password: 123456
```

H2数据库控制台仅用于开发阶段，线上项目请务必关闭控制台功能

```yaml
server:
  port: 80
spring:
  h2:
    console:
      enabled: false
      path: /h2
```

SpringBoot可以根据url地址自动识别数据库种类，在保障驱动类存在的情况下，可以省略配置。

注意：H2数据库线上运行时请务必关闭。

**NoSQL解决方案**

市面上常见的NoSQL解决方案

- Redis
- Mongo
- ES
- Solr

**Redis**

Redis是一款key-value存储结构的内存级NoSQL数据库

- 支持多种数据存储格式
- 支持持久化
- 支持集群

Redis下载（ Windows版）

- https://github.com/tporadowski/redis/releases

Redis安装与启动（ Windows版）

- Windows解压安装或一键式安装
- 服务端启动命令：redis-server.exe redis.windows.conf
- 客户端启动命令：redis-cli.exe

1.导入SpringBoot整合Redis坐标

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

2.配置Redis（采用默认配置）

- 主机：localhost(默认)
- 端口：6379(默认)

```yaml
spring:
  redis:
    host: localhost
    port: 6379
```

3.RedisTemplate提供操作各种数据存储类型的接口API

```Java
@SpringBootTest
class Springboot16RedisApplicationTests {
    @Autowired
    private RedisTemplate redisTemplate;

    @Test
    void set() {
        ValueOperations ops = redisTemplate.opsForValue();
        ops.set("age",41);
    }

    @Test
    void get() {
        ValueOperations ops = redisTemplate.opsForValue();
        Object age = ops.get("age");
        System.out.println(age);
    }

    @Test
    void hset() {
        HashOperations ops = redisTemplate.opsForHash();
        ops.put("info","a","bb");
    }

    @Test
    void hget() {
        HashOperations ops = redisTemplate.opsForHash();
        Object o = ops.get("info", "a");
        System.out.println(o);
    }

}
```

SpringBoot整合Redis步骤

- 导入redis对应的starter
- 配置
- 提供操作Redis接口对象RedisTemplate
  - ops*：获取各种数据类型操作接口

客户端：RedisTemplate以对象作为key和value，内部对数据进行序列化。

客户端：StringRedisTemplate以字符串作为key和value，与Redis客户端操作等效。

```Java
@SpringBootTest
public class SpringRedisTemplateTest {

    @Autowired
    private StringRedisTemplate stringRedisTemplate;

    @Test
    void get() {
        ValueOperations<String, String> ops = stringRedisTemplate.opsForValue();
        String name = ops.get("name");
        System.out.println(name);
    }
}
```

客户端选择：jedis

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
</dependency>
```

配置客户端

```yaml
spring:
  redis:
    host: localhost
    port: 6379
    client-type: jedis
```

配置客户端专用属性

```yaml
spring:
  redis:
    host: localhost
    port: 6379
    client-type: jedis
    lettuce:
      pool:
        max-active: 16
    jedis:
      pool:
        max-active: 16
```

lettcus与jedis区别

- jedis连接Redis服务器是直连模式，当多线程模式下使用jedis会存在线程安全问题，解决方案可以通过配置连接池使每个连接专用，这样整体性能就大受影响。
- lettcus基于Netty框架进行与Redis服务器连接，底层设计中采用StatefulRedisConnection。 StatefulRedisConnection自身是线程安全的，可以保障并发访问安全问题，所以一个连接可以被多线程复用。当然lettcus也支持多连接实例一起工作。

SpringBoot整合Redis客户端选择

- lettuce（默认）
- jedis

**Mongodb**

MongoDB是一个开源、高性能、无模式的文档型数据库。NoSQL数据库产品中的一种，是最像关系型数据库的非关系型数据库。 

淘宝用户数据

- 存储位置：数据库
- 特征：永久性存储，修改频度极低

游戏装备数据、游戏道具数据

- 存储位置：数据库、Mongodb
- 特征：永久性存储与临时存储相结合、修改频度较高

直播数据、打赏数据、粉丝数据

- 存储位置：数据库、Mongodb
- 特征：永久性存储与临时存储相结合，修改频度极高

物联网数据

- 存储位置：Mongodb
- 特征：临时存储，修改频度飞速

Windows版Mongo下载：https://www.mongodb.com/try/download

Windows版Mongo安装：解压缩后设置数据目录

Windows版Mongo启动

- 服务端启动：mongod --dbpath=..\data\db
- 客户端启动：mongo --host=127.0.0.1 --port=27017

Windows版Mongo安装问题及解决方案

问题：由于找不到VCRUNTIME140_1.dll，无法继续执行代码。重新安装程序可能会解决此问题。

解决步骤

- 步骤一：下载对应的dll文件（通过互联网搜索即可）
- 步骤二：拷贝到windows安装路径下的system32目录中
- 步骤三：执行命令注册对应dll文件
  - regsvr32 vcruntime140_1.dll

可视化客户端推荐：Robo 3T

Mongodb基础操作

- 新增：db.集合名称.insert/save/insertOne(文档)
- 修改：db.集合名称.remove(条件)
- 删除：db.集合名称.update(条件，{操作种类:{文档}})

基础查询

- 查询全部：db.集合.find()

- 查第一条：db.集合.findOne()

- 查询指定数量文档：db.集合.find().limit(10)  //查10条文档

- 跳过指定数量文档：db.集合.find().skip(20)  //跳过20条文档

- 统计：db.集合.count()

- 排序：db.集合.sort({age:1})  //按age升序排序

- 投影：db.集合名称.find(条件,{name:1,age:1})  //仅保留name与age域

条件查询

- 基本格式：db.集合.find({条件})

- 模糊查询：db.集合.find({域名:/正则表达式/})  //等同SQL中的like，比like强大，可以执行正则所有规则

- 条件比较运算：db.集合.find({域名:{$gt:值}})  //等同SQL中的数值比较操作，例如：name>18

- 包含查询：db.集合.find({域名:{$in:[值1，值2]}})  //等同于SQL中的in

- 条件连接查询：db.集合.find({$and:[{条件1},{条件2}]}) //等同于SQL中的and、or

SpringBoot整合MongoDB

1.导入Mongodb驱动

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

2.配置客户端

```yaml
spring:
  data:
    mongodb:
      uri: mongodb://localhost/itheima
```

3.客户端读写Mongodb

```Java
@SpringBootTest
class Springboot17MongodbApplicationTests {
    @Autowired
    private MongoTemplate mongoTemplate;

    @Test
    void contextLoads() {
        Book book = new Book();
        book.setId(2);
        book.setName("springboot2");
        book.setType("springboot2");
        book.setDescription("springboot2");
        mongoTemplate.save(book);
    }

    @Test
    void find() {
        List<Book> all = mongoTemplate.findAll(Book.class);
        System.out.println(all);
    }

}
```

SpringBoot整合Mongodb步骤

- 导入Mongodb对应的starter
- 配置mongodb访问uri
- 提供操作Mongodb接口对象MongoTemplate

**ElasticSearch（ES）**

Elasticsearch是一个分布式全文搜索引擎。

相关概念：索引、倒排索引、创建文档、使用文档。

Windows版ES下载：[https://](https://www.elastic.co/cn/downloads/elasticsearch)[www.elastic.co/cn/downloads/elasticsearch](https://www.elastic.co/cn/downloads/elasticsearch)

Windows版ES安装与启动：运行 elasticsearch.bat

基础操作

创建/查询/删除索引

- PUT http://localhost:9200/books
- GET http://localhost:9200/books
- DELETE http://localhost:9200/books

IK分词器

- 下载：https://github.com/medcl/elasticsearch-analysis-ik/releases

创建索引并指定规则

```JSON
{
    "mappings":{
        "properties":{
            "id":{
                "type":"keyword"
            },
            "name":{
                "type":"text",
                "analyzer":"ik_max_word",
                "copy_to":"all"
            },
            "type":{
                "type":"keyword"
            },
            "description":{
                "type":"text",
                "analyzer":"ik_max_word",
                "copy_to":"all"
            },
            "all":{
                "type":"text",
                "analyzer":"ik_max_word"
            }
        }
    }
}
```

基本操作

1.创建文档

```http
POST	http://localhost:9200/books/_doc		#使用系统生成id
POST	http://localhost:9200/books/_create/1		#使用指定id，
POST	http://localhost:9200/books/_doc/1		#使用指定id，不存在创建，存在更新（版本递增）
```

```JSON
{
    "name":"springboot very good",
    "type":"springboot",
    "description":"springboot very good"
}
```

2.查询文档

```http
GET	http://localhost:9200/books/_doc/1		 #查询单个文档 		
GET	http://localhost:9200/books/_search		 #查询全部文档
```

3.条件查询

```http
GET	http://localhost:9200/books/_search?q=name:springboot
```

4.删除文档

```http
DELETE	http://localhost:9200/books/_doc/1
```

5.修改文档（全量修改）

```http
PUT	http://localhost:9200/books/_doc/1
```

```JSON
{
    "name":"springboot",
    "type":"springboot",
    "description":"springboot"
}
```

6.修改文档（部分修改）

```http
POST	http://localhost:9200/books/_update/1
```

```JSON
{
    "doc":{
        "name":"springboot 非常好666"
    }
}
```

SpringBoot整合ES

1.导入坐标

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
</dependency>
```

2.配置

```yaml
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/test?serverTimezone=UTC
      username: root
      password: root
  elasticsearch:
    rest:
      uris: http://localhost:9200
```

3.客户端

```Java
@Autowired
private ElasticsearchRestTemplate template;
```

SpringBoot平台并没有跟随ES的更新速度进行同步更新，ES提供了High Level Client操作ES

导入操作

```XML
<dependency>
    <groupId>org.elasticsearch.client</groupId>
    <artifactId>elasticsearch-rest-high-level-client</artifactId>
</dependency>
```

配置（无）

客户端

```Java
@SpringBootTest
class Springboot18EsApplicationTests {
//    @Autowired
//    private ElasticsearchRestTemplate template;

    private RestHighLevelClient client;

    @BeforeEach
    void setUp() {
        HttpHost host = HttpHost.create("http://localhost:9200");
        RestClientBuilder builder = RestClient.builder(host);
        client = new RestHighLevelClient(builder);
    }

    @AfterEach
    void tearDown() throws IOException {
        client.close();
    }

//    @Test
//    void testCreateClient() throws IOException {
//        HttpHost host = HttpHost.create("http://localhost:9200");
//        RestClientBuilder builder = RestClient.builder(host);
//        client = new RestHighLevelClient(builder);
//        client.close();
//    }

    @Test
    void testCreateIndex() throws IOException {
        CreateIndexRequest request = new CreateIndexRequest("books");
        client.indices().create(request, RequestOptions.DEFAULT);
    }

}
```

创建索引

```Java
@Test
void testCreateIndexByIK() throws IOException {
    CreateIndexRequest request = new CreateIndexRequest("books");
    String json = "{\n" +
            "    \"mappings\":{\n" +
            "        \"properties\":{\n" +
            "            \"id\":{\n" +
            "                \"type\":\"keyword\"\n" +
            "            },\n" +
            "            \"name\":{\n" +
            "                \"type\":\"text\",\n" +
            "                \"analyzer\":\"ik_max_word\",\n" +
            "                \"copy_to\":\"all\"\n" +
            "            },\n" +
            "            \"type\":{\n" +
            "                \"type\":\"keyword\"\n" +
            "            },\n" +
            "            \"description\":{\n" +
            "                \"type\":\"text\",\n" +
            "                \"analyzer\":\"ik_max_word\",\n" +
            "                \"copy_to\":\"all\"\n" +
            "            },\n" +
            "            \"all\":{\n" +
            "                \"type\":\"text\",\n" +
            "                \"analyzer\":\"ik_max_word\"\n" +
            "            }\n" +
            "        }\n" +
            "    }\n" +
            "}";
    //设置请求中参数
    request.source(json, XContentType.JSON);
    client.indices().create(request, RequestOptions.DEFAULT);
}
```

添加文档

```Java
//添加文档
@Test
void testCreateDoc() throws IOException {
    Book book = bookDao.selectById(1);
    IndexRequest request = new IndexRequest("books").id(book.getId().toString());
    String json = JSON.toJSONString(book);
    request.source(json,XContentType.JSON);
    client.index(request,RequestOptions.DEFAULT);
}
```

批量添加文档

```Java
@Test
void testCreateDocAll() throws IOException {
    List<Book> bookList = bookDao.selectList(null);
    BulkRequest bulk = new BulkRequest();
    for (Book book : bookList) {
        IndexRequest request = new IndexRequest("books").id(book.getId().toString());
        String json = JSON.toJSONString(book);
        request.source(json,XContentType.JSON);
        bulk.add(request);
    }
    client.bulk(bulk,RequestOptions.DEFAULT);
}
```

按id查询文档

```Java
//按id查询
@Test
void testGet() throws IOException {
    GetRequest request = new GetRequest("books","1");
    GetResponse response = client.get(request, RequestOptions.DEFAULT);
    String json = response.getSourceAsString();
    System.out.println(json);
}
```

按条件查询文档

```Java
//按条件查询
@Test
void testSearch() throws IOException {
    SearchRequest request = new SearchRequest("books");

    SearchSourceBuilder builder = new SearchSourceBuilder();
    builder.query(QueryBuilders.termQuery("all","spring"));
    request.source(builder);

    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    SearchHits hits = response.getHits();
    for (SearchHit hit : hits) {
        String source = hit.getSourceAsString();
        //System.out.println(source);
        Book book = JSON.parseObject(source, Book.class);
        System.out.println(book);
    }
}
```

#### 2.2.5 整合第三方技术

**缓存**

缓存是一种介于数据永久存储介质与数据应用之间的数据临时存储介质。

使用缓存可以有效的减少低速数据读取过程的次数（例如磁盘IO），提高系统性能。

缓存不仅可以用于提高永久性存储介质的数据读取效率，还可以提供临时的数据存储空间。

SpringBoot提供了缓存技术，方便缓存使用。

**缓存使用**

- 启用缓存
- 设置进入缓存的数据
- 设置读取缓存的数据

1.导入缓存技术对应的starter

```XML
<!--cache-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

2.启用缓存

```Java
@SpringBootApplication
//开启缓存功能
@EnableCaching
public class Springboot19CacheApplication {

    public static void main(String[] args) {
        SpringApplication.run(Springboot19CacheApplication.class, args);
    }

}
```

3.设置当前操作的结果数据进入缓存

```Java
@Cacheable(value="cacheSpace",key="#id")
public Book getById(Integer id) {
    return bookDao.selectById(id);
}
```

SpringBoot提供的缓存技术除了提供默认的缓存方案，还可以对其他缓存技术进行整合，统一接口，方便缓存技术的开发与管理。

- Generic
- JCache
- ==Ehcache==
- Hazelcast
- Infinispan
- Couchbase
- ==Redis==
- Caffeine
- Simple（默认）
- ==memcached==

**缓存使用案例——手机验证码**

需求

- 输入手机号获取验证码，组织文档以短信形式发送给用户（页面模拟）
- 输入手机号和验证码验证结果

需求分析

- 提供controller，传入手机号，业务层通过手机号计算出独有的6位验证码数据，存入缓存后返回此数据
- 提供controller，传入手机号与验证码，业务层通过手机号从缓存中读取验证码与输入验证码进行比对，返回比对结果

1.开启缓存

2.业务层接口

```Java
public interface SMSCodeService {
    public String sendCodeToSMS(String tele);
    public boolean checkCode(SMSCode smsCode);
}
```

3.业务层设置获取验证码操作，并存储缓存，手机号为key，验证码为value

```Java
@Autowired
private CodeUtils codeUtils;

@Override
@CachePut(value = "smsCode",key="#tele")
public String sendCodeToSMS(String tele) {
    String code = codeUtils.generator(tele);
    return code;
}
```

4.业务层设置校验验证码操作，校验码通过缓存读取，返回校验结果

```Java
@Override
public boolean checkCode(SMSCode smsCode) {
    //取出内存中的验证码与传递过来的验证码比对，如果相同，返回true
    String code = smsCode.getCode();
    String cacheCode = codeUtils.get(smsCode.getTele());
    return code.equals(cacheCode);
}
```

生成获取验证码工具类

```Java
@Component
public class CodeUtils {

    private String [] patch = {"000000","00000","0000","000","00","0",""};

    public String generator(String tele){
        int hash = tele.hashCode();
        int encryption = 20206666;
        long result = hash ^ encryption;
        long nowTime = System.currentTimeMillis();
        result = result ^ nowTime;
        long code = result % 1000000;
        code = code < 0 ? -code : code;
        String codeStr = code + "";
        int len = codeStr.length();
        return patch[len] + codeStr;
    }

    @Cacheable(value = "smsCode",key="#tele")
    public String get(String tele){
        return null;
    }
}
```

**缓存供应商变更：Ehcache**

1.加入Ehcache坐标（缓存供应商实现）

```XML
<dependency>
    <groupId>net.sf.ehcache</groupId>
    <artifactId>ehcache</artifactId>
</dependency>
```

2.缓存设定为使用Ehcache

```yaml
spring:
  cache:
    type: ehcache
    ehcache:
      config: ehcache.xml
```

3.提供ehcache配置文件ehcache.xml

```XML
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
         updateCheck="false">
    <diskStore path="D:\ehcache" />

    <!--默认缓存策略 -->
    <!-- external：是否永久存在，设置为true则不会被清除，此时与timeout冲突，通常设置为false-->
    <!-- diskPersistent：是否启用磁盘持久化-->
    <!-- maxElementsInMemory：最大缓存数量-->
    <!-- overflowToDisk：超过最大缓存数量是否持久化到磁盘-->
    <!-- timeToIdleSeconds：最大不活动间隔，设置过长缓存容易溢出，设置过短无效果，可用于记录时效性数据，例如验证码-->
    <!-- timeToLiveSeconds：最大存活时间-->
    <!-- memoryStoreEvictionPolicy：缓存清除策略-->
    <defaultCache
        eternal="false"
        diskPersistent="false"
        maxElementsInMemory="1000"
        overflowToDisk="false"
        timeToIdleSeconds="60"
        timeToLiveSeconds="60"
        memoryStoreEvictionPolicy="LRU" />

    <cache
        name="smsCode"
        eternal="false"
        diskPersistent="false"
        maxElementsInMemory="1000"
        overflowToDisk="false"
        timeToIdleSeconds="10"
        timeToLiveSeconds="10"
        memoryStoreEvictionPolicy="LRU" />

</ehcache>
```

**缓存供应商变更：Redis**

1.加入Redis坐标（缓存供应商实现）

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

2.配置Redis服务器，缓存设定为使用Redis，并l设置Redis相关配置

```yaml
spring:
  cache:
    type: redis
    redis:
      use-key-prefix: false
      key-prefix: sms_
      cache-null-values: false
      time-to-live: 10s
  redis:
    host: localhost
    port: 6379
```

**缓存供应商变更：memcached**

下载memcached

- 地址：https://www.runoob.com/memcached/window-install-memcached.html

安装memcached

- 使用管理员身份运行cmd指令
- memcached.exe -d install

运行memcached

- 启动服务：memcached.exe -d start
- 停止服务：memcached.exe -d stop

memcached客户端选择

- Memcached Client for Java：最早期客户端，稳定可靠，用户群广
- SpyMemcached：效率更高
- Xmemcached：并发处理更好

SpringBoot未提供对memcached的整合，需要使用硬编码方式实现客户端初始化管理

1.加入Xmemcache坐标（缓存供应商实现）

```XML
<dependency>
    <groupId>com.googlecode.xmemcached</groupId>
    <artifactId>xmemcached</artifactId>
    <version>2.4.7</version>
</dependency>
```

2.配置memcached服务器必要属性

```yaml
memcached:
  servers: localhost:11211
  poolSize: 10
  opTimeout: 3000
```

3.创建读取属性配置信息类，加载配置

```Java
@Component
@ConfigurationProperties(prefix = "memcached")
@Data
public class XMemcachedProperties {
    private String servers;
    private int poolSize;
    private long opTimeout;
}
```

4.创建客户端配置类

```Java
@Configuration
public class XMemcachedConfig {

    @Autowired
    private XMemcachedProperties memcachedProperties;

    @Bean
    public MemcachedClient getMemcachedClient() throws IOException {
        MemcachedClientBuilder memcachedClientBuilder = new XMemcachedClientBuilder(memcachedProperties.getServers());
        memcachedClientBuilder.setConnectionPoolSize(memcachedProperties.getPoolSize());
        memcachedClientBuilder.setOpTimeout(memcachedProperties.getOpTimeout());
        MemcachedClient memcachedClient = memcachedClientBuilder.build();
        return memcachedClient;
    }
}
```

5.配置memcached属性

```Java
@Service
public class SMSCodeServiceImpl implements SMSCodeService {

    @Autowired
    private CodeUtils codeUtils;

    //以下是springboot中使用xmemcached
    @Autowired
    private MemcachedClient memcachedClient;

    @Override
    public String sendCodeToSMS(String tele) {
        String code = codeUtils.generator(tele);
        try {
            memcachedClient.set(tele,10,code);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return code;
    }

    @Override
    public boolean checkCode(SMSCode smsCode) {
        String code = null;
        try {
            code = memcachedClient.get(smsCode.getTele()).toString();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return smsCode.getCode().equals(code);
    }

}
```

**缓存供应商变更：jetcache**

jetCache对SpringCache进行了封装，在原有功能基础上实现了多级缓存、缓存统计、自动刷新、异步调用、数据报表等功能。

jetCache设定了本地缓存与远程缓存的多级缓存解决方案

- 本地缓存（local）
  - LinkedHashMap
  - Caffeine
- 远程缓存（remote）
  - Redis
  - Tair

1.加入jetcache坐标

```XML
<dependency>
    <groupId>com.alicp.jetcache</groupId>
    <artifactId>jetcache-starter-redis</artifactId>
    <version>2.6.2</version>
</dependency>
```

2.配置远程缓存必要属性

```yaml
jetcache:
  remote:
    default:
      type: redis
      host: localhost
      port: 6379
      keyConvertor: fastjson
      valueEncode: java
      valueDecode: java
      poolConfig:
        maxTotal: 50
    sms:
      type: redis
      host: localhost
      port: 6379
      poolConfig:
        maxTotal: 50
```

3.配置本地缓存必要属性

```yaml
jetcache:
  local:
    default:
      type: linkedhashmap
      keyConvertor: fastjson
```

4.配置属性说明

| 属性                                                      | 默认值 | 说明                                                         |
| :-------------------------------------------------------- | ------ | ------------------------------------------------------------ |
| jetcache.statIntervalMinutes                              | 0      | 统计间隔，0表示不统计                                        |
| jetcache.hiddenPackages                                   | 无     | 自动生成name时，隐藏指定的包名前缀                           |
| jetcache.[local\|remote].${area}.type                     | 无     | 缓存类型，本地支持linkedhashmap、caffeine，远程支持redis、tair |
| jetcache.[local\|remote].${area}.keyConvertor             | 无     | key转换器，当前仅支持fastjson                                |
| jetcache.[local\|remote].${area}.valueEncoder             | java   | 仅remote类型的缓存需要指定，可选java和kryo                   |
| jetcache.[local\|remote].${area}.valueDecoder             | java   | 仅remote类型的缓存需要指定，可选java和kryo                   |
| jetcache.[local\|remote].${area}.limit                    | 100    | 仅local类型的缓存需要指定，缓存实例最大元素数                |
| jetcache.[local\|remote].${area}.expireAfterWriteInMillis | 无穷大 | 默认过期时间，毫秒单位                                       |
| jetcache.local.${area}.expireAfterAccessInMillis          | 0      | 仅local类型的缓存有效，毫秒单位，最大不活动间隔              |

5.开启jetcache注解支持

```Java
@SpringBootApplication
//jetcache启用缓存的主开关
@EnableCreateCacheAnnotation
public class Springboot20JetCacheApplication {

    public static void main(String[] args) {
        SpringApplication.run(Springboot20JetCacheApplication.class, args);
    }

}
```

6.声明缓存对象并操作缓存

```Java
@Service
public class SMSCodeServiceImpl implements SMSCodeService {

    @Autowired
    private CodeUtils codeUtils;
    //remote
    //@CreateCache(area="sms",name="jetCache_",expire = 10,timeUnit = TimeUnit.SECONDS)

    @CreateCache(name="jetCache_",expire = 1000,timeUnit = TimeUnit.SECONDS,cacheType = CacheType.LOCAL)
    private Cache<String ,String> jetCache;

    @Override
    public String sendCodeToSMS(String tele) {
        String code = codeUtils.generator(tele);
        jetCache.put(tele,code);
        return code;
    }

    @Override
    public boolean checkCode(SMSCode smsCode) {
        String code = jetCache.get(smsCode.getTele());
        return smsCode.getCode().equals(code);
    }

}
```

启用方法注解

```Java
@SpringBootApplication
//jetcache启用缓存的主开关
@EnableCreateCacheAnnotation
//开启方法注解缓存
@EnableMethodCache(basePackages = "com.itheima")
public class Springboot20JetCacheApplication {

    public static void main(String[] args) {
        SpringApplication.run(Springboot20JetCacheApplication.class, args);
    }

}
```

使用方法注解操作缓存

```Java
@Service
public class BookServiceImpl implements BookService {

    @Autowired
    private BookDao bookDao;

    @Override
    @Cached(name="book_",key="#id",expire = 3600,cacheType = CacheType.REMOTE)
//    @CacheRefresh(refresh = 5)
    public Book getById(Integer id) {
        return bookDao.selectById(id);
    }

    @Override
    public boolean save(Book book) {
        return bookDao.insert(book) > 0;
    }

    @Override
    @CacheUpdate(name="book_",key="#book.id",value="#book")
    public boolean update(Book book) {
        return bookDao.updateById(book) > 0;
    }

    @Override
    @CacheInvalidate(name="book_",key = "#id")
    public boolean delete(Integer id) {
        return bookDao.deleteById(id) > 0;
    }

    @Override
    public List<Book> getAll() {
        return bookDao.selectList(null);
    }
}
```

缓存对象必须保障可序列化

```Java
@Data
public class Book implements Serializable {
    private Integer id;
    private String type;
    private String name;
    private String description;
}
```

```yaml
jetcache:
  #查看缓存统计报告
  statIntervalMinutes: 1
  local:
    default:
      type: linkedhashmap
      keyConvertor: fastjson
  remote:
    default:
      type: redis
      host: localhost
      port: 6379
      keyConvertor: fastjson
      valueEncode: java
      valueDecode: java
      poolConfig:
        maxTotal: 50
    sms:
      type: redis
      host: localhost
      port: 6379
      poolConfig:
        maxTotal: 50
```

**缓存供应商变更：j2cache**

j2cache是一个缓存整合框架，可以提供缓存的整合方案，使各种缓存搭配使用，自身不提供缓存功能

基于 ehcache + redis 进行整合

1.加入j2cache坐标，加入整合缓存的坐标

```XML
<dependency>
    <groupId>net.oschina.j2cache</groupId>
    <artifactId>j2cache-core</artifactId>
    <version>2.8.4-release</version>
</dependency>

<dependency>
    <groupId>net.oschina.j2cache</groupId>
    <artifactId>j2cache-spring-boot2-starter</artifactId>
    <version>2.8.0-release</version>
</dependency>

<dependency>
    <groupId>net.sf.ehcache</groupId>
    <artifactId>ehcache</artifactId>
</dependency>
```

2.配置使用j2cache（application.yml）

```yaml
server:
  port: 80

j2cache:
  config-location: j2cache.properties
```

3.配置一级缓存与二级缓存以及一级缓存数据到二级缓存的发送方式（j2cache.properties）

```Properties
# 1级缓存
j2cache.L1.provider_class = ehcache
ehcache.configXml = ehcache.xml

# 设置是否启用二级缓存
j2cache.l2-cache-open = false

# 2级缓存
j2cache.L2.provider_class = net.oschina.j2cache.cache.support.redis.SpringRedisProvider
j2cache.L2.config_section = redis
redis.hosts = localhost:6379

# 1级缓存中的数据如何到达二级缓存
j2cache.broadcast = net.oschina.j2cache.cache.support.redis.SpringRedisPubSubPolicy

redis.mode = single

redis.namespace = j2cache
```

4.设置使用缓存

```Java
@Service
public class SMSCodeServiceImpl implements SMSCodeService {

    @Autowired
    private CodeUtils codeUtils;

    @Autowired
    private CacheChannel cacheChannel;

    @Override
    public String sendCodeToSMS(String tele) {
        String code = codeUtils.generator(tele);
        cacheChannel.set("sms",tele,code);
        return code;
    }

    @Override
    public boolean checkCode(SMSCode smsCode) {
        String code = cacheChannel.get("sms",smsCode.getTele()).asString();
        return smsCode.getCode().equals(code);
    }

}
```

**任务**

定时任务是企业级应用中的常见操作

- 年度报表
- 缓存统计报告
- ......

市面上流行的定时任务技术

- Quartz
- Spring Task

**SpringBoot整合Quartz**

相关概念

- 工作（Job）：用于定义具体执行的工作
- 工作明细（JobDetail）：用于描述定时工作相关的信息
- 触发器（Trigger）：用于描述触发工作的规则，通常使用cron表达式定义调度规则
- 调度器（Scheduler）：描述了工作明细与触发器的对应关系

1.导入SpringBoot整合quartz的坐标

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-quartz</artifactId>
</dependency>
```

2.定义具体要执行的任务，继承QuartzJobBean

```Java
public class MyQuratz extends QuartzJobBean {
    @Override
    protected void executeInternal(JobExecutionContext jobExecutionContext) throws JobExecutionException {
        System.out.println("quartz task run...");
    }
}
```

3.定义工作明细与触发器，并绑定对应关系

```Java
@Configuration
public class QuartzConfig {
    @Bean
    public JobDetail printJobDetail() {
        //绑定具体的工作
        return JobBuilder.newJob(MyQuratz.class).storeDurably().build();
    }

    @Bean
    public Trigger printJobTrigger() {
        ScheduleBuilder schedBuilder = CronScheduleBuilder.cronSchedule("0/5 * * * * ?");
        //绑定对应的工作明细
        return TriggerBuilder.newTrigger().forJob(printJobDetail()).withSchedule(schedBuilder).build();
    }
}
```

**Spring Task**

开启定时任务功能

```Java
@SpringBootApplication
//开启定时任务功能
@EnableScheduling
public class Springboot22TaskApplication {

    public static void main(String[] args) {
        SpringApplication.run(Springboot22TaskApplication.class, args);
    }

}
```

设置定时执行的任务，并设定执行周期

```Java
@Component
public class MyBean {
    @Scheduled(cron = "0/1 * * * * ?")
    public void print() {
        System.out.println(Thread.currentThread().getName() + ": spring task run...");
    }
}
```

定时任务相关配置

```yaml
spring:
  task:
    scheduling:
      # 任务调度线程池大小 默认 1
	  pool:
	    size: 1
	  # 调度线程名称前缀 默认 scheduling-
	  thread-name-prefix: ssm_
	  shutdown:
		# 线程池关闭时等待所有任务完成
		await-termination: false
		# 调度线程关闭前最大等待时间，确保最后一定关闭
		await-termination-period: 10s
```

Spring Task相关注解

- EnableScheduling
- Scheduled

**邮件**

**SpringBoot整合JavaMail**

SMTP（Simple Mail Transfer Protocol）：简单邮件传输协议，用于==发送==电子邮件的传输协议。

POP3（Post Office Protocol - Version 3）：用于==接收==电子邮件的标准协议。

IMAP（Internet Mail Access Protocol）：互联网消息协议，是POP3的替代协议。

1.导入SpringBoot整合JavaMail的坐标

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

2.配置JavaMail

```yaml
spring:
  mail:
    host: smtp.163.com
    username: ******@163.com
    password: ******
```

3.开启定时任务功能

```Java
@Service
public class SendMailServiceImpl implements SendMailService {
    @Autowired
    private JavaMailSender javaMailSender;

    //发送人
    private String from = "******@163.com";
    //接收人
    private String to = "******@qq.com";
    //标题
    private String subject = "测试邮件";
    //正文
    private String context = "测试邮件正文内容";

    @Override
    public void sendMail() {
        SimpleMailMessage message = new SimpleMailMessage();
        message.setFrom(from+"(小甜甜)");
        message.setTo(to);
        message.setSubject(subject);
        message.setText(context);
        javaMailSender.send(message);
    }
}
```

4.附件与HTML文本支持

```Java
@Service
public class SendMailServiceImpl2 implements SendMailService {
    @Autowired
    private JavaMailSender javaMailSender;

    //发送人
    private String from = "******@163.com";
    //接收人
    private String to = "******@qq.com";
    //标题
    private String subject = "测试邮件";
    //正文
    private String context = "<img src='https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fbkimg.cdn.bcebos.com%2Fpic%2F8326cffc1e178a82b9018131e84f648da97739124247&refer=http%3A%2F%2Fbkimg.cdn.bcebos.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1651889662&t=a959d1a3131f959cd79359d7d2c2c115'/><a href='https://www.baidu.com'>点开有惊喜</a>";

    @Override
    public void sendMail() {
        try {
            MimeMessage message = javaMailSender.createMimeMessage();
            MimeMessageHelper helper = new MimeMessageHelper(message,true);
            helper.setFrom(from+"(小甜甜)");
            helper.setTo(to);
            helper.setSubject(subject);
            helper.setText(context,true);
            //添加附件
            File file1 = new File("F:\\JavaPros\\springboot\\springboot_23_mail\\target\\springboot_23_mail-0.0.1-SNAPSHOT.jar");
            File file2 = new File("F:\\JavaPros\\springboot\\springboot_23_mail\\src\\main\\resources\\MyImages2.jpg");

            helper.addAttachment(file1.getName(),file1);
            helper.addAttachment("发送附件图片.jpg",file2);

            javaMailSender.send(message);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**消息**

消息发送方：生产者

消息接收方：消费者

消息类型

- 同步消息
- 异步消息

企业级应用中广泛使用的三种异步消息传递技术

- JMS
- AMQP
- MQTT

JMS（Java Message Service）：一个规范，等同于JDBC规范，提供了与消息服务相关的API接口

JMS消息模型

- peer-2-peer：点对点模型，消息发送到一个队列中，队列保存消息。队列的消息只能被一个消费者消费，或超时
- publish-subscribe：发布订阅模型，消息可以被多个消费者消费，生产者和消费者完全独立，不需要感知对方的存在

JMS消息种类

- TextMessage
- MapMessage
- ==BytesMessage==
- StreamMessage
- ObjectMessage
- Message（只有消息头和属性）

JMS实现：ActiveMQ、Redis、HornetMQ、RabbitMQ、RocketMQ（没有完全遵守JMS规范）

AMQP（advanced message queuing protocol）：一种协议（高级消息队列协议，也是消息代理规范），规范了网络交换的数据格式，兼容JMS

优点：具有跨平台性，服务器供应商，生产者，消费者可以使用不同的语言来实现

AMQP消息模型

- direct exchange
- fanout exchange
- topic exchange
- headers exchange
- system exchange

AMQP消息种类：byte[]

AMQP实现：RabbitMQ、StormMQ、RocketMQ

MQTT（Message Queueing Telemetry Transport）消息队列遥测传输，专为小设备设计，是物联网（IOT）生态系统中主要成分之一

Kafka，一种高吞吐量的分布式发布订阅消息系统，提供实时消息功能

消息案例——订单短信通知

**ActiveMQ**

下载地址：[https://activemq.apache.org/components/classic/download](https://activemq.apache.org/components/classic/download/)[/](https://activemq.apache.org/components/classic/download/)

安装：解压缩

启动服务：activemq.bat

访问服务器：http://127.0.0.1:8161/

- 服务端口：61616，管理后台端口：8161
- 用户名&密码：admin

**SpringBoot整合ActiveMQ**

1.导入SpringBoot整合ActiveMQ坐标

```XML
<!--activemq-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-activemq</artifactId>
</dependency>
```

2.配置ActiveMQ（采用默认配置）

```yaml
spring:
  activemq:
    broker-url: tcp://localhost:61616
  jms:
    pub-sub-domain: true
    template:
      default-destination: itheima
```

3.生产与消费消息（指定消息存储队列）

```Java
@Service
public class MessageServiceActivemqImpl implements MessageService {
    @Autowired
    private JmsMessagingTemplate messagingTemplate;

    @Override
    public void sendMessage(String id) {
        System.out.println("待发送短信的订单已纳入处理队列，id：" + id);
        messagingTemplate.convertAndSend("order.queue.id",id);
    }

    @Override
    public String doMessage() {
        String id = messagingTemplate.receiveAndConvert("order.queue.id",String.class);
        System.out.println("已完成短信发送业务，id：" + id);
        return id;
    }
}
```

4.使用消息监听器对消息队列监听，使用@SendTo确保流程性业务消息消费完转入下一个消息队列

```Java
@Component
public class MessageListener {
    @JmsListener(destination = "order.queue.id")
    @SendTo("order.other.queue.id")
    public String receive(String id) {
        System.out.println("已完成短信发送业务，id：" + id);
        return "new:" + id;
    }
}
```

**RabbitMQ**

RabbitMQ基于Erlang语言编写，需要安装Erlang

Erlang

- 下载地址：[https](https://www.erlang.org/downloads)[://www.erlang.org/downloads](https://www.erlang.org/downloads)
- 安装：一键傻瓜式安装，安装完毕需要重启，需要依赖Windows组件
- 环境变量配置
  - ERLANG_HOME
  - PATH

RabbitMQ

- 下载地址：[https://](https://rabbitmq.com/install-windows.html)[rabbitmq.com/install-windows.html](https://rabbitmq.com/install-windows.html)
- 安装：一键傻瓜式安装
- 启动服务：rabbitmq-service.bat start
- 关闭服务：rabbitmq-service.bat stop
- 查看服务状态：rabbitmqctl status
- 服务管理可视化（插件形式）
- 查看已安装的插件列表：rabbitmq-plugins.bat list
- 开启服务管理插件：rabbitmq-plugins.bat enable rabbitmq_management
- 访问服务器：http://localhost:15672
  - 服务端口：5672，管理后台端口：15672
  - 用户名&密码：guest

**SpringBoot整合RabbitMQ**

==直连交换机模式==

1.导入SpringBoot整合RabbitMQ坐标

```XML
<!--rabbitmq-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

2.配置RabbitMQ （采用默认配置）

```yaml
spring:
  rabbitmq:
    host: localhost
    port: 5672
```

3.定义消息队列(direct)

```Java
@Configuration
public class RabbitConfigDirect {
    @Bean
    public Queue directQueue() {
        return new Queue("direct_queue");
    }

    @Bean
    public Queue directQueue2() {
        return new Queue("direct_queue2");
    }

    @Bean
    public DirectExchange directExchange() {
        return new DirectExchange("directExchange");
    }

    @Bean
    public Binding bindingDirect() {
        return BindingBuilder.bind(directQueue()).to(directExchange()).with("direct");
    }

    @Bean
    public Binding bindingDirect2() {
        return BindingBuilder.bind(directQueue2()).to(directExchange()).with("direct2");
    }
}
```

4.生产与消费消息(direct)

```Java
@Service
public class MessageServiceRabbitmqDirectImpl implements MessageService {
    @Autowired
    private AmqpTemplate amqpTemplate;

    @Override
    public void sendMessage(String id) {
        System.out.println("待发送短信的订单已纳入处理队列(rabbitmq direct)，id：" + id);
        amqpTemplate.convertAndSend("directExchange","direct",id);
    }

    @Override
    public String doMessage() {
        return null;
    }
}
```

5.使用消息监听器对消息队列监听(direct)

```Java
@Component
public class MessageListener {
    @RabbitListener(queues = "direct_queue")
    public void receive(String id) {
        System.out.println("已完成短信发送业务(rabbitmq direct)，id：" + id);
    }
}
```

6.使用多消息监听器对消息队列监听进行消息轮循处理(direct)

```Java
@Component
public class MessageListener2 {
    @RabbitListener(queues = "direct_queue")
    public void receive(String id) {
        System.out.println("已完成短信发送业务(rabbitmq direct two)，id：" + id);
    }
}
```

==主题交换机模式==

1.定义消息队列(topic)

```Java
@Configuration
public class RabbitConfigTopic {
    @Bean
    public Queue topicQueue() {
        return new Queue("topic_queue");
    }

    @Bean
    public Queue topicQueue2() {
        return new Queue("topic_queue2");
    }

    @Bean
    public TopicExchange topicExchange() {
        return new TopicExchange("topicExchange");
    }

    @Bean
    public Binding bindingTopic() {
        return BindingBuilder.bind(topicQueue()).to(topicExchange()).with("topic.*.id");
    }

    @Bean
    public Binding bindingTopic2() {
        return BindingBuilder.bind(topicQueue2()).to(topicExchange()).with("topic.orders.*");
    }
}
```

2.绑定键匹配规则

- \* (星号)： 用来表示一个单词 ，且该单词是必须出现的
- \# (井号)： 用来表示任意数量

|    **匹配键**     | **topic.\*.\*** | **topic.#** |
| :---------------: | :-------------: | :---------: |
|  topic.order.id   |      true       |    true     |
|  order.topic.id   |      false      |    false    |
| topic.sm.order.id |      false      |    true     |
|    topic.sm.id    |      false      |    true     |
|  topic.id.order   |      true       |    true     |
|     topic.id      |      false      |    true     |
|    topic.order    |      false      |    true     |

3.生产与消费消息(topic)

```Java
@Service
public class MessageServiceRabbitmqTopicImpl implements MessageService {
    @Autowired
    private AmqpTemplate amqpTemplate;

    @Override
    public void sendMessage(String id) {
        System.out.println("待发送短信的订单已纳入处理队列(rabbitmq topic)，id：" + id);
        amqpTemplate.convertAndSend("topicExchange","topic.orders.id",id);
    }

    @Override
    public String doMessage() {
        return null;
    }
}
```

4.使用消息监听器对消息队列监听(topic)

```Java
@Component
public class MessageListener {
    @RabbitListener(queues = "topic_queue")
    public void receive(String id) {
        System.out.println("已完成短信发送业务(rabbitmq topic 1)，id：" + id);
    }

    @RabbitListener(queues = "topic_queue2")
    public void receive2(String id) {
        System.out.println("已完成短信发送业务(rabbitmq topic 222)，id：" + id);
    }
}
```

**RocketMQ**

下载地址：[https://rocketmq.apache.org](https://rocketmq.apache.org/)[/](https://rocketmq.apache.org/)

安装：解压缩

- 默认服务端口：9876

环境变量配置

- ROCKETMQ_HOME
- PATH
- NAMESRV_ADDR （建议）：127.0.0.1:9876

启动命名服务器：mqnamesrv

启动broker：mqbroker

服务器功能测试：生产者

- tools org.apache.rocketmq.example.quickstart.Producer

服务器功能测试：消费者

- tools org.apache.rocketmq.example.quickstart.Consumer

**SpringBoot整合RocketMQ**

1.导入SpringBoot整合RocketMQ坐标

```XML
<!--rocketmq-->
<dependency>
    <groupId>org.apache.rocketmq</groupId>
    <artifactId>rocketmq-spring-boot-starter</artifactId>
    <version>2.2.1</version>
</dependency>
```

2.配置RocketMQ （采用默认配置）

```yaml
rocketmq:
  name-server: localhost:9876
  producer:
    group: group_rocketmq
```

3.生产消息

```Java
@Service
public class MessageServiceRocketmqImpl implements MessageService {
    @Autowired
    private RocketMQTemplate rocketMQTemplate;

    @Override
    public void sendMessage(String id) {
        System.out.println("待发送短信的订单已纳入处理队列(rocketmq)，id：" + id);
        rocketMQTemplate.convertAndSend("order_id",id);
    }

    @Override
    public String doMessage() {
        return null;
    }
}
```

4.生产异步消息

```Java
@Service
public class MessageServiceRocketmqImpl implements MessageService {
    @Autowired
    private RocketMQTemplate rocketMQTemplate;

    @Override
    public void sendMessage(String id) {
        System.out.println("待发送短信的订单已纳入处理队列(rocketmq)，id：" + id);
        //rocketMQTemplate.convertAndSend("order_id",id);
        SendCallback callback = new SendCallback() {
            @Override
            public void onSuccess(SendResult sendResult) {
                System.out.println("消息发送成功");
            }

            @Override
            public void onException(Throwable throwable) {
                System.out.println("消息发送失败");
            }
        };
        rocketMQTemplate.asyncSend("order_id",id,callback);
    }

    @Override
    public String doMessage() {
        return null;
    }
}
```

5.使用消息监听器对消息队列监听

```Java
@Component
@RocketMQMessageListener(topic = "order_id",consumerGroup = "group_rocketmq")
public class MessageListener implements RocketMQListener<String> {
    @Override
    public void onMessage(String id) {
        System.out.println("已完成短信发送业务(rocketmq)，id：" + id);
    }
}
```

**Kafka**

下载地址：[https://](https://kafka.apache.org/downloads)[kafka.apache.org/downloads](https://kafka.apache.org/downloads)

- windows 系统下3.0.0版本存在BUG，建议使用2.X版本

安装：解压缩

启动zookeeper

- zookeeper-server-start.bat ..\\..\config\zookeeper.properties
- 默认端口：2181

启动kafka

- kafka-server-start.bat ..\\..\config\server.properties
- 默认端口：9092

创建topic

- kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic itheima

查看topic

- kafka-topics.bat --zookeeper 127.0.0.1:2181 --list

删除topic

- kafka-topics.bat --delete --zookeeper localhost:2181 --topic itheima

生产者功能测试

- kafka-console-producer.bat --broker-list localhost:9092 --topic itheima

消费者功能测试

- kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic itheima --from-beginning

**SpringBoot整合Kafka**

1.导入SpringBoot整合Kafka坐标

```XML
<!--kafka-->
<dependency>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>spring-kafka</artifactId>
</dependency>
```

2.配置Kafka （采用默认配置）

```yaml
spring:
  kafka:
    bootstrap-servers: localhost:9092
    consumer:
      group-id: order
```

3.生产消息

```Java
@Service
public class MessageServiceKafkaImpl implements MessageService {
    @Autowired
    private KafkaTemplate<String,String> kafkaTemplate;

    @Override
    public void sendMessage(String id) {
        System.out.println("待发送短信的订单已纳入处理队列(kafka)，id：" + id);
        kafkaTemplate.send("itheima2022",id);
    }

    @Override
    public String doMessage() {
        return null;
    }
}
```

4.使用消息监听器对消息队列监听

```Java
@Component
public class MessageListener {
    @KafkaListener(topics = "itheima2022")
    public void onMessage(ConsumerRecord<String,String> record) {
        System.out.println("已完成短信发送业务(kafka)，id：" + record.value());
    }
}
```

#### 2.2.6 监控

**监控的意义**

- 监控服务状态是否宕机
- 监控服务运行指标（内存、虚拟机、线程、请求等）
- 监控日志
- 管理服务（服务下线）

监控的实施方式

- 显示监控信息的服务器：用于获取服务信息，并显示对应的信息
- 运行的服务：启动时主动上报，告知监控服务器自己需要受到监控

**可视化监控平台**

Spring Boot Admin，开源社区项目，用于管理和监控SpringBoot应用程序。 客户端注册到服务端后，通过HTTP请求方式，服务端定期从客户端获取对应的信息，并通过UI界面展示对应信息。

Admin服务端

```XML
<properties>
    <spring-boot-admin.version>2.5.4</spring-boot-admin.version>
</properties>
<dependencies>
    <dependency>
        <groupId>de.codecentric</groupId>
        <artifactId>spring-boot-admin-starter-server</artifactId>
    </dependency>
</dependencies>
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>de.codecentric</groupId>
            <artifactId>spring-boot-admin-dependencies</artifactId>
            <version>${spring-boot-admin.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

Admin客户端

```XML
<properties>
    <spring-boot-admin.version>2.5.4</spring-boot-admin.version>
</properties>
<dependencies>
    <dependency>
        <groupId>de.codecentric</groupId>
        <artifactId>spring-boot-admin-starter-client</artifactId>
    </dependency>
</dependencies>
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>de.codecentric</groupId>
            <artifactId>spring-boot-admin-dependencies</artifactId>
            <version>${spring-boot-admin.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

Admin服务端(精简)

```XML
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-server</artifactId>
    <version>2.5.4</version>
</dependency>
```

Admin客户端(精简)

```XML
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-client</artifactId>
    <version>2.5.4</version>
</dependency>
```

Admin服务端

```yaml
server:
  port: 8080
```

设置启用Spring-Admin

```Java
@SpringBootApplication
@EnableAdminServer
public class Springboot25AdminServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(Springboot25AdminServerApplication.class, args);
    }

}
```

Admin客户端

```yaml
server:
  port: 80

spring:
  boot:
    admin:
      client:
        url: http://localhost:8080
management:
  endpoint:
    health:
      show-details: always
  endpoints:
    web:
      exposure:
        include: "*"
```

**监控原理**

- Actuator提供了SpringBoot生产就绪功能，通过端点的配置与访问，获取端点信息
- 端点描述了一组监控信息，SpringBoot提供了多个内置端点，也可以根据需要自定义端点信息
- 访问当前应用所有端点信息：/actuator
- 访问端点详细信息：/actuator/端点名称

| **ID**               | **描述**                                                     | **默认启用** |
| -------------------- | ------------------------------------------------------------ | ------------ |
| **auditevents**      | 暴露当前应用程序的审计事件信息。                             | 是           |
| **beans**            | 显示应用程序中所有  Spring bean 的完整列表。                 | 是           |
| **caches**           | 暴露可用的缓存。                                             | 是           |
| **conditions**       | 显示在配置和自动配置类上评估的条件以及它们匹配或不匹配的原因。 | 是           |
| **configprops**      | 显示所有 @ConfigurationProperties 的校对清单。               | 是           |
| **env**              | 暴露  Spring ConfigurableEnvironment 中的属性。              | 是           |
| **flyway**           | 显示已应用的  Flyway 数据库迁移。                            | 是           |
| **health**           | 显示应用程序健康信息                                         | 是           |
| **httptrace**        | 显示  HTTP 追踪信息（默认情况下，最后  100 个  HTTP 请求/响应交换）。 | 是           |
| **info**             | 显示应用程序信息。                                           | 是           |
| **integrationgraph** | 显示  Spring Integration 图。                                | 是           |
| **loggers**          | 显示和修改应用程序中日志记录器的配置。                       | 是           |
| **liquibase**        | 显示已应用的  Liquibase 数据库迁移。                         | 是           |
| **metrics**          | 显示当前应用程序的指标度量信息。                             | 是           |
| **mappings**         | 显示所有 @RequestMapping 路径的整理清单。                    | 是           |
| **scheduledtasks**   | 显示应用程序中的调度任务。                                   | 是           |
| **sessions**         | 允许从 Spring Session 支持的会话存储中检索和删除用户会话。当使用 Spring Session 的响应式 Web 应用程序支持时不可用。 | 是           |
| **shutdown**         | 正常关闭应用程序。                                           | 否           |
| **threaddump**       | 执行线程 dump。                                              | 是           |

Web程序专用端点

| **ID**         | **描述**                                                     | **默认启用** |
| -------------- | ------------------------------------------------------------ | ------------ |
| **heapdump**   | 返回一个 hprof 堆  dump 文件。                               | 是           |
| **jolokia**    | 通过  HTTP 暴露  JMX bean（当  Jolokia 在  classpath 上时，不适用于  WebFlux）。 | 是           |
| **logfile**    | 返回日志文件的内容（如果已设置 logging.file 或 logging.path 属性）。支持使用  HTTP Range 头来检索部分日志文件的内容。 | 是           |
| **prometheus** | 以可以由  Prometheus 服务器抓取的格式暴露指标。              | 是           |

启用指定端点

```yaml
management:
  endpoint:
    health:  #端点名称
      show-details: always
    info:    #端点名称
      enabled: true
```

启用所有端点

```yaml
management:
  endpoints:
    enabled-by-default: true
```

暴露端点功能

- 端点中包含的信息存在敏感信息，需要对外暴露端点功能时手动设定指定端点信息

| **属性**                                      | **默认**     |
| --------------------------------------------- | ------------ |
| **management.endpoints.jmx.exposure.exclude** |              |
| **management.endpoints.jmx.exposure.include** | *            |
| **management.endpoints.web.exposure.exclude** |              |
| **management.endpoints.web.exposure.include** | info, health |

暴露端点功能

| **ID**               | **JMX** | **Web** |
| -------------------- | ------- | ------- |
| **auditevents**      | 是      | 否      |
| **beans**            | 是      | 否      |
| **caches**           | 是      | 否      |
| **conditions**       | 是      | 否      |
| **configprops**      | 是      | 否      |
| **env**              | 是      | 否      |
| **flyway**           | 是      | 否      |
| **health**           | 是      | 是      |
| **heapdump**         | N/A     | 否      |
| **httptrace**        | 是      | 否      |
| **info**             | 是      | 是      |
| **integrationgraph** | 是      | 否      |
| **jolokia**          | N/A     | 否      |
| **logfile**          | N/A     | 否      |
| **loggers**          | 是      | 否      |
| **liquibase**        | 是      | 否      |
| **metrics**          | 是      | 否      |
| **mappings**         | 是      | 否      |
| **prometheus**       | N/A     | 否      |
| **scheduledtasks**   | 是      | 否      |
| **sessions**         | 是      | 否      |
| **shutdown**         | 是      | 否      |
| **threaddump**       | 是      | 否      |

**自定义监控指标**

为info端点添加自定义指标

```yaml
info:
  appName: @project.artifactId@
  version: @project.version@
  company: 监控教程
  author: itheima
```

```Java
@Component
public class InfoConfig implements InfoContributor {
    @Override
    public void contribute(Info.Builder builder) {
        builder.withDetail("runTime",System.currentTimeMillis());
        Map infoMap = new HashMap();
        infoMap.put("buildTime","2006");
        builder.withDetails(infoMap);
    }
}
```

为Health端点添加自定义指标

```Java
@Component
public class HealthConfig extends AbstractHealthIndicator {
    @Override
    protected void doHealthCheck(Health.Builder builder) throws Exception {
        boolean condition = false;
        if (condition) {
            builder.status(Status.UP);
            builder.withDetail("runTime",System.currentTimeMillis());
            Map infoMap = new HashMap();
            infoMap.put("buildTime","2006");
            builder.withDetails(infoMap);
            //builder.up();
        } else {
            builder.status(Status.OUT_OF_SERVICE);
            builder.withDetail("上线了吗？","你做梦");
            //builder.down();
        }
    }
}
```

为Metrics端点添加自定义指标

```Java
@Service
public class BookServiceImpl extends ServiceImpl<BookDao, Book> implements IBookService {
    @Autowired
    private BookDao bookDao;

    private Counter counter;
    public BookServiceImpl(MeterRegistry meterRegistry) {
        counter = meterRegistry.counter("用户付费操作次数: ");
    }

    @Override
    public boolean delete(Integer id) {
        //每次执行删除业务等同于执行了付费业务
        counter.increment();
        return bookDao.deleteById(id) > 0;
    }
}
```

自定义端点

```Java
@Component
@Endpoint(id = "pay",enableByDefault = true)
public class PayEndpoint {
    @ReadOperation
    public Object getPay() {
        Map payMap = new HashMap();
        payMap.put("level 1","300");
        payMap.put("level 2","291");
        payMap.put("level 3","666");
        return payMap;
    }
}
```

## 3. SpringBoot原理篇

### 3.1 自动配置

#### 3.1.1 bean加载方式

bean的加载方式（一）

- XML方式声明bean

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--xml方式声明自己开发的bean-->
    <bean id="cat" class="com.itheima.bean.Cat"/>
    <bean class="com.itheima.bean.Dog"/>

    <!--xml方式声明第三方开发的bean-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"/>
    <bean class="com.alibaba.druid.pool.DruidDataSource"/>
</beans>
```

bean的加载方式（二）

- XML+注解方式声明bean

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd
    ">

    <!--指定加载bean的位置，component-->
    <context:component-scan base-package="com.itheima.bean,com.itheima.config"/>
</beans>
```

- 使用@Component及其衍生注解@Controller 、@Service、@Repository定义bean

```Java
@Component("tom")
public class Cat {
}
```

- 使用@Bean定义第三方bean，并将所在类定义为配置类或Bean

```Java
//@Component
@Configuration
public class DbConfig {
    @Bean
    public DruidDataSource dataSource() {
        DruidDataSource ds = new DruidDataSource();
        return ds;
    }
}
```

bean的加载方式（三）

- 注解方式声明配置类

```Java
@ComponentScan({"com.itheima.bean","com.itheima.config"})
public class SpringConfig3 {
}
```

- @Configuration配置项如果不用于被扫描可以省略

bean的加载方式——扩展1

- 初始化实现FactoryBean接口的类，实现对bean加载到容器之前的批处理操作

```Java
public class DogFactoryBean implements FactoryBean<Dog> {
    @Override
    public Dog getObject() throws Exception {
        Dog d = new Dog();
        //........
        return d;
    }

    @Override
    public Class<?> getObjectType() {
        return Dog.class;
    }

    @Override
    public boolean isSingleton() {
        return FactoryBean.super.isSingleton();
    }
}
```

```Java
@ComponentScan({"com.itheima.bean","com.itheima.config"})
public class SpringConfig3 {
    @Bean
    public DogFactoryBean dog() {
        return new DogFactoryBean();
    }
}
```

bean的加载方式——扩展2

- 加载配置类并加载配置文件（系统迁移）

```Java
@ImportResource("applicationContext1.xml")
public class SpringConfig32 {
}
```

bean的加载方式——扩展3

- 使用proxyBeanMethods=true可以保障调用此方法得到的对象是从容器中获取的而不是重新创建的

```Java
@Configuration(proxyBeanMethods = true)
public class SpringConfig33 {
    @Bean
    public Cat cat() {
        return new Cat();
    }
}
```

```Java
public class App33 {
    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig33.class);
        String[] names = ctx.getBeanDefinitionNames();
        for (String name : names) {
            System.out.println(name);
        }
        System.out.println("-----------------------------");
        SpringConfig33 springConfig33 = ctx.getBean("springConfig33", SpringConfig33.class);
        System.out.println(springConfig33.cat());
        System.out.println(springConfig33.cat());
        System.out.println(springConfig33.cat());
    }
}
```

bean的加载方式（四）

- 使用@Import注解导入要注入的bean对应的字节码

```Java
@Import({Dog.class})
public class SpringConfig4 {
}
```

- 被导入的bean无需使用注解声明为bean

```Java
public class Dog {
}
```

- 此形式可以有效的降低源代码与Spring技术的耦合度，在spring技术底层及诸多框架的整合中大量使用
- 使用@Import注解导入配置类

```Java
@Import({Dog.class,DbConfig.class})
public class SpringConfig4 {
}
```

bean的加载方式（五）

- 使用上下文对象在容器初始化完毕后注入bean

```Java
public class App5 {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig4.class);
        //上下文容器对象已经初始化完毕后，手工加载bean
        ctx.registerBean("tom", Cat.class,0);
        ctx.registerBean("tom", Cat.class,1);
        ctx.registerBean("tom", Cat.class,2);
        ctx.register(Mouse.class);
        String[] names = ctx.getBeanDefinitionNames();
        for (String name : names) {
            System.out.println(name);
        }
        System.out.println("--------------------");
        System.out.println(ctx.getBean(Cat.class));
    }
}
```

bean的加载方式（六）

- 导入实现了ImportSelector接口的类，实现对导入源的编程式处理

```Java
public class MyImportSelector implements ImportSelector {
    @Override
    public String[] selectImports(AnnotationMetadata metadata) {
//        System.out.println("=========================");
//        System.out.println("提示：" + metadata.getClassName());
//        System.out.println(metadata.hasAnnotation("org.springframework.context.annotation.Configuration"));
//        Map<String, Object> attributes = metadata.getAnnotationAttributes("org.springframework.context.annotation.ComponentScan");
//        System.out.println(attributes);
//        System.out.println("=========================");

        //各种条件的判定，判定完毕后，决定是否装载指定的bean
        boolean flag = metadata.hasAnnotation("org.springframework.context.annotation.Configuration");
        if (flag) {
            return new String[]{"com.itheima.bean.Dog"};
        }
        return new String[]{"com.itheima.bean.Cat"};
    }
}
```

bean的加载方式（七）

- 导入实现了ImportBeanDefinitionRegistrar接口的类，通过BeanDefinition的注册器注册实名bean，实现对容器中bean的裁定，例如对现有bean的覆盖，进而达成不修改源代码的情况下更换实现的效果

```Java
public class MyRegistrar implements ImportBeanDefinitionRegistrar {
    @Override
    public void registerBeanDefinitions(AnnotationMetadata importingClassMetadata, BeanDefinitionRegistry registry) {
        //1.使用元数据去做判定

        BeanDefinition beanDefinition = BeanDefinitionBuilder.rootBeanDefinition(Dog.class).getBeanDefinition();
        registry.registerBeanDefinition("yellow",beanDefinition);
    }
}
```

bean的加载方式（八）

- 导入实现了BeanDefinitionRegistryPostProcessor接口的类，通过BeanDefinition的注册器注册实名bean，实现对容器中bean的最终裁定

```Java
public class MyPostProcessor implements BeanDefinitionRegistryPostProcessor {
    @Override
    public void postProcessBeanDefinitionRegistry(BeanDefinitionRegistry beanDefinitionRegistry) throws BeansException {
        BeanDefinition beanDefinition = BeanDefinitionBuilder.rootBeanDefinition(BookServiceImpl4.class).getBeanDefinition();
        beanDefinitionRegistry.registerBeanDefinition("bookService",beanDefinition);
    }

    @Override
    public void postProcessBeanFactory(ConfigurableListableBeanFactory configurableListableBeanFactory) throws BeansException {

    }
}
```

小结

1. xml+\<bean/>
2. xml:context+注解（@Component+4个@Bean）
3. 配置类+扫描+注解（@Component+4个@Bean）
   - @Bean定义FactoryBean接口
   - @ImportResource
   - @Configuration注解的proxyBeanMethods属性
4. @Import导入bean的类
   - @Import导入配置类
5. AnnotationConfigApplicationContext调用register方法
6. @Import导入ImportSelector接口
7. @Import导入ImportBeanDefinitionRegistrar接口
8. @Import导入BeanDefinitionRegistryPostProcessor接口

#### 3.1.2 bean的加载控制

bean的加载控制指根据特定情况对bean进行选择性加载以达到适用于项目的目标。

bean的加载控制

1. xml+\<bean/>
2. xml:context+注解（@Component+4个@Bean）
3. 配置类+扫描+注解（@Component+4个@Bean）
   - @Bean定义FactoryBean接口
   - @ImportResource
   - @Configuration注解的proxyBeanMethods属性
4. @Import导入bean的类
   - @Import导入配置类
5. **AnnotationConfigApplicationContext调用register方法**
6. **@Import导入ImportSelector接口**
7. **@Import导入ImportBeanDefinitionRegistrar接口**
8. **@Import导入BeanDefinitionRegistryPostProcessor接口**

根据任意条件确认是否加载bean

```Java
public class MyImportSelector implements ImportSelector {
    @Override
    public String[] selectImports(AnnotationMetadata annotationMetadata) {
        try {
            Class<?> clazz = Class.forName("com.itheima.bean.Mouse");
            if (clazz != null) {
                return new String[]{"com.itheima.bean.Cat"};
            }
        } catch (ClassNotFoundException e) {
//            e.printStackTrace();
            return new String[0];
        }
        return null;
    }
}
```

使用@Conditional注解的派生注解设置各种组合条件控制bean的加载

- 匹配指定类
- 未匹配指定类
- 匹配指定类型的bean
- 匹配指定名称的bean
- 匹配指定环境

```Java
//@Import(Mouse.class)
@ComponentScan("com.itheima.bean")
public class SpringConfig {
    @Bean
//    @ConditionalOnClass(name = "com.itheima.bean.Wolf")
//    @ConditionalOnMissingClass("com.itheima.bean.Mouse")
    @ConditionalOnBean(name = "jerry")
//    @ConditionalOnMissingClass("com.itheima.bean.Dog")
//    @ConditionalOnNotWebApplication
    @ConditionalOnWebApplication
    public Cat tom() {
        return new Cat();
    }

    @Bean
    @ConditionalOnClass(name = "com.mysql.jdbc.Driver")
    public DruidDataSource dataSource() {
        return new DruidDataSource();
    }
}
```

```Java
@Component("tom")
@ConditionalOnBean(name = "jerry")
//@ConditionalOnWebApplication
@ConditionalOnNotWebApplication
public class Cat {
}
```

#### 3.1.3 bean依赖的属性配置

1.将业务功能bean运行需要的资源抽取成独立的属性类（******Properties），设置读取配置文件信息

```Java
@ConfigurationProperties(prefix = "cartoon")
@Data
public class CartoonProperties {
    private Cat cat;
    private Mouse mouse;
}
```

2.配置文件中使用固定格式为属性类注入数据

```yaml
cartoon:
  cat:
    name: "图多盖洛"
    age: 5
  mouse:
    name: "泰菲"
    age: 1
```

3.定义业务功能bean，通常使用@Import导入，解耦强制加载bean

4.使用@EnableConfigurationProperties注解设定使用属性类时加载bean

```Java
@Data
@EnableConfigurationProperties(CartoonProperties.class)
public class CartoonCatAndMouse {
    private Cat cat;
    private Mouse mouse;

    private CartoonProperties cartoonProperties;

    public CartoonCatAndMouse(CartoonProperties cartoonProperties) {
        this.cartoonProperties = cartoonProperties;
        cat = new Cat();
        cat.setName(cartoonProperties.getCat() != null && StringUtils.hasText(cartoonProperties.getCat().getName()) ? cartoonProperties.getCat().getName() : "tom");
        cat.setAge(cartoonProperties.getCat() != null && cartoonProperties.getCat().getAge() != null ? cartoonProperties.getCat().getAge() : 3);
        mouse = new Mouse();
        mouse.setName(cartoonProperties.getMouse() != null && StringUtils.hasText(cartoonProperties.getMouse().getName()) ? cartoonProperties.getMouse().getName() : "jerry");
        mouse.setAge(cartoonProperties.getMouse() != null && cartoonProperties.getMouse().getAge() != null ? cartoonProperties.getMouse().getAge() : 4);
    }

    public void play() {
        System.out.println(cat.getAge() + "岁的"+cat.getName()+"和"+ mouse.getAge()+"岁的"+mouse.getName()+"打起来了");
    }
}
```

```Java
@SpringBootApplication
@Import(CartoonCatAndMouse.class)
public class App {
    public static void main(String[] args) {
        ConfigurableApplicationContext ctx = SpringApplication.run(App.class);
        CartoonCatAndMouse bean = ctx.getBean(CartoonCatAndMouse.class);
        bean.play();
    }
}
```

小结

- 业务bean的属性可以为其设定默认值
- 当需要设置时通过配置文件传递属性
- 业务bean应尽量避免设置强制加载，而是根据需要导入后加载，降低spring容器管理bean的强度

#### 3.1.4 自动配置原理

1.收集Spring开发者的编程习惯，整理开发过程使用的常用技术列表——>(技术集A)

2.收集常用技术(技术集A)的使用参数，整理开发过程中每个技术的常用设置列表——>(设置集B)

3.初始化SpringBoot基础环境，加载用户自定义的bean和导入的其他坐标，形成初始化环境

4.将技术集A包含的所有技术都定义出来，在Spring/SpringBoot启动时默认全部加载

5.将技术集A中具有使用条件的技术约定出来，设置成按条件加载，由开发者决定是否使用该技术（与初始化环境比对）

6.将设置集B作为默认配置加载（约定大于配置），减少开发者配置工作量

7.开放设置集B的配置覆盖接口，由开发者根据自身需要决定是否覆盖默认配置

```Java
public final class SpringFactoriesLoader {
    public static final String FACTORIES_RESOURCE_LOCATION = "META-INF/spring.factories";
}
```

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
    <version>2.5.4</version>
</dependency>
```

```Java
@Configuration(proxyBeanMethods = false)
@ConditionalOnClass(RedisOperations.class)
@EnableConfigurationProperties(RedisProperties.class)
@Import({ LettuceConnectionConfiguration.class, JedisConnectionConfiguration.class })
public class RedisAutoConfiguration {
}
```

```Java
@ConfigurationProperties(prefix = "spring.redis")
public class RedisProperties {
    private String url;
    private String host = "localhost";
    private int port = 6379;
}
```

小结

- 先开发若干种技术的标准实现
- SpringBoot启动时加载所有的技术实现对应的自动配置类
- 检测每个配置类的加载条件是否满足并进行对应的初始化
- 切记是先加载所有的外部资源，然后根据外部资源进行条件比对

#### 3.1.5 变更自动配置

自定义自动配置（META-INF/spring.factories）

```Properties
# Auto Configure
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
  com.itheima.bean.CartoonCatAndMouse
```

控制SpringBoot内置自动配置类加载

```yaml
spring:
  autoconfigure:
    exclude:
      - org.springframework.boot.autoconfigure.task.TaskExecutionAutoConfiguration
```

```Java
@SpringBootApplication(excludeName = "org.springframework.boot.autoconfigure.context.LifecycleAutoConfiguration")
```

变更自动配置：去除tomcat自动配置（条件激活），添加jetty自动配置（条件激活）

```XML
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <!--web起步依赖环境中，排除Tomcat起步依赖，匹配自动配置条件-->
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-tomcat</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <!--添加Jetty起步依赖，匹配自动配置条件-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-jetty</artifactId>
    </dependency>
</dependencies>
```

小结

- 通过配置文件exclude属性排除自动配置
- 通过注解@EnableAutoConfiguration属性排除自动配置项
- 启用自动配置只需要满足自动配置条件即可
- 可以根据需求开发自定义自动配置项

### 3.2 自定义starter

#### 3.2.1 案例：统计独立IP访问次数

案例：记录系统访客独立IP访问次数

- 每次访问网站行为均进行统计
- 后台每10秒输出一次监控信息（格式：IP+访问次数）

需求分析

1. 数据记录位置：Map/ Redis
2. 功能触发位置：每次web请求（拦截器）
   - 步骤一：降低难度，主动调用，仅统计单一操作访问次数（例如查询）
   - 步骤二：开发拦截器
3. 业务参数（配置项）
   - 输出频度，默认10秒
   - 数据特征：累计数据/ 阶段数据，默认累计数据
   - 输出格式：详细模式/ 极简模式
4. 校验环境，设置加载条件

#### 3.2.2 自定义starter

业务功能开发

```Java
public class IpCountService {
    private Map<String,Integer> ipCountMap = new HashMap<String,Integer>();

    @Autowired
    //当前的request对象的注入工作由使用当前starter的工程提供自动装配
    private HttpServletRequest httpServletRequest;

    public void count() {
        //每次调用当前操作，就记录当前访问的IP，然后累加访问次数
        //1.获取当前操作的IP地址
        String ip = httpServletRequest.getRemoteAddr();
        System.out.println("----------------------------" + ip);
        //2.根据IP地址从Map取值，并递增
        Integer count = ipCountMap.get(ip);
        if (count == null) {
            ipCountMap.put(ip,1);
        } else {
            ipCountMap.put(ip,ipCountMap.get(ip) + 1);
        }
    }
}
```

自动配置类

```Java
public class IpAutoConfiguration {
    @Bean
    public IpCountService ipCountService() {
        return new IpCountService();
    }
}
```

配置

```Properties
# Auto Configure
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
  cn.itcast.autoconfig.IpAutoConfiguration
```

模拟调用（非最终版）

```Java
@RestController
@RequestMapping("/books")
public class BookController {
    @Autowired
    private IBookService bookService;

    @GetMapping
    public R getAll() {
        return new R(true,bookService.list());
    }

    @Autowired
    private IpCountService ipCountService;

    @GetMapping("{currentPage}/{pageSize}")
    public R getPage(@PathVariable int currentPage, @PathVariable int pageSize, Book book) {
        ipCountService.count();

        IPage<Book> page = bookService.getPage(currentPage, pageSize, book);
        //如果当前页码值大于总页码值，那么重新执行查询操作，使用最大页码值作为当前页码值
        if (currentPage > page.getPages()) {
            page = bookService.getPage((int) page.getPages(),pageSize,book);
        }
        return new R(true,page);
    }
}
```

小结

- 使用自动配置加载业务功能
- 切记使用之前先clean后install安装到maven仓库，确保资源更新

开启定时任务功能

```Java
@EnableScheduling
public class IpAutoConfiguration {
    @Bean
    public IpCountService ipCountService() {
        return new IpCountService();
    }
}
```

设置定时任务

```Java
public class IpCountService {
    private Map<String,Integer> ipCountMap = new HashMap<String,Integer>();

    @Autowired
    //当前的request对象的注入工作由使用当前starter的工程提供自动装配
    private HttpServletRequest httpServletRequest;

    public void count() {
        //每次调用当前操作，就记录当前访问的IP，然后累加访问次数
        //1.获取当前操作的IP地址
        String ip = httpServletRequest.getRemoteAddr();
        //2.根据IP地址从Map取值，并递增
        Integer count = ipCountMap.get(ip);
        if (count == null) {
            ipCountMap.put(ip,1);
        } else {
            ipCountMap.put(ip,ipCountMap.get(ip) + 1);
        }
    }

    @Scheduled(cron = "0/5 * * * * ?")
    public void print() {
        System.out.println("         IP访问监控");
        System.out.println("+-----ip-address-----+--num--+");
        for (Map.Entry<String, Integer> entry : ipCountMap.entrySet()) {
            String key = entry.getKey();
            Integer value = entry.getValue();
            System.out.println(String.format("|%18s  |%5d  |",key,value));
        }
        System.out.println("+--------------------+-------+");
    }
}
```

小结

- 完成业务功能定时显示报表
- String.format()

定义属性类，加载对应属性

```Java
@ConfigurationProperties(prefix = "tools.ip")
public class IpProperties {
    /**
     * 日志显示周期
     */
    private Long cycle = 5L;

    /**
     * 是否周期内重置数据
     */
    private Boolean cycleReset = false;

    /**
     * 日志输出模式 detail：详细模式  Simple：极简模式
     */
    private String model = LogModel.DETAIL.value;

    public enum LogModel{
        DETAIL("detail"),
        SIMPLE("simple");
        private String value;
        LogModel(String value) {
            this.value = value;
        }
        public String getValue() {
            return value;
        }
    }

    public Long getCycle() {
        return cycle;
    }

    public void setCycle(Long cycle) {
        this.cycle = cycle;
    }

    public Boolean getCycleReset() {
        return cycleReset;
    }

    public void setCycleReset(Boolean cycleReset) {
        this.cycleReset = cycleReset;
    }

    public String getModel() {
        return model;
    }

    public void setModel(String model) {
        this.model = model;
    }
}
```

设置加载Properties类为bean

```Java
@EnableScheduling
@EnableConfigurationProperties(IpProperties.class)
public class IpAutoConfiguration {
    @Bean
    public IpCountService ipCountService() {
        return new IpCountService();
    }
}
```

根据配置切换设置

```Java
@Autowired
private IpProperties ipProperties;

@Scheduled(cron = "0/5 * * * * ?")
public void print() {
    if (ipProperties.getModel().equals(IpProperties.LogModel.DETAIL.getValue())) {
        System.out.println("         IP访问监控");
        System.out.println("+-----ip-address-----+--num--+");
        for (Map.Entry<String, Integer> entry : ipCountMap.entrySet()) {
            String key = entry.getKey();
            Integer value = entry.getValue();
            System.out.println(String.format("|%18s  |%5d  |",key,value));
        }
        System.out.println("+--------------------+-------+");
    } else if (ipProperties.getModel().equals(IpProperties.LogModel.SIMPLE.getValue())) {
        System.out.println("     IP访问监控");
        System.out.println("+-----ip-address-----+");
        for (String key : ipCountMap.keySet()) {
            System.out.println(String.format("|%18s  |",key));
        }
        System.out.println("+--------------------+");
    }


    if (ipProperties.getCycleReset()) {
        ipCountMap.clear();
    }
}
```

配置信息

```yaml
tools:
  ip:
    cycle: 5
    cycle-reset: true
    model: "simple"
```

自定义bean名称

```Java
@Component("ipProperties")
@ConfigurationProperties(prefix = "tools.ip")
public class IpProperties {
}
```

放弃配置属性创建bean方式，改为手工控制

```Java
@EnableScheduling
//@EnableConfigurationProperties(IpProperties.class)
@Import(IpProperties.class)
public class IpAutoConfiguration {
    @Bean
    public IpCountService ipCountService() {
        return new IpCountService();
    }
}
```

使用#{beanName.attrName}读取bean的属性

```Java
@Scheduled(cron = "0/#{ipProperties.cycle} * * * * ?")
public void print() {
}
```

自定义拦截器

```Java
public class IpCountInterceptor implements HandlerInterceptor {
    @Autowired
    private IpCountService ipCountService;

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        ipCountService.count();
        return true;
    }
}
```

设置核心配置类，加载拦截器

```Java
@Configuration
public class SpringMvcConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(ipCountInterceptor()).addPathPatterns("/**");
    }

    @Bean
    public IpCountInterceptor ipCountInterceptor() {
        return new IpCountInterceptor();
    }
}
```

#### 3.2.3 辅助功能开发

yml提示功能开发

导入配置处理器坐标

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
</dependency>
```

进行自定义提示功能开发

```Json
"hints": [
  {
    "name": "tools.ip.model",
    "values": [
      {
        "value": "detail",
        "description": "详细模式."
      },
      {
        "value": "simple",
        "description": "极简模式."
      }
    ]
  }
]
```

### 3.3 核心原理

#### 3.3.1 SpringBoot启动流程

1.初始化各种属性，加载成对象

- 读取环境属性（Environment）
- 系统配置（spring.factories）
- 参数（Arguments、application.properties）

2.创建Spring容器对象ApplicationContext，加载各种配置

3.在容器创建前，通过监听器机制，应对不同阶段加载数据、更新数据的需求

4.容器初始化过程中追加各种功能，例如统计时间、输出日志等

#### 3.3.2 监听器类型

1.在应用运行但未进行任何处理时，将发送ApplicationStartingEvent。

2.当Environment被使用，且上下文创建之前，将发送ApplicationEnvironmentPreparedEvent。

3.在开始刷新之前，bean定义被加载之后发送ApplicationPreparedEvent。

4.在上下文刷新之后且所有的应用和命令行运行器被调用之前发送ApplicationStartedEvent。

5.在应用程序和命令行运行器被调用之后，将发出ApplicationReadyEvent，用于通知应用已经准备处理请求。

6.启动时发生异常，将发送ApplicationFailedEvent。
