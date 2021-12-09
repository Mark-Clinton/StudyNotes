<center>
    <h1>
        Java进阶
    </h1>
</center>

## 1. 复习回顾

- 定义类。一个Java文件可以定义多个类。但是只有一个类是用public修饰，public修饰的类名必须称为Java文件名。
- 类中有且仅有5大成分(五大金刚)
  - 成员变量Field：描述类或者对象的属性信息的。
  - 成员方法Method：描述类或者对象的行为的。
  - 构造器(构造方法，Constructor)：初始化类的一个对象返回。
  - 代码块：还没有学。
  - 内部类：还没有学。
  - 注意：只要不是这5大成分放在类下就会报错。
- 封装
  - 面向对象的三大特征之一：封装，继承，多态。
  - 形成了规范，即使毫无意义还是会这样写代码！
  - 合理隐藏，合理暴露。
  - 封装的规范：成员变量私有，方法一般公开，提供成套的getter和setter方法暴露成员变量的取值和赋值。
  - 封装的作用：提高安全性，提高代码的组件化思想。
  - 封装已经成为Java代码的规范，即使毫无意义，我们也要这样写代码(成员变量私有，方法公开)
- this关键字
  - this代表了当前对象的引用。
  - this可以出现在构造器和方法中。
  - this出现在构造器中代表构造器正在初始化的对象。
  - this出现在方法中，哪个对象调用方法，this就代表哪个对象。
  - this可以访问对象的成员变量，区分成员变量是局部的还是对象中的成员变量。
- static关键字
  - 静态。
  - 修饰方法和变量都是属于类的。没有static修饰的方法和变量是属于每个对象的。
- 继承
  - 是面向对象的三大特征之一：封装，继承，多态。
  - 继承是Java中一般到特殊的关系，是一种子类到父类的关系。例如：学生类继承了人类。猫类继承了动物类。
  - 被继承的类称为：父类/超类。
  - 继承父类的类称为：子类。
  - 可提高代码的复用。
  - 子类更强大，子类不仅得到了父类的功能，它还有自己的功能。
  - 继承的特点：子类继承了一个父类，子类就可以直接得到父类的属性(成员变量)和行为(方法)了。单继承，多层继承。若支持多继承会出现类的二义性，故不支持多继承。
  - 子类不能继承父类的构造器：子类有自己的构造器。
  - 有争议的观点(拓展)
    - 认为子类是可以继承父类的私有成员的，只是不能直接访问而已。以后可以利用反射暴力去访问继承自父类的私有成员。
    - 认为子类是不能继承父类的静态成员的，子类只是可以访问父类的静态成员，父类的静态成员只有一份可以被子类共享访问。共享并非继承。
  - this代表了当前对象的引用，可以用于访问当前子类对象的成员变量。
  - super代表了父类对象的引用，可以用于访问父类中的成员变量。
  - 子类的构造器的第一行默认有一个super()调用父类的无参数构造器，写不写都存在。
  - 子类继承父类，子类就得到了父类的属性和行为。当我们调用子类构造器初始化子类对象数据的时候，必须先调用父类构造器初始化继承自父类的属性和行为。
  - 可以在子类构造器中通过super(...)根据参数选择调用分类的构造器，以便调用父类构造器初始化继承自父类的数据。
  - this(...)和super(...)必须放在构造器的第一行，否则报错。所以this(...)和super(...)不能同时出现在构造器中。
- 方法重写
  - 方法重写是子类重写一个与父类申明一样的方法覆盖父类的方法。
  - 方法重写建议加上@Override注解。
  - 方法重写的核心要求：方法名称形参列表必须与被重写的方法一致。
  - 建议“申明不变，重新实现”。
  - 静态方法和私有方法都不可以被重写，加上@Override都报错。
- 引用类型
  - 除了基本数据类型都是引用数据类型，引用类型存的都是地址。
  - 引用类型作为数据类型可以在一切可以使用类型的地方使用。
  - 引用类型可以作为成员变量的类型(复合类型)。

## 2. 抽象类

### 2.1 抽象类概述

父类知道子类一定要完成某个功能，但是每个子类完成的情况是不一样的。子类以后也只会用自己重写的功能，那么父类的该功能可以定义成抽象方法，子类重写调用子类自己的就可以了。

**抽象方法**

抽象方法：没有方法体，只有方法签名，必须用abstract修饰。

拥有抽象方法的类必须定义成抽象类。

抽象类：必须用abstract修饰。

**小结**

抽象类：拥有抽象方法类必须定义成抽象类，抽象类必须用abstract修饰。

抽象方法：没有方法体，只有方法签名，必须用abstract修饰。

抽象类是为了被子类继承，必须重写完抽象类的全部抽象方法，否则这个类也必须定义成抽象类。

### 2.2 抽象类的特征

抽象类的特征是：有得有失。

- 有得：抽象类得到了拥有抽象方法的能力。
- 有失：抽象类失去了创建对象的能力。(抽象类不能创建对象)

抽象类作为类一定有构造器，而且抽象类必须有构造器。提供给子类创建对象调用父类构造器使用的。

抽象类虽然有构造器但是抽象类不能创建对象。抽象类中的抽象方法不能执行，因为它没有方法体，所以抽象类不能创建对象。

注意：抽象类除了有得有失，类的其他成分它都具备。

抽象类存在的意义有2点：

1. 抽象类就是为了被子类继承(就是为了派生子类)，否则抽象类毫无意义。(基本准则)
2. 抽象类体现的是模板思想，部分实现，部分抽象。

### 2.3 抽象类设计模板模式

设计模式：设计模式是前人或者技术大牛或者软件行业在生产实践中发现的优秀软件设计架构和思想。后来者可以直接用这些架构或者思想就可以设计出优秀，提高效率，提高软件可扩展性和可维护性的软件。

模板设计模式就是一种经典的设计模式思想。

模板设计模式的作用：优化代码架构，提高代码的复用性，相同功能的重复代码无需反复书写。可以做到部分实现，部分抽象，抽象的东西交给使用模板的人重写实现。

```Java
public class AbstractDemo {
    public static void main(String[] args) {
        Student ss = new Student();
        ss.write();
    }
}

class Student extends Template {
    @Override
    public String writeMain() {
        return "\t\t我的学校很好，很牛逼。";
    }
}

abstract class Template {
    private String title = "\t\t\t\t\t\t《我的大学》";
    private String one = "\t\t请介绍一下你的大学，说说你的大学有多好，说说有多牛逼。";
    private String last = "\t\t我的大学真棒，能在这样的大学里读书真是太好了。";

    public void write() {
        System.out.println(title);
        System.out.println(one);
        System.out.println(writeMain());
        System.out.println(last);
    }

    public abstract String writeMain();
}
```

## 3. 接口

### 3.1 接口的概述

接口的概念

- 接口是更加彻底的抽象，在JDK1.8之前接口中只能是抽象方法和常量。
- 接口体现的是规范思想，实现接口的子类必须重写完接口的全部抽象方法。

接口的定义格式：修饰符 interface 接口名称 {}

接口中成分的研究：在JDK1.8之前接口中只能是抽象方法和常量。

接口中常量

- 变量值只有一个，而且在程序运行的过程中不可更改。
- 常量一般修饰符是：public static final。
- 常量的变量名称建议字母全大写，多个单词用“_”连接。
- 接口中常量是可以省去public stati final的。

### 3.2 接口的基本实现

类与类是继承关系，类与接口是实现关系。接口是被类实现的。

实现接口的类称为：实现类。

implements：类实现接口的关键字。

接口可以多实现。

一个类实现接口必须重写完接口中全部的抽象方法，否则这个类要定义成抽象类。

接口与接口的多继承：一个接口可以同时继承多个接口。

JDK1.8开始之后的接口

- JDK1.8之前接口中只能是抽象方法和常量，JDK1.8之后接口新增了三个方法。
  - 默认方法：其实就是之前的实例方法。
    - 必须用default修饰
    - 默认会加public修饰
    - 只能用接口的实现类的对象来调用
  - 静态方法：
    - 可以直接加static修饰
    - 默认会加public修饰
    - 接口的静态方法只能用接口的类名称调用
  - 私有方法(其实是从JDK1.9开始才支持的)：
    - 其实就是私有的实例方法，必须加private修饰
    - 私有的实例方法，只能在本接口中被访问
    - 私有方法通常是给其他私有方法或者给默认方法调用的

注意事项

- 如果实现了多个接口，多个接口中存在同名的静态方法并不冲突
  - 原因是只能通过各自接口名访问各自静态方法
- 当一个类，既继承一个父类，又实现若干个接口时
  - 父类中的成员方法与接口中的默认方法重名，子类就近选择执行父类的成员方法
- 当一个类实现多个接口时，多个接口中存在同名的默认方法
  - 实现类必须重写这个方法
- 接口中，没有构造器，不能创建对象
  - 接口是更彻底的抽象，连构造器都没有，自然不能创建对象

## 4. 代码块

### 4.1 静态代码块

类有5大成分：成员变量，方法，构造器，代码块，内部类。

代码块按照有无static修饰可分为：静态代码块、实例代码块。

静态代码块

- 格式：static {}
- 必须用static修饰。属于类，会与类一起优先加载，而且自动触发执行一次
- 静态代码块可以用于在执行类的方法之前进行静态资源的初始化操作

### 4.2 实例代码块

实例代码块

- 格式：{}
- 必须无static修饰。属于类的每个对象的，会与每个类的对象一起加载，每次创建对象的时候，实例代码块就会触发执行一次
- 实例代码块可以用于初始化实例资源
- 实例代码块的代码实际上是提取到每个构造器中去执行的

### 4.3 其他知识点

final关键字

- final可以用于修饰类，方法，变量。
- final修饰类：类不能被继承了。
- final修饰方法：方法不能被重写。
- final修饰变量，变量有且仅能被赋值一次。
- abstract和final是互斥关系，不能同时出现修饰成员。
- final修饰局部变量，让值被固定或者说保护起来，执行的过程中防止被修改。
- final修饰静态成员变量，变量变成了常量。
- final修饰静态成员变量可以在哪些地方赋值一次。
  - 定义的时候赋值一次。
  - 可以在静态代码块中赋值一次。
- final修饰变量的总规则：有且仅能被赋值一次。
- final修饰实例成员变量可以在哪些地方赋值一次。
  - 定义的时候赋值一次。
  - 可以在实例代码块中赋值一次。
  - 可以在每个构造器中赋值一次。

### 4.4 单例设计模式

单例：单例的意思是一个类永远只存在一个对象，不能创建多个对象。

为什么要用单例：开发中有很多类的对象我们只需要一个，例如虚拟机对象，任务管理器对象。对象越多越占内存，有些时候只需要一个对象就可以实现业务，单例可以节约内存，提高性能。

单例的实现方式目前学习两种方式

- 饿汉单例设计模式

  - 通过类获取单例对象的时候，对象已经提前做好了。
  - 实现步骤
    - 定义一个单例类
    - 把类的构造器私有
    - 定义一个静态成员变量用于存储对象。(饿汉单例在返回对象的时候，对象已经做好，所以这里直接创建出来)
    - 定义一个方法返回单例对象。

- 懒汉单例设计模式

  - 通过类获取单例对象的时候发现没有对象才会去创建一个对象。
  - 实现步骤
    - 定义一个单例类
    - 把类的构造器私有
    - 定义一个静态成员变量用于存储对象。(懒汉单例不能直接创建对象，必须需要的时候才创建)
    - 定义一个方法返回单例对象，判断对象不存在才创建一次，存在直接返回。
  - 某种意义上来说，懒汉单例模式在需要时才创建对象，能够节约内存。

  ### 4.5 枚举类

  枚举类的作用：枚举是用于做信息标志和信息分类。

  ```Java
  // 枚举类的格式
  修饰符 enum 枚举名称 {
      实例1名称,实例2名称...;
  }
  ```

  枚举类第一行罗列的必须是枚举类的对象名称。

  枚举类的特点

  - 枚举类是final修饰的，不能被继承。
  - 枚举类默认继承了枚举类型：java.lang.Enum。
  - 枚举类的第一行罗列的是枚举类的对象。而且是用常量存储的。
  - 所以枚举类的第一行写的都是常量名称，默认存储了枚举对象。
  - 枚举类的构造器默认是私有的。
  - 枚举类相当于是多例设计模式。

  常量做信息标志和分类：虽然也挺好，但是入参不受控制，入参太随性无法严谨。

  枚举类用于做信息标志和分类：优雅。

  建议做信息标志和信息分类采用枚举进行。

  ```Java
  enum Oritation {
      UP,DOWN,LEFT,RIGHT;
  }
  
  public class EnumDemo01 {
      public static void main(String[] args) {
          move(Oritation.LEFT);
      }
  
      public static void move(Oritation oritation) {
          switch (oritation) {
              case UP:
                  System.out.println("控制玛丽往上");
                  break;
              case DOWN:
                  System.out.println("控制玛丽往下");
                  break;
              case LEFT:
                  System.out.println("控制玛丽往左");
                  break;
              case RIGHT:
                  System.out.println("控制玛丽往右");
                  break;
          }
      }
  }
  ```

## 5. 多态

### 5.1 多态的概述

多态的形式

- 父类类型 对象名称 = new 子类构造器;
- 接口         对象名称 = new 实现类构造器;
- 父类类型的范围 > 子类类型的范围

多态的概念：同一个类型的对象，执行同一个行为，在不同状态下会表现出不同的行为特征。

多态的识别技巧

- 对于方法的调用：编译看左边，运行看右边。
- 对于变量的调用：编译看左边，运行看左边。

多态的使用前提

- 必须存在继承和实现关系。

- 必须存在父类类型的变量引用子类类型的对象。
- 需要存在方法重写。

多态的优劣势

- 优势
  - 在多态形式下，右边对象可以实现组件化切换，业务功能也随之改变，便于拓展和维护。可以实现类与类之间的解耦。
  - 实际开发的过程中，父类类型作为方法形式参数，传递子类对象给方法，可以传入一切子类对象进行方法的调用，更能体现出多态的扩展性与便利。
- 劣势
  - 多态形式下，不能直接调用子类特有的功能。编译看左边，左边父类中没有子类独有的功能，所以代码在编译阶段就直接报错了。

### 5.2 多态的下的类型转换

基本数据类型的转换

- 小范围类型的变量或者值可以直接赋值给大范围类型的变量。
- 大范围类型的变量或者值必须强制类型转换给小范围类型的变量。

引用数据类型转换的思想是一样的

- 父类类型的范围 > 子类类型的范围
- Animal                    Cat

引用数据类型的自动类型转换语法

- 子类类型的对象或者变量可以自动类型转换赋值给父类类型的变量。(不能解决多态的劣势)

引用类型强制类型转换的语法

- 父类类型的变量或者对象必须强制类型转换成子类类型的变量，否则报错。

强制类型转换的格式

- 类型 变量名称 = (类型) (对象或者变量)

注意：有继承/实现关系的两个类型就可以进行强制类型转换，编译阶段一定不报错。但是运行阶段可能出现：类型转换异常 ClassCastException

Java建议在进行强制类型转换之前先判断变量的真实类型，再强制类型转换。

- 变量 instanceof 类型：判断前面的变量是否是后面的类型或者其子类类型。

练习：面向对象思想设计一个电脑对象，可以接入2个USB设备。

```Java
public class Demo {
    public static void main(String[] args) {
        Computer c = new Computer();
        USB xiaoMi = new Mouse("小米鼠标");
        c.installUSB(xiaoMi);

        KeyBoard sfy = new KeyBoard("双飞燕键盘");
        c.installUSB(sfy);
    }
}

class Computer {
    public void installUSB(USB usb) {
        usb.connect();
        if (usb instanceof Mouse) {
            Mouse m = (Mouse) usb;
            m.dbclick();
        } else if (usb instanceof KeyBoard) {
            KeyBoard k = (KeyBoard) usb;
            k.keydown();
        }
        usb.unconnect();
    }
}

// 定义2个USB设备：鼠标，键盘
class Mouse implements USB {
    private String name;

    public Mouse(String name) {
        this.name = name;
    }

    public void dbclick() {
        System.out.println(name + "双击了·老铁·666666~~~");
    }

    @Override
    public void connect() {
        System.out.println(name + "成功接入了设备~~~~");
    }

    @Override
    public void unconnect() {
        System.out.println(name + "成功拔出了设备~~~~");
    }
}

class KeyBoard implements USB {
    private String name;

    public KeyBoard(String name) {
        this.name = name;
    }

    public void keydown() {
        System.out.println(name + "写下了·来了·老弟~~记得点亮小♥♥♥");
    }

    @Override
    public void connect() {
        System.out.println(name + "成功接入了设备~~~~");
    }

    @Override
    public void unconnect() {
        System.out.println(name + "成功拔出了设备~~~~");
    }
}

// 定义USB的规范，必须要完成接入和拔出的功能
interface USB {
    void connect();
    void unconnect();
}
```

## 6. 内部类

内部类是类的五大成分之一：成员变量，方法，构造器，代码块，内部类。

内部类：定义在一个类里面的类就是内部类。

内部类作用

- 可以提供更好的封装性，内部类有更多权限修饰符，封装性有更多的控制。
- 可以体现出组件的思想。

内部类的分类

- 静态内部类
- 实例内部类(成员内部类)
- 局部内部类
- 匿名内部类

**静态内部类**

静态内部类：有static修饰，属于外部类本身，会和外部类一起加载一次。

静态内部类中的成分研究

- 类有的成分它都有，静态内部类属于外部类本身，只会加载一次。
- 所以它的特点与外部类是完全一样的，只是位置在被人里面而已。
- 外部类 = 宿主   内部类 = 寄生

静态内部类的访问格式

- 外部类名称.内部类名称

静态内部类创建对象的格式

- 外部类名称.内部类名称 对象名称 = new 外部类名称.内部类构造器;

静态内部类的访问拓展

- 静态内部类中可以直接访问外部类的静态成员。外部类的静态成员只有一份，可以被共享。
- 静态内部类中不可以直接访问外部类的实例成员。外部类的实例成员必须用外部类对象访问。

**实例内部类**

实例内部类：无static修饰的内部类，属于外部类的每个对象的，跟着对象一起加载的。

实例内部类的成分特点

- 实例内部类中不能定义静态成员，其他都可以定义。
- 可以定义常量。

实例内部类的访问格式

- 外部类名称.内部类名称

创建对象的格式

- 外部类名称.内部类名称 对象名称 = new 外部类构造器.new 内部类构造器;

实例内部类的访问拓展

- 实例内部类中可以直接访问外部类的静态成员。外部类的静态成员可以被共享访问。
- 实例内部类中可以直接访问外部类的实例成员。实例内部类属于外部类对象，可以直接访问当前外部类对象的实例成员。

**局部内部类**

局部内部类：定义在方法中，在构造器中，代码块中，for循环中定义的内部类就是局部内部类

局部内部类中的成分特点

- 只能定义实例成员，不能定义静态成员。
- 可以定义常量。

**匿名内部类**

匿名内部类：就是一个没有名字的局部内部类。匿名内部类可以简化代码，也是开发中常用的形式。

匿名内部类的格式

```Java
new 类名|抽象类|接口(形参) {
    方法重写。
}
```

匿名内部类的特点

- 匿名内部类是一个没有名字的内部类。
- 匿名内部类一旦写出来，就会立即创建一个匿名内部类的对象返回。
- 匿名内部类的对象的类型相当于是当前new的那个类型的子类类型。

```Java
public class InnerClass {
    public static void main(String[] args) {
        Animal a = new Animal() {
            @Override
            public void run() {
                System.out.println("猫跑得贼溜~~~~");
            }
        };
        a.run();
        a.go();
    }
}

abstract class Animal {
    public abstract void run();

    public void go() {
        System.out.println("开始Go.....");
    }
}
```

使用形式

```Java
public class Anonymity {
    public static void main(String[] args) {
        Swim bozai = new Swim() {
            @Override
            public void swimming() {
                System.out.println("老师游泳贼溜~~~~~");
            }
        };
        go(bozai);

        Swim boniu = new Swim() {
            @Override
            public void swimming() {
                System.out.println("波妞学生快乐的狗爬式~~~~~");
            }
        };
        go(boniu);
        
        go(new Swim() {
            @Override
            public void swimming() {
                System.out.println("波妞学生快乐的狗爬式~~~~~");
            }
        });
    }

    public static void go(Swim s) {
        System.out.println("开始.....");
        s.swimming();
        System.out.println("结束.....");
    }
}

interface Swim {
    void swimming();
}
```

```Java
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Anonymity01 {
    public static void main(String[] args) {
        // 1.创建一个窗口
        JFrame win = new JFrame("登录界面");

        // 2.设置窗口的大小
        win.setSize(400,300);

        // 3.居中
        win.setLocationRelativeTo(null);

        // 4.为当前界面加上一个按钮对象
        JButton btn = new JButton("开始登陆");
        JPanel panel = new JPanel();
        panel.add(btn);
        win.add(panel);

        // 5.为当前按钮对象绑定一个点击事件监听器
        btn.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println("用户点击了触发登陆~~~");
            }
        });
        //btn.addActionListener(s -> System.out.println("用户点击了触发登陆~~~"));

        // 6.显示窗口
        win.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        win.setVisible(true);
    }
}
```

## 7. 包与权限修饰符

### 7.1 包

包

- 分门别类的管理各种不同的技术。
- 企业的代码必须用包分区。便于管理技术，扩展技术，阅读技术。

定义包的格式

- package 包名;    必须放在类名的最上面。
- 一般工具已经帮我们做好了。

包名的命名规范

- 一般是公司域名的倒写+技术名称
- http://www.baidu.com => com.baidu.技术名称
- 包名建议全部用英文，多个单词用“.”连接，必须是合法标识符，不能用关键字

注意

- 相同包下的类可以直接访问。
- 不同包下的类必须导包，才可以使用。
- 导包格式：import 包名.类名;

### 7.2 权限修饰符

权限修饰符

- 有四种(private -> 缺省 -> protected -> public)
- 可以修饰成员变量，修饰方法，修饰构造器，内部类，不同修饰符修饰的成员能够被访问的权限将受到限制。

四种修饰符的访问权限范围

|                  | private | 缺省 | protected | public |
| ---------------- | :-----: | :--: | :-------: | :----: |
| 本类中           |    √    |  √   |     √     |   √    |
| 本包下其他类中   |    ×    |  √   |     √     |   √    |
| 其他包下的类中   |    ×    |  ×   |     ×     |   √    |
| 其他包下的子类中 |    ×    |  ×   |     √     |   √    |

## 8. 常用API

### 8.1 Object

Object类的常用方法

- public String toString()
  - 默认是返回当前对象在堆内存中的地址信息。
  - 默认的地址信息格式：类的全限名@内存地址。
  - 直接输出对象名称，默认会自动调用toString()方法，所以输出对象toString()调用可以省略不写。
  - 开发中直接输出对象，默认输出对象的地址其实是毫无意义的。
  - 开发中输出对象变量，更多的时候是希望看到对象的内容数据而不是对象的地址信息。所以父类toString()方法存在的意义就是为了被子类重写，以便返回对象的内容信息。
- public boolean equals(Object o)
  - 默认是比较两个对象的地址是否相同。相同则返回true，反之false。
  - 直接比较两个对象的地址是否相同完全可以用“==”代替equals。
  - 所以equals存在的意义是为了被子类重写，以便程序员可以自己来定制比较规则。
  - 注意：字符串的比较建议使用equals比较，只要内容一样结果就是true。基本数据类型用“==”比较。

### 8.2 Objects

Objects类与Object还是继承关系。Objects类是从JDK1.7开始之后才有的。

Objects的方法

- public static boolean equals(Object a, Object b)
  - 比较两个对象
  - 底层进行非空判断，从而可以避免空指针异常。更安全
- public static boolean isNull(Object obj)
  - 判断变量是否为null，为null返回true，反之

### 8.3 Date日期类

Date类在Java中代表的是系统当前此刻日期时间对象。

Date类

- 包：java.util.Date
- 构造器
  - public Date()：创建当前系统的此刻日期时间对象
  - public Date(long time)：把时间毫秒值转换成日期对象
- 方法
  - public long getTime()：返回自1970年1月1日00:00:00GMT以来走过的总的毫秒数
- 时间记录的两种方式
  - Date日期对象
  - 时间毫秒值：从1970年1月1日00:00:00GMT开始走到此刻的总的毫秒值。1s = 1000ms
- 流程
  - Date日期对象 -> getTime -> 时间毫秒值
  - 时间毫秒值 -> new Date(时间毫秒值) -> Date日期对象

### 8.4 SimpleDateFormat简单日期格式化类

DateFormat作用

- 可以把日期对象或者时间毫秒值格式化成我们喜欢的时间形式。
- 可以把字符串的时间形式解析成日期对象。

DateFormat是一个抽象类，不能直接使用，要找它的子类：SimpleDateFormat。我们需要用的是简单日期格式化类：SimpleDateFormat。

SimpleDateFormat简单日期格式化类

- 构造器
  - public SimpleDateFormat(String pattern)：指定时间的格式创建简单日期格式化对象。
- 方法
  - public String format(Date date)：可以把日期对象格式化成我们喜欢的时间形式，返回的是字符串。
  - public String format(Object time)：可以把时间毫秒值格式化成我们喜欢的时间形式，返回的是字符串。
  - public Date parse(String date) throws ParseException：把字符串的时间解析成日期对象。

```Java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class DateFormatDemo01 {
    public static void main(String[] args) throws ParseException {
        String date = "2019-11-04 09:30:30";
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        Date d = sdf.parse(date);
        long time = d.getTime() + (24L * 60 * 60 + 15 * 60 * 60 + 30 * 60 + 29) * 1000;

        String rs = sdf.format(time);
        System.out.println(rs);
    }
}
```

### 8.5 日历类Calendar

Calendar代表了系统此刻日期对应的日历对象

Calendar是一个抽象类，不能直接创建对象。

Calendar日历类创建日历对象的语法

- Calendar rightNow = Calendar.getInstance();

Calendar的方法

- public static Calendar getInstance()：返回一个日历类的对象。
- public int get(int field)：取日期中的某个字段信息。
- public void set(int field, int value)：修改日历的某个字段信息。
- public void add(int field, int amount)：为某个字段增加/减少指定的值。
- public final Date getTime()：拿到此刻日期对象。
- public long getTimeInMillis()：拿到此刻时间毫秒值。

### 8.6 Math类

Math用于做数学运算。

Math类中的方法全部是静态方法，直接用类名调用即可。

方法

- public static int abs(int a)：获取参数a的绝对值。
- public static double ceil(double a)：向上取整。
- public static double floor(double a)：向下取整。
- public static double pow(double a, double b)：获取a的b次幂。
- public static long round(double a)：四舍五入取整。

### 8.7 System系统类

System代表当前系统。

静态方法

- public static void exit(int status)：终止JVM虚拟机看，非0是异常终止。
- public static longcurrentTimeMillis()：获取当前系统此刻时间毫秒值。
- 可以做数组的拷贝。
  - arraycopy(Object var0, int var1, Object var2, int var3, int var4);
  - 参数一：原数组
  - 参数二：从原数组的哪个位置开始赋值
  - 参数三：目标数组
  - 参数四：赋值到目标数组的哪个位置
  - 参数五：赋值几个

### 8.8 BigDecimal类

浮点型运算的时候直接 + * / 可能会出现数据失真(精度问题)。

BigDecimal可以解决浮点型运算数据失真的问题。

创建对象方式

- public static BigDecimal valueOf(double val)：包装浮点数成为大数据对象。

方法

- public BigDecimal add(BigDecimal value)：加法运算
- public BigDecimal subtract(BigDecimal value)：减法运算
- public BigDecimal multiply(BigDecimal value)：乘法运算
- public BigDecimal divide(BigDecimal value)：除法运算
- public double doubleValue()：把BigDecimal转换成double类型

### 8.9 包装类

Java认为一切皆对象。引用数据类型就是对象了。但是在Java中8种基本数据类型不是对象，只是表示一种数据的类型形式。

Java为了一切皆对象的思想统一，把8种基本数据类型转换成对应的类，这个类称为基本数据类型的包装类。

| 基本数据类型 | 包装类(引用数据类型) |
| :----------: | :------------------: |
|     byte     |         Byte         |
|    short     |        Short         |
|     int      |       Integer        |
|     long     |         Long         |
|    float     |        Float         |
|    double    |        Double        |
|     char     |      Character       |
|   boolean    |       Boolean        |

自动装箱：可以直接把基本数据类型的值或者变量赋值给包装类。

自动拆箱：可以把包装类的变量直接赋值给基本数据类型。

Java为包装类做了一些特殊功能，以便程序员使用。

包装类作为类首先拥有了Object类的方法。

包装类作为引用类型的变量可以存储null值。

特殊功能主要有：

- 可以把基本数据类型的值转换成字符串类型的值。
  - 调用toString()方法。
  - 调用Integer.toString(基本数据类型的值)得到字符串。
  - 直接把基本数据类型+空字符串就得到了字符串。
- 把字符串类型的数值转换成对应的基本数据类型的值。
  - Xxx.parseXxx("字符串类型的数值")
  - Xxx.valueOf("字符串类型的数值")：推荐使用

### 8.10 正则表达式

正则表达式的作用：是一些特殊字符组成的校验规则，可以验证信息的正确性，校验邮箱、电话号码、金额等是否合法。

需求：演示不用正则表达式和用正则表达式校验QQ号码。

```Java
public class RegexDemo {
    public static void main(String[] args) {
        System.out.println(checkQQ("42422332"));
        System.out.println(checkQQRegex("42422332"));
    }

    public static boolean checkQQRegex(String qq) {
        return qq != null && qq.matches("\\d{4,}");
    }

    public static boolean checkQQ(String qq) {
        if (qq == null) {
            return false;
        } else {
            if (qq.length() >= 4) {
                boolean rs = true;
                for (int i = 0; i < qq.length(); i++) {
                    char ch = qq.charAt(i);
                    if (ch < '0' || ch > '9') {
                        rs = false;
                    }
                }
                return rs;
            } else {
                return false;
            }
        }
    }
}
```

深入学习正则表达式的写法

字符类

- [abc] a、b或c (简单类)
- [^abc] 任何字符，除了a、b或c (否定)
- [a-zA-Z] a到z或A到Z，两头的字母包括在内 (范围)
- [a-d[m-p]] a到d或m到p：[a-dm-p] (并集)
- [a-z&&[def23]] d、e或f (交集)
- [a-z&&\[^bc]] a到z，除了b和c：[ad-z] (减去)
- [a-z&&\[^m-p]] a到z，而非m到p：[a-lq-z] (减去)

Greedy数量词

- X? X，一次或一次也没有
- X* X，零次或多次
- X+ X，一次或多次
- X{n} X，恰好n次
- X{n,} X，至少n次
- X{n,m} X，至少n次，但是不超过m次 

表示规则太多，具体查看Java文档。

```Java
public class RegexDemo01 {
    public static void main(String[] args) {
        checkEmail();
        checkTell();
    }

    // 校验手机号码
    private static void checkTell() {
        Scanner sc = new Scanner(System.in);
        System.out.println("请您输入手机号码：");
        String email = sc.nextLine();
        if (email.matches("1[3-9]\\d{9}")) {
            System.out.println("手机号码合法了！");
        } else {
            System.err.println("手机号码格式不正确！");
        }
    }

    // 校验邮箱
    public static void checkEmail() {
        Scanner sc = new Scanner(System.in);
        System.out.println("请您输入邮箱：");
        String email = sc.nextLine();
        if (email.matches("\\w{1,}@\\w{2,10}(\\.\\w{2,10}){1,2}")) {
            System.out.println("邮箱合法了！");
        } else {
            System.err.println("邮箱格式不正确！");
        }
    }
}
```

正则表达式在方法中的应用

- public String[] split(String regex)：按照正则表达式匹配的内容进行分割字符串，返回一个字符串数组。
- public String replaceAll(String regex, String newStr)：按照正则表达式匹配的内容进行替换。

正则表达式爬取信息

```Java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexDemo03 {
    public static void main(String[] args) {
        String rs = "来的进口件Java，电话020-15645646，大姐夫IE和" +
                "djfh@ustc.cn，电话13544659457，0203232323" +
                "邮箱bozai@itahu.cn，400-100-3233，4001003232";
        String regex = "(\\w{1,}@\\w{2,10}(\\.\\w{2,10}){1,2})|(1[3-9]\\d{9})|(0\\d{2,5}-?\\d{5,15})|(400-?\\d{3,8}-?\\d{3,8})";
        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(rs);
        while (matcher.find()) {
            System.out.println(matcher.group());
        }
    }
}
```

## 9. 泛型

### 9.1 泛型的概述

泛型就是一个标签：<数据类型>

泛型可以在编译阶段约束只能操作某种数据类型。

注意：JDK1.7开始之后，泛型后面的申明可以省略不写。泛型和集合都只能支持引用数据类型，不支持基本数据类型。

泛型好处：泛型在编译阶段约束了操作的数据类型，从而不会出现类型转换异常。

### 9.2 自定义泛型

使用泛型定义的类就是泛型类。

泛型类的格式

```Java
修饰符 class 类名<泛型变量>{
    
}
```

泛型变量建议使用E，T，K，V

泛型的核心思想：是把出现泛型变量的地方全部替换成传输的真实数据类型。

泛型方法：定义了泛型的方法就是泛型方法。

泛型方法的定义格式

```Java
修饰符 <泛型变量> 返回值类型 方法名称(形参列表){
    
}
```

注意：方法定义了是什么泛型变量，后面就只能用什么泛型变量。

```Java
import java.util.ArrayList;

public class GenericityDemo {
    public static void main(String[] args) {
        MyArrayList<String> lists1 = new MyArrayList<>();
        lists1.add("Hello");
        lists1.add("World");
        lists1.add("Java");
        System.out.println(lists1);

        lists1.remove("World");
        System.out.println(lists1);
        System.out.println("--------------------");

        Integer[] arr = {10,20,30,40};
        String[] arr1 = {"Hello","World","Java"};
        String s = arrToString(arr);
        String s1 = arrToString(arr1);
        System.out.println(s);
        System.out.println(s1);
    }

    public static <T> String arrToString(T[] nums) {
        StringBuilder sb = new StringBuilder();
        sb.append("[");
        if (nums != null && nums.length > 0) {
            for (int i = 0; i < nums.length; i++) {
                T ele = nums[i];
                sb.append(i==nums.length-1?ele:ele+",");
            }
        }
        sb.append("]");
        return sb.toString();
    }
}

class MyArrayList<E> {
    private ArrayList lists = new ArrayList();

    public void add(E e) {
        lists.add(e);
    }

    public void remove(E e) {
        lists.remove(e);
    }

    @Override
    public String toString() {
        return lists.toString();
    }
}
```

泛型接口形式

```Java
修饰符 interface 接口名称<泛型变量>{
    
}
```

泛型接口的核心思想：在实现接口的时候传入真实的数据类型，这样重写的方法就是对该数据类型进行操作。

泛型通配符：？，？可以用在使用泛型的时候代表一切类型。

泛型的上下限

- ? extends Car：那么？必须是Car或者其子类。(泛型的上限)
- ? super Car：那么？必须是Car或者其父类。(泛型的下限，不是很常见)

## 10. 集合

集合特点

- Set系列集合：添加的元素是无序，不重复，无索引的。
  - HashSet：添加的元素是无序，不重复，无索引的。
  - LinkedHashSet：添加的元素是有序，不重复，无索引的。
  - TreeSet：不重复，无索引，按照大小默认升序排序。
- List系列集合：添加的元素是有序，可重复，有索引的。
  - ArrayList：添加的元素是有序，可重复，有索引的。
  - LinkedList：添加的元素是有序，可重复，有索引的。

Collection是集合的祖宗类，Collection集合的功能是一切集合都可以直接使用的。

Collection集合的遍历方式有三种

- 迭代器
- foreach(增强for循环)
- JDK1.8开始之后的新技术Lambda表达式

迭代器方法

- public Iterator iterator()：获取集合对应的迭代器，用来遍历集合中的元素
- E next()：获取下一个元素值
- boolean hasNext()：判断是否有下一个元素，有返回true，反之返回false

foreach遍历集合或者数组很方便。

缺点：foreach遍历无法知道遍历到了哪个元素了，因为没有索引。

Lambda表达式

- lists.forEach(s -> System.out.println(s));
- lists.forEach(System.out::println);

**红黑树**

红黑树就是平衡的二叉查找树。

红黑树是一种自平衡的二叉查找树，是计算机科学中用到的一种数据结构，它是在1972年由Rudolf Bayer发明的，当时被称为平衡二叉B树，后来，在1978年被Leoj.Guibas和Robert Sedgewick修改为如今的”红黑树“。它是一种特殊的二叉查找树，红黑树的每一个节点上都有存储位表示节点的颜色，可以是红或者黑。

红黑树不是高度平衡的，它的平衡是通过”红黑树的特性“进行实现的。

红黑树的特性：

- 每一个节点或是红色的，或者是黑色的。
- 根节点必须是黑色。
- 每个叶节点(Nil)是黑色的；(如果一个节点没有子节点或者父节点，则该节点相应的指针属性值为Nil，这些Nil视为叶节点)。
- 如果某一个节点是红色，那么它的子节点必须是黑色(不能出现两个红色节点相连的情况)。
- 对每一个节点，从该节点到其所有后代叶节点的简单路径上，均包含相同数目的黑色节点。

在进行元素插入的时候，和之前一样；每一次插入完毕以后，使用黑色规则进行校验，如果不满足红黑规则，就需要通过变色，左旋和右旋来调整树看，使其满足红黑规则。

红黑树的增删改查性能都好！

List遍历方式

- for循环
- 迭代器
- foreach
- JDK 1.8新技术

LinkedList也是List的实现类：底层是基于链表的，增删比较快，查询慢。

LinkedList是支持双链表，定位前后的元素都是非常快的，增删首尾的元素也是最快的。

所以LinkedList除了拥有List集合的全部功能还多了很多操作首尾元素的特殊功能。

如果查询多而增删少用ArrayList集合；如果查询少而增删首尾较多用LinkedList集合。

Set集合

- 对于有值特性的，Set集合可以直接判断进行去重复。
- 对于引用数据类型的类对象，Set集合是按照如下流程进行是否重复的判断。
  - Set集合会让两两对象，先调用自己的hashCode()方法得到彼此的哈希值(所谓的内存地址)
  - 然后比较两个对象的哈希值是否相同，如果不相同则直接认为两个对象不重复
  - 如果哈希值相同，会继续让两个对象进行equals比较内容是否相同，如果相同认为真的重复了，如果不相同认为不重复
- 只要对象内容一样，就希望集合认为它们重复了，需要重写hashCode和equals方法。
- Set系列集合添加元素无序的根本原因是因为底层采用了哈希表存储元素。
  - JDK 1.8之前：哈希表 = 数组 + 链表 + (哈希算法)
  - JDK 1.8之后：哈希表 = 数组 + 链表 + 红黑树 + (哈希算法)
  - 当链表的长度超过阈值(8)时，将链表转换为红黑树，这样大大减少了查找时间

哈希表的增删改查性能都很好。

LinkedHashSet底层依然是使用哈希表存储元素的，但是每个元素都额外带一个链来维护添加顺序。

不光增删查快，还有序。缺点是多了一个存储顺序的链会占内存空间。而且不允许重复，无索引。

总结

- 如果希望元素可以重复，又有索引，查询要快用ArrayList集合。
- 如果希望元素可以重复，又有索引，增删要快要用LinkedList集合。
- 如果希望增删改查都很快，但是元素不重复以及无索引，那么用HashSet集合。
- 如果希望增删改查都很快且有序，但是元素不重复以及无索引，那么用LinkedHashSet集合。
- 这里的有序指的都是插入的顺序和遍历结果顺序一致。

TreeSet集合称为排序不重复集合，可以对元素及逆行默认的升序排序。

TreeSet集合自排序的方式

- 有值特性的元素直接可以升序排序。
- 字符串类型的元素会按照首字母的编号排序。
- 对于自定义的引用数据类型，TreeSet默认无法排序，执行的时候直接报错，因为人家不知道排序规则。

自定义的引用数据类型的排序实现

- 对于自定义的引用数据类型，TreeSet默认无法排序，所以我们需要定制排序的大小规则。
- 程序员定义大小规则的方案有2种
  - 直接为对象的类实现比较器规则接口Comparable，重写比较方法。
    - 如果程序员认为比较者大于被比较者，返回正数。
    - 如果程序员认为比较者小于被比较者，返回负数。
    - 如果程序员认为比较者等于被比较者，返回0。
  - 直接为集合设置比较器Comparator对象，重写比较方法。
    - 如果程序员认为比较者大于被比较者，返回正数。
    - 如果程序员认为比较者小于被比较者，返回负数。
    - 如果程序员认为比较者等于被比较者，返回0。
  - 如果类和集合都带有比较规则，优先使用集合自带的比较规则。

Collections并不属于集合，是用来操作集合的工具类。

可变参数

- 可变参数用在形参中可以接收多个数据。
- 可变参数的形式：数据类型...参数名称

可变参数的作用

- 传输参数非常灵活，方便
- 可以不传输参数
- 可以传输一个参数
- 可以传输多个参数
- 可以传输一个数组

可变参数在方法内部本质上就是一个数组。

可变参数的注意事项

- 一个形参列表中可变参数只能有一个
- 可变参数必须放在形参列表的最后面

```Java
import java.util.Arrays;

public class SetDemo {
    public static void main(String[] args) {
        sum();
        sum(10);
        sum(10,20,30);
        sum(new int[]{10,30,50,70,90});
    }

    public static void sum(int... nums) {
        System.out.println(nums.length);
        System.out.println(Arrays.toString(nums));
        System.out.println("---------------------------");
    }
}
```

练习：斗地主游戏。

扑克牌类

```Java
public class Card {
    private String number;
    private String color;
    private int index;

    public Card() {
    }

    public Card(String number, String color, int index) {
        this.number = number;
        this.color = color;
        this.index = index;
    }

    public String getNumber() {
        return number;
    }

    public void setNumber(String number) {
        this.number = number;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public int getIndex() {
        return index;
    }

    public void setIndex(int index) {
        this.index = index;
    }

    @Override
    public String toString() {
        return number + color;
    }
}
```

斗地主游戏类

```Java
import java.util.*;

public class GameDemo {
    public static final List<Card> ALL_CARDS = new LinkedList<>();

    static {
        String[] numbers = {"3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A", "2"};
        String[] colors = {"♠","♥","♣","♦"};

        int index = 0;
        for (String number : numbers) {
            for (String color : colors) {
                Card card = new Card(number,color,index++);
                ALL_CARDS.add(card);
            }
        }

        Collections.addAll(ALL_CARDS,new Card("","🃏",index++),new Card("","👲",index++));
        System.out.println("输出新牌：" + ALL_CARDS);
    }

    public static void main(String[] args) {
        Collections.shuffle(ALL_CARDS);
        System.out.println("洗牌后：" + ALL_CARDS);

        List<Card> lingHuChong = new ArrayList<>();
        List<Card> jiuMoZhi = new ArrayList<>();
        List<Card> dongfangbubai = new ArrayList<>();

        for (int i = 0; i < ALL_CARDS.size() - 3; i++) {
            Card c = ALL_CARDS.get(i);
            if (i % 3 == 0) {
                lingHuChong.add(c);
            } else if (i % 3 == 1) {
                jiuMoZhi.add(c);
            } else if (i % 3 == 2) {
                dongfangbubai.add(c);
            }
        }

        sortCards(lingHuChong);
        sortCards(jiuMoZhi);
        sortCards(dongfangbubai);

        System.out.println("令狐冲：" + lingHuChong);
        System.out.println("鸠摩智：" + jiuMoZhi);
        System.out.println("东方不败：" + dongfangbubai);

        List<Card> lastThreeCards = ALL_CARDS.subList(ALL_CARDS.size() - 3, ALL_CARDS.size());
        System.out.println("底牌：" + lastThreeCards);

    }

    private static void sortCards(List<Card> cards) {
        Collections.sort(cards, new Comparator<Card>() {
            @Override
            public int compare(Card o1, Card o2) {
                return o2.getIndex() - o1.getIndex();
            }
        });
    }
}
```

## 11. Map集合

### 11.1 Map集合概述

Map集合是另一个集合体系，Collection是单值集合体系。

Map集合是一种双列集合，每个元素包含两个值。

Map集合的每个元素的格式：key=value(键值对集合)

Map集合也被称为“键值对集合”。

注意：集合和泛型都只能支持引用数据类型，集合完全可以称为是对象容器，存储都是对象。

Map集合的特点

- Map集合的特点都是由键决定的。
- Map集合的键是无序，不重复，无索引的。
  - Map集合后面重复的键对应的元素会覆盖前面的整个元素。
- Map集合的值无要求。
- Map集合的键值对都可以为null。

HashMap：元素按照键是无序，不重复，无索引，值不做要求。

LinkedHashMap：元素按照键是有序，不重复，无索引，值不做要求。

Map集合的遍历方式

- “键值对”的方式遍历：先获取Map集合全部的键，再根据键找值。
- “键值对”的方式遍历：难度较大。
- JDK 1.8 开始之后的新技术：Lambda表达式。

```Java
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

public class MapDemo01 {
    public static void main(String[] args) {
        Map<String,Integer> maps = new HashMap<>();
        maps.put("娃娃",30);
        maps.put("iphoneX",100);
        maps.put("huawei",1000);
        maps.put("生活用品",10);
        maps.put("手表",10);
        System.out.println(maps);

        Set<String> keys = maps.keySet();
        for (String key : keys) {
            Integer value = maps.get(key);
            System.out.println(key + "=" + value);
        }
        System.out.println("------------------------");

        Set<Map.Entry<String, Integer>> entries = maps.entrySet();
        for (Map.Entry<String, Integer> entry : entries) {
            String key = entry.getKey();
            Integer value = entry.getValue();
            System.out.println(key + "=" + value);
        }
        System.out.println("------------------------");

        maps.forEach((k, v) -> System.out.println(k + "=" + v));
    }
}
```

Map集合的键和值都可以存储自定义类型。

如果希望Map集合认为自定义类型的键对象重复了，必须重写对象的hashCode()和equals()方法。

LinkedHashMap集合

- LinkedHashMap是HashMap的子类，添加的元素按照键有序，不重复的。
- HashSet集合相当于是HashMap集合的键都不带值。
- LinkedHashSet集合相当于是LinkedHashMap集合的键都不带值。
- 底层原理完全一样，都是基于哈希表按照键存储数据的，只是HashMap或者LinkedHashMap的键都多一个附属值。

TreeMap集合

- TreeMap集合和TreeSet集合都是排序不重复集合。
- TreeSet集合的底层是基于TreeMap，只是键没有附属值而已。
- TreeMap集合指定大小规则有2中方式
  - 直接为对象的类实现比较器规则接口Comparable，重写比较方法
  - 直接为集合设置比较器Comparator对象，重写比较方法

练习：计算字符串中各字符出现的次数。

```Java
public class MapDemo01 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请您输入一个字符串：");
        String datas = sc.nextLine();

        Map<Character,Integer> infos = new HashMap<>();
        for (int i = 0; i < datas.length(); i++) {
            char ch = datas.charAt(i);
            if (infos.containsKey(ch)) {
                infos.put(ch,infos.get(ch) + 1);
            } else {
                infos.put(ch,1);
            }
        }
        System.out.println("结果：" + infos);
    }
}
```

练习：使用Map集合实现斗地主小案例。

```Java
import java.util.*;

public class GameDemo {
    public static final Map<Card,Integer> ALL_CARDS_SIZE = new HashMap<>();
    public static final List<Card> ALL_CARDS = new ArrayList<>();
    static {
        String[] numbers = {"3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A", "2"};
        String[] colors = {"♠","♥","♣","♦"};

        int index = 0;
        for (String number : numbers) {
            for (String color : colors) {
                Card card = new Card(number,color);
                ALL_CARDS.add(card);
                ALL_CARDS_SIZE.put(card,index++);
            }
        }
        Card c1 = new Card("","🃏");
        Card c2 = new Card("","👲");
        ALL_CARDS.add(c1);
        ALL_CARDS.add(c2);
        ALL_CARDS_SIZE.put(c1,index++);
        ALL_CARDS_SIZE.put(c2,index++);
        System.out.println("输出新牌：" + ALL_CARDS);
    }

    public static void main(String[] args) {
        Collections.shuffle(ALL_CARDS);
        System.out.println("洗牌后：" + ALL_CARDS);

        List<Card> lingHuChong = new ArrayList<>();
        List<Card> jiuMoZhi = new ArrayList<>();
        List<Card> dongfangbubai = new ArrayList<>();

        for (int i = 0; i < ALL_CARDS.size() - 3; i++) {
            Card c = ALL_CARDS.get(i);
            if (i % 3 == 0) {
                lingHuChong.add(c);
            } else if (i % 3 == 1) {
                jiuMoZhi.add(c);
            } else if (i % 3 == 2) {
                dongfangbubai.add(c);
            }
        }

        sortCards(lingHuChong);
        sortCards(jiuMoZhi);
        sortCards(dongfangbubai);

        System.out.println("令狐冲：" + lingHuChong);
        System.out.println("鸠摩智：" + jiuMoZhi);
        System.out.println("东方不败：" + dongfangbubai);

        List<Card> lastThreeCards = ALL_CARDS.subList(ALL_CARDS.size() - 3, ALL_CARDS.size());
        System.out.println("底牌：" + lastThreeCards);

    }

    private static void sortCards(List<Card> cards) {
        Collections.sort(cards, new Comparator<Card>() {
            @Override
            public int compare(Card o1, Card o2) {
                return ALL_CARDS_SIZE.get(o1) - ALL_CARDS_SIZE.get(o2);
            }
        });
    }
}
```

练习：简单图书管理系统的开发。

书籍Book类

```Java
public class Book {
    private String name;
    private double price;
    private String author;

    public Book() {
    }

    public Book(String name, double price, String author) {
        this.name = name;
        this.price = price;
        this.author = author;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }
}
```

图书管理BookSystem类

```Java
import java.util.*;

public class BookSystem {
    public static final Map<String, List<Book>> BOOK_STORE = new HashMap<>();
    public static final Scanner SYS_SCANNER = new Scanner(System.in);

    public static void main(String[] args) {
        showCommand();
    }

    private static void showCommand() {
        System.out.println("====================欢迎您进入系统====================");
        System.out.println("(1) 查看全部书籍。query");
        System.out.println("(2) 添加书本信息。add");
        System.out.println("(3) 删除书本信息。delete");
        System.out.println("(4) 修改书本信息。update");
        System.out.println("(5) 退出系统。exit");
        System.out.print("请您输入您的操作命令：");
        String command = SYS_SCANNER.nextLine();

        switch (command) {
            case "query":
                queryBooks();
                break;
            case "add":
                addBook();
                break;
            case "delete":
                deleteBook();
                break;
            case "update":
                updateBook();
                break;
            case "exit":
                System.out.println("退出成功，期待您下次光临！");
                System.exit(0);
                break;
            default:
                System.err.println("您的输入有误，请重新确认！");
        }
        showCommand();
    }

    private static void deleteBook() {
        queryBooks();
        System.out.println("====================欢迎您进入删除书本业务====================");
        while (true) {
            System.out.println("请您输入删除书本的栏目：");
            String type = SYS_SCANNER.nextLine();
            if (BOOK_STORE.containsKey(type)) {
                while (true) {
                    System.out.println("请问您要删除的书本名称是：");
                    String name = SYS_SCANNER.nextLine();
                    Book book = getBookByTypeAndName(type, name);
                    if (book == null) {
                        System.out.println("不存在这本书！");
                    } else {
                        List<Book> books = BOOK_STORE.get(type);
                        books.remove(book);
                        System.out.println("删除成功！");
                        queryBooks();
                        return;
                    }
                }
            } else {
                System.err.println("您的栏目输入有误，请确认！");
            }
        }
    }

    private static void updateBook() {
        if (BOOK_STORE.size() == 0) {
            System.out.println("您现在根本没有任何栏目可以修改！");
        } else {
            queryBooks();
            System.out.println("====================欢迎您进入修改书本业务====================");
            while (true) {
                System.out.println("请您输入修改书本的栏目：");
                String type = SYS_SCANNER.nextLine();
                if (BOOK_STORE.containsKey(type)) {
                    while (true) {
                        System.out.println("请您输入修改书本的名称：");
                        String name = SYS_SCANNER.nextLine();
                        Book book = getBookByTypeAndName(type, name);
                        if (book == null) {
                            System.err.println("您输入的书名是不存在的，请重新确认！");
                        } else {
                            System.out.println("请您输入修改书本的新名称：");
                            String newName = SYS_SCANNER.nextLine();
                            System.out.println("请您输入修改书本的新价格：");
                            String newPrice = SYS_SCANNER.nextLine();
                            System.out.println("请您输入修改书本的新作者：");
                            String newAuthor = SYS_SCANNER.nextLine();
                            book.setName(newName);
                            book.setPrice(Double.valueOf(newPrice));
                            book.setAuthor(newAuthor);
                            queryBooks();
                            System.out.println("您修改的书本成功，请看如上信息确认！");
                            return;
                        }
                    }
                } else {
                    System.out.println("您输入的栏目不存在，请重新确认！");
                }
            }
        }
    }

    public static Book getBookByTypeAndName(String type,String name) {
        List<Book> books = BOOK_STORE.get(type);
        for (Book book : books) {
            if (book.getName().equals(name)) {
                return book;
            }
        }
        return null;
    }

    private static void queryBooks() {
        System.out.println("====================欢迎您进入查询书本业务====================");
        if (BOOK_STORE.size() == 0) {
            System.out.println("您的图书馆一本书都没有，请赶紧买书去！");
        } else {
            System.out.println("类型\t\t\t\t书名\t\t\t\t\t价格\t\t\t作者");
            BOOK_STORE.forEach((type,books) -> {
                System.out.println(type);
                for (Book book : books) {
                    System.out.println("\t\t\t\t" + book.getName() + "\t\t\t\t" + book.getPrice() + "\t\t\t" + book.getAuthor());
                }
            });
        }
    }

    private static void addBook() {
        System.out.println("====================欢迎您进入添加书本业务====================");
        System.out.println("请您输入添加书本的栏目：");
        String type = SYS_SCANNER.nextLine();
        List<Book> books = null;
        if (BOOK_STORE.containsKey(type)) {
            books = BOOK_STORE.get(type);
        } else {
            books = new ArrayList<>();
            BOOK_STORE.put(type,books);
        }

        System.out.println("请您输入添加书本的名称：");
        String name = SYS_SCANNER.nextLine();
        System.out.println("请您输入添加书本的价格：");
        String price = SYS_SCANNER.nextLine();
        System.out.println("请您输入添加书本的作者：");
        String author = SYS_SCANNER.nextLine();
        Book book = new Book(name,Double.valueOf(price),author);
        books.add(book);
        System.out.println("您添加在" + type + "下的书本" + book.getName() + "成功！");

    }
}
```

## 12. 基础算法

**冒泡排序**

作用：可以用于对数组或者对集合的元素进行大小排序。

核心算法思想：每次从数组的第一个位置开始两两比较。把较大的元素与较小的元素进行层层交换。最终把当前最大的一个元素存入到数组当前的末尾。这就是冒泡思想。

```Java
import java.util.Arrays;

public class BubbleSort {
    public static void main(String[] args) {
        int[] arr = new int[]{55, 22, 99, 88};
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = 0; j < arr.length - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
        System.out.println(Arrays.toString(arr));
    }
}
```

**选择排序**

选择排序的思想：从当前位置开始找出后面的较小值与该位置交换。

思路

- 控制选择几轮：数组的长度-1
- 控制每轮从当前位置开始比较几次

```Java
import java.util.Arrays;

public class SelectSort {
    public static void main(String[] args) {
        int[] arr = new int[]{5, 1, 3, 2};
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[i] > arr[j]) {
                    int temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }
        System.out.println(Arrays.toString(arr));
    }
}
```

**二分查找**

二分查找的前提：对数组是有要求的，数组必须已经排好序。

思路：每次先与中间的元素进行比较，如果大于往右边找，如果小于往左边找，如果等于就返回该元素索引位置。如果没有该元素，返回-1。综合性能比较好。

```Java
public class BinarySearch {
    public static void main(String[] args) {
        int[] arr = {10, 14, 21, 38, 45, 47, 53, 81, 87, 99};
        int index = binarySearch(arr, 53);
        System.out.println(index);
    }

    public static int binarySearch(int[] arr, int number) {
        int start = 0;
        int end = arr.length - 1;
        while (start <= end) {
            int middleIndex = (start + end) / 2;
            if (number > arr[middleIndex]) {
                start = middleIndex + 1;
            } else if (number < arr[middleIndex]) {
                end = middleIndex - 1;
            } else if (number == arr[middleIndex]) {
                return middleIndex;
            }
        }
        return -1;
    }
}
```

## 13. 异常

### 13.1 异常的概念和体系

什么是异常

- 异常是程序在“编译”或者“执行”的过程中可能出现的问题。
- 异常是应该尽量提前避免的。
- 异常可能也是无法做到绝对避免的，异常可能有太多情况了，开发中只能提前干预。
- 异常一旦出现了，若果没有提前处理，程序就会退出JVM虚拟机而终止，开发中异常是需要提前处理的。

研究异常并且避免异常，然后提前处理异常，体现的是程序的安全，健壮性。

Java会为常见的代码异常都设计一个类来代表。

Error：错误的意思，严重错误Error，无法通过处理的错误，一旦出现，程序员无能为力了。只能重启系统，优化项目。比如内存崩溃，JVM本身的崩溃。这个程序员无需理会。

Exception：异常类，它才是开发中代码在编译或者执行的过程中可能出现的错误，它是需要提前处理的。以便程序更健壮。

Exception异常的分类

- 编译时异常：继承自Exception的异常或者其子类，编译阶段就会报错，必须程序员处理的。否则代码编译就不能通过。
- 运行时异常：继承自RuntimeException的异常或者其子类，编译阶段是不会报错的，它是在运行时阶段可能出现，运行时异常可以处理也可以不处理，编译阶段是不会出错的，但是运行阶段可能出现，还是建议提前处理。

**运行时异常**

运行时异常概念

- 继承自RuntimeException的异常或者其子类
- 编译阶段是不会出错的，它是在运行时阶段可能出现的错误
- 运行时异常编译阶段可以处理也可以不处理，代码编译都能通过

常见运行时异常

- 数组索引越界异常：ArrayIndexOutOfBoundsException。
- 空指针异常：NullPointerException。直接输出没有问题，但是调用空指针的变量的功能就会报错。
- 类型转换异常：ClassCastException。
- 迭代器遍历没有此元素异常：NoSuchElementException。
- 数学操作异常：ArithmeticException。
- 数字转换异常：NumberFormatException。

**编译时异常**

编译时异常继承自Exception的异常或者其子类，没有继承RuntimeException。“编译时异常是编译阶段就会报错”。必须程序员编译阶段就处理的，否则代码编译就报错。

编译时异常的作用：是担心程序员的技术不行，在编译阶段就报出一个错误，目的在于提醒。提醒程序员这里很可能出错，请检查并注意不要出bug。

### 13.2 异常处理

异常产生默认的处理过程解析

- 默认会在出现异常的代码哪里自动的创建一个异常对象：ArithmeticException。
- 异常会从方法中出现的点这里抛出给调用者，调用者最终抛出给JVM虚拟机。
- 虚拟机接收到异常对象后，先在控制台直接输出异常栈信息数据。
- 直接从当前执行的异常点干掉当前程序。
- 后续代码没有机会执行了，因为程序已经死亡。

**编译时异常的处理**

方式一：出现异常的地方层层抛出，谁都不处理，最终抛给虚拟机。这种方式虽然可以解决编译时异常，但是如果异常真的出现了，程序会直接死亡，所以这种方式并不好。

方式二：使用try...catch捕获异常，可以处理异常，并且出现异常后代码也不会死亡。这种方案还是可以的。但从理论上来说，这种方式不是最好的，上层调用者不能直接知道底层的执行情况。

方式三：在出现异常的地方把异常一层一层地抛出给最外层调用者，最外层调用者集中捕获处理。这种方案最外层调用者可以知道底层执行的情况，同时程序在出现异常后也不会立即死亡，这是理论上最好的方案。

虽然异常有三种处理方式，但是开发中只要能解决你的问题，每种方式都有可能用到。

**运行时异常的处理**

运行时异常可以自动抛出，不需要我们手工抛出。

运行时异常的处理规范：直接在最外层捕获处理即可，底层会自动抛出。

finally的作用：可以在代码执行完毕以后进行资源的释放操作。

什么是资源：资源都是实现了Closeable接口的，都自带close()关闭方法。

异常的语法注意

- 运行时异常被抛出可以不处理。可以自动抛出，编译时异常必须处理，按照规范都应该处理。
- 重写方法申明抛出的异常，应该与父类被重写方法申明抛出的异常一样或者更小。
- 方法默认都可以自动抛出运行时异常，throws RuntimeException可以省略不写。
- 在多异常处理时，捕获处理，前边的异常类不能是后边异常类的父类。
- 在try/catch后可以追加finally代码块，其中的代码一定会被执行，通常用于资源回收操作。

### 13.3 自定义异常

自定义编译时异常

- 定义一个异常类继承Exception
- 重写构造器
- 在出现异常的地方用throw new 自定义对象抛出
- 编译时异常是编译阶段就报错，提醒更加强烈，一定需要处理

自定义运行时异常

- 定义一个异常类继承RuntimeException
- 重写构造器
- 在出现异常的地方用throw new 自定义对象抛出
- 提醒不强烈，编译阶段不报错

异常的作用

- 可以处理代码问题，防止程序出现异常后的死亡
- 提高了程序的健壮性和安全性

## 14. 多线程

### 14.1 多线程概述

进程：程序是静止的，运行中的程序就是进程。

进行的三个特征

- 动态性：进程是运行中的程序，要动态的占用内存，CPU和网络资源。
- 独立性：进程与进程之间是相互独立的，彼此有自己的独立内存区域。
- 并发性：假如CPU是单核，同一个时刻其实内存中只有一个进程在被执行。CPU会分时轮询切换依次为每个进程服务，因为切换的速度非常快，给我们的感觉这些进程在同时执行，这就是并发性。

并行：同一个时刻同时有多个在执行。

线程

- 线程是属于进程的。一个进程可以包含多个线程，这就是多线程。
- 线程创建开销相对于进程来说比较小。
- 线程也支持并发性。

线程的作用

- 可以提高程序的效率，线程也支持并发性，可以有更多机会得到CPU。
- 多线程可以解决很多业务模型。
- 大型高并发技术的核心技术。
- 涉及到多线程的开发可能都比较难理解。

### 14.2 线程的创建

创建线程的方式有三种

1. 直接定义一个类继承线程类Thread，重写run方法，创建线程对象，调用线程对象的start()方法启动线程。
2. 定义一个线程任务类实现Runnable接口，重写run()方法，创建线程任务对象，把线程任务对象包装成线程对象，调用线程对象的start()方法启动线程。
3. 实现Callable接口(拓展)。

继承Thread类的方式

- 定义一个线程类继承Thread类
- 重写run()方法
- 创建一个新的线程对象
- 调用线程对象的start()方法启动线程

继承Thread类的优缺点

- 优点：编码简单
- 缺点：线程类已经继承了Thread类无法继承其他类了，功能不能通过继承拓展

线程的注意事项

- 线程启动必须调用start()方法。否则当成普通类处理。
  - 如果线程直接调用run()方法，相当于变成了普通类的执行，此时将只有主线程在执行他们
  - start()方法底层其实是给CPU注册当前的线程，并且触发run()方法执行
- 建议线程先创建子线程，主线程的任务放在之后。否则主线程是先执行完。

Thread类的API

- public void setName(String name)：给当前线程取名字。
- public void getName()：获取当前线程的名字。
  - 线程存在默认名称，子线程的默认名称是：Thread-索引。
  - 主线程的默认名称就是：main。
- public static Thread currentThread()：获取当前线程对象，这个代码在哪个线程中，就得到哪个线程对象。
- public static void sleep(long time)：让当前线程休眠多少毫秒再继续执行。

实现Runnable接口的方式

- 创建一个线程任务类实现Runnable接口
- 重写run()方法
- 创建一个线程任务对象
- 把线程任务对象包装成线程对象
- 调用线程对象的start()方法启动线程

实现Runnable接口的优缺点

- 优点
  - 线程任务类只是实现了Runnable接口，可以继续继承其他类，同时可以继续实现其他接口
  - 一个线程任务对象可以被共享成多个线程对象，适合做多线程的资源共享操作
  - 实现解耦操作，线程任务代码可以被多个线程共享，任务代码和线程独立
  - 线程池可以放入实现Runnable或Callable线程任务对象
  - 很适合做线程池的执行任务
- 缺点
  - 编码相对复杂
  - 无法直接得到线程执行的结果

实现Callable接口

- 定义一个线程任务类实现Callable接口，申明线程执行的结果类型
- 重写线程任务类的call方法，这个方法可以直接返回执行的结果
- 创建一个Callable的线程任务对象
- 把Callable的线程任务对象包装成一个未来任务对象
- 把未来任务对象包装成线程对象
- 调用线程的start()方法启动线程

优缺点

- 优点：全是优点。
  - 线程任务类只是实现了Callable接口，可以继续继承其他类，同时可以继续实现其他接口
  - 一个线程任务对象可以被共享成多个线程任务对象，适合做多线程的资源共享操作
  - 很适合做线程池的执行操作
  - 可以直接获取线程执行的结果
- 缺点：编码复杂。

案例

```Java
import java.util.concurrent.Callable;
import java.util.concurrent.FutureTask;

public class ThreadDemo02 {
    public static void main(String[] args) {
        Callable<String> call = new MyCallable();
        // 把Callable任务对象包装成一个未来任务对象
        FutureTask<String> task = new FutureTask<>(call);
        Thread t = new Thread(task);
        t.start();

        for (int i = 1; i <= 10; i++) {
            System.out.println(Thread.currentThread().getName() + ":" + i);
        }

        try {
            String rs = task.get(); // 获取call方法返回的结果
            System.out.println(rs);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class MyCallable implements Callable<String> {
    @Override
    public String call() throws Exception {
        int sum = 0;
        for (int i = 1; i <= 10; i++) {
            System.out.println(Thread.currentThread().getName() + ":" + i);
            sum += i;
        }
        return Thread.currentThread().getName() + "执行的结果是：" + sum;
    }
}
```

### 14.3 线程安全

线程安全问题：多个线程同时操作同一个共享资源的时候可能会出现线程安全问题。

问题案例：两人同时从银行账户取钱。

银行账户类Account

```Java
public class Account {
    private String cardID;
    private double money;

    public Account() {
    }

    public Account(String cardID, double money) {
        this.cardID = cardID;
        this.money = money;
    }

    public String getCardID() {
        return cardID;
    }

    public void setCardID(String cardID) {
        this.cardID = cardID;
    }

    public double getMoney() {
        return money;
    }

    public void setMoney(double money) {
        this.money = money;
    }

    public void drawMoney(double money) {
        String name = Thread.currentThread().getName();
        if (this.money >= money) {
            System.out.println(name + "来取钱，余额足够，吐出" + money);
            this.money -= money;
            System.out.println(name + "来取钱后，余额剩余" + this.money);
        } else {
            System.out.println(name + "来取钱，余额不足！");
        }
    }
}
```

取钱线程类DrawThread

```Java
public class DrawThread extends Thread {
    private Account acc;
    public DrawThread(Account acc,String name) {
        super(name);
        this.acc = acc;
    }
    @Override
    public void run() {
        acc.drawMoney(100000);
    }
}
```

取钱类ThreadSafe

```Java
public class ThreadSafe {
    public static void main(String[] args) {
        Account acc = new Account("ICBC-110",100000);

        Thread littleMing = new DrawThread(acc,"小明");
        littleMing.start();

        Thread littleRed = new DrawThread(acc,"小红");
        littleRed.start();
    }
}
```

线程同步的作用：就是为了解决线程安全问题的方案。

线程同步解决线程安全问题的核心思想：让多个线程实现先后依次访问共享资源，这样就解决了安全问题。

线程同步的做法：是把共享资源进行上锁，每次只能一个线程进入，访问完毕以后，其他线程才能进来。

线程同步的方式有三种

- 同步代码块
- 同步方法
- lock显示锁

**同步代码块**

作用：把出现线程安全问题的核心代码给上锁，每次只能一个线程进入，执行完毕以后自动解锁，其他线程才可以进来执行。

格式

```Java
synchronized(锁对象){
    // 访问共享资源的核心代码
}
```

锁对象：理论上可以是任意的“唯一”对象即可。

原则上：锁对象建议使用共享资源。

- 在实例方法中建议用this作为锁对象。此时this正好是共享资源。
- 在静态方法中建议用类名.class字节码作为锁对象。

修改代码如下

```Java
public void drawMoney(double money) {
    String name = Thread.currentThread().getName();
    synchronized (this) {
        if (this.money >= money) {
            System.out.println(name + "来取钱，余额足够，吐出" + money);
            this.money -= money;
            System.out.println(name + "来取钱后，余额剩余" + this.money);
        } else {
            System.out.println(name + "来取钱，余额不足！");
        }
    }
}
```

**同步方法**

作用：把出现线程安全问题的核心方法给锁起来，每次只能一个线程进入访问，其他线程必须在方法外面等待。

用法：直接给方法加上一个修饰符synchronized。

原理：同步方法的原理和同步代码块的底层原理其实是完全一样的，只是同步方法是把整个方法的代码都锁起来。

同步方法其实底层也是有锁对象的

- 如果方法是实例方法：同步方法默认用this作为锁对象。
- 如果方法是静态方法：同步方法默认用类名.class作为的锁对象。

修改代码

```Java
public synchronized void drawMoney(double money) {
    String name = Thread.currentThread().getName();
    if (this.money >= money) {
        System.out.println(name + "来取钱，余额足够，吐出" + money);
        this.money -= money;
        System.out.println(name + "来取钱后，余额剩余" + this.money);
    } else {
        System.out.println(name + "来取钱，余额不足！");
    }
}
```

**lock显示锁**

java.util.concurrent.locks.Lock机制提供了比synchronized代码块和synchronized方法更广泛的锁定操作，同步代码块/同步方法具有的功能Lock都有，除此之外更强大。

Lock锁也称同步锁，加锁与释放锁方法化了，如下：

- public void lock()：加同步锁
- public void unlock()：释放同步锁

修改代码

```Java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class Account {
    private String cardID;
    private double money;
    private final Lock lock = new ReentrantLock();

    public Account() {
    }

    public Account(String cardID, double money) {
        this.cardID = cardID;
        this.money = money;
    }

    public String getCardID() {
        return cardID;
    }

    public void setCardID(String cardID) {
        this.cardID = cardID;
    }

    public double getMoney() {
        return money;
    }

    public void setMoney(double money) {
        this.money = money;
    }

    public void drawMoney(double money) {
        String name = Thread.currentThread().getName();
        lock.lock();
        try {
            if (this.money >= money) {
                System.out.println(name + "来取钱，余额足够，吐出" + money);
                this.money -= money;
                System.out.println(name + "来取钱后，余额剩余" + this.money);
            } else {
                System.out.println(name + "来取钱，余额不足！");
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
}
```

### 14.4 线程通信

线程通信：多个线程因为在同一个进程中，所以互相通信是比较容易的。

线程通信的经典模型：生产者与消费者问题。

- 生产者负责生成商品，消费者负责消费商品
- 生产不能过剩，消费不能没有

注意：线程通信一定是多个线程在操作同一个资源才需要进行通信。线程通信必须先保证线程安全，否则毫无意义，代码也会报错。

线程通信的核心方法

- public void wait()：让当前线程进入到等待状态，此方法必须锁对象调用。
- public void notify()：唤醒当前锁对象上等待状态的某个线程，此方法必须锁对象调用。
- public void notifyAll()：唤醒当前锁对象上等待状态的全部线程，此方法必须锁对象调用。

小结：是一种等待唤醒机制。必须是在同一个共享资源才需要通信，而且必须保证线程安全。

练习：银行存取钱案例。

银行账户类Account

```Java
public class Account {
    private String cardId;
    private double money;

    public Account() {
    }

    public Account(String cardId, double money) {
        this.cardId = cardId;
        this.money = money;
    }

    public String getCardId() {
        return cardId;
    }

    public void setCardId(String cardId) {
        this.cardId = cardId;
    }

    public double getMoney() {
        return money;
    }

    public void setMoney(double money) {
        this.money = money;
    }

    public synchronized void drawMoney(double money) {
        try {
            String name = Thread.currentThread().getName();
            if (this.money >= money) {
                this.money -= money;
                System.out.println(name + "来取钱，取钱：" + money + "剩余：" + this.money);
                this.notifyAll();
                this.wait();
            } else {
                this.notifyAll();
                this.wait();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public synchronized void saveMoney(double money) {
        try {
            String name = Thread.currentThread().getName();
            if (this.money > 0) {
                this.notifyAll();
                this.wait();
            } else {
                this.money += money;
                System.out.println(name + "来存钱：" + money);
                this.notifyAll();
                this.wait();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

存钱线程类SaveThread

```Java
public class SaveThread extends Thread {
    private Account acc;
    public SaveThread(Account acc, String name) {
        super(name);
        this.acc = acc;
    }
    @Override
    public void run() {
        while (true) {
            try {
                Thread.sleep(3000);
            } catch (Exception e) {
                e.printStackTrace();
            }
            acc.saveMoney(10000);
        }
    }
}
```

取钱线程类DrawThread

```Java
public class DrawThread extends Thread {
    private Account acc;
    public DrawThread(Account acc, String name) {
        super(name);
        this.acc = acc;
    }
    @Override
    public void run() {
        while (true) {
            try {
                Thread.sleep(3000);
            } catch (Exception e) {
                e.printStackTrace();
            }
            acc.drawMoney(10000);
        }
    }
}
```

线程通信类ThreadCommunication

```Java
public class ThreadCommunication {
    public static void main(String[] args) {
        Account acc = new Account("ICBC-111",0);

        new DrawThread(acc,"小明").start();
        new DrawThread(acc,"小红").start();

        new SaveThread(acc,"亲爹").start();
        new SaveThread(acc,"干爹").start();
        new SaveThread(acc,"岳父").start();
    }
}
```

### 14.5 线程池

线程池：其实就是一个容纳多个线程的容器，其中的线程可以反复地使用，省去了频繁创建和销毁线程对象的操作，无需反复创建线程而消耗过多资源。

合理利用线程池能够带来三个好处

1. 降低资源消耗。
   - 减少了创建和销毁线程的次数，每个工作线程都可以被重复利用，可执行多个任务。
2. 提高响应速度。
   - 不需要频繁地创建线程，如果有线程可以直接用，不会出现系统僵死。
3. 提高线程的可管理性(线程池可以约束系统最多只能有多少个线程，不会因为线程过多而死机)

线程池的核心思想：线程复用，同一个线程可以被重复使用，来处理多个任务。

线程池在Java中的代表类：ExecutorService(接口)。

Java在Executors类下提供了一个静态方法得到一个线程池的对象

- public static ExecutorService newFixedThreadPool(int nThreads)：创建一个线程池返回。

ExecutorService提交线程任务对象执行的方法

- Future<?> submit(Runnable task)：提交一个Runnable的任务对象给线程池执行。
- Future<?> submit(Callable task)：提交一个Callable的任务对象给线程池执行。

小结

- pools.shutdown()：等待任务执行完毕以后才会关闭线程池。
- pools.shutdownNow()：立即关闭线程池的代码，无论任务是否执行完毕。
- 线程池中的线程可以被复用，线程用完以后可以继续去执行其他任务。
- Callable做线程池的任务可以得到线程执行的结果。

```Java
public class ThreadPoolsDemo01 {
    public static void main(String[] args) {
        ExecutorService pools = Executors.newFixedThreadPool(3);
        Future<String> t1 = pools.submit(new MyCallable(100));
        Future<String> t2 = pools.submit(new MyCallable(200));
        Future<String> t3 = pools.submit(new MyCallable(300));
        Future<String> t4 = pools.submit(new MyCallable(400));

        try {
            String rs1 = t1.get();
            String rs2 = t2.get();
            String rs3 = t3.get();
            String rs4 = t4.get();
            System.out.println(rs1);
            System.out.println(rs2);
            System.out.println(rs3);
            System.out.println(rs4);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class MyCallable implements Callable<String> {
    private int n;
    public MyCallable(int n) {
        this.n = n;
    }
    @Override
    public String call() throws Exception {
        int sum = 0;
        for (int i = 1; i <= n; i++) {
            sum += i;
        }
        return Thread.currentThread().getName() + "执行的结果是：" + sum;
    }
}
```

### 14.6 死锁

死锁是这样一种情形：多个线程同时被阻塞，它们中的一个或者全部都在等待某个资源被释放。由于线程被无限期地阻塞，因此程序不可能正常终止。

Java死锁产生的四个必要条件

- 互斥使用：即当资源被一个线程使用(占用)时，别的线程不能使用。
- 不可抢占：资源请求者不能强制从资源占有者手中夺取资源，资源只能由资源占有者主动释放。
- 请求和保持：即当资源请求者在请求其他的资源的同时保持对原有资源的占有。
- 循环等待：即存在一个等待循环队列，p1要p2的资源，p2要p1的资源。这样就形成了一个等待环路。

当上述四个条件都成立的时候，便形成死锁。当然，死锁的情况下如果打破上述任何一个条件，便可让死锁消失。

实现死锁案例代码

```Java
public class ThreadDead {
    public static Object resources01 = new Object();
    public static Object resources02 = new Object();

    public static void main(String[] args) {
        new Thread(new Runnable() {
            @Override
            public void run() {
                synchronized (resources01) {
                    System.out.println("线程1占用资源1请求资源2");
                    try {
                        Thread.sleep(1000);
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                    synchronized (resources02) {
                        System.out.println("线程1成功占用资源2");
                    }
                }
            }
        }).start();

        new Thread(new Runnable() {
            @Override
            public void run() {
                synchronized (resources02) {
                    System.out.println("线程2占用资源2请求资源1");
                    try {
                        Thread.sleep(1000);
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                    synchronized (resources01) {
                        System.out.println("线程2成功占用资源1");
                    }
                }
            }
        }).start();
    }
}
```

## 15. Volatile关键字

### 15.1 变量不可见性

多个线程访问共享变量，会出现一个线程修改变量的值后，其他线程看不到最新值的情况。

并发变量下变量不可见性案例

```Java
public class VolatileDemo extends Thread {
    private boolean flag = false;

    @Override
    public void run() {
        try {
            Thread.sleep(1000);
        } catch (Exception e) {
            e.printStackTrace();
        }
        flag = true;
        System.out.println("flag = " + flag);
    }

    public boolean isFlag() {
        return flag;
    }

    public void setFlag(boolean flag) {
        this.flag = flag;
    }
}

class VisibilityDemo {
    public static void main(String[] args) {
        VolatileDemo t = new VolatileDemo();
        t.start();

        while (true) {
            if (t.isFlag()) {
                System.out.println("主线程进入执行~~~~");
            }
        }
    }
}
```

不可见性的原因：每个线程都有自己的工作内存，线程都是从主内存拷贝共享变量的副本值。每个线程是在自己的工作内存中操作共享变量的。

解决方案有两种常见方式

1. 加锁
   - 每次加锁会清空线程自己的工作内存，重新读取主内存最新值。
2. 对共享的变量进行volatile关键字修饰
   - volatile修饰的变量可以在多线程并发修改下，实现线程间变量的可见性。
   - 一旦一个线程修改了volatile修饰的变量，另一个线程可以立即取到最新值。

加锁方式

修改后的代码

```Java
while (true) {
    synchronized (VisibilityDemo01.class) {
        if (t.isFlag()) {
            System.out.println("主线程进入执行~~~~");
        }
    }
}
```

某一个线程进入synchronized代码块前后，执行过程如下

- 线程获得锁
- 清空工作内存
- 从主内存拷贝共享变量最新的值到工作内存成为副本
- 执行代码
- 将修改后的副本的值刷新回主内存中
- 线程释放锁

volatile关键字修饰

修改代码

```Java
private volatile boolean flag = false;
```

工作流程

- 子线程从主内存读取到数据放入其对应的工作内存
- 将flag的值更改为true，但是这个时候flag的值还没有写回主内存
- 此时main方法读取到了flag的值为false
- 当子线程将flag的值写回去后，失效其他线程对此变量的副本
- 再次对flag进行操作的时候线程会从主内存读取最新的值，放入到工作内存中

**volatile与synchronized**

- volatile只能修饰实例变量和类变量，而synchronized可以修饰方法，以及代码块。
- volatile保证数据的可见性，但是不保证原子性(多线程进行写操作，不保证线程安全)；而synchronized是一种排他(互斥)的机制。

### 15.2 原子性

概述：所谓的原子性是指在一次操作或者多次操作中，要么所有的操作全部都得到了执行并且不会受到任何因素的干扰而中断，要么所有的操作都不执行。

volatile只能保证线程间变量的可见性，但是不能保证变量操作的原子性。

加锁保证原子性代码

```Java
public class VolatileAtomicDemo {
    public static void main(String[] args) {
        Runnable target = new MyRunnable();
        for (int i = 1; i <= 100; i++) {
            new Thread(target).start();
        }
    }
}

class MyRunnable implements Runnable {
    private int count;

    @Override
    public void run() {
        synchronized ("DiLei") {
            for (int i = 1; i <= 100; i++) {
                count++;
                System.out.println("count=====>>>" + count);
            }
        }
    }
}
```

加锁机制性能较差。

**原子类**

概述：Java从JDK1.5开始提供了java.util.concurrent.atomic包(简称Atomic包)，这个包中的原子操作类提供了一种用法简单，性能高效，线程安全的更新一个变量的方式。

使用原子类实现原子性操作

```Java
import java.util.concurrent.atomic.AtomicInteger;

public class VolatileAtomicDemo {
    public static void main(String[] args) {
        Runnable target = new MyRunnable();
        for (int i = 1; i <= 100; i++) {
            new Thread(target).start();
        }
    }
}

class MyRunnable implements Runnable {
    private AtomicInteger atomicInteger = new AtomicInteger();

    @Override
    public void run() {
        for (int i = 1; i <= 100; i++) {
            System.out.println("count=====>>>" + atomicInteger.incrementAndGet());
        }
    }
}
```

**原子类CAS机制**

CAS的全称是：Compare And Swap(比较再交换)；是现代CPU广泛支持的一种对内存中的共享数据进行操作的一种特殊指令。CAS可以将read-modify-check-write转换为原子操作，这个原子操作直接由处理器保证。

CAS机制当中使用了3个基本操作数：内存地址V，旧的预期值A，要修改的新值B。

**CAS与Synchronized：乐观锁，悲观锁**

CAS和Synchronized都可以保证多线程环境下共享数据的安全性。那么他们两者有什么区别？

Synchronized是从悲观的角度出发

总是假设最坏的情况，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会阻塞直到它拿到锁。

共享资源每次只给一个线程使用，其他线程阻塞，用完后再把资源转让给其它线程。因此Synchronized我们也将其称之为悲观锁。JDK中的ReentrantLock也是一种悲观锁，性能较差。

CAS是从乐观的角度出发

总是假设最好的情况，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据。

CAS这种机制我们也可以将其称之为乐观锁，综合性能较好。

## 16. 并发包

并发包的来历：在实际开发中如果不需要考虑线程安全问题，大家不需要做线程安全，因为如果做了反而性能不好。但是开发中有很多业务是需要考虑线程安全问题的，此时就必须考虑了。否则业务出现问题。Java为很多业务场景提供了性能优异，且线程安全的并发包，程序员可以选择使用。

### 16.1 ConcurrentHashMap

Map集合中的经典集合：HashMap它是线程不安全的，性能好。

- 如果在要求线程安全的业务情况下就不能用这个集合做Map集合，否则业务会崩溃

为了保证线程安全，可以使用Hashtable。注意：线程中加入了计时。

- Hashtable是线程安全的Map集合，但是性能较差。(已经被淘汰，虽然安全，但是性能差)

为了保证线程安全，再看ConcurrentHashMap(不只线程安全，而且效率高，性能好，最新最好用的线程安全的类)。

- ConcurrentHashMap保证了线程安全，综合性能较好

HashMap、Hashtable与ConcurrentHashMap的案例

```Java
import java.util.HashMap;
import java.util.Hashtable;
import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;

public class ConcurrentHashMapDemo {
    public static Map<String,String> maps = new ConcurrentHashMap<>();

    public static void main(String[] args) {
        Runnable target = new MyRunnable();
        Thread t1 = new Thread(target,"线程1");
        Thread t2 = new Thread(target,"线程2");
        t1.start();
        t2.start();

        try {
            t1.join();  // 让t1跑完，让当前主线程不能竞争t1的CPU。
            t2.join();  // 让t2跑完，让当前主线程不能竞争t2的CPU。
        } catch (Exception e) {
            e.printStackTrace();
        }

        System.out.println("元素个数：" + maps.size());
    }
}

class MyRunnable implements Runnable {
    @Override
    public void run() {
        long start = System.currentTimeMillis();
        for (int i = 1; i <= 500000; i++) {
            ConcurrentHashMapDemo.maps.put(Thread.currentThread().getName() + i, Thread.currentThread().getName() + i);
        }
        long end = System.currentTimeMillis();
        System.out.println(Thread.currentThread().getName() + "耗时：" + (end - start) / 1000.0 + "s");
    }
}
```

### 16.2 CountDownLatch

CountDownLatch允许一个或多个线程等待其他线程完成操作，再执行自己。

例如：线程1要执行打印：A和C，线程2要执行打印：B，但线程1在打印A后，要线程2打印B之后才能打印C，所以：线程1在打印A后，必须等待线程2打印完B之后才能继续执行。

构造器

- public CountDownLatch(int count) ：初始化唤醒需要的down几步。

方法

- public void await() throws InterruptedException：让当前线程等待，必须down
- public void countDown()：计数器进行减1 （down 1）

打印机案例

```Java
import java.util.concurrent.CountDownLatch;

public class CountDownLatchDemo {
    public static void main(String[] args) {
        CountDownLatch c = new CountDownLatch(1);
        new ThreadA(c).start();
        new ThreadB(c).start();
    }
}

class ThreadA extends Thread {
    private CountDownLatch c;
    public ThreadA(CountDownLatch c) {
        this.c = c;
    }

    @Override
    public void run() {
        System.out.println("A");
        try {
            c.await();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("C");
    }
}

class ThreadB extends Thread {
    private CountDownLatch c;
    public ThreadB(CountDownLatch c) {
        this.c = c;
    }

    @Override
    public void run() {
        System.out.println("B");
        c.countDown(); // 让监督者中的计数器减1，被等待的线程就唤醒了
    }
}
```

### 16.3 CyclicBarrier

CyclicBarrier作用：某个线程任务必须等待其他线程执行完毕以后才能最终触发自己执行。

构造器

- public CyclicBarrier(int parties, Runnable barrierAction)：用于在线程到达屏障5时，优先执行barrierAction，方便处理更复杂的业务场景

方法

- public int await()：每个线程调用await方法告诉CyclicBarrier我已经到达了屏障，然后当前线程被阻塞

可以实现多线程中，某个任务在等待其他线程执行完毕以后触发。循环屏障可以实现达到一组屏障就触发一个任务执行。

员工进入会议室开会案例

```Java
import java.util.concurrent.CyclicBarrier;

public class CyclicBarrierDemo {
    public static void main(String[] args) {
        CyclicBarrier c = new CyclicBarrier(5, new Meeting());
        for (int i = 1; i <= 5; i++) {
            new EmployeeThread("员工" + i,c).start();
        }
    }
}

class Meeting implements Runnable {
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName() + "开始组织会议！");
    }
}

class EmployeeThread extends Thread {
    private CyclicBarrier c;
    public EmployeeThread(String name,CyclicBarrier c) {
        super(name);
        this.c = c;
    }

    @Override
    public void run() {
        try {
            Thread.sleep(3000);
            System.out.println(Thread.currentThread().getName() + "正在进入会议室");
            c.await();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 16.4 Semaphore

Semaphore(发信号)的主要作用是控制线程的并发数量。

synchronized可以起到“锁”的作用，但某个时间段内，只能有一个线程允许执行。

Semaphore可以设置同时允许几个线程执行。

Semaphore字面意思是信号量的意思，它的作用是控制访问特定资源的线程数目

Semaphore构造方法

- public Semaphore(int permits)：permits表示许可线程的数量
- public Semaphore(int permits, boolean fair)：fair表示公平性，如果这个设为true的话，下次执行的线程会是等待最久的线程

Semaphore重要方法

- public void acquire() throws InterruptException：表示获取许可
- public void release()：release()表示释放许可

Semaphore可以控制线程并发占锁的数量。

练习案例

```Java
import java.util.concurrent.Semaphore;

public class SemaphoreDemo {
    public static void main(String[] args) {
        Service service = new Service();
        for (int i = 1; i <= 5; i++) {
            MyThread a = new MyThread(service);
            a.start();
        }
    }
}

class MyThread extends Thread {
    private Service service;
    public MyThread(Service service) {
        this.service = service;
    }

    @Override
    public void run() {
        service.login();
    }
}

class Service {
    private Semaphore semaphore = new Semaphore(1);

    public void login() {
        try {
            semaphore.acquire();
            System.out.println(Thread.currentThread().getName() + "进入 时间=" + System.currentTimeMillis());
            try {
                Thread.sleep(1000);
                System.out.println(Thread.currentThread().getName() + "登录成功！");
            } catch (Exception e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName() + "离开 时间=" + System.currentTimeMillis());
            semaphore.release();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 16.5 Exchanger

作用：Exchanger(交换者)是一个用于线程间协作的工具类。Exchanger用于进行线程间的数据交换。这两个线程通过exchange方法交换数据，如果第一个线程先执行exchange()方法，它会一直等待第二个线程也执行exchange方法。当两个线程都达到同步点时，这两个线程就可以交换数据，将本线程生产出来的数据传递给对方。

Exchanger构造方法

- public Exchanger()

Exchanger重要方法

- public V exchange(V x)

分析

- 需要2个线程
- 需要一个交换对象负责交换两个线程执行的结果

小结：Exchanger可以实现线程间的数据交换。一个线程如果等不到对方的数据交换就会一直等待。我们也可以控制一个线程等待的时间，必须双方都进行交换才可以正常进行数据的交换。

练习案例如下

```Java
import java.util.concurrent.Exchanger;
import java.util.concurrent.TimeUnit;

public class ExchangerDemo {
    public static void main(String[] args) {
        Exchanger<String> exchanger = new Exchanger();
        new Boy(exchanger).start();
        new Girl(exchanger).start();
    }
}

class Boy extends Thread {
    private Exchanger<String> exchanger;
    public Boy(Exchanger<String> exchanger) {
        this.exchanger = exchanger;
    }

    @Override
    public void run() {
        System.out.println("男孩开始做好自己的定情信物：同心🔒！");
        try {
            String rs = exchanger.exchange("同心🔒",5, TimeUnit.SECONDS);
            System.out.println("男孩收到礼物：" + rs);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class Girl extends Thread {
    private Exchanger<String> exchanger;
    public Girl(Exchanger<String> exchanger) {
        this.exchanger = exchanger;
    }

    @Override
    public void run() {
        System.out.println("女孩开始做好自己的定情信物：钥匙🔑！");
        try {
            Thread.sleep(6000);
            String rs = exchanger.exchange("钥匙🔑");
            System.out.println("女孩收到礼物：" + rs);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 17. Lambda表达式

概述：Lambda表达式是JDK1.8开始之后的新技术，是一种代码的新语法。是一种特殊写法。

作用：“核心目的是为了简化匿名内部类的代码写法”。

Lambda表达式的格式

```Java
(匿名内部类被重写方法的形参列表) -> {
    被重写方法的方法体代码。
}
```

Lambda表达式的使用前提

- Lambda表达式并不能简化所有匿名内部类的写法
- Lambda表达式只能简化接口中只有一个抽象方法的匿名内部类形式

Lambda表达式只能简化函数式接口的匿名内部类写法

- 首先必须是接口
- 接口中只能有一个抽象方法

**Lambda表达式简化Runnable接口的匿名内部类写法**

**@FunctionalInterface函数式接口注解：**一旦某个接口加上了这个注解，这个接口只能有且仅有一个抽象方法。这个接口就可以被Lambda表达式简化。

```Java
public class LambdaDemo {
    public static void main(String[] args) {
        Thread t = new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println(Thread.currentThread().getName() + "：执行~~~");
            }
        });
        t.start();

        Thread t1 = new Thread(() -> System.out.println(Thread.currentThread().getName() + "：执行~~~"));
        t1.start();
    }
}
```

**Lambda简化Comparator接口匿名内部类写法**

```Java
public class LambdaDemo01 {
    public static void main(String[] args) {
        List<Student> lists = new ArrayList<>();
        Student s1 = new Student("李铭",18,'男');
        Student s2 = new Student("冯龙",23,'男');
        Student s3 = new Student("王乐乐",21,'男');
        Collections.addAll(lists,s1,s2,s3);

        Collections.sort(lists, new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                return o1.getAge() - o2.getAge();
            }
        });

        Collections.sort(lists,(Student o1, Student o2) -> {
            return o1.getAge() - o2.getAge();
        });
        System.out.println(lists);
    }
}
```

## 18. 方法引用

方法引用：方法引用是为了进一步简化Lambda表达式的写法。

方法引用的格式：类型或者对象::引用的方法。

关键语法是："::"。

```Java
import java.util.ArrayList;
import java.util.List;

public class MethodDemo {
    public static void main(String[] args) {
        List<String> lists = new ArrayList<>();
        lists.add("Java1");
        lists.add("Java2");
        lists.add("Java3");

        lists.forEach(s -> System.out.println(s));
        System.out.println("-------------------------");
        lists.forEach(System.out::println);
    }
}
```

方法引用有四种形式

- 静态方法的引用
- 实例方法的引用
- 特定类型方法的引用
- 构造器的引用

静态方法的引用

引用格式：类名::静态方法。

注意：被引用的方法的参数列表要和函数式接口中的抽象方法的参数列表一致。

实例方法的引用

引用格式：对象::实例方法。

特定类型方法的引用

特定类型：String，任何类型。

引用格式：特定类型::方法。

注意：如果第一个参数列表中的形参中的第一个参数作为了后面的方法的调用者，并且其余参数作为后面方法的形参，那么就可以用特定类型方法引用了。

```Java
import java.util.Arrays;
import java.util.Comparator;

public class MethodDemo {
    public static void main(String[] args) {
        String[] strs = new String[]{"James","AA","John","Patricia","Dlei","Robert","Boom","Cao","black","Michael","Linda","cao","after","sBBB"};

        Arrays.sort(strs);
        System.out.println(Arrays.toString(strs));

        Arrays.sort(strs, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return o1.compareToIgnoreCase(o2);
            }
        });

        Arrays.sort(strs,(o1, o2) -> o1.compareToIgnoreCase(o2));
        Arrays.sort(strs,String::compareToIgnoreCase);
        System.out.println(Arrays.toString(strs));
    }
```

构造器引用

引用格式：类名::new

注意：前后参数一致的情况下，又在创建对象就可以使用构造器引用。

## 19. Stream流

### 19.1 概述

Stream流：在Java 8中，得益于Lambda所带来的函数式编程，引入了一个全新的Stream流概念，用于解决已有集合/数组类库既有的弊端。

Stream流解决问题：可以解决已有集合类库或者数组API的弊端。Stream认为集合和数组操作的API很不好用，所以采用了Stream流简化集合和数组的操作。

小结：Stream流的核心思想是把集合或者数组转成一个Stream流(传送带)，然后使用Stream流的强大功能进行元素的处理。

```Java
import java.util.ArrayList;
import java.util.List;

public class StreamDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("张无忌");
        list.add("周芷若");
        list.add("赵敏");
        list.add("张强");
        list.add("张三丰");

        list.stream().filter(s -> s.startsWith("张")).filter(s -> s.length() == 3).forEach(System.out::println);
    }
```

### 19.2 Stream流操作

集合获取流的API

- default Stream\<E> stream()

小结

- 集合获取stream流用 stream();
- 数组：Arrays.stream(数组) / Stream.of(数组)

Stream流的常用API

- forEach：逐一处理(遍历)
- count：统计个数
  - long count();
- filter：过滤元素
  - Stream\<T> filter(Predicate<? super T> predicate)
- limit：取前几个元素
- skip：跳过前几个
- map：加工方法(把原来的元素加工以后，重新放上去)
- concat：合并流

```Java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Stream;

public class StreamDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("张无忌");
        list.add("周芷若");
        list.add("赵敏");
        list.add("张强");
        list.add("张三丰");

        Stream<Integer> s1 = Stream.of(10,20,30,40);
        Stream<String> s2 = list.stream();
        Stream<Object> allStream = Stream.concat(s1, s2);
        allStream.forEach(System.out::println);
        System.out.println("--------------------------");

        list.stream().filter(s -> s.length() == 3).filter(s -> s.startsWith("张")).forEach(System.out::println);
        System.out.println("--------------------------");

        long count = list.stream().count();
        System.out.println(count);
        System.out.println("--------------------------");

        list.stream().filter(s -> s.length() == 3).limit(1).forEach(System.out::println);
        System.out.println("--------------------------");

        list.stream().map(s -> "武当的：" + s).forEach(System.out::println);
    }
}
```

Stream终结与非终结方法

终结方法：一旦Stream调用了终结方法，流的操作就全部终结了，不能继续使用，只能创新的Stream操作

终结方法：forEach，count

非终结方法：每次调用完成以后返回一个新的流对象，可以继续使用，支持链式编程。

收集Stream流：把Stream流的数据转回成集合。

Stream的作用：把集合转换成一根传送带，借用Stream流的强大功能进行的操作。但是实际开发中数据最终的形式还是应该是集合，最终Stream流操作完毕以后还是要转换成集合。这就是收集Stream流。

Stream流：手段。

集合：才是目的。

流：只能操作一次。

```Java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class StreamDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("张无忌");
        list.add("周芷若");
        list.add("赵敏");
        list.add("张强");
        list.add("张三丰");
        list.add("张三丰");

        Stream<String> zhangLists = list.stream().filter(s -> s.startsWith("张"));
        Set<String> sets = zhangLists.collect(Collectors.toSet());
        System.out.println(sets);

        Stream<String> zhangLists1 = list.stream().filter(s -> s.startsWith("张"));
        List<String> lists = zhangLists1.collect(Collectors.toList());
        System.out.println(lists);

        Stream<String> zhangLists2 = list.stream().filter(s -> s.startsWith("张"));
        Object[] arrs = zhangLists2.toArray();
        Stream<String> zhangLists3 = list.stream().filter(s -> s.startsWith("张"));
        String[] arrs1 = zhangLists3.toArray(String[]::new);
        System.out.println(Arrays.toString(arrs1));

    }
}
```

## 20. File类

File类：代表操作系统的文件对象。是用来操作操作系统的文件对象的，删除文件，获取文件信息，创建文件(文件夹)。

广义来说：操作系统认为文件包含文件和文件夹。

File类创建文件对象的格式

- File f = new File("绝对路径/相对路径");
- 绝对路径：从磁盘的盘符一路走到目的位置的路径。
  - 绝对路径依赖具体的环境，一旦脱离环境，代码可能出错
  - 一般是定位某个操作系统中的某个文件对象
- 相对路径：不带盘符的。
  - 默认是直接相对到工程目录下寻找文件的
  - 相对路径只能用于寻找工程下的文件
  - 能用相对路径就应该尽量使用，可以跨平台
- File f = new File("文件对象/文件夹对象");

File类的获取功能的API

- public String getAbsolutePath()：返回此File的绝对路径名字符串。
- public String getPath()：获取创建文件对象的时候用的路径。
- public String getName()：返回由此File表示的文件或目录的名称。
- public long length()：返回由此File表示的文件的长度。

```Java
import java.io.File;

public class FileDemo {
    public static void main(String[] args) {
        File f1 = new File("D:\\Photo\\MyImages2.jpg");
        System.out.println(f1.getAbsolutePath());
        System.out.println(f1.getPath());
        System.out.println(f1.getName());
        System.out.println(f1.length());
        System.out.println("-------------------------------------");

        File f2 = new File("Day05Demo\\src\\dlei01.txt");
        System.out.println(f2.getAbsolutePath());
        System.out.println(f2.getPath());
        System.out.println(f2.length());
    }
}
```

File类的判断功能的方法

- public boolean exists()：此File表示的文件或目录是否实际存在。
- public boolean isDirectory()：此File表示的是否为目录。
- public boolean isFile()：此File表示的是否为文件。

File类的创建和删除的方法

- public boolean createNewFile()：当且仅当具有该名称的文件尚不存在时，创建一个新的空文件。(几乎不用的，因为以后文件都是自动创建的)
- public boolean delete()：删除由此File表示的文件或目录。(只能删除空目录)
- public boolean mkdir()：创建由此File表示的目录。(只能创建一级目录)
- public boolean mkdirs()：可以创建多级目录。(建议使用的)

File针对目录的遍历

- public String[] list()：获取当前目录下所有的“一级文件名称”到一个字符串数组中去返回。
- public File[] listFiles()：常用，获取当前目录下所有的“一级文件对象”到一个文件对象数组中去返回。

```Java
import java.io.File;
import java.text.SimpleDateFormat;

public class FileDemo01 {
    public static void main(String[] args) {
        File dir = new File("F:\\Git");
        String[] names = dir.list();
        for (String name : names) {
            System.out.println(name);
        }
        System.out.println("----------------------");

        File[] files = dir.listFiles();
        for (File file : files) {
            System.out.println(file.getAbsolutePath());
        }

        File f1 = new File("D:\\Photo\\MyImages2.jpg");
        long time = f1.lastModified();
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        System.out.println(sdf.format(time));
    }
}
```

## 21. 递归

递归：方法在方法中又调用了自己。

直接递归：自己的方法调用自己。

间接递归：自己的方法调用别的方法，别的方法又调用自己。

注意：递归如果控制的不恰当，会形成递归的死循环，从而导致栈内存溢出错误。

递归的三要素

- 递归的公式
- 递归的终结点
- 递归的方法必须走向终结点

练习案例：猴子吃桃，猴子第一天摘了若干个桃子，当即吃了一半，觉得好不过瘾，然后又多吃了一个。第二天又吃了前一天剩下的一半，觉得好不过瘾，然后又多吃了一个。以后每天都是如此，等到第十天再吃的时候发现只有1个桃子，请问猴子第一天总共摘了多少个桃子。

非规律化递归应该按照业务流程开发。

```Java
public class RecursionDemo {
    public static void main(String[] args) {
        System.out.println(f(1));
    }

    public static int f(int x) {
        if (x == 10) {
            return 1;
        } else {
            return  2 * f(x + 1) + 2;
        }
    }
}
```

递归实现文件搜索：去F:/Git目录寻找出8859-1.txt文件。

```Java
import java.io.File;

public class RecursionDemo {
    public static void main(String[] args) {
        searchFiles(new File("F:/Git"), "8859-1.txt");
    }

    public static void searchFiles(File dir, String fileName) {
        if (dir.exists() && dir.isDirectory()) {
            File[] files = dir.listFiles();
            if (files != null && files.length > 0) {
                for (File file : files) {
                    if (file.isFile()) {
                        if (file.getName().contains(fileName)) {
                            System.out.println(file.getAbsolutePath());
                        }
                    } else {
                        searchFiles(file,fileName);
                    }
                }
            }
        }
    }
}
```

## 22. IO流

### 22.1 IO流概述

字符集：各个国家为自己国家的字符取的一套编号规则。

小结

- 英文和数字在任何编码集中都是一样的，都占1个字节
- GBK编码中，1个中文字符一般占2个字节
- UTF-8编码中，1个中文字符一般占3个字节
- 技术人员都应该使用UTF-8编码

IO输入输出流：输入/输出流。

- Input：输入
- Output：输出

引入：File类只能操作文件对象本身，不能读写文件对象的内容。读写数据内容，应该使用IO流。

IO流是一个水流模型：IO理解成水管，把数据理解成水流。

IO流的分类

- 按照流的方向分为：输入流(读)，输出流(写)
- 按照流的内容分为：字节流，字符流

### 22.2 字节输入输出流

|     字节输入流      |      字节输出流      |   字符输入流   |   字符输出流   |            |
| :-----------------: | :------------------: | :------------: | :------------: | :--------: |
|     InputStream     |     OutputStream     |     Reader     |     Writer     |   抽象类   |
|   FileInputStream   |   FileOutputStream   |   FileReader   |   FileWriter   | 子类实现类 |
| BufferedInputStream | BufferedOutputStream | BufferedReader | BufferedWriter |   实现类   |

```Java
import java.io.File;
import java.io.FileInputStream;
import java.io.InputStream;

public class FileInputStreamDemo {
    public static void main(String[] args) throws Exception {
        File file = new File("Day05Demo\\src\\dlei01.txt");
        InputStream is = new FileInputStream(file);

        int ch = 0;
        while ((ch = is.read()) != -1) {
            System.out.print((char) ch);
        }
    }
}
```

小结

- 一个一个字节读取英文和数字没有问题
- 但是一旦读取中文输出无法避免乱码，因为会截断中文的字节
- 一个一个字节的读取数据，性能也较差，所以不推荐使用此方案

字节数组读取

- 使用字节数组读取内容，效率可以
- 但是使用字节数组读取文本内容输出，也无法避免中文读取输出乱码的问题

字节流读取解决中文乱码问题

- 定义一个字节数组与文件的大小刚好一样大，然后一桶水读取全部字节数据再输出
- 可以避免中文读取输出乱码，但是如果读取的文件过大，会出现内存溢出
- 字节流并不适合读取文本文件内容输出，读写文件内容建议使用字符流

FileOutputStream文件字节输出流

作用：以内存为基准，把内存中的数据，按照字节的形式写出到磁盘文件中去。

```Java
import java.io.FileOutputStream;
import java.io.OutputStream;

public class FileOutputStreamDemo {
    public static void main(String[] args) throws Exception {
        OutputStream os = new FileOutputStream("Day05Demo\\src\\dlei02.txt",true);
        os.write(97);
        os.write('b');
        os.write("\r\n".getBytes());

        byte[] bytes = new byte[]{98,99,100,111,104};
        os.write(bytes);
        os.write("\r\n".getBytes());
        byte[] bytes1 = "Java是最优美的语言，我爱Java！".getBytes();
        System.out.println(bytes1.length);
        os.write(bytes1);

        os.flush();
        os.close();
    }
}
```

小结

- 字节输出流可以写字节数据到文件中去
- 可以写一个字节，写一个字节数组，写一个字节数组的一部分出去
- 管道用完需要关闭，数据要生效需要刷新，关闭包含刷新，刷新后流可以继续使用，关闭后流无法继续使用了
- 字节输出流管道默认是覆盖管道，启动管道写数据前会清空数据

字节流做文件复制

字节流复制思想

- 字节是计算机中一切文件的组成，所以字节流适合做一切文件的复制。
- 复制是把源文件的全部字节一字不漏的转移到目标文件，只要文件前后的格式一样，绝对不会有问题。

```Java
import java.io.*;

public class FileCopyDemo {
    public static void main(String[] args) {
        InputStream is = null;
        OutputStream os = null;
        try {
            is = new FileInputStream("D:\\Photo\\MyImages2.jpg");
            os = new FileOutputStream("Day05Demo\\src\\photo.jpg");

            byte[] buffer = new byte[1024];
            int len;
            while ((len = is.read(buffer)) != -1) {
                os.write(buffer,0,len);
            }
            System.out.println("复制完成！");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if (is != null) {
                try {
                    is.close();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
            if (os != null) {
                try {
                    os.close();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

JDK 1.7开始之后释放资源的新方式

try-with-resources

```Java
try (
    // 这里只能放置资源对象，用完会自动调用close()关闭
) {
    
} catch(Exception e) {
    e.printStackTrace();
}
```

什么是资源：资源类一定是实现了Closeable接口，实现这个接口的类就是资源。

```Java
import java.io.*;

public class FileCopyDemo {
    public static void main(String[] args) {
        try (
                InputStream is  = new FileInputStream("D:\\Photo\\MyImages2.jpg");
                OutputStream os = new FileOutputStream("Day05Demo\\src\\photo.jpg");
                ) {
            byte[] buffer = new byte[1024];
            int len;
            while ((len = is.read(buffer)) != -1) {
                os.write(buffer,0,len);
            }
            System.out.println("复制完成！");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 22.3 字符输入输出流

FileReader：文件字符输入流。

作用：以内存为基准，把磁盘文件的数据以字符的形式读入到内存。简单来说，读取文本文件内容到内存中去。

```Java
import java.io.FileReader;
import java.io.Reader;

public class FileReaderDemo {
    public static void main(String[] args) throws Exception {
        Reader fr = new FileReader("Day05Demo\\src\\dlei02.txt");
        int ch;
        while ((ch = fr.read()) != -1) {
            System.out.print((char) ch);
        }
    }
}
```

小结

- 字符流一个一个字符的读取文本内容输出，可以解决中文读取输出乱码的问题
- 字符流很适合操作文本文件内容
- 但是一个一个字符地读取文本内容性能较差

```Java
import java.io.FileReader;
import java.io.Reader;

public class FileReaderDemo {
    public static void main(String[] args) throws Exception {
        Reader fr = new FileReader("Day05Demo\\src\\dlei02.txt");
        char[] buffer = new char[1024];
        int len;
        while ((len = fr.read(buffer)) != -1) {
            String rs = new String(buffer,0,len);
            System.out.print(rs);
        }
    }
}
```

字符流按照字符数组循环读取数据，可以解决中文读取输出乱码的问题，而且性能也较好。

FileWriter文件字符输出流的使用

作用：以内存为基准，把内存中的数据按照字符的形式写出到磁盘文件中去。简单来说，就是把内存的数据以字符写出到文件中去。

```Java
import java.io.FileWriter;
import java.io.Writer;

public class FileWriterDemo {
    public static void main(String[] args) throws Exception {
        Writer fw = new FileWriter("Day05Demo\\src\\dlei01.txt",true);
        fw.write(97);
        fw.write('b');
        fw.write("\r\n");
        fw.write('中');
        fw.write("\r\n");
        fw.write("Java是最优美的语言");
        fw.write("\r\n");
        fw.write("我爱中国".toCharArray());
        fw.write("\r\n");
        fw.write("Java是最优美的语言",0,9);
        fw.write("\r\n");
        fw.write("我爱中国".toCharArray(),0,2);
        fw.close();
    }
}
```

小结：字符输出流可以写字符数据出去，总共有5个方法写字符。

### 22.4 缓冲流

缓冲流：缓冲流可以提高字节流和字符流的读写数据的性能。

缓冲流分为四类

- BufferedInputStream：字节缓冲输入流，可以提高字节输入流读数据的性能。
- BufferedOutputStream：字节缓冲输出流，可以提高字节输出流写数据的性能。
- BufferedReader：字符缓冲输出流，可以提高字符输入流读数据的性能。
- BufferedWriter：字符缓冲输出流，可以提高字符输出流写数据的性能。

字节缓冲输入流：BufferedInputStream

作用：可以把低级的字节输入流包装成一个高级的缓冲字节输入流管道，从而提高字节输入流读数据的性能。

构造器：public BufferedInputStream(InputStream in)

```Java
import java.io.BufferedInputStream;
import java.io.FileInputStream;

public class BufferedInputStreamDemo {
    public static void main(String[] args) throws Exception {
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream("Day05Demo\\src\\dlei02.txt"));
        byte[] buffer = new byte[1024];
        int len;
        while ((len = bis.read(buffer)) != -1) {
            String rs = new String(buffer,0,len);
            System.out.print(rs);
        }
    }
}
```

字节缓冲输出流：BufferedOutputStream

作用：可以把低级的字节输出流包装成一个高级的缓冲字节输出流，从而提高写数据的性能。

构造器：public BufferedOutputStream(OutputStream os)

原理：缓冲字节输出流自带了8KB缓冲池，数据就直接写入到缓冲池中去，性能提高了。

字符缓冲输入流：BufferedReader

作用：字符缓冲输入流可以把字符输入流包装成一个高级的缓冲字符输入流，可以提高字符输入流读数据的性能。

构造器：public BufferedReader(Reader reader)

原理：缓冲字符输入流默认会有一个8KB的字符缓冲流，可以提高读字符的性能。

```Java
import java.io.BufferedReader;
import java.io.FileReader;

public class BufferedReaderDemo {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new FileReader("Day05Demo\\src\\dlei02.txt"));

        String line;
        while ((line = br.readLine()) != null) {
            System.out.println(line);
        }
        br.close();
    }
}
```

字符缓冲输出流：BufferedWriter

作用：把字符输出流包装成一个高级的缓冲字符输出流，提高写字符数据的性能。

构造器：public BufferedWriter(Writer writer)

原理：高级的字符缓冲输出流多了一个8KB的字符缓冲池，写数据性能极大提高了。

```Java
import java.io.BufferedWriter;
import java.io.FileWriter;

public class BufferedWriterDemo {
    public static void main(String[] args) throws Exception {
        BufferedWriter bw = new BufferedWriter(new FileWriter("Day05Demo\\src\\dlei01.txt",true));

        bw.write("我在学Java中的IO流~~~");
        bw.newLine();
        bw.write("Java是最优美的语言~~~");
        bw.newLine();
        bw.close();
    }
}
```

练习：将文档中带有中文序号的内容读出、排序并写入新的文档。

```Java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class ExecDemo {
    public static void main(String[] args) {
        try (
                BufferedReader br = new BufferedReader(new FileReader("Day05Demo\\src\\dlei01.txt"));
                BufferedWriter bw = new BufferedWriter(new FileWriter("Day05Demo\\src\\dlei02.txt"));
                ) {
            List<String> datas = new ArrayList<>();
            String line;
            while ((line = br.readLine()) != null) {
                datas.add(line);
            }

            List<Character> sizes = new ArrayList<>();
            Collections.addAll(sizes,'零','一','二','三','四','五','六','七','八','九','十');

            Collections.sort(datas, (o1, o2) -> sizes.indexOf(o1.charAt(0)) - sizes.indexOf(o2.charAt(0)));
            System.out.println(datas);

            for (String data : datas) {
                bw.write(data);
                bw.newLine();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

注意：如果代码编码和读取的文件编码一致，字符流读取的时候不会乱码，反之则会乱码。

### 22.5 字符输入输出转换流

字符输入转换流：InputStreamReader

作用：可以把原始的字节流按照当前默认的代码编码转换成字符输入流。也可以把原始的字节流按照指定编码转换成字符输入流。

构造器

- public InputStreamReader(InputStream is)：可以使用当前代码默认编码转换成字符流，几乎不用
- public InputStreamReader(InputStream is, String charset)：可以指定编码把字节流转换成字符流

字符输出转换流：OutputStreamWriter

作用：可以指定编码把字节输出流转换成字符输出流，可以指定写出去的字符编码。

构造器

- public OutputStreamWriter(OutputStream os)：用当前默认编码UTF-8把字节输出流转换成字符输出流
- public OutputStreamWriter(OutputStream os, String charset)：指定编码把字节输出流转换成字符输出流

### 22.6 对象序列化技术

对象序列化：就是把Java对象数据直接存储到文件中去。

对象反序列化：就是把Java对象的文件数据恢复到Java对象中去。

对象序列化流(对象字节输出流)：ObjectOutputStream

作用：把内存中的Java对象数据保存到文件中去。

构造器：public ObjectOutputStream(OutputStream out)

序列化方法：public final void writeObject(Object obj)

注意：如果要序列化对象，那么对象必须实现序列化接口：implements Serializable。

```Java
import java.io.FileOutputStream;
import java.io.ObjectOutputStream;
import java.io.OutputStream;

public class SerializeDemo {
    public static void main(String[] args) throws Exception {
        User user = new User("铁扇公主","003197","铁扇公主");
        OutputStream os = new FileOutputStream("Day05Demo\\src\\obj.dat");
        ObjectOutputStream oos = new ObjectOutputStream(os);
        oos.writeObject(user);
        oos.close();
        System.out.println("序列化成功~~~");
    }
}
```

对象反序列化(对象字节输入流)：ObjectInputStream

作用：读取序列化的对象文件恢复到Java对象中。

构造器：public ObjectInputStream(InputStream is)

方法：public final Object readObject()

注意：transient修饰的成员变量将不参与序列化。

对象假如序列版本号：private static final long serialVersionUID = 2L;

反序列化使用的对象版本号必须与序列化使用的版本号一致才不会报错。

```Java
import java.io.FileInputStream;
import java.io.InputStream;
import java.io.ObjectInputStream;

public class SerializeDemo01 {
    public static void main(String[] args) throws Exception {
        InputStream is = new FileInputStream("Day05Demo\\src\\obj.dat");
        ObjectInputStream ois = new ObjectInputStream(is);
        User user = (User) ois.readObject();
        System.out.println(user);
        System.out.println("反序列化完成~~~");
    }
}
```

### 22.7 打印流

打印流：PrintStream/PrintWriter。

打印流的作用

- 可以方便，快速的写数据出去
- 可以实现打印啥出去，就是啥出去

打印流的构造器

- public PrintStream(OutputStream os)
- public PrintStream(String filepath)

小结

- PrintStream可以方便快速打印数据出去，同时可以写字节输出
- PrintWriter可以方便快速打印数据出去，同时可以写字符输出

```Java
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.io.PrintStream;

public class PrintStreamDemo {
    public static void main(String[] args) throws Exception {
        OutputStream os = new FileOutputStream("Day05Demo\\src\\dlei02.txt");
        PrintStream ps = new PrintStream(os);

        ps.println(97);
        ps.println(110);
        ps.println("Java是最优美的语言");
        ps.println(99.8);
        ps.println(false);
        ps.println('中');
        ps.close();
    }
}
```

打印流改变输出的流向，重定向。

```Java
import java.io.PrintStream;

public class PrintStreamDemo {
    public static void main(String[] args) throws Exception {
        PrintStream ps = new PrintStream("Day05Demo\\src\\log.txt");
        System.setOut(ps);

        System.out.println("==Hello==");
        System.out.println("==World==");
        System.out.println("==Java==");
        System.out.println("==JavaSE==");
    }
}
```

### 22.8 Properties

Properties：属性集对象。

其实就是一个Map集合。也就是一个键值对集合。但是我们一般不会当集合使用，因为有HashMap。

Properties核心作用

- Properties代表的是一个属性文件，可以把键值对的数据存入到一个属性文件中去。
- 属性文件：后缀是.properties结尾的文件，里面的内容都是key=value。

属性集对象Properties实际上是一个Map集合，可以实现把键值对数据保存到属性文件中去。

```Java
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.util.Properties;

public class PropertiesDemo {
    public static void main(String[] args) throws Exception {
        Properties properties = new Properties();
        properties.setProperty("admin","123456");
        properties.setProperty("dlei","101333");
        System.out.println(properties);

        OutputStream os = new FileOutputStream("Day05Demo\\src\\user.properties");
        properties.store(os,"保存用户数据");
    }
}
```

Properties读取属性文件中的键值对信息

```Java
import java.io.FileInputStream;
import java.util.Properties;

public class PropertiesDemo {
    public static void main(String[] args) throws Exception {
        Properties properties = new Properties();
        System.out.println(properties);

        properties.load(new FileInputStream("Day05Demo\\src\\user.properties"));
        System.out.println(properties);

        System.out.println(properties.getProperty("dlei"));
    }
}
```

## 23. 编程思维拓展

啤酒问题：啤酒2元一瓶，4个盖子可以换一瓶，2个空瓶可以换一瓶。

```Java
public class BeerDemo {
    public static int totalNum;
    public static int lastPingZiNum;
    public static int lastGaiZiNum;

    public static void main(String[] args) {
        buyBeer(10);
        System.out.println("总数：" + totalNum);
        System.out.println("剩余盖子：" + lastGaiZiNum);
        System.out.println("剩余瓶子：" + lastPingZiNum);
    }

    public static void buyBeer(int money) {
        int number = money / 2;
        totalNum += number;

        int currentPingZiNum = lastPingZiNum + number;
        int currentGaiZiNum = lastGaiZiNum + number;

        int totalMoney = 0;
        totalMoney += (currentPingZiNum / 2) * 2;
        lastPingZiNum = currentPingZiNum % 2;

        totalMoney += (currentGaiZiNum / 4) * 2;
        lastGaiZiNum = currentGaiZiNum % 4;

        if (totalMoney >= 2) {
            buyBeer(totalMoney);
        }
    }
}
```

复制文件夹

```Java
import java.io.*;

public class CopyDirDemo {
    public static void main(String[] args) {
        CopyDir(new File("D:\\letsvpn"), new File("F:\\copylets"));
    }

    public static void CopyDir(File srcDir, File destDir) {
        if (srcDir.exists() && srcDir.isDirectory()) {
            destDir.mkdirs();
            File[] files = srcDir.listFiles();
            if (files != null && files.length > 0) {
                for (File file : files) {
                    if (file.isFile()) {
                        copyFile(file,new File(destDir,file.getName()));
                    } else {
                        CopyDir(file,new File(destDir,file.getName()));
                    }
                }
            }
        }
    }

    private static void copyFile(File srcFile, File destFile) {
        try (
                BufferedInputStream bis = new BufferedInputStream(new FileInputStream(srcFile));
                BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(destFile))
        ) {
            byte[] buffer = new byte[1024];
            int len;
            while ((len = bis.read(buffer)) != -1) {
                bos.write(buffer,0,len);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 24. 网络通信

### 24.1 概述

通信一定是基于软件结构实现的

- C/S结构：全称为Client/Server结构，是指客户端和服务器端结构。
  - 常见程序有QQ、迅雷、IDEA等
- B/S结构：全称为Browser/Server结构，是指浏览器和服务器结构。
  - 常见浏览器有谷歌、火狐等、网站有京东、淘宝等
  - 开发中的重点，基于网页设计页面，界面效果可以更丰富：Java Web开发

两种架构各有优势，但是无论哪种架构，都离不开网络的支持。网络编程，就是在一定的协议下，实现两台计算机的通信技术。

网络通信的三要素

1. 协议：计算机网络客户端与服务端通信必须事先约定和彼此遵守的通信规则。HTTP，FTP，TCP，UDP，SSH，SMTP。
2. IP地址：指互联网协议地址(Internet Protocol Address)，俗称IP。IP地址用来给一个网络中的计算机设备做唯一的编号。
   - IPv4：4个字节，32位组成。
   - IPv6：可以实现为所有设备分配IP，128位。
   - 注意：特殊的IP地址：本机IP地址。(不受环境的影响，任何时候都存在这两个IP，可以直接找本机。)127.0.0.1 == localhost。
3. 端口：端口号就可以唯一标识设备中的进程(应用程序)。
   - 端口号：用两个字节表示的整数，它的取值范围是0~65535。
   - 0~1023之间的端口号用于一些知名的网络服务和应用。
   - 如果端口号被另外一个服务或应用所占用，会导致当前程序启动失败。报出端口被占用异常。

TCP/IP协议：传输控制协议(Transmission Control Protocol)。

- TCP协议是面向连接的安全的可靠的传输通信协议
- 在通信之前必须确定对方在线并且连接成功才可以通信
- 例如下载文件、浏览网页等(要求可靠传输)

UDP：用户数据报协议(User Datagram Protocol)。

- UDP协议是一个面向无连接的不可靠传输的协议
- 直接发消息给对方，不管对方是否在线，发消息后也不需要确认
- 无线(视频会议，通话)，性能好，可能丢失一些数据

### 24.2 通信编程基础

InetAddress类：一个该类的对象就代表一个IP地址对象。

InetAddress类成员方法

- static InetAddress getLocalHost()：获得本地主机IP地址对象。
- static InetAddress getByName(String host)：根据IP地址字符串或主机名获得对应的IP地址对象。
- String getHostName()：获得主机名。
- String getHostAddress()：获得IP地址字符串。

```Java
import java.net.InetAddress;

public class InetAddressDemo {
    public static void main(String[] args) throws Exception {
        InetAddress ip = InetAddress.getLocalHost();
        System.out.println(ip.getHostName());
        System.out.println(ip.getHostAddress());

        InetAddress ip1 = InetAddress.getByName("www.baidu.com");
        System.out.println(ip1.getHostName());
        System.out.println(ip1.getHostAddress());

        System.out.println(ip1.isReachable(5000));
    }
}
```

UDP通信

客户端程序

```Java
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;

public class UDPClientDemo {
    public static void main(String[] args) throws Exception {
        System.out.println("==启动客户端程序==");
        byte[] buffer = "今晚月色真美！".getBytes();
        DatagramPacket packet = new DatagramPacket(buffer,buffer.length, InetAddress.getLocalHost(),6666);
        DatagramSocket socket = new DatagramSocket(8888);
        socket.send(packet);
        socket.close();
    }
}
```

服务端程序

```Java
import java.net.DatagramPacket;
import java.net.DatagramSocket;

public class UDPServerDemo {
    public static void main(String[] args) throws Exception {
        System.out.println("==启动服务端程序==");
        byte[] buffer = new byte[1024*64];
        DatagramPacket packet = new DatagramPacket(buffer,buffer.length);
        DatagramSocket socket = new DatagramSocket(6666);
        socket.receive(packet);
        int len = packet.getLength();
        String rs = new String(buffer,0,len);
        System.out.println(rs);

        String ip = packet.getAddress().getHostAddress();
        int port = packet.getPort();
        System.out.println("对方：" + ip + "：" + port);
        socket.close();
    }
}
```

TCP协议相关的类

- Socket：一个该类的对象就代表一个客户端程序。
- ServerSocket：一个该类的对象就代表一个服务器端程序。

TCP通信也叫Socket网络编程，只要代码基于Socket开发，底层就是基于了可靠传输的TCP通信。

客户端开发流程

- 客户端要求请求于服务端的socket管道连接。
- 从socket通信管道中得到一个字节输入流。
- 通过字节输入流给服务端写出数据。

服务端的开发流程

- 注册端口。
- 接收客户端的socket管道连接。
- 从socket通信管道中得到一个字节输入流。
- 从字节输入流中读取客户端发来的数据。

练习案例：客户端发送一行数据，服务端接收一行数据。

客户端程序

```Java
import java.io.OutputStream;
import java.io.PrintStream;
import java.net.Socket;

public class ClientDemo {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("10.100.159.153",8888);
        OutputStream os = socket.getOutputStream();
        PrintStream ps = new PrintStream(os);
        ps.println("我是客户端，第一次给你发消息，只想说：初次见面，请多关照！");
        ps.flush();
        System.out.println("客户端发送完毕~~~");
    }
}
```

服务端程序

```Java
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.Reader;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerDemo {
    public static void main(String[] args) throws Exception {
        System.out.println("---服务端启动---");
        ServerSocket ss = new ServerSocket(8888);
        Socket socket = ss.accept();
        InputStream is = socket.getInputStream();
        Reader isr = new InputStreamReader(is);
        BufferedReader br = new BufferedReader(isr);
        String msg;
        if ((msg = br.readLine()) != null) {
            System.out.println("收到：" + msg);
        }
    }
}
```

实现反复发送和接收消息

服务端修改部分代码

```Java
while ((msg = br.readLine()) != null) {
    System.out.println("收到：" + msg);
}
```

客户端代码

```Java
import java.io.OutputStream;
import java.io.PrintStream;
import java.net.Socket;
import java.util.Scanner;

public class ClientDemo01 {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("10.100.159.153",8888);
        OutputStream os = socket.getOutputStream();
        PrintStream ps = new PrintStream(os);
        while (true) {
            Scanner sc = new Scanner(System.in);
            System.out.println("请说：");
            ps.println(sc.nextLine());
            ps.flush();
        }
    }
}
```

实现一个服务端可以接收多个客户端消息

客户端程序代码如上，无需修改

服务器端程序代码

```Java
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.Reader;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerDemo01 {
    public static void main(String[] args) throws Exception {
        System.out.println("---服务端启动---");
        ServerSocket ss = new ServerSocket(8888);
        while (true) {
            Socket socket = ss.accept();
            new ServerReaderThread(socket).start();
        }
    }
}

class ServerReaderThread extends Thread {
    private Socket socket;
    public ServerReaderThread(Socket socket) {
        this.socket = socket;
    }

    @Override
    public void run() {
        try {
            InputStream is = socket.getInputStream();
            Reader isr = new InputStreamReader(is);
            BufferedReader br = new BufferedReader(isr);
            String msg;
            while ((msg = br.readLine()) != null) {
                System.out.println(socket.getRemoteSocketAddress() + "说：" + msg);
            }
        } catch (Exception e) {
            System.out.println(socket.getRemoteSocketAddress() + "下线了~~~");
        }
    }
}
```

引入：我们之前引入的线程解决一个服务端可以接收多个客户端消息，客户端与服务端的线程模型是：N-N的关系。一个客户端要一个线程。这种模型是不行的，并发越高，系统瘫痪越快。

解决：我们可以在服务端引入线程池，使用线程池来处理与客户端的消息通信。线程池不会引起出现过多的线程而导致系统死机。

优劣势

- 优势：不会引起系统的死机，可以控制并发线程的数量。
- 劣势：同时可以并发的线程将受到限制。

使用线程池实现客户端和服务器端交互

客户端程序

```Java
import java.io.OutputStream;
import java.io.PrintStream;
import java.net.Socket;
import java.util.Scanner;

public class ClientDemo {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("10.100.159.153",8888);
        OutputStream os = socket.getOutputStream();
        PrintStream ps = new PrintStream(os);
        while (true) {
            Scanner sc = new Scanner(System.in);
            System.out.println("请说：");
            ps.println(sc.nextLine());
            ps.flush();
        }
    }
}
```

服务器端程序

```Java
import java.net.ServerSocket;
import java.net.Socket;

public class ServerDemo {
    public static void main(String[] args) {
        try {
            System.out.println("---服务端启动---");
            ServerSocket ss = new ServerSocket(8888);
            HandlerSocketThreadPool handlerSocketThreadPool = new HandlerSocketThreadPool(3,100);
            while (true) {
                Socket socket = ss.accept();
                System.out.println("有人上线了！！");
                handlerSocketThreadPool.execute(new ReaderClientRunnable(socket));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

线程任务类

```Java
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.Reader;
import java.net.Socket;

public class ReaderClientRunnable implements Runnable {
    private Socket socket;
    public ReaderClientRunnable(Socket socket) {
        this.socket = socket;
    }

    @Override
    public void run() {
        try {
            InputStream is = socket.getInputStream();
            Reader isr = new InputStreamReader(is);
            BufferedReader br = new BufferedReader(isr);
            String msg;
            while ((msg = br.readLine()) != null) {
                System.out.println(socket.getRemoteSocketAddress() + "说：" + msg);
            }
        } catch (Exception e) {
            System.out.println(socket.getRemoteSocketAddress() + "下线了~~~");
        }
    }
}
```

线程池类

```Java
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

public class HandlerSocketThreadPool {
    private ExecutorService executor;
    public HandlerSocketThreadPool(int maxPoolSize, int queueSize) {
        this.executor = new ThreadPoolExecutor(
                maxPoolSize,
                maxPoolSize,
                120L,
                TimeUnit.SECONDS,
                new ArrayBlockingQueue<Runnable>(queueSize)
        );
    }

    public void execute(Runnable task) {
        this.executor.execute(task);
    }
}
```

练习案例：图片上传。

客户端程序

```Java
import java.io.*;
import java.net.Socket;

public class ClientDemo {
    public static final String SRC_IMAGE = "D:\\Photo\\MyImages2.jpg";

    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("10.100.159.153",7777);
        OutputStream os = socket.getOutputStream();
        BufferedOutputStream bos = new BufferedOutputStream(os);
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream(SRC_IMAGE));

        byte[] buffer = new byte[1024];
        int len;
        while ((len = bis.read(buffer)) != -1) {
            bos.write(buffer,0,len);
        }
        bos.flush();
        bis.close();
        socket.shutdownOutput();
        System.out.println("传输图片数据成功了！！！");

        BufferedReader br = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        System.out.println(br.readLine());
    }
}
```

服务器端程序

```Java
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.UUID;

public class ServerDemo {
    public static final String DEST_FILE = "F:\\TestUP\\";
    public static void main(String[] args) throws Exception {
        System.out.println("---服务端启动---");
        ServerSocket ss = new ServerSocket(7777);
        while (true) {
            Socket socket = ss.accept();
            System.out.println(socket.getRemoteSocketAddress() + "来了，老弟！");
            new ServerReaderThread(socket).start();
        }
    }
}

class ServerReaderThread extends Thread {
    private Socket socket;
    public ServerReaderThread(Socket socket) {
        this.socket = socket;
    }

    @Override
    public void run() {
        try {
            InputStream is = socket.getInputStream();
            BufferedInputStream bis = new BufferedInputStream(is);
            BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(ServerDemo.DEST_FILE + UUID.randomUUID().toString() + ".jpg"));
            byte[] buffer = new byte[1024];
            int len;
            while ((len = bis.read(buffer)) != -1) {
                bos.write(buffer,0,len);
            }
            bos.flush();
            bos.close();

            PrintStream ps = new PrintStream(socket.getOutputStream());
            ps.println("亲爱的客户端，我已经收到你的图片，谢谢");
            ps.flush();

            Thread.sleep(10000);
        } catch (Exception e) {
            System.out.println(socket.getRemoteSocketAddress() + "下线了~~~");
        }
    }
}
```

### 24.3 BS架构模拟

客户端：浏览器

服务端：自己开发

需求：在浏览器中请求本程序，响应一个网页文字给浏览器显示。

服务器端程序代码如下

```Java
import java.io.PrintStream;
import java.net.ServerSocket;
import java.net.Socket;

public class BSserverDemo {
    public static void main(String[] args) {
        try {
            ServerSocket ss = new ServerSocket(8080);
            while (true) {
                Socket socket = ss.accept();
                new ServerReaderThread(socket).start();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class ServerReaderThread extends Thread {
    private Socket socket;
    public ServerReaderThread(Socket socket) {
        this.socket = socket;
    }

    @Override
    public void run() {
        try {
            PrintStream ps = new PrintStream(socket.getOutputStream());
            ps.println("HTTP/1.1 200 OK");
            ps.println("Content-Type:text/html;charset=UTF-8");
            ps.println();

            ps.println("<span style='color:green;font-size:60px;'>优秀的Java语言是世界上最好的语言!!</span>");
            Thread.sleep(3000);
            ps.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 24.4 通信模型

1.BIO通信模式：同步阻塞式通信。(Socket网络编程也就是上面的通信架构)

- 同步、异步、阻塞、非阻塞

2.伪异步通信：引入了线程池。

3.NIO表示同步非阻塞IO，服务器实现模式为请求对应一个线程，即客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。

4.AIO表示异步非阻塞IO，服务器实现模式为一个有效请求一个线程，客户端的I/O请求都是由操作系统先完成IO操作后再通知服务器应用来启动线程进行处理。

应用场景

- BIO适用于连接数目比较小且固定的架构，该方式对服务器资源要求比较高，JDK 1.4以前的唯一选择。
- NIO适用于连接数目多且连接比较短(轻操作)的架构，如聊天服务器，编程复杂，JDK 1.4开始支持。
- AIO适用于连接数目多且连接比较长(重操作)的架构，如相册服务器，充分调用操作系统参与并发操作，编程复杂，JDK 1.7开始支持。

## 25. 单元测试

单元测试是指程序员写的测试代码给自己的类中的方法进行预期正确性的验证。

单元测试一旦写好了这些测试代码，就可以一直使用，可以实现一定程度上的自动化测试。

单元测试一般要使用框架进行

- 框架是前人或者一些强大的技术公司在实战或者研发中设计的一些优良的设计方案或者成型的代码功能，作为一个完整的技术体系发行出来称为框架。
- 框架可以让程序员快速拥有一个强大的解决方案，可以快速的开发功能，提高效率并且直接就有了很好的性能。

单元测试的经典框架：Junit。

单元测试概念

- 单元：在Java中，一个类就是一个单元
- 单元测试：程序员用Junit编写的一小段代码，用来对某个类中的某个方法进行功能测试或业务逻辑测试

Junit单元测试框架的作用

- 用来对类中的方法功能进行有目的的测试，以保证程序的正确性和稳定性
- 能够独立的测试某个方法或者所有方法的预期正确性

业务代码示例

```Java
public class UserService {
    public String login(String loginName, String passWord) {
        if ("admin".equals(loginName) && "123456".equals(passWord)) {
            return "success";
        }
        return "用户名或者密码错误";
    }

    public void chu(int a, int b) {
        int c = a / b;
        System.out.println(c);
    }
}
```

测试类代码示例

```Java
import org.junit.Assert;
import org.junit.Test;

public class UserServiceTest {
    @Test
    public void testLogin() {
        UserService userService = new UserService();
        String rs = userService.login("admin", "123456");
        Assert.assertEquals("登录业务方法有错误，请检查","success",rs);
    }

    @Test
    public void testChu() {
        UserService userService = new UserService();
        userService.chu(10,2);
    }
}
```

## 26. 反射

### 26.1 反射概述

反射，注解，代理，泛型是Java的高级技术，是以后框架的底层原理必须使用到的技术。

反射：是Java独有的技术，是Java技术显著的特点。

反射是指对于任何一个类，在“运行的时候”都可以直接得到这个类全部成分。

- 在运行时，可以直接得到这个类的构造器对象。(Constructor)
- 在运行时，可以直接得到这个类的成员变量对象。(Field)
- 在运行时，可以直接得到这个类的成员方法对象。(Method)

反射的核心思想和关键就是得到：编译以后的class文件对象。

反射提供了一个Class类型，就是可以得到编译以后的class文件对象。

- HelloWorld.java -> javac -> HelloWorld.class
- Class c = HelloWorld.class

注意：反射是工作在运行时的技术，因为只有运行之后才会有class类对象。

反射获取Class类对象的三种方式

- 类名.class
- 通过类的对象.getClass()方法
- Class.forName("类的全限名")
  - public static Class<?> forName(String className)

Class类下的方法

- String getSimpleName()：获得类名字符串：类名
- String getName()：获得类全名：包名+类名
- T newInstance()：创建Class对象关联类的对象，其实底层也是调用无参数构造器，已经被淘汰

案例代码

```Java
public class ReflectDemo {
    public static void main(String[] args) throws Exception {
        Class c1 = Student.class;
        System.out.println(c1);

        Student swk = new Student();
        Class c2 = swk.getClass();
        System.out.println(c2);

        Class c3 = Class.forName("com.itahu.Code07.Student");
        System.out.println(c3);

        System.out.println(c1.getSimpleName());
        System.out.println(c1.getName());
        Student s1 = (Student) c1.newInstance();
    }
}
```

### 26.2 Class类的各种对象获取

反射中Class类获取构造器对象

- Constructor getConstructor(Class... parameterTypes)：根据参数匹配获取某个构造器，只能拿public修饰的构造器，几乎不用。
- Constructor getDeclaredConstructor(Class... parameterTypes)：根据参数匹配获取某个构造器，只要申明就可以定位，不关心权限修饰符，建议使用。
- Constructor[] getConstructors()：获取所有的构造器，只能拿public修饰的构造器，几乎不用。
- Constructor[] getDeclaredConstructors()：获取所有申明的构造器，只要你写我就能拿到，无所谓权限，建议使用。

```Java
import org.junit.Test;
import java.lang.reflect.Constructor;

public class ReflectDemo01 {
    @Test
    public void getConstructors() {
        Class c = Student.class;
        Constructor[] cons = c.getConstructors();
        for (Constructor con : cons) {
            System.out.println(con.getName() + "==>" + con.getParameterCount());
        }
    }

    @Test
    public void getDeclaredConstructors() {
        Class c = Student.class;
        Constructor[] cons = c.getDeclaredConstructors();
        for (Constructor con : cons) {
            System.out.println(con.getName() + "==>" + con.getParameterCount());
        }
    }

    @Test
    public void getConstructor() throws Exception {
        Class c = Student.class;
        Constructor con = c.getConstructor(String.class, int.class);
        System.out.println(con.getName() + "==>" + con.getParameterCount());
    }

    @Test
    public void getDeclaredConstructor() throws Exception {
        Class c = Student.class;
        Constructor con = c.getDeclaredConstructor();
        System.out.println(con.getName() + "==>" + con.getParameterCount());
    }
}
```

反射获取Class中的构造器对象Constructor作用：也是初始化并得到类的一个对象返回。

Constructor的API

- T newInstance(Object... initargs)：创建对象，注入构造器需要的数据。
- void setAccessible(true)：修改访问权限，true代表暴力攻破权限，false表示保留不可访问权限。(暴力反射)

```Java
import org.junit.Test;
import java.lang.reflect.Constructor;

public class ReflectDemo02 {
    @Test
    public void createObj01() throws Exception {
        Class c = Student.class;
        Constructor constructor = c.getDeclaredConstructor();
        constructor.setAccessible(true);
        Student swk = (Student) constructor.newInstance();
        System.out.println(swk);
    }

    @Test
    public void createObj02() throws Exception {
        Class c = Student.class;
        Constructor constructor = c.getDeclaredConstructor(String.class, int.class);
        Student swk = (Student) constructor.newInstance("孙悟空", 1000);
        System.out.println(swk);
    }
}
```

反射获取成员变量

- Field getField(String name)：根据成员变量名称获得对应Field对象，只能获得public修饰。
- Field getDeclaredField(String name)：根据成员变量名获得对应Field对象，只要申明了就可以得到。
- Field[] getFields()：获得所有的成员变量对应的Field对象，只能获得public的。
- Field[] getDeclaredFields()：获得所有的成员变量对应的Field对象，只要申明了就可以得到。

反射获取成员变量：取值和赋值

Field方法：给成员变量赋值和取值

- void set(Object obj, Object value)：给对象注入某个成员变量数据。
- Object get(Object obj)：获取对象的成员变量的值。
- void setAccessible(true)：暴力反射，设置为可以直接访问私有类型的属性。
- Class getType()：获取属性的类型，返回Class对象。
- String getName()：获取属性的名称。

```Java
import org.junit.Test;
import java.lang.reflect.Field;

public class FieldDemo01 {
    @Test
    public void setField() throws Exception {
        Class c = Dog.class;
        Field nameF = c.getDeclaredField("name");
        Dog taidi = new Dog();
        nameF.setAccessible(true);
        nameF.set(taidi, "勇敢的泰迪");
        System.out.println(taidi);

        String value = nameF.get(taidi) + "";
        System.out.println(value);
    }
}
```

反射获取类的Method方法对象

- Method getMethod(String name, Class... args)：根据方法名和参数类型获得对应的方法对象，只能获得public的。
- Method getDeclaredMethod(String name, Class... args)：根据方法名和参数类型获得对应的方法对象，包括private的。
- Method[] getMethods()：获得类中所有成员方法的对象，返回数组，只能获得public修饰的且包含父类的。
- Method[] getDeclaredMethods()：获得类中的所有成员方法对象，返回数组，只获得本类申明的方法。

Method的方法

- Object invoke(Object obj, Object... args)
  - 参数一：触发的是哪个对象的方法执行。
  - 参数二：args是调用方法时传递的实际参数。

```Java
import org.junit.Test;
import java.lang.reflect.Method;

public class MethodDemo {
    @Test
    public void getDeclaredMethod() throws Exception {
        Class c = Dog.class;
        Method run = c.getDeclaredMethod("run");
        Dog jinMao = new Dog();
        run.invoke(jinMao);

        Method eat = c.getDeclaredMethod("eat", String.class);
        eat.setAccessible(true);
        Object rs = eat.invoke(jinMao, "骨头");
        System.out.println(rs);
    }
}
```

反射拓展

- 反射可以破坏面向对象的封装性
- 同时可以破坏泛型的约束性

```Java
import java.lang.reflect.Method;
import java.util.ArrayList;
import java.util.List;

public class ReflectDemo03 {
    public static void main(String[] args) throws Exception {
        List<Double> scores = new ArrayList<>();
        scores.add(99.3);
        scores.add(199.3);
        scores.add(89.5);

        Class c = scores.getClass();
        Method add = c.getDeclaredMethod("add", Object.class);
        add.invoke(scores,"波仔");
        System.out.println(scores);
    }
}
```

反射适合做通用技术框架的底层实现，在框架的底层源码中我们经常看到反射的影子。

如反射可以实现：任何对象只要给我，我就可以把信息和字段都解析并存储起来。

## 27. 注解

### 27.1 注解概述

注解

- 用在类上，方法上，成员变量，构造器，...上对成分进行编译约束，标记等操作的。
- 注解是JDK 1.5的新特性。
- 注解相当一种标记，是类的组成部分，可以给类携带一些额外信息。
- 注解是给编译器或JVM看的，编译器或JVM可以根据注解来完成对应的功能。

注解作用

- 标记
- 方法重写约束。@Override
- 函数式接口约束。@FunctionInterface
- 现今有名的框架技术多半都是在使用注解和反射，都是属于框架的基础技术。

### 27.2 注解的使用

自定义注解的格式

```Java
修饰符 @interface 注解名 {
    // 注解属性
}
```

注意：自定义注解用@interface关键字，注解默认可以标记很多地方。

注解的属性

属性格式

- 格式1：数据类型 属性名();
- 格式2：数据类型 属性名() default 默认值;

属性适用的数据类型：八种数据类型(int，short，long，double，byte，char，boolean，float)，String，Class。以上类型的数组形式都支持。

```Java
@Book(name = "《精通Java基础》",authors = {"波仔","Dlei","波妞"},price = 99.9)
public class MyBook {
    @Book(name = "《精通MySQL数据库入门到删库跑路》",authors = {"小白","小黑"},price = 19.9,address = "北京")
    public static void main(String[] args) {

    }
}

@interface Book{
    String name();
    String[] authors();
    double price();
    String address() default "广州";
}
```

注意：在用注解的时候，属性必须赋值，除非这个属性有默认值。

注解的特殊属性名称：value

- value属性，如果只有一个value属性的情况下，使用value属性的时候可以省略value名称不写。
- 但是如果有多个属性，且多个属性没有默认值，那么value是不能省略的。

```Java
@Books("/deleteBook.action")
//@Books(value = "/deleteBook.action")
public class AnnotationDemo {
}

@interface Books {
    String value();
}
```

元注解

- 元注解是sun公司提供的。
- 元注解是用在自定义注解上的注解。
- 元注解是用来注解自定义注解的。

元注解有两个

- @Target：约束自定义注解只能在哪些地方使用
  - 但是默认的注解可以在类，方法，构造器，成员变量，...使用。
- @Retention：申明注解的生命周期
  - 申明注解的作用范围：编译时，运行时。

@Target可使用的值定义在ElementType枚举类中，常用值有

- TYPE，类、接口
- FIELD，成员变量
- METHOD，成员方法
- PARAMETER，方法参数
- CONSTRUCTOR，构造器
- LOCAL_VARIABLE，局部变量

@Retention可使用的值定义在RetentionPolicy枚举类中，常用值有

- SOURCE：注解只作用在源码阶段，生成的字节码文件中不存在。
- CLASS：注解作用在源码阶段，字节码文件阶段，运行阶段不存在，默认值。
- RUNTIME：注解作用在源码阶段，字节码文件阶段，运行阶段。(开发常用)

```Java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

public class AnnotationDemo {
    @MyTest
    public static void main(String[] args) {
    }
}

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
@interface MyTest {
}
```

注解的解析：我们会使用注解注释一个类的成分，那么就涉及到要解析出这些注解的数据。开发中经常要知道一个类的成分上面到底有哪些注解，注解有哪些属性数据，这都需要进行注解的解析。

与注解解析相关的接口

- Annotation：注解类型，该类是所有注解的父类。注解都是一个Annotation的对象。
- AnnotatedElement：该接口定义了与注解解析相关的方法。所有的类成分Class，Method，Field，Constructor：都实现了AnnotatedElement接口，他们都拥有解析注解的能力。
  - Annotation[] getDeclaredAnnotations()：获得当前对象上使用的所有注解，返回注解数组。
  - T getDeclaredAnnotation(Class\<T> annotationClass)：根据注解类型获得对应注解对象。
  - boolean isAnnotationPresent(Class\<Annotation> annotationClass)：判断当前对象是否使用了指定的注解，如果使用了则返回true，否则false。

解析注解数据的原理：注解在哪个成分上，我们就先拿哪个成分对象，再拿该对象上面的注解。

```Java
import org.junit.Test;
import java.lang.annotation.*;
import java.lang.reflect.Method;
import java.util.Arrays;

public class AnnotationDemo {
    @Test
    public void parseClass() {
        Class c = BookStore.class;
        if (c.isAnnotationPresent(Books.class)) {
            Books book = (Books) c.getDeclaredAnnotation(Books.class);
            System.out.println(book.value());
            System.out.println(book.price());
            System.out.println(Arrays.toString(book.authors()));
        }
    }

    @Test
    public void parseMethod() throws Exception {
        Class c = BookStore.class;
        Method run = c.getDeclaredMethod("run");
        if (run.isAnnotationPresent(Books.class)) {
            Books book = (Books) run.getDeclaredAnnotation(Books.class);
            System.out.println(book.value());
            System.out.println(book.price());
            System.out.println(Arrays.toString(book.authors()));
        }
    }
}

@Books(value = "《Java基础到精通》",price = 99.5,authors = {"Mark","波仔"})
class BookStore {
    @Books(value = "《MyBatis持久层框架》",price = 199.5,authors = {"Dlei","小黑"})
    public void run() {
    }
}

@Target({ElementType.TYPE,ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@interface Books {
    String value();
    double price() default 100;
    String[] authors();
}
```

自定义注解模拟写一个Junit框架的基本使用

需求：定义若干个方法，只要加了MyTest注解，就可以被自动触发执行。

分析

- 定义一个自定义注解MyTest
  - 只能注解方法
  - 存活范围一直都在
- 定义若干个方法，只要有@MyTest注解的方法就能被触发执行，没有这个注解的方法不能执行

```Java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import java.lang.reflect.Method;

public class TestDemo {
    @MyTest
    public void test01() {
        System.out.println("===test01===");
    }

    public void test02() {
        System.out.println("===test02===");
    }

    @MyTest
    public void test03() {
        System.out.println("===test03===");
    }

    @MyTest
    public void test04() {
        System.out.println("===test04===");
    }

    public static void main(String[] args) throws Exception {
        TestDemo t = new TestDemo();
        Class c = TestDemo.class;
        Method[] methods = c.getDeclaredMethods();
        for (Method method : methods) {
            if (method.isAnnotationPresent(MyTest.class)) {
                method.invoke(t);
            }
        }
    }
}

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
@interface MyTest {
}
```

注意：注解和反射可以配合解决一些框架思想，注解可以实现标记的成分做特殊处理。

## 28. XML

### 28.1 XML概述

XML概念

- 英文：Extensible Markup Language可扩展的标记语言，由各种标记(标签==元素)组成。
- 可扩展：所有的标签都是自定义的，可以随意扩展的。如：\<abc/>，\<bobby>，\<sex>。
- 标记语言：整个文档由各种标签组成。清晰，数据结构化。
- XML是通过格式标准，全球所有的技术人员都知道这个东西，都可能会按照XML的规范存储数据，交互数据。

XML作用

- 数据交换：不同的计算机语言之间，不同的操作系统之间，不同的数据库之间，进行数据交换。
- 配置文件：在后期我们主要用于各种框架的配置文件。

XML的特点

- 用于数据交互，用于数据的存储，用于做系统的配置文件
- 区分大小写
- 非常严谨，只要有错误，解析器就不能解析
- 可以扩展的，所有的标签都是程序员自己创建出来
- XML文件的后缀为.xml

### 28.2 XML的使用

创建一个XML文件

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<person>
    <name>王熙凤</name>
    <age>29</age>
    <sex>女</sex>
    <hobby>笑得很犀利</hobby>
</person>
```

XML由七种组成元素构成

- 声明(抬头)
- 元素(标签)
- 属性
- 注释
- 实体字符
- CDATA字符数据区
- 处理指令

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<?xml-stylesheet type="text/css" href="../css/xml.css" ?>
<!--处理指令：导入外部的css样式控制xml的界面效果，没有啥用，xml不是为了展示好看的！-->
<!--声明 抬头 必须在第一行-->
<!--注释，本处就是注释，必须用前后尖括号围起来-->
<!--标签(元素)，注意一个XML文件只能有一个根标签-->
<student>
    <!--属性信息：id，desc-->
    <name id="1" desc="高富帅">西门庆</name>
    <age>32</age>
    <!--实体字符：在XML文件中，我们不能直接写小于号等一些特殊字符，会与XML文件本身的内容冲突。此时必须用转义的实体字符。-->
    <sql>
        <!--select * from student where age < 18 && age > 10;-->
        select * from student where age &lt; 18 &amp;&amp; age &gt; 10;
    </sql>
    <!--字符数据区：在XML文件中，我们不能直接写小于号等一些特殊字符，会与XML文件本身的内容冲突。此时必须用转义的实体字符。
    或者也可以选择使用字符数据区，里面的内容可以随便了-->
    <sql2>
        <![CDATA[
            select * from student where age < 18 && age > 10;
        ]]>
    </sql2>
</student>
```

使用的CSS文件如下

```CSS
name {
    font-size: 30px;
    color: green;
}

sql2 {
    font-size: 60px;
    color: red;
    font-family: 楷体;
}
```

**XML的两种约束**

- DTD约束
- Schema约束(是最牛的约束技术，最重要的)
- 我们只要能懂就好了，以后约束文件都是框架写好的，我们会用即可

DTD约束的概念

- DTD：Document Type Definiation 文档类型定义
- 作用：纯文本文件，指定了XML约束规则

在企业实际开发中，不会自己编写DTD约束文档，我们后期只需通过框架提供的DTD约束文档编写出相应的XML配置文档。只要回导入别人的DTD约束自己即可。

Schema约束的引入

DTD的不足

- 不能验证数据类型
- 因为DTD是一个文本文件，本身不能验证是否正确

Schema特点

- 约束文件本身也是一个XML文件，它本身也会被其它xsd文档约束。
- 内置多种数据类型，可以检查数据类型是否正确。
- 支持命名空间，一个XML文件可以同时引入多个xsd的约束文件，让约束规则重用。
- 扩展名为xsd：XML Schema Definition。
- 约束文件本身也是XML文件，所以也有根元素，根元素的名字叫：schema。

模式文档和实例文档

模式文档：制定约束的XML文档(类似于：类)。Schema

实例文档：被约束的XML文档(类似于：对象)

**XML的解析**：使用Java语言去解析XML文件，读取XML中的元素，属性，文本等数据就是XML解析。

XML的两种解析方式

- DOM解析：Document Object Model文档对象模型(面向对象的解析方式)
  - 优点：将整个XML文件加载到内存中，生成一棵DOM树。随意访问树上任何一个节点，可以修改和删除节点，程序开发比较方便。纯面向对象开发。
  - 缺点：占内存，如果XML文件很大，可能出现内存溢出。
- SAX解析
  - 优点：事件驱动型解析，读取一行就解析一行，释放内存。理论上可以解析任意大小的XML文件。
  - 缺点：使用过的元素不能再访问了，不能修改元素，只能查找。

Java中DOM解析开发包

- JAXP
- JDOM
- Dom4j
- Jsoup

**XML文档生成DOM树原理**

XML DOM和HTML DOM一样，XML DOM将整个XML文档加载到内存，生成一个DOM树，并获得一个Document对象，通过Document对象就可以对DOM进行操作。

XML文件==document文档对象树\==DOM树

### 28.3 Dom4J

Dom4J：获取Document对象和根元素。

Dom4J安装步骤

- 去Dom4J官网下载Dom4J的框架：都是一些jar包。
- 把Dom4J的核心jar包导入到当前项目中去。
- 在项目中创建一个文件夹：lib。
- 将dom4j-2.1.1.jar文件复制到lib文件夹。
- 在jar文件上点右键，选择Add as Library -> 点击OK。
- 在类中导包使用。

Java提供了Class下的一个方法

- public InputStream getResourceAsStream(String path)：用于加载文件成为一个字节输入流返回。

Document文档

- Element getRootElement()：获取根元素。

books.xml文档内容如下

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<books>
    <book id="0001" desc="第一本书">
        <name>JavaWeb开发教程</name>
        <author>张孝祥</author>
        <sale>100.00元</sale>
    </book>
    <book id="0002">
        <name>三国演义</name>
        <author>罗贯中</author>
        <sale>100.00元</sale>
    </book>
    <user>
    </user>
</books>
```

获取document对象和根元素

```Java
import org.dom4j.Document;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;
import java.io.InputStream;

public class Dom4JDemo {
    public static void main(String[] args) throws Exception {
        SAXReader saxReader = new SAXReader();
        InputStream is = Dom4JDemo.class.getResourceAsStream("/books.xml");
        Document document = saxReader.read(is);
        System.out.println(document);
        Element root = document.getRootElement();
        System.out.println(root.getName());
    }
}
```

Dom4J解析XML的子元素

Element元素的API

- String getName()：取元素的名称。
- List\<Element> elements()：取当前元素下的全部子元素(一级)。
- List\<Element> elements(String name)：获取当前元素下的指定名称的全部子元素(一级)。
- Element element(String name)：获取当前元素下的指定名称的某个子元素，默认取第一个(一级)。

```Java
import org.dom4j.Document;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

import java.io.File;
import java.util.List;

public class Dom4JDemo01 {
    public static void main(String[] args) throws Exception {
        SAXReader saxReader = new SAXReader();
        Document document = saxReader.read(new File("Day07Demo/src/books.xml"));
        Element root = document.getRootElement();
        System.out.println(root.getName());

        List<Element> sonElement = root.elements();
        for (Element element : sonElement) {
            System.out.println(element.getName());
        }
        System.out.println("-------------------------");

        List<Element> sonElement1 = root.elements("book");
        for (Element element : sonElement1) {
            System.out.println(element.getName());
        }
        System.out.println("-------------------------");

        Element son = root.element("book");
        System.out.println(son.getName());
        System.out.println(son.attributeValue("id"));
    }
}
```

Dom4J解析XML的属性

Element元素的API

- List\<Attribute> attributes()：获取元素的全部属性对象。
- Attribute attribute(String name)：根据名称获取某个元素的属性对象。
- String attributeValue(String var1)：直接获取某个元素的某个属性名称的值。

Attribute对象的API

- String getName()：获取属性名称。
- String getValue()：获取属性值。

```Java
import org.dom4j.Attribute;
import org.dom4j.Document;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

import java.io.File;
import java.util.List;

public class Dom4JDemo02 {
    public static void main(String[] args) throws Exception {
        SAXReader saxReader = new SAXReader();
        Document document = saxReader.read(new File("Day07Demo/src/books.xml"));
        Element root = document.getRootElement();
        Element bookEle = root.element("book");
        List<Attribute> attributes = bookEle.attributes();
        for (Attribute attribute : attributes) {
            System.out.println(attribute.getName() + "=>" + attribute.getValue());
        }

        Attribute descAttr = bookEle.attribute("desc");
        System.out.println(descAttr.getName() + "=>" + descAttr.getValue());

        System.out.println(bookEle.attributeValue("id"));
        System.out.println(bookEle.attributeValue("desc"));
    }
}
```

Dom4J解析XML的文本

Element

- String elementText(String name)：可以直接获取当前元素的子元素的文本内容。
- String elementTextTrim(String name)：去前后空格，直接获取当前元素的子元素的文本内容。
- String getText()：直接获取当前元素的文本内容。
- String getTextTrim()：去前后空格，直接获取当前元素的文本内容。

```Java
import org.dom4j.Document;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

import java.io.File;

public class Dom4JDemo03 {
    public static void main(String[] args) throws Exception {
        SAXReader saxReader = new SAXReader();
        Document document = saxReader.read(new File("Day07Demo/src/books.xml"));
        Element root = document.getRootElement();

        Element bookEle = root.element("book");
        System.out.println(bookEle.elementText("name"));
        System.out.println(bookEle.elementTextTrim("name"));
        System.out.println(bookEle.elementText("author"));
        System.out.println(bookEle.elementTextTrim("author"));
        System.out.println(bookEle.elementText("sale"));
        System.out.println(bookEle.elementTextTrim("sale"));

        Element bookNameEle = bookEle.element("name");
        System.out.println(bookNameEle.getText());
        System.out.println(bookNameEle.getTextTrim());
    }
}
```

Dom4J解析XML文件：Contacts.xml成为一个Java的对象(集合对象)。

Contacts.xml解析成===>List\<Contact>

Contacts.xml文件

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<contactList>
    <contact id="1" vip="true">
        <name>潘金莲</name>
        <gender>女</gender>
        <email>panpan@ithei.cn</email>
    </contact>
    <contact id="2" vip="false">
        <name>武松</name>
        <gender>男</gender>
        <email>wusong@ithei.cn</email>
    </contact>
    <contact id="3" vip="false">
        <name>武大郎</name>
        <gender>男</gender>
        <email>wuda@ithei.cn</email>
    </contact>
</contactList>
```

Contact.java类

```Java
public class Contact {
    private int id;
    private boolean vip;
    private String name;
    private char sex;
    private String email;

    public Contact() {
    }

    public Contact(int id, boolean vip, String name, char sex, String email) {
        this.id = id;
        this.vip = vip;
        this.name = name;
        this.sex = sex;
        this.email = email;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public boolean isVip() {
        return vip;
    }

    public void setVip(boolean vip) {
        this.vip = vip;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public char getSex() {
        return sex;
    }

    public void setSex(char sex) {
        this.sex = sex;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    @Override
    public String toString() {
        return "Contact{" +
                "id=" + id +
                ", vip=" + vip +
                ", name='" + name + '\'' +
                ", sex=" + sex +
                ", email='" + email + '\'' +
                '}';
    }
}
```

Dom4J解析类

```Java
import org.dom4j.Document;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

import java.io.File;
import java.util.ArrayList;
import java.util.List;

public class Dom4JDemo04 {
    public static void main(String[] args) throws Exception {
        SAXReader saxReader = new SAXReader();
        Document document = saxReader.read(new File("Day07Demo/src/Contacts.xml"));
        Element root = document.getRootElement();

        List<Element> sonElements = root.elements();
        List<Contact> contactList = new ArrayList<>();
        if (sonElements != null && sonElements.size() > 0) {
            for (Element sonElement : sonElements) {
                Contact contact = new Contact();
                contact.setId(Integer.valueOf(sonElement.attributeValue("id")));
                contact.setVip(Boolean.valueOf(sonElement.attributeValue("vip")));
                contact.setName(sonElement.elementText("name"));
                contact.setSex(sonElement.elementText("gender").charAt(0));
                contact.setEmail(sonElement.elementText("email"));
                contactList.add(contact);
            }
        }
        System.out.println(contactList);
    }
}
```

### 28.4 XPath技术

XPath作用：一种用于快速查找XML元素的路径表达式，是用于方便地检索XML文件中的信息。

XPath表达式分类

- 绝对路径
- 相对路径
- 全文搜索
- 属性查找

XPath常用API

- List\<Node> selectNodes(String var1)：检索出一批节点集合。
- Node selectSingleNode(String var1)：检索出一个节点返回。

```Java
import org.dom4j.Attribute;
import org.dom4j.Document;
import org.dom4j.Element;
import org.dom4j.Node;
import org.dom4j.io.SAXReader;
import org.junit.Test;

import java.io.InputStream;
import java.util.List;

public class XPathDemo {
    @Test
    public void path01() throws Exception {
        SAXReader saxReader = new SAXReader();
        InputStream is = Dom4JDemo04.class.getResourceAsStream("/Contacts.xml");
        Document document = saxReader.read(is);
        List<Node> nameNodes = document.selectNodes("/contactList/contact/name");
        for (Node nameNode : nameNodes) {
            System.out.println(nameNode.getText());
        }
    }

    @Test
    public void path02() throws Exception {
        SAXReader saxReader = new SAXReader();
        InputStream is = Dom4JDemo04.class.getResourceAsStream("/Contacts.xml");
        Document document = saxReader.read(is);
        Element root = document.getRootElement();
        List<Node> nameNodes = root.selectNodes("./contact/name");
        for (Node nameNode : nameNodes) {
            System.out.println(nameNode.getText());
        }
    }

    @Test
    public void path03() throws Exception {
        SAXReader saxReader = new SAXReader();
        InputStream is = Dom4JDemo04.class.getResourceAsStream("/Contacts.xml");
        Document document = saxReader.read(is);
        List<Node> nameNodes = document.selectNodes("//name");
        for (Node nameNode : nameNodes) {
            System.out.println(nameNode.getText());
        }
        System.out.println("-----------------------------------------------");
        List<Node> nameNodes1 = document.selectNodes("//contact/name");
        for (Node nameNode : nameNodes1) {
            System.out.println(nameNode.getText());
        }
        System.out.println("-----------------------------------------------");
        List<Node> nameNodes2 = document.selectNodes("//contact//name");
        for (Node nameNode : nameNodes2) {
            System.out.println(nameNode.getText());
        }
    }

    @Test
    public void path04() throws Exception {
        SAXReader saxReader = new SAXReader();
        InputStream is = Dom4JDemo04.class.getResourceAsStream("/Contacts.xml");
        Document document = saxReader.read(is);
        List<Node> attributes = document.selectNodes("//@id");
        for (Node attribute : attributes) {
            Attribute attr = (Attribute) attribute;
            System.out.println(attr.getName() + "--->" + attr.getValue());
        }
        System.out.println("-----------------------------------------------");
        List<Node> nodeEles = document.selectNodes("//contact[@id]");
        for (Node nodeEle : nodeEles) {
            System.out.println(nodeEle.getName());
        }
        System.out.println("-----------------------------------------------");
        Node nodeEle = document.selectSingleNode("//contact[@id=2]");
        Element ele = (Element) nodeEle;
        System.out.println(ele.elementTextTrim("name"));
    }
}
```

注意：XPath依赖Dom4J技术 ，必须先导入Dom4J，且使用XPath需要另外导入jaxen-1.1.2.jar包。

## 29. 设计模式等思想

工厂设计模式：工厂模式(Factory Pattern)是Java中最常用的设计模式之一。这种类型的设计模式属于创建型模式，它提供了一种创建对象的方式。之前我们创建对象时，都是使用new 对象的形式创建，除new 对象方式以外，工厂模式也可以创建对象。

工厂设计模式的作用

- 对象通过工厂的方法创建返回，工厂的方法可以为该对象进行加工和数据注入。
- 可以实现类与类之间的解耦操作。

小结

- 优点：工厂模式的存在可以改变创建对象的方式，解决类与类之间的耦合。
- 缺点：工厂设计模式多了一个工厂类。

工厂类

```Java
public class FactoryPattern {
    public static Animal creatAnimal() {
        return new Dog();
    }
}
```

测试类

```Java
public class FactoryDemo {
    public static void main(String[] args) {
        Animal a = FactoryPattern.creatAnimal();
        a.run();
    }
}
```

装饰模式：装饰模式指的是在不改变原类，不使用继承的基础上，动态地扩展一个类的功能。

思想：是创建一个新类，包装原始类，从而在新类中提升原来类的功能。

小结

- 装饰模式可以在不改变原类的基础上对类中的方法进行扩展增强，实现原则如下
  - 定义父类
  - 定义原始类，继承父类，定义功能
  - 定义装饰类，继承父类，包装原始类，增强功能

父类

```Java
public abstract class InputStream {
    public abstract void read();
    public abstract void close();
}
```

原始类

```Java
public class FileInputStream extends InputStream {
    @Override
    public void read() {
        System.out.println("读取数据~~~");
    }

    @Override
    public void close() {
        System.out.println("关闭流~~~");
    }
}
```

装饰类

```Java
public class BufferedInputStream extends InputStream {
    private InputStream is;
    public BufferedInputStream(InputStream is) {
        this.is = is;
    }
    @Override
    public void read() {
        System.out.println("开启高效缓冲读取~");
        is.read();
    }

    @Override
    public void close() {
        is.close();
    }
}
```

测试用例类

```Java
public class Demo {
    public static void main(String[] args) {
        InputStream is = new BufferedInputStream(new FileInputStream());
        is.read();
        is.close();
    }
}
```

**Commons-io包**

Commons-io包：commons-io是apache开源基金组织提供的一组有关IO操作的类库，可以提高IO功能开发的效率。commons-io工具包提供了很多有关io操作的类。

小结：IOUtils和FileUtils可以方便地复制文件和文件夹。

```Java
import org.apache.commons.io.FileUtils;
import org.apache.commons.io.IOUtils;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.nio.file.Files;
import java.nio.file.Paths;

public class CommonsIODemo {
    public static void main(String[] args) throws Exception {
        IOUtils.copy(new FileInputStream("Day07Demo/src/books.xml"),new FileOutputStream("Day07Demo/new.xml"));
        FileUtils.copyFileToDirectory(new File("Day07Demo/src/books.xml"), new File("F:/test"));
        FileUtils.copyDirectoryToDirectory(new File("D:\\letsvpn"), new File("F:\\test"));
        Files.copy(Paths.get("Day07Demo/src/books.xml"), new FileOutputStream("Day07Demo/new1.xml"));
    }
}
```

**Base64**

Base64概述：Base64是网络上最常见的用于传输8Bit字节码的编码方式之一，Base64就是一种基于64个可打印字符来表示二进制数据的方法。

在Java 8中，Base64编码已经成为Java类库的标准。

Java 8内置了Base64编码的编码器和解码器。

Base64工具类提供了一套静态方法获取下面三种BASE64编解码器

- 基本：输出被映射到一组字符A-Za-z0-9+/，编码不添加任何行标，输出的解码仅支持A-Za-z0-9+/。
- URL：输出映射到一组字符A-Za-z0-9+_，输出是URL和文件。
- MIME：输出映射到MIME友好格式。输出每行不超过76字符，并且使用‘\r’并跟随‘\n’作为分割。编码输出最后没有行分割。

```Java
import java.util.Base64;
import java.util.UUID;

public class Base64Demo {
    public static void main(String[] args) {
        try {
            String rs1 = Base64.getEncoder().encodeToString("全栈程序员".getBytes());
            System.out.println(rs1);
            byte[] buffer = Base64.getDecoder().decode(rs1);
            System.out.println(new String(buffer));

            String rs2 = Base64.getUrlEncoder().encodeToString("?loginName=全栈&password=123456".getBytes());
            System.out.println(rs2);
            byte[] buffer1 = Base64.getUrlDecoder().decode(rs2);
            System.out.println(new String(buffer1));

            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < 10; i++) {
                sb.append(UUID.randomUUID().toString());
            }
            String rs3 = Base64.getMimeEncoder().encodeToString(sb.toString().getBytes());
            System.out.println(rs3);
            byte[] buffer2 = Base64.getMimeDecoder().decode(rs3);
            System.out.println(new String(buffer2));

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 30. JDK8日期API解析

### 30.1 引入

老版本API计算时间困难，在毫秒计算时容易出现误差

```Java
import java.time.LocalDate;
import java.time.temporal.ChronoUnit;
import java.util.Calendar;
import java.util.Date;

public class JavaUtilTimeCalculateDemo {
    public static void main(String[] args) {
        Date d = new Date();
        long s1 = d.getTime();

        Calendar c = Calendar.getInstance();
        c.set(1995,11,16);
        Date d2 = c.getTime();
        long s2 = d2.getTime();

        long intervalDay = (s1 - s2) / 1000 / 60 / 60 / 24;
        System.out.println("1995年12月16日距离现在已经过了" + intervalDay + "天");
        System.out.println("-------------------------------------------------");

        long day = ChronoUnit.DAYS.between(LocalDate.of(1995, 12, 16), LocalDate.now());
        System.out.println("1995年12月16日距离现在已经过了" + day + "天");
    }
}
```

老版本API会出现线程安全问题

- SimpleDateFormat类是线程不安全的，在多线程的情况下，全局共享一个SimpleDateFormat类中的Calendar对象有可能会出现异常。需要考虑加锁来解决线程安全问题。

```Java
import java.text.SimpleDateFormat;
import java.util.Date;

public class SimpleDateFormatUnsafeDemo {
    final static SimpleDateFormat SIMPLE_DATE_FORMAT = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    try {
                        synchronized (SIMPLE_DATE_FORMAT) {
                            Date date = SIMPLE_DATE_FORMAT.parse("2018-12-12 12:12:12");
                            System.out.println(date);
                        }
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                }
            }).start();
        }
    }
}
```

老版本使用规范问题

```Java
import java.util.Calendar;

public class CalendarUnSafeDemo {
    public static void main(String[] args) {
        Calendar calendar = Calendar.getInstance();
        // 开发规范：不允许使用没有定义的魔法数字.
        calendar.set(2008,Calendar.AUGUST,8);
    }
}
```

### 30.2 常用类的概述与功能介绍

**Instant类**

- Instant类对时间轴上的单一瞬时点建模，可以用于记录应用程序中的事件时间戳，在之后学习的类型转换中，均可以使用Instant类作为中间类完成转换。

**Duration类**

- Duration类表示秒或纳秒时间间隔，适合处理较短的时间，需要更高的精确性。

**Period类**

- Period类表示一段时间的年、月、日。

**LocalDate类**

- LocalDate是一个不可变的日期时间对象，表示日期，通常被视为年月日。

**LocalTime类**

- LocalTime是一个不可变的日期时间对象，通常被看作是小时-秒，时间表示为纳秒精度。

**LocalDateTime类**

- LocalDateTime是一个不可变的日期时间对象，代表日期时间，通常被视为年-月-日-时-分-秒。

**ZonedDateTime类**

- ZonedDateTime是具有时区的日期时间的不可变表示，此类存储所有日期和时间字段，精度为纳秒，时区为区域偏移量，用于处理模糊的本地日期时间。

Date-Time API中的所有类均生成不可变实例，它们是线程安全的，并且这些类不提供公共构造函数，也就是说没办法通过new的方式直接创建，需要采用工厂方法加以实例化。

now方法在日期/时间类的使用

- now方法可以根据当前日期或时间创建实例。

```Java
import java.time.*;

public class JavaTimeDemo {
    public static void main(String[] args) {
        Instant instantNow = Instant.now();
        LocalDate localDateNow = LocalDate.now();
        LocalTime localTimeNow = LocalTime.now();
        LocalDateTime localDateTimeNow = LocalDateTime.now();
        ZonedDateTime zonedDateTimeNow = ZonedDateTime.now();
        System.out.println(instantNow);
        System.out.println(localDateNow);
        System.out.println(localTimeNow);
        System.out.println(localDateTimeNow);
        System.out.println(zonedDateTimeNow);
    }
}
```

```Java
import java.time.*;

public class JavaTimeDemo {
    public static void main(String[] args) {
        Year year = Year.now();
        YearMonth yearMonth = YearMonth.now();
        MonthDay monthDay = MonthDay.now();
        System.out.println(year);
        System.out.println(yearMonth);
        System.out.println(monthDay);
    }
}
```

of方法在日期/时间类的应用

- of方法可以根据给定的参数生成对应的日期/时间对象，基本上每个基本类都有of方法用于生成的对应的对象，而且重载形式多变，可以根据不同的参数生成对应的数据。

```Java
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;

public class JavaTimeDemo01 {
    public static void main(String[] args) {
        LocalDate localDate = LocalDate.of(2018, 8, 8);
        System.out.println(localDate);

        LocalTime localTime = LocalTime.of(20, 0,0,0);
        System.out.println(localTime);

        LocalDateTime localDateTime = LocalDateTime.of(2018, 8, 8, 20, 0);
        System.out.println(localDateTime);
        LocalDateTime localDateTime1 = LocalDateTime.of(localDate, localTime);
        System.out.println(localDateTime1);
    }
}
```

时区信息的获取

```Java
import java.time.ZoneId;
import java.util.Set;

public class JavaTimeDemo01 {
    public static void main(String[] args) {
        Set<String> availableZoneIds = ZoneId.getAvailableZoneIds();
        System.out.println(availableZoneIds.size());
        for (String availableZoneId : availableZoneIds) {
            System.out.println(availableZoneId);
        }
        System.out.println("---------------------------------------");
        ZoneId zoneId = ZoneId.systemDefault();
        System.out.println(zoneId);
    }
}
```

为LocalDateTime添加时区信息

- 封装时间LocalDateTime并添加时区信息
- 更改时区信息查看对应时间

```Java
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.ZonedDateTime;

public class JavaTimeDemo01 {
    public static void main(String[] args) {
        LocalDateTime localDateTime = LocalDateTime.of(2018, 11, 11, 8, 54, 38);
        ZonedDateTime zonedDateTime = localDateTime.atZone(ZoneId.of("Asia/Shanghai"));
        System.out.println("上海当前的时间是：" + zonedDateTime);

        ZonedDateTime zonedDateTime1 = zonedDateTime.withZoneSameInstant(ZoneId.of("Asia/Tokyo"));
        System.out.println("同一时刻东京的时间是：" + zonedDateTime1);
    }
}
```

Month枚举类的使用

java.time包中引入了Month的枚举，Month中包含标准日历中的12个月份的常量(从JANURAY到DECEMBER)也提供了一些方便的方法供我们使用。

推荐在初始化LocalDate和LocalDateTime对象的时候，月份的参数使用枚举的方式传入，这样更简单易懂而且不易出错，因为如果是老的思维，Calendar传入0的话，那么会出现异常。

```Java
import java.time.LocalDateTime;
import java.time.Month;

public class JavaTimeDemo02 {
    public static void main(String[] args) {
        LocalDateTime.of(2011, Month.MAY, 15, 11, 11, 11);
        Month month = Month.of(12);
        System.out.println(month);
    }
}
```

### 30.2 plus和with等其他方法的使用

想要修改某个日期/时间对象的现有实例时，我们可以使用plus和minus方法来完成操作。

Java 8中日期时间相关的API中的所有实例都是不可改变的，一旦创建LocalDate，LocalTime，LocalDateTime就无法修改他们(类似于String)，这对于线程安全非常有利。

```Java
import java.time.*;

public class JavaTimeDemo02 {
    public static void main(String[] args) {
        LocalDate localDate = LocalDate.of(2016, 2, 13);
        System.out.println("当前时间是：" + localDate);
        LocalDate localDate1 = localDate.plusDays(4);
        System.out.println("4天后时间是：" + localDate1);
        System.out.println(localDate == localDate1);
        LocalDate localDate2 = localDate.plusWeeks(3);
        System.out.println("3周后时间是：" + localDate2);
        LocalDate localDate3 = localDate.plusMonths(5);
        System.out.println("5月后时间是：" + localDate3);
        LocalDate localDate4 = localDate.plusYears(2);
        System.out.println("2年后时间是：" + localDate4);
    }
}
```

需求案例：今天程序员小张查看自己的车辆保险记录的时候看到还有2年3月8天就到期了，计算到期的时间是什么时候。

```Java
import java.time.*;

public class JavaTimeDemo02 {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        LocalDateTime endTime = now.plusYears(2).plusMonths(3).plusDays(8);
        System.out.println("当前时间：" + now + "，到期时间：" + endTime);
        Period period = Period.of(2, 3, 8);
        LocalDateTime endT = now.plus(period);
        System.out.println("当前时间：" + now + "，到期时间：" + endT);
    }
}
```

需求案例：结婚10年称为锡婚，2020年2月2日11点11分11秒称为对称日，很多情侣准备在那天结婚，如果在那天结婚了，那么锡婚会发生在什么时候。

```Java
import java.time.*;
import java.time.temporal.ChronoUnit;

public class JavaTimeDemo02 {
    public static void main(String[] args) {
        LocalDateTime marryTime = LocalDateTime.of(2020, Month.FEBRUARY, 2, 11, 11, 11);
        LocalDateTime time = marryTime.plus(1, ChronoUnit.DECADES);
        System.out.println("结婚时间：" + marryTime + "，锡婚时间：" + time);
        LocalDateTime eatTime = time.plus(1, ChronoUnit.HALF_DAYS);
        System.out.println("请客吃饭时间：" + eatTime);
    }
}
```

with方法的使用

- 如果不需要对日期进行加减而是要直接修改日期的话，那么可以使用with方法，with方法提供了很多种修改时间的方式。

```Java
import java.time.LocalDateTime;
import java.time.temporal.ChronoField;

public class JavaTimeDemo03 {
    public static void main(String[] args) {
        LocalDateTime time = getTime();
        LocalDateTime resultTime = time.withDayOfMonth(1);
        System.out.println("修改前：" + time + "，修改后：" + resultTime);
        LocalDateTime result = time.with(ChronoField.DAY_OF_MONTH, 8);
        System.out.println("修改前：" + time + "，修改后：" + result);
    }

    public static LocalDateTime getTime() {
        return LocalDateTime.of(1999,12,12,12,12,0);
    }
}
```

调节器TemporalAdjuster与查询TemporalQuery

- TemporalAdjusters主要也是修改日期的作用

```Java
import java.time.LocalDate;
import java.time.temporal.TemporalAdjusters;

public class JavaTimeDemo03 {
    public static void main(String[] args) {
        LocalDate now = LocalDate.now();
        LocalDate localDate = now.with(TemporalAdjusters.firstDayOfMonth());
        System.out.println("时间修改为当月的第一天:" + localDate);
        LocalDate localDate1 = now.with(TemporalAdjusters.firstDayOfNextMonth());
        System.out.println(localDate1);
        LocalDate localDate2 = now.with(TemporalAdjusters.firstDayOfNextYear());
        System.out.println(localDate2);
        LocalDate localDate3 = now.with(TemporalAdjusters.lastDayOfMonth());
        System.out.println(localDate3);
        LocalDate localDate4 = now.with(TemporalAdjusters.lastDayOfYear());
        System.out.println(localDate4);
    }
}
```

DayOfWeek的使用

```Java
import java.time.DayOfWeek;
import java.time.LocalDate;
import java.time.temporal.TemporalAdjusters;

public class JavaTimeDemo03 {
    public static void main(String[] args) {
        LocalDate now = LocalDate.now();
        LocalDate localDate = now.with(DayOfWeek.SUNDAY);
        System.out.println("时间修改为:" + localDate);
        LocalDate w = now.with(TemporalAdjusters.previous(DayOfWeek.WEDNESDAY));
        System.out.println("时间修改为:" + w);
    }
}
```

自定义TemporalAdjuster调节器

调整发薪日类

```Java
import java.time.DayOfWeek;
import java.time.LocalDate;
import java.time.temporal.Temporal;
import java.time.temporal.TemporalAdjuster;
import java.time.temporal.TemporalAdjusters;

public class PayDayAdjuster implements TemporalAdjuster {
    @Override
    public Temporal adjustInto(Temporal temporal) {
        LocalDate payDay = LocalDate.from(temporal);
        int day;
        if (payDay.getDayOfMonth() != 15) {
            day = 15;
        } else {
            day = payDay.getDayOfMonth();
        }
        LocalDate realPayDay = payDay.withDayOfMonth(day);
        if (realPayDay.getDayOfWeek() == DayOfWeek.SUNDAY || realPayDay.getDayOfWeek() == DayOfWeek.SATURDAY) {
            realPayDay = realPayDay.with(TemporalAdjusters.previous(DayOfWeek.FRIDAY));
        }
        return realPayDay;
    }
}
```

测试用例类

```Java
import java.time.LocalDate;

public class JavaTimeDemo {
    public static void main(String[] args) {
        LocalDate payDay = LocalDate.of(2018, 12, 15);
        LocalDate realDay = LocalDate.from(new PayDayAdjuster().adjustInto(payDay));
        System.out.println("预计发薪日：" + payDay + "，真实发薪日：" + realDay);
    }
}
```

TemporalQuery日期查询的应用

```Java
import java.time.LocalDate;
import java.time.Month;
import java.time.temporal.ChronoUnit;
import java.time.temporal.TemporalAccessor;
import java.time.temporal.TemporalQuery;

public class TestQueryImpl implements TemporalQuery<Long[]> {
    @Override
    public Long[] queryFrom(TemporalAccessor temporal) {
        LocalDate date = LocalDate.from(temporal);
        LocalDate d1 = LocalDate.of(date.getYear(), Month.DECEMBER, 25);
        LocalDate d2 = LocalDate.of(date.getYear(), Month.JUNE, 1);
        LocalDate d3 = LocalDate.of(date.getYear(), Month.MAY, 1);
        if (date.isAfter(d1)) {
            d1 = d1.plusYears(1);
        }
        if (date.isAfter(d2)) {
            d2 = d2.plusYears(1);
        }
        if (date.isAfter(d3)) {
            d3 = d3.plusYears(1);
        }
        Long[] lon = {ChronoUnit.DAYS.between(date,d1),ChronoUnit.DAYS.between(date,d2),ChronoUnit.DAYS.between(date,d3)};
        return lon;
    }
}
```

```Java
import java.time.LocalDate;

public class JavaTimeDemo01 {
    public static void main(String[] args) {
        LocalDate date = LocalDate.of(2020,5,30);
        Long[] longs = date.query(new TestQueryImpl());
        System.out.println("距离下一个圣诞节还有" + longs[0] + "天，距离下一个儿童节还有" + longs[1] + "天，距离下一个劳动节还有" + longs[2] + "天");
    }
}
```

**日期类之间的转换**

Java 8中的java.time包中并没有提供太多的内置方式来转换java.util包中用预处理标准日期和时间的类，我们可以使用Instant类作为中介，也可以使用java.sql.Date和java.sql.Timestamp类提供的方法进行转换。

利用Instant类进行转换

```Java
import java.time.Instant;
import java.time.LocalDate;
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.util.Date;

public class JavaTimeDemo02 {
    public static void main(String[] args) {
        Date d = new Date();
        Instant i = d.toInstant();
        ZonedDateTime zonedDateTime = i.atZone(ZoneId.systemDefault());
        LocalDate localDate = zonedDateTime.toLocalDate();
        System.out.println(d);
        System.out.println(localDate);
    }
}
```

利用java.sql.Date和java.sql.Timestamp类

```Java
import java.sql.Date;
import java.sql.Timestamp;
import java.time.LocalDate;
import java.time.LocalDateTime;

public class JavaTimeDemo02 {
    public static void main(String[] args) {
        Date d = new Date(System.currentTimeMillis());
        LocalDate localDate = d.toLocalDate();
        System.out.println(d);
        System.out.println(localDate);

        Timestamp t = new Timestamp(System.currentTimeMillis());
        LocalDateTime time = t.toLocalDateTime();
        System.out.println(t);
        System.out.println(time);
    }
}
```

```Java
import java.time.LocalDate;
import java.util.Date;

public class JavaTimeDemo03 {
    public static void main(String[] args) {
        Date d = new Date();
        java.sql.Date date = new java.sql.Date(d.getTime());
        LocalDate localDate = date.toLocalDate();
        System.out.println(d);
        System.out.println(date);
        System.out.println(localDate);
    }
}
```

Calendar转换为ZonedDateTime

```Java
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.util.Calendar;
import java.util.TimeZone;

public class JavaTimeDemo03 {
    public static void main(String[] args) {
        Calendar cal = Calendar.getInstance();
        TimeZone timeZone = cal.getTimeZone();
        ZoneId zoneId = timeZone.toZoneId();
        ZonedDateTime zonedDateTime = ZonedDateTime.ofInstant(cal.toInstant(), zoneId);
        System.out.println(cal);
        System.out.println(zonedDateTime);
    }
}
```

Calendar转换为LocalDateTime

```Java
import java.time.LocalDateTime;
import java.util.Calendar;

public class JavaTimeDemo04 {
    public static void main(String[] args) {
        Calendar cal = Calendar.getInstance();
        int year = cal.get(Calendar.YEAR);
        int month = cal.get(Calendar.MONTH);
        int day = cal.get(Calendar.DAY_OF_MONTH);
        int hour = cal.get(Calendar.HOUR);
        int minute = cal.get(Calendar.MINUTE);
        int second = cal.get(Calendar.SECOND);
        LocalDateTime localDateTime = LocalDateTime.of(year, month + 1, day, hour, minute, second);
        System.out.println(localDateTime);
    }
}
```

### 30.3 日期的解析与格式化DateTimeFormatter

DateTimeFormatter类提供了大量预定义格式化器，包括常量(如ISO_LOCAL_DATE)，模式字母(如yyyy-MM-dd)以及本地化样式。

与SimpleDateFormat不同的是，新版本的日期/时间API的格式化与不需要在创建转换器对象再进行转换了，通过时间日期对象的parse/format方法可以直接进行转换。

```Java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class JavaTimeDemo05 {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        String s1 = now.format(DateTimeFormatter.ISO_DATE_TIME);
        String s2 = now.format(DateTimeFormatter.ISO_DATE);
        System.out.println(now);
        System.out.println(s1);
        System.out.println(s2);

        LocalDateTime time = LocalDateTime.parse(s1);
        System.out.println(time);
    }
}
```

DateTimeFormatter.ofLocalizedDate()方法的使用

```Java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.time.format.FormatStyle;

public class JavaTimeDemo05 {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        String s1 = now.format(DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL));
        String s2 = now.format(DateTimeFormatter.ofLocalizedDate(FormatStyle.LONG));
        String s3 = now.format(DateTimeFormatter.ofLocalizedDate(FormatStyle.MEDIUM));
        String s4 = now.format(DateTimeFormatter.ofLocalizedDate(FormatStyle.SHORT));
        System.out.println(now);
        System.out.println(s1);
        System.out.println(s2);
        System.out.println(s3);
        System.out.println(s4);
    }
}
```

自定义格式化器

```Java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class JavaTimeDemo05 {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        String s = now.format(DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss:SSS"));
        System.out.println(s);
    }
}
```

练习案例：将1998年3月18日17时19分28秒格式化为以下格式1998-03月-18---17:19分28秒。

```Java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class JavaTimeDemo06 {
    public static void main(String[] args) {
        LocalDateTime time = LocalDateTime.of(1998, 3, 18, 17, 19, 28);
        String s = time.format(DateTimeFormatter.ofPattern("yyyy-MM月-dd---HH:mm分:ss秒"));
        System.out.println(s);
    }
}
```

