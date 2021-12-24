<center>
    <h1>
        JavaSE(基础)
    </h1>
</center>

## 1. JDK的安装及环境变量配置

### 1.1 JRE (Java Runtime Environment)

JRE是Java程序的运行环境，包含JVM和运行时所需要的核心类库。如果我们只是想要运行一个已有的Java程序，那么只需安装JRE即可。

### 1.2 JDK (Java Development Kit)

JDK是Java程序开发工具包，包含JRE和开发人员使用的工具。

其中的开发工具：编译工具(javac.exe)和运行工具(java.exe)。

### 1.3 JDK的下载

JDK需要从Oracle官网下载，这是：[官网地址](https://www.oracle.com)

在官网底部找到What's New中的Java SE Dowanloads，点击它跳转到JDK下载页面。

![Snipaste_2020-10-16_16-23-42](https://gitee.com/mark-clinton/images/raw/master/Snipaste_2020-10-16_16-23-42.png)

然后即可选择自己所需要的JDK版本进行下载(现在官网下载需要注册Oracle账号，登录后下载)。这里是JDK8的具体：[下载地址](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)

### 1.4 JDK的安装

JDK安装只需点击下一步即可。若有需要，可以选择更改安装路径，但路径中最好不要有含有中文。下面是更改安装默认路径的地方：

![Snipaste_2020-10-16_16-53-53](https://gitee.com/mark-clinton/images/raw/master/Snipaste_2020-10-16_16-53-53.png)

### 1.5 环境变量的配置

1. 右击此电脑->属性->高级系统设置->高级->环境变量。

2. 在系统变量下点击新建，在变量名栏写JAVA_HOME，在变量值栏写下JDK安装路径。

   例如：F:\Java\jdk1.8.0_261 (方便此路径引用)

   ![Snipaste_2020-10-16_18-17-47](https://gitee.com/mark-clinton/images/raw/master/Snipaste_2020-10-16_18-17-47.png)

3. 在系统变量下选择Path，点击编辑->新建，添加路径指定到JDK的安装路径的bin文件夹，此时可引用JAVA_HOME。

   路径为：%JAVA_HOME%\BIN

   ![Snipaste_2020-10-16_18-23-31](https://gitee.com/mark-clinton/images/raw/master/Snipaste_2020-10-16_18-23-31.png)

4. 在系统变量下点击新建，在变量名栏写CLASSPATH，在变量值栏添加dt.jar和tools.jar的路径。

   用途：告诉JVM要使用或执行的class放在什么路径上，便于JVM加载class文件，其中.;表示当前路径，tools.jar和dt.jar为类库路径。

   路径为：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar   

   (注意用英文标点符号，不要丢了前面的.;符号)

## 2. 基础语法

### 2.1 注释

**注释概述**：注释是在程序指定位置添加的说明性信息。注释不参与程序运行，仅起到说明作用。

**注释分类**

- 单行注释		格式：//注释信息
- 多行注释        格式：/\*注释信息*/
-  文档注释       格式：/\*\*注释信息*/     

### 2.2 关键字

**关键字概述：**关键字就是Java语言赋予了特定含义的单词。

**关键字特点**

- 关键字的字母全部小写。
- 常用的代码编辑器，针对关键字有特殊的颜色标记，非常直观。

### 2.3 常量

**常量概述：**常量是在程序运行过程中，其值不可以发生改变的量。

**常量分类**

|  常量类型  |               说明               |             举例              |
| :--------: | :------------------------------: | :---------------------------: |
| 字符串常量 |       用双引号括起来的内容       | "Hello World", "你还怕大雨吗" |
|  整数常量  |          不带小数的数字          |           666，-88            |
|  小数常量  |           带小数的数字           |         13.14，-5.20          |
|  字符常量  |       用单引号括起来的内容       |        'A', '0', '我'         |
|  布尔常量  |         布尔值，表示真假         |    只有两个值：true，false    |
|   空常量   | 一个特殊的值，空值，不能直接输出 |          值是：null           |

### 2.4 数据类型

Java语言是强类型语言，对于每一种数据都给出了明确的数据类型，不同的数据类型也分配了不同的内存空间，所以它们表示的数据大小也是不一样的。

![image-20201115160725980](https://gitee.com/mark-clinton/images/raw/master/image-20201115160725980.png)

注：字符串类型是一个类，属于引用数据类型。

**数据类型内存占用和取值范围**

| 关键字  | 数据类型 | 内存占用(字节) |                           取值范围                           |
| :-----: | :------: | :------------: | :----------------------------------------------------------: |
|  byte   |   整数   |       1        |                           -128~127                           |
|  short  |   整数   |       2        |                         -32768~32767                         |
|   int   |   整数   |       4        |                    $-2^{31}\sim 2^{31}-1$                    |
|  long   |   整数   |       8        |                    $-2^{63}\sim 2^{63}-1$                    |
|  float  |  浮点数  |       4        | 负数：-3.402823E+38到-1.401298E-45<br />正数：1.401298E-45到3.402823E+38 |
| double  |  浮点数  |       8        | 负数：-1.797693E+308到-4.9000000E-324<br />正数：4.9000000E-324到1.797693E+308 |
|  char   |   字符   |       2        |                           0-65535                            |
| boolean |   布尔   |       1        |                         true，false                          |

### 2.5 变量

**变量：**在程序运行过程中，其值是可以发生改变的量。从本质上讲，变量是内存中一小块区域。

**变量的定义**

- 格式：数据类型 变量名 = 变量值;
- 范例：int a = 10;

**变量使用注意事项**

- 名字不能重复
- 变量未赋值，不能使用
- long类型的变量定义的时候，为了防止整数过大，后面要加L

### 2.6 标识符

**标识符：**就是给类，方法，变量等起名字的符号。

**标识符定义规则**

- 由数字、字母、下划线(_)和美元符($)组成
- 不能以数字开头
- 不能是关键字
- 区分大小写

**常见命名约定**

小驼峰命名法：方法、变量

- 标识符是一个单词的时候，首字母小写                                                                         范例：name
- 标识符由多个单词组成的时候，第一个单词首字母小写，其他单词首字母大写       范例：firstName

大驼峰命名法：类

- 标识符是一个单词的时候，首字母大写                                                范例：Student
- 标识符由多个单词组成的时候，每个单词的首字母大写                     范例：GoodStudent

### 2.7 类型转换

**类型转换分类**：自动类型转换、强制类型转换

**自动类型转换：**把一个表示数据范围小的数值或者变量赋值给另一个表示数据范围大的变量。

范例：double d = 10;

数据范围从小到大如下：

(byte ---> short), (char) ---> int ---> long ---> float ---> double

**强制类型转换：**把一个表示数据范围大的数值或者变量赋值给另一个表示数据范围小的变量。

- 格式：目标数据类型 变量名 = (目标数据类型)值或者变量;
- 范例：int k = (int)88.88;

## 3. 运算符

**运算符：**对常量或者变量进行操作的符号。

**表达式：**用运算符把常量或者变量连接起来符合Java语法的式子就可以称为表达式。不同运算符连接的表达式体现的是不同类型的表达式。

### 3.1 算术运算符

| 符号 | 作用 |             说明             |
| :--: | :--: | :--------------------------: |
|  +   |  加  |      与基础数学“+”相同       |
|  -   |  减  |      与基础数学“-”相同       |
|  *   |  乘  |      与基础数学“x”相同       |
|  /   |  除  |   与基础数学“÷”相同，取商    |
|  %   | 取余 | 获取的是两个数据做除法的余数 |

注意：/和%的区别在于，两个数据做除法，/取结果的商，%取结果的余数。整数操作只能得到整数，要想得到小数，必须有浮点数参与运算。

**字符的加操作**

是拿字符在计算机底层对应的数值来进行计算的。常用字符代表数字如下(详见ASCII码表):

- 'A' --------> 65                         A-Z是连续的
- 'a' --------> 97                         a-z是连续的
- '0' --------> 48                         0-9是连续的

算数表达式中包含多个基本数据类型的值的时候，整个算术表达式的类型会自动进行提升。提升规则如下：

- byte类型，short类型和char类型将被提升到int类型
- 整个表达式的类型自动提升到表达式中最高等级操作数同样的类型
- 等级顺序：byte,short,char --> int --> long --> float --> double

**字符串的加操作**

- 当 "+" 操作中出现字符串时，这个 "+" 是字符串连接符，而不是算数运算。

- 在 "+" 操作中，如果出现了字符串，就是连接运算符，否则就是算术运算。当连续进行 "+" 操作时，从左到右逐个执行。

### 3.2 赋值运算符

| 符号 |    作用    |         说明          |
| :--: | :--------: | :-------------------: |
|  =   |    赋值    | a=10，将10赋值给变量a |
|  +=  |  加后赋值  |  a+=b，将a+b的值给a   |
|  -=  |  减后赋值  |  a-=b，将a-b的值给a   |
|  *=  |  乘后赋值  |  a\*=b，将axb的值给a  |
|  /=  |  除后赋值  |  a/=b，将a÷b的商给a   |
|  %=  | 取余后赋值 | a%=b，将a÷b的余数给a  |

注意：扩展的赋值运算符隐含了强制类型转换。

### 3.3 自增自减运算符

| 符号 | 作用 |    说明     |
| :--: | :--: | :---------: |
|  ++  | 自增 | 变量的值加1 |
|  --  | 自减 | 变量的值减1 |

注意事项：

- ++ 和 -- 既可以放在变量的后边，也可以放在变量的前边。
- 单独使用的时候，++ 和 -- 无论是放在变量的前边还是后边，结果是一样的。
- 参与操作的时候，如果放在变量的后边，先拿变量参与操作，后拿变量做 ++ 或 -- 。
- 参与操作的时候，如果放在变量的前边，先拿变量做 ++ 或 -- ，后拿变量参与操作。

最常见用法：单独使用。

### 3.4 关系运算符

| 符号 |                          说明                           |
| :--: | :-----------------------------------------------------: |
|  ==  |  a==b，判断a和b的值是否相等，成立为true，不成立为false  |
|  !=  | a!=b，判断a和b的值是否不相等，成立为true，不成立为false |
|  >   |     a>b，判断a是否大于b，成立为true，不成立为false      |
|  >=  |   a>=b，判断a是否大于等于b，成立为true，不成立为false   |
|  <   |     a<b，判断a是否小于b，成立为true，不成立为false      |
|  <=  |   a<=b，判断a是否小于等于b，成立为true，不成立为false   |

注意事项：关系运算符的结果都是boolean类型，要么是true，要么是false。千万不要把"=="误写成"="。

### 3.5 逻辑运算符

在数学中，一个数据x，大于3，小于6，可以这样来进行表示：3<x<6。而在Java中，需要把之前的式子先进行拆解，在进行合并表达。表示为：x>3 && x<6。

&&其实就是一个逻辑运算符。逻辑运算符，就是用来连接关系表达式的运算符。当然，逻辑运算符也可以直接连接布尔类型的常量或者变量。

| 符号 |   作用   |                     说明                     |
| :--: | :------: | :------------------------------------------: |
|  &   |  逻辑与  |  a&b，a和b都是true，结果为true，否则为false  |
|  \|  |  逻辑或  | a\|b，a和b都是false，结果为false，否则为true |
|  ^   | 逻辑异或 |     a^b，a和b结果不同为true，相同为false     |
|  !   |  逻辑非  |          !a，结果和a的结果正好相反           |

**短路逻辑运算符**

| 符号 |  作用  |             说明             |
| :--: | :----: | :--------------------------: |
|  &&  | 短路与 | 作用和&相同，但是有短路效果  |
| \|\| | 短路或 | 作用和\|相同，但是有短路效果 |

注意事项：

- 逻辑与&，无论左边真假，右边都要执行。

  短路与&&，如果左边为真，右边执行；如果左边为假，右边不执行。

- 逻辑或|，无论左边真假，右边都要执行。

  短路或||，如果左边为假，右边执行；如果左边为真，右边不执行。

### 3.6 三元运算符

格式：关系表达式?表达式1:表达式2;

范例：a > b ? a : b;

计算规则：首先计算关系表达式的值。如果为true，表达式1的值就是运算结果；如果为false，表达式2的值就是运算结果。

## 4. 分支语句

**流程控制语句分类**

- 顺序结构
- 分支结构(if,switch)
- 循环结构(for,while,do...while)

### 4.1 顺序结构

顺序结构是程序中最简单最基本的流程控制，没有特定的语法结构，按照代码的先后顺序，依次执行，程序中大多数的代码都是这样执行的。

### 4.2 if语句

if语句格式1：

```java
if(关系表达式){
    语句体;
}
```

执行流程：

1. 首先计算关系表达式的值
2. 如果关系表达式的值为true就执行语句体
3. 如果关系表达式的值为false就不执行语句体
4. 继续执行后面的语句内容

if语句格式2：

```java
if(关系表达式){
    语句体1;
}else{
    语句体2;
}
```

执行流程：

1. 首先计算关系表达式的值
2. 如果关系表达式的值为true就执行语句体1
3. 如果关系表达式的值为false就执行语句体2
4. 继续执行后面的语句内容

if语句格式3：

```java
if(关系表达式1){
    语句体1;
}else if(关系表达式2){
    语句体2;
}
...
else{
    语句体n+1;
}
```

执行流程：

1. 首先计算关系表达式1的值
2. 如果值为true就执行语句体1；如果值为false就计算关系表达式2的值
3. 如果值为true就执行语句体2；如果值为false就计算关系表达式3的值
4. ……
5. 如果没有任何关系表达式为true，就执行语句体n+1

练习：小明快期末考试了，小明爸爸对他说，会根据他不同的考试成绩，送他不同的礼物，假如你可以控制小明的得分，请用程序实现小明到底该获得什么样的礼物，并在控制台输出。

```java
import java.util.Scanner;

public class Demo{
	public static void main(String[] args){
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入一个分数：");
		int score = sc.nextInt();
		
		if(score > 100 || score < 0){
			System.out.println("你输入的分数有误");
		} else if (score >= 95 && score <= 100){
			System.out.println("山地自行车一辆");
		} else if(score >= 90 && score <= 94){
			System.out.println("游乐场玩一次");
		} else if(score >= 80 && score <= 89){
			System.out.println("变形金刚玩具一个");
		} else {
			System.out.println("胖揍一顿");
		}
	}
}
```

### 4.3 switch语句

switch语句格式：

```java
switch(表达式){
    case 值1:
        语句体1;
        break;
    case 值2:
        语句体2;
        break;
    ...
    default:
        语句体n+1;
        [break;]
}
```

格式说明：

1. 表达式：取值为byte、short、int、char，JDK5以后可以是枚举，JDK7以后可以是String。
2. case：后面跟的是要和表达式进行比较的值。
3. break：表示中断，结束的意思，用来结束switch语句。
4. default：表示所有情况都不匹配的时候，就执行该处的内容，和if语句的else相似。

练习：一年有12个月，分属于春夏秋冬4个季节，键盘录入一个月份，请用程序实现判断该月份属于哪个季节，并输出。

- 春：3、4、5
- 夏：6、7、8
- 秋：9、10、11
- 冬：1、2、12

```java
import java.util.Scanner;

public class Demo{
	public static void main(String[] args){
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入一个月份：");
		int month = sc.nextInt();
		
		switch(month) {
			case 1:
			case 2:
			case 12:
				System.out.println("冬季");
				break;
			case 3:
			case 4:
			case 5:
				System.out.println("春季");
				break;
			case 6:
			case 7:
			case 8:
				System.out.println("夏季");
				break;
			case 9:
			case 10:
			case 11:
				System.out.println("秋季");
				break;
			default:
				System.out.println("你输入的月份有误");
		}
	}
}
```

注意：在switch语句中，如果case控制的语句体后面不写break，将出现穿透现象，在不判断下一个case值的情况下，向下运行，直到遇到break，或者整体switch语句结束。

## 5. 循环语句

### 5.1 for循环语句

**循环结构的特征：**重复做某件事情，具有明确的开始和停止标志。

**循环结构的组成**

- 初始化语句：用于表示循环开启时的起始状态，简单说就是循环开始的时候什么样
- 条件判断语句：用于表示循环反复执行的条件，简单说就是判断循环是否能一直执行下去
- 循环体语句：用于表示循环反复执行的内容，简单说就是循环反复执行的事情
- 条件控制语句：用于表示循环执行中每次变化的内容，简单说就是控制循环是否能执行下去

**循环结构对应的用法**

- 初始化语句：这里可以是一条或者多条语句，这些语句可以完成一些初始化操作
- 条件判断语句：这里使用一个结果值为boolean类型的表达式，这个表达式能决定是否执行循环体
- 循环体语句：这里可以是任意语句，这些语句将反复执行
- 条件控制语句：这里通常是使用一条语句来改变变量的值，从而达到控制循环是否继续向下执行的效果，常见i++,i--这样的操作

**for循环语句格式**

```java
for (初始化语句;条件判断语句;条件控制语句) {
    循环体语句;
}
```

执行流程：

1. 执行初始化语句
2. 执行条件判断语句，看其结果是true还是false。如果是false，循环结束；如果是true，继续执行
3. 执行循环体语句
4. 执行条件控制语句
5. 回到2继续执行

练习：在控制台输出所有的水仙花数以及水仙花数的个数。水仙花数是一个三位数，且水仙花数的个位、十位、百位的数字立方和等于原数。

```java
public class Demo{
	public static void main(String[] args){
		int count = 0;
		for(int i = 100; i < 1000; i++) {
			int a = i / 100;
			int b = i / 10 % 10;
			int c = i % 10;
			if (a*a*a + b*b*b + c*c*c == i) {
				System.out.println(i);
				count++;
			}
		}
		System.out.println("水仙花共有：" + count + "个");
	}
}
```

### 5.2 while循环语句

**while循环语句基本格式**

```java
while(条件判断语句) {
    循环体语句;
}
```

**while循环语句完整格式**

```java
初始化语句;
while(条件判断语句) {
    循环体语句;
    条件控制语句;
}
```

执行流程：

1. 执行初始化语句
2. 执行条件判断语句，看其结果是true还是false。如果是false，循环结束；如果是true，继续执行
3. 执行循环体语句
4. 执行条件控制语句
5. 回到2继续执行

练习：世界最高山峰是珠穆朗玛峰(8844.43米=8844430毫米)，假如我有一张足够大的纸，它的厚度是0.1毫米。请问，我折叠多少次，可以折成珠穆朗玛峰的高度？

```java
public class Demo{
	public static void main(String[] args){
		int count =0;
		double paper = 0.1;
		int zf = 8844430;
		while(paper <= zf) {
			paper *= 2;
			count ++;
		}
		System.out.println("需要折叠：" + count + "次");
	}
}
```

### 5.3 do...while循环语句

**基本格式**

```java
do {
    循环体语句;
}while(条件判断语句);
```

**完整格式**

```java
初始化语句;
do {
    循环体语句;
    条件控制语句;
}while(条件判断语句);
```

执行流程：

1. 执行初始化语句
2. 执行循环体语句
3. 执行条件控制语句
4. 执行条件判断语句，看其结果是true还是false。如果是false，循环结束；如果是true，继续执行
5. 回到2继续执行

**三种循环的区别**

- for循环和while循环先判断条件是否成立，然后决定是否执行循环体(先判断后执行)
- do...while循环先执行一次循环体，然后判断条件是否成立，是否继续执行循环体(先执行后判断)
- 条件控制语句所控制的自增变量，因为归属for循环的语法结构中，在for循环结束后，就不能再次被访问到了
- 条件控制语句所控制的自增变量，对于while循环来说不归属其语法结构中，在while循环结束后，该变量还可以继续使用

### 5.4 跳转控制语句

**跳转控制语句**

- continue   用在循环中，基于条件控制，跳过某次循环体内容的执行，继续下一次的执行
- break         用在循环中，基于条件控制，终止循环体内容的执行，也就是说结束当前的整个循环

### 5.5 循环嵌套

**语句结构**

- 顺序语句      以分号结尾，表示一句话的结束

- 分支语句      一对大括号表示if的整体结构，整体描述一个完整的if语句                                                                                                                                                                                    

  ​                     一对大括号表示switch的整体结构，整体描述一个完整的switch语句

- 循环语句     一对大括号表示for的整体结构，整体描述一个完整的for语句

  ​                    一对大括号表示while的整体结构，整体描述一个完整的while语句

  ​                     do...while以分号结尾，整体描述一个完整的do...while语句

任何语句对外都可以看成是一句话，一句代码

分支语句中包含分支语句称为分支嵌套

循环语句中包含循环语句称为循环嵌套

### 5.6 Random

**作用：**用于产生一个随机数。

练习：猜数字小游戏，程序自动生成一个1-100之间的数字，使用程序实现猜出这个数字是多少？当猜错时需给出对应的提示，提示你猜的数字是比真实数字大还是小，猜中时会提示猜中了。

```java
import java.util.Random;
import java.util.Scanner;

public class Demo{
	public static void main(String[] args){
		Random r = new Random();
		int number = r.nextInt(100) + 1;
		
		Scanner sc = new Scanner(System.in);
		System.out.println("请输入你要猜的数字");
		int guessNumber = sc.nextInt();
		
		while(true) {
			if(guessNumber == number) {
				System.out.println("恭喜你，猜中啦！");
				break;
			} else if(guessNumber > number) {
				System.out.println("你猜的数字" + guessNumber + "大了，请重新输入：");
				guessNumber = sc.nextInt();
			} else {
				System.out.println("你猜的数字" + guessNumber + "小了，请重新输入：");
				guessNumber = sc.nextInt();
			}
		}
	}
}
```

## 6. 数组

### 6.1 数组定义与初始化

**数组概述：**数组(array)是一种用于存储多个相同类型数据的存储类型。一次性声明大量的用于存储数据的变量。要存储的数据通常是同类型的数据，例如：考试成绩。

**定义格式**

- 格式一：数据类型[]  变量名                                范例：int[]  arr
- 定义了一个int类型的数组，数组名是arr
- 格式二：数据类型  变量名[]                                范例：int  arr[]
- 定义了一个int类型的变量，变量名是arr数组

**数组初始化概述：**Java中的数组必须先初始化，然后才能使用。初始化就是为数组中的数组元素分配内存空间，并为每个数组元素赋值。

**数组初始化方式：**有动态初始化和静态初始化。

**动态初始化**

动态初始化：初始化时只指定数组长度，由系统为数组分配初始值。

- 格式：数据类型[] 变量名 = new 数据类型[数组长度];
- 范例：int[] arr = new int[3];

**静态初始化**

静态初始化：初始化时由程序员自己为数组对象的每个元素赋值，由系统自动计算出数组的长度。

- 格式：数据类型[] 变量名 = new 数据类型[]{数据1，数据2，数据3...};
- 范例：String[] s = new String[]{"Hello","World","Java"};
- 简化格式：数据类型[] 变量名 = {数据1，数据2，数据3...};
- 范例：String[] s = {"Hello","World","Java"};

### 6.2 数组元素访问

**数组变量访问方式(格式)：**数组名

**数组内部保存的数据的访问方式(格式)：**数组名[索引]

**索引：**索引是数组中数据的编号方式。索引用于访问数组中的数据使用，数组名[索引]等同于变量名，是一种特殊的变量名。

- 索引从0开始
- 索引是连续的
- 索引逐一增加，每次加1

### 6.3 内存分配

Java程序在运行时，需要在内存中分配空间。为了提高运算效率，就对空间进行了不同区域的划分，因为每一片区域都有特定的处理数据方式和内存管理方式。

**Java中内存分配**

- 栈内存：存储局部变量，即定义在方法中的变量，例如：arr。使用完毕，立即消失。
- 堆内存：存储new出来的内容(实体，对象)。每一个new出来的东西都有一个地址值，使用完毕，会在垃圾回收器空闲时被回收。

数组在初始化时，会为存储空间添加默认值

- 整数：默认值0
- 浮点数：默认值0.0
- 布尔值：默认值false
- 字符：默认值是空字符
- 引用数据类型：默认值是null

### 6.4 数组操作的两个常见小问题

索引越界：访问了数组中不存在的索引对应的元素，造成索引越界问题。

空指针异常：访问的数组已经不再指向堆内存的数据，造成空指针异常。

null：空值，引用数据类型的默认值，表示不指向任何有效对象。

### 6.5 数组常见操作

**遍历**

获取数组元素数量(格式)：数组名.length。

范例：arr.length

数组遍历的通用格式

```java
int[] arr = {...};

for(int i=0;i<arr.length;i++){
    System.out.println(arr[i]);
}
```

**获取最值**

```java
public class ArrayDemo {
    public static void main(String[] args) {
        int[] arr = {12,45,98,73,60};

        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if(arr[i] > max){
                max = arr[i];
            }
        }
        System.out.println("max:" + max);
    }
}
```

## 7. 方法

### 7.1 方法的基本概念

**方法：**方法(method)是将具有独立功能的代码块组织成为一个整体，使其具有特殊功能的代码集。

- 方法必须先创建才可以使用，该过程称为方法定义
- 方法创建后并不是直接运行的，需要手动使用后才执行，该过程称为方法调用。

**方法的定义**

```java
//方法定义格式
public static void 方法名(){
    //方法体
}
```

**方法调用**

```java
//调用格式
方法名();
```

注意：方法必须先定义后调用，否则程序将报错。

练习：设计一个方法用于打印两个数中的较大数。

```java
public class MethodDemo {
    public static void main(String[] args) {
        getMax(10,20);
    }

    public static void getMax(int a,int b){
        int max = a > b ? a : b;
        System.out.println("max:" + max);
    }
}
```

**带参数方法的定义**

```java
//基本格式
public static void 方法名(参数){......}

//单个参数
public static void 方法名(数据类型 变量名){......}

//多个参数
public static void 方法名(数据类型 变量名1, 数据类型 变量名2, ...){......}
```

注意：

- 方法定义时，参数中的数据类型与变量名都不能缺少，缺少任意一个程序将报错
- 方法定义时，多个参数之间使用逗号(,)分隔

**带参数方法的调用**

```java
//基本格式
方法名(参数);

//单个参数
方法名(变量名/常量值);

//多个参数
方法名(变量名1/常量值1, 变量名2/常量值2, ...);
```

注意：方法调用时，参数的数量与类型必须与方法定义中的设置相匹配，否则程序将报错。

**形参和实参**

形参：方法定义中的参数，等同于变量定义。

实参：方法调用中的参数，等同于使用变量或常量。

**带返回值方法定义**

```java
//格式
public static 数据类型 方法名(参数){
    return 数据;
}

//范例
public static boolean isEvenNumber(int number){
    return true;
}
```

带返回值方法调用

```java
//格式1
方法名(参数);

//格式2
数据类型 变量名 = 方法名(参数);
```

注意：方法的返回值通常会使用变量接收，否则该返回值将无意义。

练习：设计一个方法可以获取两个数的较大值，数据来源于参数。

```java
public class MethodDemo {
    public static void main(String[] args) {
        int max = getMax(10,20);
        System.out.println("max:" + max);
        System.out.println(getMax(10,20));
    }

    public static int getMax(int a,int b){
        int max = a > b ? a : b;
        return max;
    }
}
```

**方法注意事项**

- 方法不能嵌套定义
- void表示无返回值，可以省略return，也可以单独的书写return，后面不加数据

**方法的通用格式**

```java
//通用格式
public static 返回值类型 方法名(参数){
    方法体;
    return 数据;
}
```

- public static：修饰符，目前记住这个格式

- 返回值类型：方法操作完毕之后返回的数据的数据类型

  ​                       如果方法操作完毕，没有数据返回，这里写void，而且方法体中一般不写return

- 方法名：调用方法时使用的标识

- 参数：由数据类型和变量名组成，多个参数之间用逗号隔开

- 方法体：完成功能的代码块

- return：如果方法操作完毕，有数据返回，用于把数据返回给调用者

定义方法时，要做到两个明确

- 明确返回值类型：主要是明确方法操作完毕之后是否有数据返回，如果没有，写void；如果有，写对应的数据类型
- 明确参数：主要是明确参数的类型和数量

调用方法时

- void类型的方法，直接调用即可
- 非void类型的方法，推荐用变量接收调用

### 7.2 方法的重载

**方法重载概述**

方法重载指同一个类中定义的多个方法之间的关系，满足下列条件的多个方法相互构成重载。

- 多个方法在同一个类中
- 多个方法具有相同的方法名
- 多个方法的参数不相同，类型不同或者数量不同

**方法重载特点**

- 重载仅对应方法的定义，与方法的定义无关，调用方式参照标准格式
- 重载仅针对同一个类中方法的名称与参数进行识别，与返回值无关，换句话说，不能通过返回值来判定两个方法是否构成重载

练习：使用方法重载的思想，设计比较两个整数是否相同的方法，兼容全整数类型(byte,short,int,long)。

```java
public class MethodDemo {
    public static void main(String[] args) {
        System.out.println(compare(10,20));
        System.out.println(compare((byte)10,(byte)20));
        System.out.println(compare((short)10,(short)20));
        System.out.println(compare(10L,20L));
    }

    public static boolean compare(int a, int b){
        System.out.println("int");
        return a == b;
    }

    public static boolean compare(long a, long b){
        System.out.println("long");
        return a == b;
    }

    public static boolean compare(byte a, byte b){
        System.out.println("byte");
        return a == b;
    }

    public static boolean compare(short a, short b){
        System.out.println("short");
        return a == b;
    }
}
```

### 7.3 方法的参数传递

对于基本数据类型的参数，形式参数的改变，不影响实际参数的值。

```java
public class MethodDemo {
    public static void main(String[] args) {
        int number = 100;
        System.out.println("调用change方法前：" + number);
        change(number);
        System.out.println("调用change方法后：" + number);
    }

    public static void change(int number){
        number = 200;
    }
}
-------------------------------------------------------------------------------------
//输出
调用change方法前：100
调用change方法后：100
```

**方法参数传递(引用类型)**

对于引用类型的参数，形式参数的改变，影响实际参数的值。

```java
public class MethodDemo {
    public static void main(String[] args) {
        int[] arr = {10,20,30};
        System.out.println("调用change方法前：" + arr[1]);
        change(arr);
        System.out.println("调用change方法后：" + arr[1]);
    }

    public static void change(int[] arr){
        arr[1] = 200;
    }
}
-------------------------------------------------------------------------------------
//输出
调用change方法前：20
调用change方法后：200
```

练习1：设计一个方法用于数组遍历，要求便利的结果是在一行上的。例如：[11,22,33,44,55]。

```java
public class MethodDemo {
    public static void main(String[] args) {
        int[] arr = {11,22,33,44,55};
        printArray(arr);
    }

    public static void printArray(int[] arr){
        System.out.print("[");
        for (int i = 0; i < arr.length; i++) {
            if(i == arr.length - 1){
                System.out.print(arr[i]);
            } else {
                System.out.print(arr[i] + ",");
            }
        }
        System.out.println("]");
    }
}
```

练习2：设计一个方法用于获取数组中元素的最大值，调用方法并输出结果。

```java
public class MethodDemo {
    public static void main(String[] args) {
        int[] arr = {12,45,98,73,60};
        int number = getMax(arr);
        System.out.println("number:" + number);
    }

    public static int getMax(int[] arr){
        int max = arr[0];
        for (int i = 0; i < arr.length; i++) {
            if(arr[i] > max){
                max = arr[i];
            }
        }
        return max;
    }
}
```

## 8. Debug

**Debug：**是供程序员使用的程序调试工具，它可以用于查看程序的执行流程，也可以用于追踪程序执行过程来调试程序。

**Debug操作流程**

Debug调试，又被称为断点调试，断点其实就是一个标记，告诉我们从哪里开始查看。

1. 如何加断点：选择要设置断点的代码行，在行号的区域后面单击鼠标左键即可。
2. 如何运行加了断点的程序：在代码区域右键Debug执行。
3. 看哪里：看Debug窗口，看Console窗口。
4. 点哪里：点Step Into(F7)这个箭头，也可以直接按F7，执行完后点Stop结束。
5. 如何删除断点：选择要删除的断点，单击鼠标左键即可。

注意事项：如果数据来自于键盘输入，一定要记住输入数据，不然就不能继续往下查看了。

练习：在编程竞赛中，有6个评委为参赛的选手打分，分数为0-100的整数分。选手的最后得分为：去掉一个最高分和一个最低分后的4个评委的平均值(不考虑小数部分)。

```java
import java.util.Scanner;

public class MethodDemo {
    public static void main(String[] args) {
        int[] arr = new int[6];
        Scanner sc = new Scanner(System.in);

        for (int i = 0; i < arr.length; i++) {
            System.out.println("请输入第" + (i + 1) + "个评委的打分：");
            arr[i] = sc.nextInt();
        }

        int max = getMax(arr);
        int min = getMin(arr);
        int sum = getSum(arr);
        int avg = (sum - max - min) / (arr.length - 2);
        System.out.println("选手的最终得分是：" + avg);
    }

    public static int getSum(int[] arr) {
        int sum = 0;
        for (int i = 0; i < arr.length; i++) {
            sum += arr[i];
        }
        return sum;
    }

    public static int getMin(int[] arr) {
        int min = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] < min) {
                min = arr[i];
            }
        }
        return min;
    }

    public static int getMax(int[] arr) {
        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }
        return max;
    }

    public static void printArray(int[] arr){
        System.out.print("[");
        for (int i = 0; i < arr.length; i++) {
            if (i == arr.length - 1) {
                System.out.print(arr[i]);
            } else {
                System.out.print(arr[i] + ",");
            }
        }
        System.out.println("]");
    }
}
```

## 9. 面向对象基础

### 9.1 类和对象

**对象：**万物皆对象，客观存在的事物皆为对象。是能够看得到摸得着的真实存在的实体。

**类：**类是对现实生活中一类具有共同属性和行为的事物的抽象。

**类的特点**

- 类是对象的数据类型
- 类是具有相同属性和行为的一组对象的集合

**对象的属性：**对象具有的各种特征，每个对象的每个属性都拥有特定的值。

**对象的行为：**对象能够执行的操作。

**类和对象的关系：**类是对象的抽象，对象是类的实体。

**类的定义**

类的重要性：是Java程序的基本组成单位。

类：是对现实生活中一类具有共同属性和行为的事物的抽象，确定对象将会拥有的属性和行为。

类的组成：属性和行为。

- 属性：在类中通过成员变量来实现(类中方法外的变量)
- 行为：在类中通过成员方法来体现(去掉static关键字的方法)

类的定义

```java
public class 类名 {
    //成员变量
    变量1的数据类型 变量1;
    变量2的数据类型 变量2;
    ...
    //成员方法
    方法1;
    方法2;
    ...
}
```

范例

```java
public class Phone {
    //成员变量
    String brand;
    int price;

    //成员方法
    public void call() {
        System.out.println("打电话");
    }

    public void sendMessage() {
        System.out.println("发短信");
    }
}
```

**对象的使用**

创建对象

- 格式：类名 对象名 = new 类名();
- 范例：Phone p = new Phone();

使用对象

1. 使用成员变量
   - 格式：对象名.变量名
   - 范例：p.brand

2. 使用成员方法
   - 格式：对象名.方法名()
   - 范例：p.call()

### 9.2 成员变量和局部变量

**成员变量：**类中方法外的变量。

**局部变量：**方法中的变量。

**成员变量和局部变量的区别**

|      区别      |                     成员变量                     |                       局部变量                       |
| :------------: | :----------------------------------------------: | :--------------------------------------------------: |
|  类中位置不同  |                    类中方法外                    |                  方法内或方法声明上                  |
| 内存中位置不同 |                      堆内存                      |                        栈内存                        |
|  生命周期不同  | 随着对象的存在而存在，随着对象的<br />消失而消失 | 随着方法的调用而存在，随着方法的调<br />用完毕而消失 |
|   初始化不同   |                 有默认的初始化值                 | 没有默认的初始化值，必须先定义，赋<br />值，才能使用 |

### 9.3 封装

**private关键字**

- 是一个权限修饰符
- 可以修饰成员(成员变量和成员方法)
- 作用是保护成员不被别的类使用，被private修饰的成员只在本类中才能使用

针对private修饰的成员变量，如果需要被其他类使用，提供相应的操作

- 提供"get变量名()"方法，用于获取成员变量的值，方法用public修饰
- 提供"set变量名(参数)"方法，用于设置成员变量的值，方法用public修饰

**this关键字**

1. this修饰的变量用于指代成员变量
   - 方法的形参如果与成员变量同名，不带this修饰的变量指的是形参，而不是成员变量
   - 方法的形参没有与成员变量同名，不带this修饰的变量指的是成员变量

2. 什么时候使用this：解决局部变量隐藏成员变量
3. this：代表所在类的对象的引用
   - 记住：方法被哪个对象调用，this就代表哪个对象

**封装概述**

- 是面向对象三大特征之一(封装，继承，多态)
- 是面向对象编程语言对客观世界的模拟，客观世界里成员变量都是隐藏在对象内部的，外界无法直接操作的

**封装原则**

将类的某些信息隐藏在类内部，不允许外部程序直接访问，而是通过该类提供的方法来实现对隐藏信息的操作和访问成员变量private，提供对应的getXxx()/setXxx()方法

**封装好处**

- 通过方法来控制成员变量的操作，提高了代码的安全性
- 把代码用方法进行封装，提高了代码的复用性

### 9.4 构造方法

**构造方法概述**：构造方法是一种特殊的方法。

作用：创建对象。

```java
//格式
public class 类名 {
    修饰符 类名(参数) {
        
    }
}
```

**构造方法的注意事项**

1. 构造方法的创建
   - 如果没有定义构造方法，系统将给出一个默认的无参构造方法
   - 如果定义了构造方法，系统将不再提供默认的构造方法

2. 构造方法的重载
   - 如果定义了带参构造方法，还要使用无参构造方法，就必须再写一个无参数构造方法

3. 推荐的使用方式
   - 无论是否使用，都手工书写无参数构造方法

**标准类制作**

1. 成员变量
   - 使用private修饰

2. 构造方法
   - 提供一个无参构造方法
   - 提供一个带多个参数的构造方法

3. 成员方法
   - 提供每一个成员变量对应的setXxx()/getXxx()
   - 提供一个显示对象信息的show()

4. 创建对象并为其成员变量赋值的两种方式
   - 无参构造方法创建对象后使用setXxx()赋值
   - 使用带参构造方法直接创建带有属性值的对象

类的案例

```java
public class Student {
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }

    public void show() {
        System.out.println(name + "," + age);
    }

}
```

## 10. 字符串

### 10.1 API

**API(Application Programming Interface)：**应用程序编程接口。

**Java API：**指的是JDK中提供的各种功能的Java类。这些类将底层的实现封装了起来，我们不需要关心这些类是如何实现的，只需要学习这些类如何使用即可，可以通过帮助文档来学习这些API如何使用。

注意：调用方法的时候，如果方法有明确的返回值，我们用变量接收。可以手动完成，也可以使用快捷键的方式完成(Ctrl + Alt + V)。

### 10.2 String

**String概述**

String类在java.lang包下，所以使用的时候不需要导包。

String类代表字符串，Java程序中的所有字符串文字(例如 "abc")都被实现为此类的实例，也就是说，Java程序中所有的双引号字符串，都是String类的对象。

**字符串特点**

- 字符串不可变，它们的值在创建后不能被更改
- 虽然String的值是不可变的，但是它们可以被共享
- 字符串效果上相当于字符数组(char[])，但是底层原理是字节数组(byte[])

**String常用构造方法**

|          方法名           |                   说明                    |
| :-----------------------: | :---------------------------------------: |
|      public String()      |  创建一个空白字符串对象，不含有任何内容   |
| public String(char[] chs) |   根据字符数组的内容，来创建字符串对象    |
| public String(byte[] bys) |   根据字节数组的内容，来创建字符串对象    |
|     String s = "abc";     | 直接赋值的方式创建字符串对象，内容就是abc |

**String对象的特点**

1. 通过new创建的字符串对象，每一个new都会申请一个内存空间，虽然内容相同，但是地址值不同。
2. 以 "" 方式给出的字符串，只要字符序列相同(顺序和大小)，无论在程序代码中出现几次，JVM都只会建立一个String对象，并在字符串池中维护。

**字符串的比较**

使用 == 做比较

- 基本类型：比较的是数据值是否相同
- 引用类型：比较的是地址值是否相同

字符串是对象，它比较内容是否相同，是通过一个方法来实现的，这个方法叫：equals()

- public boolean equals(Object anObject)：将此字符串与指定对象进行比较。由于我们比较的是字符串对象，所以参数直接传递一个字符串

练习：已知用户名和密码，请用程序实现模拟用户登录。总共给三次机会，登录之后，给出相应的提示。

```java
import java.util.Scanner;

public class StringTest {
    public static void main(String[] args) {
        String username = "Mark";
        String password = "it123";

        for (int i = 0; i < 3; i++) {
            Scanner sc = new Scanner(System.in);
            System.out.println("请输入用户名：");
            String name = sc.nextLine();
            System.out.println("请输入密码：");
            String pwd = sc.nextLine();

            if (name.equals(username) && pwd.equals(password)) {
                System.out.println("登陆成功");
                break;
            } else {
                if (i - 2 == 0) {
                    System.out.println("你的账户被锁定，请与管理员联系");
                } else {
                    System.out.println("登录失败，你还有" + (2 - i) + "次机会");
                }
            }
        }
    }
}
```

练习：键盘录入一个字符串，使用程序实现在控制台遍历该字符串。

```java
import java.util.Scanner;

public class StringTest {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个字符串：");
        String s = sc.nextLine();
        for (int i = 0; i < s.length(); i++) {
            System.out.println(s.charAt(i));
        }
    }
}
```

练习：定义一个方法，把int数组中的数据按指定的格式拼接成一个字符串返回，调用该方法，并在控制台输出结果。例如，数组为int[] arr = {1,2,3};，执行方法后的输出结果为：[1,2,3]。

```java
public class StringTest {
    public static void main(String[] args) {
        int[] arr = {1,2,3};
        String s = arrayToString(arr);
        System.out.println(s);
    }

    public static String arrayToString(int[] arr) {
        String s = "";
        s += "[";
        for (int i = 0; i < arr.length; i++) {
            if (i == arr.length - 1) {
                s += arr[i];
            } else {
                s += arr[i] + ",";
            }
        }
        s += "]";
        return s;
    }
}
```

练习：定义一个方法，实现字符串反转。键盘录入一个字符串，调用该方法后，在控制台输出结果。例如，键盘录入abc，输出结果cba。

```java
import java.util.Scanner;

public class StringTest {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个字符串：");
        String s = sc.nextLine();
        String result = reverse(s);
        System.out.println(result);
    }

    public static String reverse(String s) {
        String result = "";
        for (int i = s.length() - 1; i >=0 ; i--) {
            result += s.charAt(i);
        }
        return result;
    }
}
```

### 10.3 StringBuilder

**StringBuilder概述**

如果对字符串进行拼接操作，每次拼接，都会构建一个新的String对象，既耗时，又浪费空间，而这种操作还不可避免。这时，我们可以通过Java提供的StringBuilder类来解决这个问题。

StringBuilder是一个可变的字符串类，我们可以把它看成是一个容器。这里的可变指的是StringBuilder对象中的类容是可变的。

**String和StringBuilder的区别**

- String：内容是不可变的
- StringBuilder：内容是可变的

**StringBuilder构造方法**

|              方法名              |                    说明                    |
| :------------------------------: | :----------------------------------------: |
|      public StringBuilder()      | 创建一个空白可变字符串对象，不含有任何内容 |
| public StringBuilder(String str) |   根据字符串的内容，来创建可变字符串对象   |

**StringBuilder的添加和反转方法**

|                方法名                 |           说明           |
| :-----------------------------------: | :----------------------: |
| public StringBuilder append(任意类型) | 添加数据，并返回对象本身 |
|    public StringBuilder reverse()     |    返回相反的字符序列    |

**StringBuilder和String相互转换**

- public String toString()：通过toString()就可以实现把StringBuilder转换为String
- public StringBuider(String s)：通过构造方法就可以实现把String转换为StringBuilder

练习：利用StringBuilder实现前面的字符串反转功能。

```java
import java.util.Scanner;

public class StringBuilderDemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个字符串：");
        String s = sc.nextLine();
        String result = myReverse(s);
        System.out.println(result);
    }

    public static String myReverse(String s) {
        return new StringBuilder(s).reverse().toString();
    }
}
```

## 11. 集合基础

**集合概述：**编程的时候如果要存储多个数据，使用长度固定的数组存储格式，不一定满足我们的需求，更适应不了变化的需求。这时，我们可以选择使用集合。

**集合类的特点：**提供一种存储空间可变的存储模型，存储的数据容量可以发生改变。

**集合类体系结构**

- 集合：集合包括单列的Collection和双列的Map
- Collection：可重复的List，不可重复的Set
- Map：HashMap等
- List：ArrayList、LinkedList等
- Set：HashSet、TreeSet等

**注意：**其中Collection、Map、List、Set表示接口，其它表示实现类。

### 11.1 Collection

**Collection集合概述和使用**

Collection集合概述

- 是单列集合的顶层接口，它表示一组对象，这些对象也称为Collection的元素
- JDK不提供此接口的任何直接实现，它提供更具体的子接口(如Set和List)实现

创建Collection集合的对象

- 多态的方式
- 具体的实现类ArrayList

**Collection集合常用方法**

|           方法名           |                说明                |
| :------------------------: | :--------------------------------: |
|      boolean add(E e)      |              添加元素              |
|  boolean remove(Object o)  |       从集合中移除指定的元素       |
|        void clear()        |          清空集合中的元素          |
| boolean contains(Object o) |    判断集合中是否存在指定的元素    |
|     boolean isEmpty()      |          判断集合是否为空          |
|         int size()         | 集合的长度，也就是集合中元素的个数 |

**Collection集合的遍历**

Iterator：迭代器，集合的专用遍历方式

- Iterator<E> iterator()：返回此集合中元素的迭代器，通过集合的iterator()方法得到
- 迭代器是通过集合的iterator()方法得到的，所以我们说它是依赖于集合而存在的

Iterator中的常用方法

- E next()：返回迭代中的下一个元素
- boolean hasNext()：如果迭代具有更多元素，则返回True

### 11.2 List

**List集合概述和特点**

List集合概述

- 有序集合(也称为序列)，用户可以精确控制列表中每个元素的插入位置。用户可以通过整数索引访问元素，并搜索列表中的元素
- 与Set集合不同，列表通常允许重复的元素

List集合特点

- 有序：存储和取出的元素顺序一致
- 可重复：存储的元素可以重复

**List集合特有方法**

|            方法名             |                  说明                  |
| :---------------------------: | :------------------------------------: |
| void add(int index,E element) |   在此集合中的指定位置插入指定的元素   |
|      E remove(int index)      | 删除指定索引处的元素，返回被删除的元素 |
|  E set(int index,E element)   | 修改指定索引处的元素，返回被修改的元素 |
|       E get(int index)        |          返回指定索引处的元素          |

**并发修改异常**

- ConcurrentModificationException

产生原因：迭代器遍历的过程中，通过集合对象修改了集合中元素的长度，造成了迭代器获取元素中判断预期修改值和实际修改值不一致。

解决方案：用for循环遍历，然后用集合对象做相应的操作即可。

**ListIterator**

ListIterator：列表迭代器

- 通过List集合的listIterator()方法得到，所以说它是List集合特有的迭代器
- 用于允许程序员沿任一方向遍历列表的列表迭代器，在迭代期间修改列表，并获取列表中迭代器的当前位置

ListIterator中的常用方法

- E next()：返回迭代中的下一个元素
- boolean hasNext()：如果迭代具有更多元素，则返回True
- E previous()：返回列表中的上一个元素
- boolean hasPrevious()：如果此列表迭代器在相反方向遍历列表时具有更多元素，则返回True
- void add(E e)：将指定的元素插入列表

**增强for循环**

增强for：简化数组和Collection集合的遍历

- 实现Iterable接口的类允许对象成为增强型for语句的目标
- 它是JDK5之后出现的，其内部原理是一个Iterator迭代器

增强for的格式

```Java
for(元素数据类型 变量名:数组或者Collection集合){
    //在此处使用变量即可，该变量就是元素
}
```

**List集合子类特点**

List集合常用子类：ArrayList，LinkedList

- ArrayList：底层数据结构是数组，查询快，增删慢
- LinkedList：底层数据结构是链表，查询慢，增删快

**LinkedList集合的特有功能**

|          方法名           | 说明                             |
| :-----------------------: | -------------------------------- |
| public void addFirst(E e) | 在该列表开头插入指定的元素       |
| public void addLast(E e)  | 将指定的元素追加到此列表的末尾   |
|    public E getFirst()    | 返回此列表中的第一个元素         |
|    public E getLast()     | 返回此列表中的最后一个元素       |
|  public E removeFirst()   | 从此列表中删除并返回第一个元素   |
|   public E removeLast()   | 从此列表中删除并返回最后一个元素 |

**常用集合ArrayList**

**ArrayList\<E>:**

- 可调整大小的数组实现。
- \<E>：是一种特殊的数据类型，泛型。在出现E的地方使用引用数据类型替换即可。

**ArrayList构造方法和添加方法**

|                方法名                |                说明                |
| :----------------------------------: | :--------------------------------: |
|          public ArrayList()          |        创建一个空的集合对象        |
|       public boolean add(E e)        |   将指定的元素追加到此集合的末尾   |
| public void add(int index,E element) | 在此集合中的指定位置插入指定的元素 |

**ArrayList集合的常用方法**

|              方法名               |                  说明                  |
| :-------------------------------: | :------------------------------------: |
|  public boolean remove(Object o)  |    删除指定的元素，返回删除是否成功    |
|    public E remove(int index)     | 删除指定索引处的元素，返回被删除的元素 |
| public E set(int index,E element) | 修改指定索引处的元素，返回被修改的元素 |
|      public E get(int index)      |          返回指定索引处的元素          |
|         public int size()         |         返回集合中的元素的个数         |

练习：创建一个存储字符串的集合，存储3个字符串元素，使用程序实现在控制台遍历该集合。

```java
import java.util.ArrayList;

public class ArrayListDemo {
    public static void main(String[] args) {
        ArrayList<String> array = new ArrayList<>();
        array.add("Hello");
        array.add("World");
        array.add("Java");
        for (int i = 0; i < array.size(); i++) {
            System.out.println(array.get(i));
        }
    }
}
```

练习：实现一个简单的终端学生管理系统，要求具有简单的增删改查功能。

学生类(Student.java)

```java
public class Student {
    //学号
    private String sid;
    //姓名
    private String name;
    //年龄
    private String age;
    //居住地
    private String address;

    public Student() {
    }

    public Student(String sid, String name, String age, String address) {
        this.sid = sid;
        this.name = name;
        this.age = age;
        this.address = address;
    }

    public String getSid() {
        return sid;
    }

    public void setSid(String sid) {
        this.sid = sid;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAge() {
        return age;
    }

    public void setAge(String age) {
        this.age = age;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }
}
```

学生管理类(StudentManager.java)

```java
import java.util.ArrayList;
import java.util.Scanner;

public class StudentManager {
    public static void main(String[] args) {
        //创建集合对象，用于存储学生数据
        ArrayList<Student> array = new ArrayList<>();
        //用循环完成再次回到主界面
        while (true) {
            //用输出语句编写主菜单
            System.out.println("----------欢迎来到学生管理系统----------");
            System.out.println("1 添加学生");
            System.out.println("2 删除学生");
            System.out.println("3 修改学生");
            System.out.println("4 查看所有学生");
            System.out.println("5 退出");
            System.out.println("请输入你的选择:");

            //用Scanner实现键盘录入数据
            Scanner sc = new Scanner(System.in);
            String line = sc.nextLine();

            //用switch语句完成操作的选择
            switch (line) {
                case "1":
                    addStudent(array);
                    break;
                case "2":
                    deleteStudent(array);
                    break;
                case "3":
                    updateStudent(array);
                    break;
                case "4":
                    findAllStudent(array);
                    break;
                case "5":
                    System.out.println("谢谢使用");
                    System.exit(0); //JVM退出
            }
        }
    }

    public static void addStudent(ArrayList<Student> array) {
        Scanner sc = new Scanner(System.in);
        String sid;
        Student s = new Student();
        while (true) {
            System.out.println("请输入学生学号:");
            sid = sc.nextLine();
            boolean flag = isUsed(array,sid);
            if (flag) {
                System.out.println("你输入的学号已经被使用，请重新输入:");
            } else {
                break;
            }
        }
        s.setSid(sid);
        System.out.println("请输入学生姓名:");
        String name = sc.nextLine();
        s.setName(name);
        System.out.println("请输入学生年龄:");
        String age = sc.nextLine();
        s.setAge(age);
        System.out.println("请输入学生地址:");
        String address = sc.nextLine();
        s.setAddress(address);
        array.add(s);
        System.out.println("添加学生成功！");
    }

    public static boolean isUsed(ArrayList<Student> array, String sid) {
        boolean flag = false;
        for (int i = 0; i < array.size(); i++) {
            Student s = array.get(i);
            if (s.getSid().equals(sid)) {
                flag = true;
                break;
            }
        }
        return flag;
    }

    public static void findAllStudent(ArrayList<Student> array) {
        if (array.size() == 0) {
            System.out.println("无信息，请先添加信息再查询！");
        } else {
            System.out.println("学号\t\t\t姓名\t\t年龄\t\t居住地");
            for (int i = 0; i < array.size(); i++) {
                Student s = array.get(i);
                System.out.println(s.getSid() + "\t" + s.getName() + "\t" + s.getAge() + "岁\t" + s.getAddress());
            }
        }
    }

    public static void deleteStudent(ArrayList<Student> array) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入你要删除的学生的学号:");
        String sid = sc.nextLine();
        int index = -1;
        for (int i = 0; i < array.size(); i++) {
            Student s = array.get(i);
            if (s.getSid().equals(sid)) {
                index = i;
                break;
            }
        }
        if (index == -1) {
            System.out.println("该信息不存在，请重新输入");
        } else {
            array.remove(index);
            System.out.println("删除学生成功！");
        }
    }

    public static void updateStudent(ArrayList<Student> array) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入你要修改的学生的学号:");
        String sid = sc.nextLine();
        int index = -1;
        for (int i = 0; i < array.size(); i++) {
            Student student = array.get(i);
            if (student.getSid().equals(sid)) {
                index = i;
                break;
            }
        }
        if (index == -1) {
            System.out.println("无该学生信息，请重新输入");
        } else {
            System.out.println("请输入学生新姓名:");
            String name = sc.nextLine();
            System.out.println("请输入学生新年龄:");
            String age = sc.nextLine();
            System.out.println("请输入学生新地址:");
            String address = sc.nextLine();
            Student s = new Student();
            s.setSid(sid);
            s.setName(name);
            s.setAge(age);
            s.setAddress(address);
            array.set(index,s);
            System.out.println("修改学生成功！");
        }
    }
}
```

### 11.3 数据结构

数据结构是计算机存储、组织数据的方式。是指相互之间存在一种或多种特定关系的数据元素的集合。通常情况下，精心选择的数据结构可以带来更高的运行或者存储效率。

**常见数据结构之栈**

数据进入栈模型的过程称为：压/进栈

数据离开栈模型的过程称为：弹/出栈

栈是一种数据先进后出的模型

**常见数据结构之队列**

数据从后端进入队列模型的过程称为：入队列

数据从前端离开队列模型的过程称为：出队列

队列是一种数据先进先出的模型

**常见数据结构之数组**

查询数据通过索引定位，查询任意数据耗时相同，查询效率高

删除数据时，要将原始数据删除，同时后面每个数据前移，删除效率低

添加数据时，添加位置后的每个数据后移，再添加元素，添加效率极低

数组是一种查询快，增删慢的模型

**常见数据结构之链表**

链表是一种查询慢，增删快的模型

### 11.4 Set

**Set集合概述和特点**

Set集合特点

- 不包含重复元素的集合
- 没有带索引的方法，所以不能for循环遍历

**哈希值**

哈希值：是JDK根据对象的地址或者字符串或者数字算出来的int类型的数值

Object类中有一个方法可以获取对象的哈希值

- public int hashCode()：返回对象的哈希码值

对象的哈希值特点

- 同一个对象多次调用hashCode()方法返回的哈希值是相同的
- 默认情况下，不同对象的哈希值是不同的。而重写hashCode()方法，可以实现让不同对象的哈希值相同

**HashSet集合概述和特点**

HashSet集合特点

- 底层数据结构是哈希表
- 对集合的迭代顺序不作任何保证，也就是说不保证存储和取出的元素一致
- 没有带索引的方法，所以不能使用普通for循环遍历
- 由于是Set集合，所以是不包含重复元素的集合
- 要保证元素唯一性，需要重写hashCode()和equals()

**常见数据结构之哈希表**

哈希表

- JDK8之前，底层采用数组+链表实现，可以说是一个元素为链表的数组
- JDK8之后，在长度较长的时候，底层实现了优化

**LinkedHashSet集合概述和特点**

LinkedHashSet集合特点

- 哈希表和链表实现的Set接口，具有可预测的迭代次序
- 由链表保证元素有序，也就是说元素的存储和取出顺序是一致的
- 由哈希表保证元素唯一，也就是说没有重复的元素

**TreeSet集合概述和特点**

TreeSet集合特点

- 元素有序，这里的顺序不是指存储和取出的顺序，而是按照一定的规则进行排序，具体排序方式取决于构造方法
  - TreeSet()：根据其元素的自然排序进行排序
  - TreeSet(Comparator comparator)：根据指定的比较器进行排序
- 没有带索引的方法，所以不能使用普通for循环遍历
- 由于是Set集合，所以不包含重复元素的集合

**自然排序Comparable的使用**

- 存储学生对象并遍历，创建TreeSet集合使用无参构造方法
- 要求：按照年龄从小到大排序，年龄相同时，按照姓名的字母顺序排序

```Java
public class Student implements Comparable<Student> {
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public int compareTo(Student s) {
        int num = this.age - s.age;
        int num2 = num == 0 ? this.name.compareTo(s.name) : num;
        return num2;
    }
}
```

结论

- 用TreeSet集合存储自定义对象，无参构造方法使用的是自然排序对元素进行排序的
- 自然排序，就是让元素所属的类实现Comparable接口，重写compareTo(T o)方法
- 重写方法时，一定要注意排序规则必须按照要求的主要条件和次要条件来写

**比较器排序Comparator的使用**

- 存储学生对象并遍历，创建TreeSet集合使用带参构造方法
- 要求：按照年龄从小到大排序，年龄相同时，按照姓名的字母顺序排序

```Java
public class TreeSetDemo {
    public static void main(String[] args) {
        TreeSet<Student> ts = new TreeSet<Student>(new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                int num = o1.getAge() - o2.getAge();
                int num2 = num == 0 ? o1.getName().compareTo(o2.getName()) : num;
                return num2;
            }
        });
        Student s1 = new Student("xishi",29);
        Student s2 = new Student("wangzhaojun",28);
        Student s3 = new Student("diaochan",30);
        Student s4 = new Student("yangyuhuan",33);
        Student s5 = new Student("linqingxia",33);
        Student s6 = new Student("linqingxia",33);

        ts.add(s1);
        ts.add(s2);
        ts.add(s3);
        ts.add(s4);
        ts.add(s5);

        for (Student s: ts){
            System.out.println(s.getName() + ":" + s.getAge());
        }
    }
}
```

结论

- 用TreeSet集合存储自定义对象，带参构造方法使用的是比较器排序对元素进行排序的
- 比较器排序，就是让集合构造方法接收Comparator的实现类对象，重写compare(T o1, T o2)方法
- 重写方法时，一定要注意排序规则必须按照要求的主要条件和次要条件来写

练习：编写一个程序，获取10个1-20之间的随机数，要求随机数不能重复，并在控制台输出。

```Java
import java.util.HashSet;
import java.util.Random;
import java.util.Set;

public class SetDemo {
    public static void main(String[] args) {
        Set<Integer> set = new HashSet<Integer>();
        Random r = new Random();

        while (set.size() < 10) {
            int number = r.nextInt(20) + 1;
            set.add(number);
        }

        for (Integer i : set) {
            System.out.println(i);
        }
    }
}
```

## 12. 继承

### 12.1 继承概述

继承是面向对象三大特征之一。可以使得子类具有父类的属性和方法，还可以在子类中重新定义，追加属性和方法。

**继承的格式**

- 格式：public class 子类名 extends 父类名 {}
- 范例：public class Zi extends Fu {}
- Fu：父类，也被称为基类，超类
- Zi：子类，也被称为派生类

**继承中子类的特点**

- 子类可以有父类的内容
- 子类还可以有自己特有的内容

### 12.2 继承的好处和弊端

**继承好处**

- 提高了代码的复用性(多个类相同的成员可以放到同一个类中)
- 提高了代码的维护性(如果方法的代码需要修改，修改一处即可)

**继承弊端**

- 继承让类与类之间产生了子关系，类的耦合性增强了，当父类发生变化时子类实现也不得不跟着变化，削弱了子类的独立性

**什么时候使用继承？**

- 继承体现的关系：is a
- 假设法：我有两个类A和B，如果他们满足A是B的一种，或者B是A的一种，就说明它们存在继承关系，这个时候就可以考虑使用继承来体现，否则就不能滥用继承
- 举例：苹果和水果，猫和动物，猫和狗(不能使用)

### 12.3 继承中变量的访问特点

在子类方法中访问一个变量

- 子类局部范围找
- 子类成员范围找
- 父类成员范围找
- 如果都没有就报错(不考虑父亲的父亲...)

**super关键字**

super关键字的用法和this关键字的用法相似

- this：代表本类对象的引用
- this关键字指向调用该方法的对象，一般我们是在当前类中使用this关键字，所以我们常说this代表本类对象的引用
- super：代表父类存储空间的标识(可以理解为父类对象的引用)

| 关键字 |             访问成员变量             |           访问构造方法           |               访问成员方法                |
| :----: | :----------------------------------: | :------------------------------: | :---------------------------------------: |
|  this  | this.成员变量<br />访问本类成员变量  | this(...)<br />访问本类构造方法  | this.成员方法(...)<br />访问本类成员方法  |
| super  | super.成员变量<br />访问父类成员变量 | super(...)<br />访问父类构造方法 | super.成员方法(...)<br />访问父类成员方法 |

### 12.4 继承中构造与成员方法的访问特点

**继承中构造方法访问特点**

子类中所有的构造方法默认都会访问父类中无参的构造方法，为什么呢？

- 因为子类会继承父类中的数据，可能还会使用父类的数据。所以，子类初始化之前，一定要先完成父类数据的初始化
- 每一个子类构造方法的第一条语句默认都是：super()

如果父类中没有无参构造方法，只有带参构造方法，该怎么办呢？

- 通过使用super关键字去显示的调用父类的带参构造方法
- 在父类中自己提供一个无参构造方法

推荐：自己给出无参构造方法

**继承中成员方法访问特点**

通过子类对象访问一个方法

- 子类成员范围找
- 父类成员范围找
- 如果都没有就报错(不考虑父亲的父亲...)

### 12.5 方法重写

**方法重写概述：**子类中出现了和父类中一模一样的方法声明。

**方法重写的应用：**当子类需要父类的功能，而功能主体子类有自己特有内容时，可以重写父类中的方法，这样，即沿袭了父类的功能，又定义了子类特有的内容。

**@Override**

- 是一个注解
- 可以帮助我们检查重写方法的方法声明的正确性

**方法重写注意事项**

- 私有方法不能被重写(父类私有成员子类是不能继承的)
- 子类方法访问权限不能更低(public > 默认 > 私有)

**Java中继承的注意事项**

- Java中类只支持单继承，不支持多继承
- Java中类支持多层继承

## 13. 修饰符

### 13.1 包

**包的概述和使用**

其实包就是文件夹

作用：对类进行分类管理

包的定义格式

- 格式：package 包名;    (多级包用.分开)
- 范例：package com.itboy;

带包的Java类编译和执行

1. 手动建包：
   - 按照以前的格式编辑java文件              javac HelloWorld.java
   - 手动创建包                                            在相应目录下建立文件夹com，然后在com下建立文件夹itboy
   - 把class文件放到包的最里面                把HelloWorld.class文件放到com下的itboy这个文件夹下
   - 带包执行                                                java com.itboy.HelloWorld

2. 自动建包：
   - javac -d . HelloWorld.java                  java.com.itboy.HelloWorld

**导包的概述和使用**

使用不同包下的类时，使用的时候要写类的全路径，写起来太麻烦了，为了简化带包的操作，Java就提供了导包的功能。

导包的格式

- 格式：import 包名;
- 范例：import cn.itcast.Teacher;

### 13.2 修饰符

**修饰符的分类**

- 权限修饰符
- 状态修饰符

**权限修饰符**

|  修饰符   | 同一个类中 | 同一个包中子类无关类 | 不同包的子类 | 不同包的无关类 |
| :-------: | :--------: | :------------------: | :----------: | :------------: |
|  private  |     √      |                      |              |                |
|   默认    |     √      |          √           |              |                |
| protected |     √      |          √           |      √       |                |
|  public   |     √      |          √           |      √       |       √        |

**状态修饰符**

- final(最终态)
- static(静态)

**final**

final关键字是最终的意思，可以修饰成员方法，成员变量，类。final修饰的特点如下：

- 修饰方法：表明该方法是最终方法，不能被重写
- 修饰变量：表明该变量是常量，不能再次被赋值
- 修饰类：表明该类是最终类，不能被继承

final修饰局部变量

- 变量是基本类型：final修饰指的是基本类型的数据值不能发生改变
- 变量是引用类型：final修饰指的是引用类型的地址值不能发生改变，但是地址里面的内容是可以发生改变的

**static**

static关键字是静态的意思，可以修饰成员方法，成员变量。static修饰的特点：

- 被类的所有对象共享      这也是我们判断是否使用静态关键字的条件
- 可以通过类名调用          当然，也可以通过对象名调用。推荐使用类名调用

static访问特点

非静态的成员方法

- 能访问静态的成员变量
- 能访问非静态的成员变量
- 能访问静态的成员方法
- 能访问非静态的成员方法

静态的成员方法

- 能访问静态的成员变量
- 能访问静态的成员方法

总结：静态成员方法只能访问静态成员

## 14. 多态

### 14.1 多态概述

同一个对象，在不同时刻表现出来的不同形态。

举例：猫

我们可以说猫是猫：猫 cat = new 猫();

我们也可以说猫是动物：动物 animal = new 猫();

这里猫在不同的时刻表现出来了不同的形态，这就是多态

多态的前提和体现

-  有继承/实现关系
- 有方法重写
- 有父类引用指向子类对象

### 14.2 多态中成员访问特点

多态中访问成员变量和成员方法的特点

- 成员变量：编译看左边，执行看左边
- 成员方法：编译看左边，执行看右边

为什么成员变量和成员方法的访问不一样呢？

- 因为成员方法有重写，而成员变量没有

多态的好处和弊端

- 多态的好处：提高了程序的扩展性

  具体体现：定义方法的时候，使用父类型作为参数，将来在使用的时候，使用具体的子类型参与操作

- 多态的弊端：不能使用子类的特有功能

### 14.3 多态中的转型

多态中有向上转型和向下转型

- 向上转型     从子到父     父类引用指向子类对象
- 向下转型     从父到子     父类引用转为子类对象   

## 15. 抽象类

**抽象的概述**

在Java中，一个没有方法体的方法应该定义为抽象方法，而类中如果有抽象方法，该类必须定义为抽象类。

**抽象类的特点**

- 抽象类和抽象方法必须使用abstract关键字修饰
  - public abstract class 类名 {}
  - public abstract void eat();

- 抽象类中不一定有抽象方法，有抽象方法的类一定是抽象类
- 抽象类不能实例化；参照多态的方式，通过子类对象实例化，这叫抽象类多态
- 抽象类的子类
  - 要么重写抽象类中的所有抽象方法
  - 要么是抽象类

**抽象类的成员特点**

- 成员变量：可以是变量，也可以是常量
- 构造方法
  - 有构造方法，但是不能实例化
  - 这里构造方法的作用是：用于子类访问父类数据的初始化

- 成员方法
  - 可以是抽象方法：限定子类必须完成某些动作
  - 也可以有非抽象方法：提高代码复用性

## 16. 接口

**接口概述**

接口就是一种公共的规范标准，只要符合规范标准，大家都可以使用。Java中的接口更多的体现在对行为的抽象。

**接口的特点**

- 接口用关键字interface修饰            public interface 接口名 {}
- 类实现接口用implements表示       public class 类名 implements 接口名 {}
- 接口不能实例化
  - 参照多态的方式，通过实现类对象实例化，这叫接口多态
  - 多态的形式：具体类多态，抽象类多态，接口多态
  - 多态的前提：有继承或者实现关系；有方法重写；有父(类/接口)引用指向(子/实现)类对象

- 接口的实现类
  - 要么重写接口中的所有抽象方法
  - 要么是抽象类

**接口的成员特点**

- 成员变量只能是常量，默认修饰符：public static final
- 构造方法：接口没有构造方法，因为接口主要是对行为进行抽象的，是没有具体存在；一个类中如果没有父类，默认继承自Object类
- 成员方法只能是抽象方法，默认修饰符：public abstract

注意：关于接口中的方法，JDK8和JDK9中有一些新特性。

**类和接口的关系**

- 类和类的关系：继承关系，只能单继承，但是可以多层继承
- 类和接口的关系：实现关系，可以单实现，也可以多实现，还可以在继承一个类的同时实现多个接口
- 接口和接口的关系：继承关系，可以单继承，也可以多继承

**抽象类和接口的区别**

- 成员区别
  - 抽象类       变量，常量；有构造方法；有抽象方法，也有非抽象方法
  - 接口           常量，抽象方法

- 关系区别
  - 类与类            继承，单继承
  - 类与接口        实现，可以单实现，也可以多实现
  - 接口与接口    继承，单继承，多继承

- 设计理念区别
  - 抽象类            对类抽象，包括属性、行为
  - 接口                对行为抽象，主要是行为

## 17. 形参和返回值

**类名作为形参和返回值**

- 方法的形参是类名，其实需要的是该类的对象
- 方法的返回值是类名，其实需要的是该类的对象

**抽象类名作为形参和返回值**

- 方法的形参是抽象类名，其实需要的是该抽象类的子类对象
- 方法的返回值是抽象类名，其实返回的是该抽象类的子类对象

**接口名作为形参和返回值**

- 方法的形参是接口名，其实需要的是该接口的实现类对象
- 方法的返回值是接口名，其实返回的是该接口的实现类对象

## 18. 内部类

**内部类概述**

内部类：就是在一个类中定义一个类。举例：在一个类A的内部定义一个类B，类B就被称为内部类。

```java
// 内部类定义的格式
public class 类名 {
    修饰符 class 类名 {
    }
}
```

**内部类的访问特点**

- 内部类可以直接访问外部类的成员，包括私有
- 外部类要访问内部类的成员，必须创建对象

**成员内部类**

按照内部类在类中定义的位置不同，可以分为如下两种形式

- 在类的成员位置：成员内部类
- 在类的局部位置：局部内部类

成员内部类，外界创建对象使用方法

- 格式：外部类名.内部类名 对象名 = 外部类对象.内部类对象;
- 范例：Outer.Inner oi = new Outer().new Inner();

**局部内部类**

局部内部类是在方法中定义的类，所以外界是无法直接使用，需要在方法内部创建对象并使用。该类可以直接访问外部类的成员，也可以访问方法内的局部变量。

**匿名内部类**

前提：存在一个类或者接口，这里的类可以是具体类也可以是抽象类

```java
// 格式
new 类名或者接口名() {
    重写方法;
};
```

本质：是一个继承了该类或者实现了该接口的子类匿名对象。

## 19. 常用API

### 19.1 Math

**Math类概述**

Math包含执行基本数字运算的方法。

Math类中成员的使用：看类的成员是否都是静态的，如果是，通过类名就可以直接调用。

**Math类的常用方法**

|                   方法名                    |                      说明                      |
| :-----------------------------------------: | :--------------------------------------------: |
|        public static int abs(int a)         |                返回参数的绝对值                |
|     public static double ceil(double a)     | 返回大于或等于参数的最小double值，等于一个整数 |
|    public static double floor(double a)     | 返回小于或等于参数的最大double值，等于一个整数 |
|      public static int round(float a)       |        按照四舍五入返回最接近参数的int         |
|     public static int max(int a,int b)      |            返回两个int值中的较大值             |
|     public static int min(int a,int b)      |            返回两个int值中的较小值             |
| public static double pow(double a,double b) |                返回a的b次幂的值                |
|        public static double random()        |        返回值为double的正值，[0.0,1.0)         |

### 19.2 System

**System类概述**

System包含几个有用的类字段和方法，它不能被实例化。

**System类的常用方法**

|                方法名                 |                    说明                    |
| :-----------------------------------: | :----------------------------------------: |
|  public static void exit(int status)  | 终止当前运行的Java虚拟机，非零表示异常终止 |
| public static long currentTimeMills() |         返回当前时间(以毫秒为单位)         |

### 19.3 Object

**Object类的概述**

Object是类层次结构的根，每个类都可以将Object作为超类。所有类都直接或者间接的继承自该类。

构造方法：public Object()

子类的构造方法默认访问的是父类的无参构造方法，因为它们的顶级父类只有无参构造方法。

**Object类的常用方法**

|              方法名               |                            说明                            |
| :-------------------------------: | :--------------------------------------------------------: |
|     public String toString()      | 返回对象的字符串表示形式。建议所有子类重写该方法，自动生成 |
| public boolean equals(Object obj) |  比较对象是否相等。默认比较地址，重写可比较内容，自动生成  |

### 19.4 Arrays

**冒泡排序**

排序：将一组数据按照固定的规则进行排序。

冒泡排序：一种排序的方式，对要进行排序的数据中相邻的数据进行两两比较，将较大的数据放在后面，依次对所有的数据进行操作，直至所有数据按要求完成排序。

**排序特点**

- 如果有n个数据进行排序，总共需要比较n-1次
- 每一次比较完毕，下一次的比较就会少一个数据参与

**Arrays类的概述和常用方法**

Arrays类包含用于操作数组的各种方法

|                 方法名                 |                说明                |
| :------------------------------------: | :--------------------------------: |
| public static String toString(int[] a) | 返回指定数组的内容的字符串表示形式 |
|    public static void sort(int[] a)    |     按照数字顺序排序指定的数组     |

**工具类的设计思想**

- 构造方法用private修饰
- 成员用public static修饰

### 19.5 基本类型包装类

**基本类型包装类概述**

将基本数据类型封装成对象的好处在于可以在对象中定义更多的功能方法操作该数据

常用的操作之一：用于基本数据类型与字符串之间的转换

| 基本数据类型 |  包装类   |
| :----------: | :-------: |
|     byte     |   Byte    |
|    short     |   Short   |
|     int      |  Integer  |
|     long     |   Long    |
|    float     |   Float   |
|    double    |  Double   |
|     char     | Character |
|   boolean    |  Boolean  |

**int和String的相互转换**

基本类型包装类的最常见操作就是：用于基本类型和字符串之间的相互转换。

**1. int转换为String**

public static String valueOf(int i)：返回int参数的字符串表示形式。该方法是String类中的方法

**2. String转换为int**

public static int parseInt(String s)：将字符串解析为int类型。该方法是Integer类中的方法

练习：有一个字符串："91 27 46 38 50"，请写程序实现最终输出结果是："27 38 46 50 91"。

```java
import java.util.Arrays;

public class IntegerTest {
    public static void main(String[] args) {
        //定义一个字符串
        String s = "91 27 46 38 50";
        System.out.println("     s:" + s);
        //把字符串中的数字数据存储到一个int类型的数组中
        String[] strArray = s.split(" ");

        int[] arr = new int[strArray.length];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = Integer.parseInt(strArray[i]);
        }
        Arrays.sort(arr);

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < arr.length; i++) {
            if (i == arr.length - 1) {
                sb.append(arr[i]);
            } else {
                sb.append(arr[i]).append(" ");
            }
        }
        String result = sb.toString();
        System.out.println("result:" + result);
    }
}
```

**自动装箱和拆箱**

- 装箱：把基本数据类型转换为对应的包装类类型
- 拆箱：把包装类类型转换为对应的基本数据类型

```java
Integer i = 100;   // 自动装箱
i += 200;          // i = i + 200; i + 200 自动拆箱; i = i + 200; 自动装箱
```

注意：在使用包装类类型的时候，如果做操作，最好先判断是否为null。

推荐：只要是对象，在使用前就必须进行不为null的判断。

### 19.6 日期类

**Date类概述和构造方法**

Date代表了一个特定的时间，精确到毫秒

|             方法名             |                             说明                             |
| :----------------------------: | :----------------------------------------------------------: |
|         public Date()          | 分配一个Date对象，并初始化，以便它代表它被分配的时间，精确到毫秒 |
|     public Date(long date)     | 分配一个Date对象，并将其初始化为表示从标准基准时间起指定的毫秒数 |
|     public long getTime()      |     获取的是日期对象从1970年1月1日00:00:00到现在的毫秒值     |
| public void setTime(long time) |                    设置时间，给的是毫秒值                    |

**SimpleDateFormat类概述**

SimpleDateFormat是一个具体的类，用于以区域设置敏感的方式格式化和解析日期。

日期和时间格式由日期和时间模式字符串指定，在日期和时间模式字符串中，从'A'到'Z'以及从'a'到'z'引号的字母被解释为表示日期或时间字符串的组件的模式字母。

常用的模式字母及对应关系如下：

- y            年
- M           月
- d            日
- H            时
- m           分
- s             秒

**SimpleDateFormat的构造方法**

|                 方法名                  |                          说明                          |
| :-------------------------------------: | :----------------------------------------------------: |
|        public SimpleDateFormat()        |    构造一个SimpleDateFormat，使用默认模式和日期格式    |
| public SimpleDateFormat(String pattern) | 构造一个SimpleDateFormat使用给定的模式和默认的日期格式 |

**SimpleDateFormat格式化和解析日期**

**1. 格式化(从Date到String)**

public final String format(Date date)：将日期格式化成日期/时间字符串

**2. 解析(从String到Date)**

public Date parse(String source)：从给定字符串的开始解析文本以生成日期

**Calendar类概述**

Calendar为某一时刻和一组日历字段之间的转换提供了一些方法，并为操作日历字段提供了一些方法。

Calendar提供了一个类方法getInstance用于获取Calendar对象，其日历字段已使用当前日期和时间初始化：Calendar rightNow = Calendar.getInstance();

**Calendar的常用方法**

|                       方法名                       |                          说明                          |
| :------------------------------------------------: | :----------------------------------------------------: |
|             public int get(int field)              |                  返回给定日历字段的值                  |
|   public abstract void add(int field,int amount)   | 根据日历的规则，将指定的时间量添加或减去给定的日历字段 |
| public final void set(int year,int month,int date) |                  设置当前日历的年月日                  |

练习：获取任意一年的二月有多少天。

```java
import java.util.Calendar;
import java.util.Scanner;

public class CalendarTest {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入年份：");
        int year = sc.nextInt();

        Calendar c = Calendar.getInstance();
        // 设置为当前年的3月1日
        c.set(year,2,1);
        // 3月1日往前推一天，就是2月份的最后一天
        c.add(Calendar.DATE,-1);
        int date = c.get(Calendar.DATE);
        System.out.println(year + "年的2月份有" + date + "天");
    }
}
```

## 20. 异常

**异常概述**：就是程序出现了不正常的情况。

Error：严重问题，不需要处理

Exception：称为异常类，它表示程序本身可以处理的问题

- RuntimeException：在编译期是不检查的，出现问题后，需要我们回来修改代码
- 非RuntimeException：编译期就必须处理的，否则程序不能通过编译，就更不能正常运行了

**JVM的默认处理方案**

如果程序出现了问题，我们没有做任何处理，最终JVM会做默认的处理

- 把异常的名称，异常原因及异常出现的位置等信息输出在了控制台
- 程序停止执行

**异常处理**

如果程序出现了问题，我们需要自己来处理，有两种方案：

- try ... catch ...
- throws

**异常处理之try...catch...**

```java
// 格式
try {
    可能出现异常的代码;
} catch(异常类名 变量名) {
    异常的处理代码;
}
```

执行流程：

1. 程序从try里面的代码开始执行
2.  出现异常，会自动生成一个异常类对象，该异常对象将被提交给Java运行时系统
3. 当Java运行时系统接收到异常对象，会到catch中去找匹配的异常类，找到后进行异常的处理
4. 执行完毕之后，程序还可以继续往下执行

**Throwable的成员方法**

|            方法名             |              说明               |
| :---------------------------: | :-----------------------------: |
|  public String getMessage()   | 返回此throwable的详细消息字符串 |
|   public String toString()    |     返回此可抛出的简短描述      |
| public void printStackTrace() |  把异常的错误信息输出在控制台   |

**编译时异常和运行时异常的区别**

Java中的异常被分为两大类：编译时异常和运行时异常，也被称为受检异常和非受检异常。所有的RuntimeException类及其子类被称为运行时异常，其他的异常都是编译时异常。

- 编译时异常：必须显式处理，否则程序就会发生错误，无法通过编译
- 运行时异常：无需显式处理，也可以和编译时异常一样处理

**异常处理之throws**

虽然我们通过try...catch...可以对异常进行处理，但是并不是所有的情况我们都有权限进行异常的处理。也就是说，有些时候可能出现的异常是我们处理不了的，针对这种情况，Java提供了throws的处理方案。

```java
// 格式
throws 异常类名;
```

注意：这个格式是跟在方法的括号后面的。

- 编译时异常必须要进行处理，两种处理方案：try...catch...或者throws，如果采用throws这种方案，将来谁调用谁处理
- 运行时异常可以不处理，出现问题后，需要我们回来修改代码

**自定义异常**

```java
// 格式
public class 异常类名 extends Exception {
    无参构造
    带参构造
}

// 范例
public class ScoreException extends Exception {
    public ScoreException() {}
    public ScoreException(String message) {
        super(message);
    }
}
```

**throws和throw的区别**

对于throws

- 用在方法声明后面，跟的是异常类名
- 表示抛出异常，由该方法的调用者来处理
- 表示出现异常的一种可能性，并不一定会发生这些异常

**throw**

- 用在方法体内，跟的是异常对象名
- 表示抛出异常，由方法体内的语句处理
- 执行throw一定抛出了某种异常

## 21. 泛型

### 21.1 泛型概述

泛型：是JDK5中引入的特性，它提供了编译时类型安全检测机制，该机制允许在编译时检测到非法的类型。它的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。

一提到参数，最熟悉的就是定义方法时有形参，然后调用此方法时传递实参。那么参数化类型怎么理解呢？

顾名思义，就是将类型由原来的具体的类型参数化，然后在使用/调用时传入具体的类型。这种参数类型可以用在类、方法和接口中，分别被称为泛型类、泛型方法、泛型接口。

泛型定义格式：

- <类型>：指定一种类型的格式。这里的类型可以看成是形参
- <类型1, 类型2...>：指定多种类型的格式，多种类型之间用逗号隔开。这里的类型可以看成是形参
- 将来具体调用时候给定的类型可以看成是实参，并且实参的类型只能是引用类型

泛型的好处：

- 把运行期间的问题提前到了编译期间
- 避免了强制类型转换

### 21.2 泛型类

**泛型类**

泛型类的定义格式：

- 格式：修饰符 class 类名<类型> {}

- 范例：public class Generic\<T> {}

  此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型

**泛型方法**

泛型方法的定义格式：

- 格式：修饰符<类型> 返回值类型 方法名(类型 变量名) {}
- 范例：public \<T> void show(T t) {}

**泛型接口**

泛型接口的定义格式：

- 格式：修饰符 interface 接口名<类型> {}
- 范例：public interface Generic\<T> {}

### 21.3 类型通配符

为了表示各种泛型List的父类，可以使用类型通配符

- 类型通配符：<?>
- List<?>：表示元素类型未知的List，它的元素可以匹配任何的类型
- 这种带通配符的List仅表示它是各种泛型List的父类，并不能把元素添加到其中

如果说我们不希望List<?>是任何泛型List的父类，只希望它代表某一类泛型List的父类，可以使用类型通配符的上限

- 类型通配符上限：<? extends 类型>
- List <? extends Number>：它表示的类型是Number或者其子类型

除了可以指定类型通配符的上限，我们也可以指定类型通配符的下限

- 类型通配符下限：<? super 类型>
- List<? super Number>：它表示的类型是Number或者其父类型

**可变参数**

可变参数又称参数个数可变，用作方法的形参出现，那么方法参数个数就是可变的了

- 格式：修饰符 返回值类型 方法名(数据类型... 变量名) {}
- 范例：public static int sum(int... a) {}

可变参数注意事项

- 这里的变量其实是一个数组
- 如果一个方法有多个参数，包含可变参数，可变参数要放在最后

**可变参数的使用**

Arrays工具类中有一个静态方法：

- public static \<T> List\<T> asList<T... a>：返回由指定数组支持的固定大小的列表
- 返回的集合不能做增删操作，可以做修改操作

List接口中有一个静态方法：

- public static \<E> List\<E> of(E... elements)：返回包含任意数量元素的不可变列表
- 返回的集合不能做增删改操作

Set接口中有一个静态方法：

- public static \<E> Set\<E> of(E... elements)：返回一个包含任意数量元素的不可变集合
- 在给元素的时候，不能给重复元素
- 返回的集合不能做增删操作，没有修改的方法

## 22. Map

### 22.1 Map集合概述和使用

**Map集合概述**

- Interface Map<K,V>    K：键的类型；   V：值的类型
- 将键映射到值的对象；不能包含重复的键；每个键可以映射到最多一个值

创建Map集合的对象

- 多态的方式
- 具体的实现类HashMap

**Map集合的基本功能**

|               方法名                |                 说明                 |
| :---------------------------------: | :----------------------------------: |
|        V put(K key, V value)        |               添加元素               |
|        V remove(Object key)         |         根据键删除键值对元素         |
|            void clear()             |         移除所有的键值对元素         |
|   boolean containsKey(Object key)   |       判断集合是否包含指定的键       |
| boolean containsValue(Object value) |       判断集合是否包含指定的值       |
|          boolean isEmpty()          |           判断集合是否为空           |
|             int size()              | 集合的长度，也就是集合中键值对的个数 |

**Map集合的获取功能**

|             方法名             |           说明           |
| :----------------------------: | :----------------------: |
|       V get(Object key)        |       根据键获取值       |
|        Set\<K> keySet()        |     获取所有键的集合     |
|    Collection\<V> values()     |     获取所有值的集合     |
| Set<Map.Entry<K,V>> entrySet() | 获取所有键值对对象的集合 |

**Map集合的遍历(方式一)**

我们可以把Map看成是一个夫妻对的集合，从而有遍历思路如下：

- 把所有的丈夫给集中起来
- 遍历丈夫的集合，获取到每一个丈夫
- 根据丈夫去找对应的妻子

转换为Map集合中的操作：

- 获取所有键的集合。用keySet()方法实现
- 遍历键的集合，获取到每一个键。用增强for实现
- 根据键去找值，用get(Object key)方法实现

**Map集合的遍历(方式二)**

我们可以把Map看成是一个夫妻对的集合，从而有遍历思路如下：

- 获取所有结婚证的集合
- 遍历结婚证的集合，得到每一个结婚证
- 根据结婚证获取丈夫和妻子

转换为Map集合中的操作：

- 获取所有键值对对象的集合
  - Set<Map.Entry<K,V>> entrySet()：获取所有键值对对象的集合
- 遍历键值对对象的集合，得到每一个键值对对象
  - 用增强for实现，得到每一个Map.Entry
- 根据键值对对象获取键和值
  - 用getKey()得到键
  - 用getValue()得到值

练习：在ArrayList里存储一个HashMap并遍历。

```Java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Set;

public class ArrayListIncludeHashMap {
    public static void main(String[] args) {
        ArrayList<HashMap<String,String>> list = new ArrayList<HashMap<String,String>>();
        HashMap<String,String> hm1 = new HashMap<String,String>();
        hm1.put("孙策","大乔");
        hm1.put("周瑜","小乔");
        list.add(hm1);

        HashMap<String,String> hm2 = new HashMap<String,String>();
        hm2.put("郭靖","黄蓉");
        hm2.put("杨过","小龙女");
        list.add(hm2);

        HashMap<String,String> hm3 = new HashMap<String,String>();
        hm3.put("令狐冲","任盈盈");
        hm3.put("林平之","岳灵珊");
        list.add(hm3);

        for (HashMap<String,String> hm : list) {
            Set<String> set = hm.keySet();
            for (String key : set) {
                String value = hm.get(key);
                System.out.println(key + "," + value);
            }
        }
    }
}
```

练习：键盘录入一个字符串，要求统计字符串中每个字符出现的次数。

```Java
import java.util.HashMap;
import java.util.Scanner;
import java.util.Set;
import java.util.TreeMap;

public class HashMapDemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个字符串：");
        String line = sc.nextLine();

//        HashMap<Character,Integer> hm = new HashMap<Character,Integer>();
        TreeMap<Character,Integer> hm = new TreeMap<Character,Integer>();

        for (int i = 0; i < line.length(); i++) {
            char key = line.charAt(i);
            Integer value = hm.get(key);

            if (value == null) {
                hm.put(key,1);
            } else {
                value++;
                hm.put(key,value);
            }
        }

        StringBuilder sb = new StringBuilder();
        Set<Character> keySet = hm.keySet();
        for (Character key : keySet) {
            Integer value = hm.get(key);
            sb.append(key).append("(").append(value).append(")");
        }

        String result = sb.toString();
        System.out.println(result);
    }
}
```

## 23. Collections

**Collections类的概述**

- 是针对集合操作的工具类

**Collections类的常用方法**

- public static <T extends Comparable<? super T>> void sort(List\<T> list)：将指定的列表按升序排列
- public static void reverse(List<?> list)：反转指定列表中元素的顺序
- public static void shuffle(List<?> list)：使用默认的随机源随机排序指定的列表

**练习：**通过程序实现斗地主过程中的洗牌，发牌和看牌。

普通版：

```Java
import java.util.ArrayList;
import java.util.Collections;

public class PokerDemo {
    public static void main(String[] args) {
        ArrayList<String> array = new ArrayList<String>();

        String[] colors = {"♦", "♣", "♥", "♠"};
        String[] numbers = {"2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A"};

        for (String color : colors) {
            for (String number : numbers) {
                array.add(color + number);
            }
        }
        array.add("小王");
        array.add("大王");

        Collections.shuffle(array);

        ArrayList<String> lqxArray = new ArrayList<String>();
        ArrayList<String> lyArray = new ArrayList<String>();
        ArrayList<String> fqyArray = new ArrayList<String>();
        ArrayList<String> dpArray = new ArrayList<String>();

        for (int i = 0; i < array.size(); i++) {
            String poker = array.get(i);
            if (i >= array.size() - 3) {
                dpArray.add(poker);
            } else if (i % 3 == 0) {
                lqxArray.add(poker);
            } else if (i % 3 == 1) {
                lyArray.add(poker);
            } else if (i % 3 == 2) {
                fqyArray.add(poker);
            }
        }

        lookPoker("林青霞", lqxArray);
        lookPoker("柳岩", lyArray);
        lookPoker("风清扬", fqyArray);
        lookPoker("底牌", dpArray);

    }

    public static void lookPoker(String name, ArrayList<String> array) {
        System.out.print(name + "的牌是： ");
        for (String poker : array) {
            System.out.print(poker + " ");
        }
        System.out.println();
    }
}
```

升级版：

```Java
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashMap;
import java.util.TreeSet;

public class PokerDemo1 {
    public static void main(String[] args) {
        HashMap<Integer, String> hm = new HashMap<Integer, String>();
        ArrayList<Integer> array = new ArrayList<Integer>();

        String[] colors = {"♦", "♣", "♥", "♠"};
        String[] numbers = {"3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A", "2"};

        int index = 0;
        for (String number : numbers) {
            for (String color : colors) {
                hm.put(index, color + number);
                array.add(index);
                index++;
            }
        }
        hm.put(index, "小王");
        array.add(index);
        index++;
        hm.put(index, "大王");
        array.add(index);

        Collections.shuffle(array);

        TreeSet<Integer> lqxSet = new TreeSet<Integer>();
        TreeSet<Integer> lySet = new TreeSet<Integer>();
        TreeSet<Integer> fqySet = new TreeSet<Integer>();
        TreeSet<Integer> dpSet = new TreeSet<Integer>();

        for (int i = 0; i < array.size(); i++) {
            int x = array.get(i);
            if (i >= array.size() - 3) {
                dpSet.add(x);
            } else if (i % 3 == 0) {
                lqxSet.add(x);
            } else if (i % 3 == 1) {
                lySet.add(x);
            } else if (i % 3 == 2) {
                fqySet.add(x);
            }
        }

        lookPoker("林青霞", lqxSet, hm);
        lookPoker("柳岩", lySet, hm);
        lookPoker("风清扬", fqySet, hm);
        lookPoker("底牌", dpSet, hm);
    }

    public static void lookPoker(String name, TreeSet<Integer> ts, HashMap<Integer, String> hm) {
        System.out.print(name + "的牌是： ");
        for (Integer key : ts) {
            String poker = hm.get(key);
            System.out.print(poker + " ");
        }
        System.out.println();
    }
}
```

## 24. File

### 24.1 File类概述和构造方法

File：它是文件和目录路径名的抽象表示

- 文件和目录是可以通过File封装成对象的
- 对于File而言，其封装的并不是一个真正存在的文件，仅仅是一个路径名而已。它可以是存在的，也可以是不存在的。将来是要通过具体的操作把这个路径的内容转换为具体存在的

|              方法名               |                            说明                            |
| :-------------------------------: | :--------------------------------------------------------: |
|       File(String pathname)       | 通过将给定的路径名字符串转换为抽象路径名来创建新的File实例 |
| File(String parent, String child) |      从父路径名字符串和子路径名字符串创建新的File实例      |
|  File(File parent, String child)  |       从父抽象路径名和子路径名字符串创建新的File实例       |

**File类创建功能**

|             方法名             |                             说明                             |
| :----------------------------: | :----------------------------------------------------------: |
| public boolean createNewFile() | 当具有该名称的文件不存在时，创建一个由该抽象路径名命名的新空文件 |
|     public boolean mkdir()     |                 创建由此抽象路径名命名的目录                 |
|    public boolean mkdirs()     |  创建由此抽象路径名命名的目录，包括任何必需但不存在的父目录  |

**File类判断和获取功能**

|             方法名              |                           说明                           |
| :-----------------------------: | :------------------------------------------------------: |
|  public boolean isDirectory()   |           测试此抽象路径名表示的File是否为目录           |
|     public boolean isFile()     |           测试此抽象路径名表示的File是否为文件           |
|     public boolean exists()     |            测试此抽象路径名表示的File是否存在            |
| public String getAbsolutePath() |            返回此抽象路径名的绝对路径名字符串            |
|     public String getPath()     |             将此抽象路径名转换为路径名字符串             |
|     public String getName()     |         返回由此抽象路径名表示的文件或目录的名称         |
|     public String[] list()      | 返回此抽象路径名表示的目录中的文件和目录的名称字符串数组 |
|    public File[] listFiles()    |  返回此抽象路径名表示的目录中的文件和目录的File对象数组  |

**File类删除功能**

|         方法名          |                说明                |
| :---------------------: | :--------------------------------: |
| public boolean delete() | 删除由此抽象路径名表示的文件或目录 |

绝对路径和相对路径的区别

- 绝对路径：完整的路径名，不需要任何其他信息就可以定位它所表示的文件。例如：E:\\\itahu\\\java.txt
- 相对路径：必须使用取自其他路径名的信息进行解释。例如：myFile\\\java.txt

删除目录时的注意事项：

- 如果一个目录中有内容(目录，文件)，不能直接删除。应该先删除目录中的内容，最后才能删除目录

### 24.2 递归

**递归概述：**以编程的角度来看，递归指的是方法定义中调用方法本身的现象。

**递归解决问题的思路**

把一个复杂的问题层层转化为一个与原问题相似的规模较小的问题来求解。递归策略只需少量的程序就可描述出解题过程所需要的多次重复计算。

**递归解决问题要找到两个内容**

- 递归出口：否则会出现内存溢出
- 递归规则：与原问题相似的规模较小的问题

练习：给定一个路径(F:\\\JavaProjects)，请通过递归完成遍历该目录下的所有内容，并把所有文件的绝对路径输出在控制台。

```Java
import java.io.File;

public class DiGuiDemo {
    public static void main(String[] args) {
        File src = new File("F:\\JavaProjects");
        getAllFilePath(src);
    }

    public static void getAllFilePath(File srcFile) {
        File[] fileArray = srcFile.listFiles();
        if (fileArray != null) {
            for (File file : fileArray) {
                if (file.isDirectory()) {
                    getAllFilePath(file);
                } else {
                    System.out.println(file.getAbsolutePath());
                }
            }
        }
    }
}
```

### 24.3 字节流

**IO流概述和分类**

IO流概述：

- IO：输入/输出(Input/Output)
- 流：是一种抽象概念，是对数据传输的总称。也就是说数据在设备间的传输称为流，流的本质是数据传输
- IO流就是用来处理设备间数据传输问题的。常见的应用：文件复制；文件上传；文件下载

IO流分类：

- 按照数据的流向
  - 输入流：读数据
  - 输出流：写数据
- 按照数据类型来分
  - 字节流：字节输入流；字节输出流
  - 字符流：字符输入流；字符输出流

一般来说，我们说IO流的分类是按照数据类型来分的。那么这两种流在什么情况下使用呢？

- 如果数据通过Windows自带的记事本软件打开，我们还可以读懂里面的内容，就是用字符流，否则使用字节流。如果你不知道该使用那种类型的流，就使用字节流。

**字节流写数据**

字节流抽象基类

- InputStream：这个抽象类是表示字节输入流的所有类的超类
- OutputStream：这个抽象类是表示字节输入流的所有类的超类
- 子类名特点：子类名称都是以其父类名作为子类名的后缀

FileOutputStream：文件输出流用于将数据写入File

- FileOutputStream(String name)：创建文件输出流以指定的名称写入文件

使用字节输出流写数据的步骤：

- 创建字节输出流对象(调用系统功能创建了文件，创建字节输出流对象，让字节输出流对象指向文件)
- 调用字节输出流对象的写数据方法
- 释放资源(关闭此文件输出流并释放与此流相关联的任何系统资源)

**字节流写数据的3种方式**

|                 方法名                 |                             说明                             |
| :------------------------------------: | :----------------------------------------------------------: |
|           void wirte(int b)            |     将指定的字节写入此文件输出流<br />一次写一个字节数据     |
|          void write(byte[] b)          | 将b.length字节从指定的字节数组写入此文件输出流<br />一次写一个字节数组数据 |
| void write(byte[] b, int off, int len) | 将len字节从指定的字节数组开始，从偏移量off开始写入此文件输出流<br />一次写一个字节数组的部分数据 |

**字节流写数据的两个小问题**

字节流写数据如何实现换行呢？

- 写完数据后，加换行符
  - Windows：\r\n
  - Linux：\n
  - Mac：\r

字节流写数据如何实现追加写入呢？

- public FileOutputStream(String name, boolean append)
- 创建文件输出流以指定的名称写入文件。如果第二个参数为true，则字节将写入文件的末尾而不是开头

**字节流写数据加异常处理**

finally：在异常处理时提供finally块来执行所有清除操作。比如说IO流中的释放资源

特点：被finally控制的语句一定会执行，除非JVM退出

```Java
try{
    可能出现异常的代码;
}catch(异常类名 变量名){
    异常的处理代码;
}finally{
    执行所有清除操作;
}
```

**字节流读数据(一次读一个字节数据)**

需求：把文件fos.txt中的内容读取出来在控制台输出

FileInputStream：从文件系统中的文件获取输入字节

- FileInputStream(String name)：通过打开与实际文件的连接来创建一个FileInputStream，该文件由文件系统中的路径名name命名

使用字节输入流读数据的步骤：

- 创建字节输入流对象
- 调用字节输入流对象的读数据方法
- 释放资源

练习：把“D:\\\Photo\\\MyImages2.jpg”复制到模块目录下的"MyImages2.jpg"。

```Java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileInputStreamDemo {
    public static void main(String[] args) throws IOException {
        FileInputStream fs = new FileInputStream("D:\\Photo\\MyImages2.jpg");
        FileOutputStream fos = new FileOutputStream("MyImages2.jpg");

        byte[] bys = new byte[1024];
        int len;
        while ((len = fs.read(bys)) != -1) {
            fos.write(bys,0,len);
        }

        fs.close();
        fos.close();
    }
}
```

**字节缓冲流**

字节缓冲流

- BufferedOutputStream：该类实现缓冲输出流，应用程序可以向底层输出流写入字节，而不必为写入的每个字节导致底层系统的调用
- BufferedInputStream：创建BufferedInputStream将创建一个内部缓冲区数组。当从流中读取或跳过字节时，内部缓冲区将根据需要从所包含的输入流中重新填充，一次很多字节

构造方法：

- 字节缓冲输入流：BufferedOutputStream(OutputStream out)
- 字节缓冲输出流：BufferedInputStream(InputStream in)

为什么构造方法需要的是字节流，而不是具体的文件或者路径呢？

- 字节缓冲流仅仅提供缓冲区，而真正的读写数据还得依靠基本的字节流对象进行操作

### 24.4 字符流

**为什么会出现字符流**

由于字节流操作中文不是特别的方便，所以Java就提供字符流

- 字符流 = 字节流 + 编码表

用字节流复制文本文件时，文本文件也会有中文，但是没有问题，原因是最终底层操作会自动进行字节拼接成中文，如何识别是中文的呢？

- 汉字在存储的时候，无论选择哪种编码存储，第一个字节都是负数

**编码表**

基础知识：

- 计算机中存储的信息都是用二进制数表示的；我们在屏幕上看到的英文、汉字等字符是二进制数转换之后的结果
- 按照某种规则，将字符存储到计算机中，称为编码。反之，将存储在计算机中的二进制数按照某种规则解析出来，称为解码。这里强调一下：按照A编码存储，必须按照A编码解析，这样才能显示正确的文本符号。否则就会导致乱码现象

字符编码：就是一套自然语言的字符与二进制数之间的对应规则(A,65)

字符集：

- 是一个系统支持的所有字符的集合，包括各国家文字、标点符号、图形符号、数字等
- 计算机要准确的存储和识别各种字符集符号，就需要进行字符编码，一套字符集必然至少有一套字符编码。常见字符集有ASCII字符集、GBXXX字符集、Unicode字符集等

ASCII字符集：

- ASCII(American Standard Code for information Interchange, 美国信息交换标准代码)：是基于拉丁字母的一套电脑编码系统，用于显示现代英语，主要包括控制字符(回车键、退格、换行键等)和可显示字符(英文大小写字符、阿拉伯数字和西文符号)
- 基本的ASCII字符集，使用7位表示一个字符，共128字符。ASCII的扩展字符集使用8位表示一个字符，共256个字符，方便支持欧洲常用字符。是一个系统支持的所有字符的集合，包括各国家文字、标点符号、图形符号、数字等

GBXXX字符集：

- GB2312：简体中文码表。一个小于127的字符的意义与原来相同，但两个大于127的字符连在一起时，就表示一个汉字，这样大约可以组合了包含7000多个简体汉字，此外数学符号、罗马希腊的字母、日文的假名等都编进去了，连在ASCII里本来就有的数字、标点、字母都统统重新编了两个字节长的编码，这就是常说的“全角”字符，而原来在127号以下的那些就叫“半角”字符了
- GBK：最常用的中文码表。是在GB2312标准基础上的扩展规范，使用了双字节编码方案，共收录了21003个汉字，完全兼容GB2312标准，同时支持繁体汉字以及日韩汉字等
- GB18030：最新的中文码表。收录汉字70244个，采用多字节编码，每个字可以由1个、2个或4个字节组成。支持中国国内少数民族的文字，同时支持繁体汉字及日韩汉字等

Unicode字符集：

- 为表达任意语言的任意字符而设计，是业界的一种标准，也称为统一码、标准万国码。它最多使用4个字节的数字来表达每个字母、符号，或者文字。有三种编码方案，UTF-8、UTF-16和UTF32。最为常用的UTF-8编码
- UTF-8编码：可以用来表示Unicode标准中任意字符，它是电子邮件、网页及其他存储或传送文字的应用中，优先采用的编码。互联网工程工作小组(IETF)要求所有互联网协议都必须支持UTF-8编码。它使用一至四个字节为每个字符编码
  - 编码规则：
    - 128个US-ASCII字符，只需一个字节编码
    - 拉丁文等字符，需要二个字节编码
    - 大部分常用字(含中文)，使用三个字节编码
    - 其他极少使用的Unicode辅助字符，使用四字节编码

小结：采用何种规则编码，就要采用对应规则解码，否则就会出现乱码。

**字符串中的编码解码问题**

编码：

- byte[] geBytes()：使用平台的默认字符集将该String编码为一系列字节，将结果存储到新的字节数组中
- byte[] getBytes(String charsetName)：使用指定的字符集将该String编码为一系列字节，将结果存储到新的字节数组中

解码：

- String(byte[] bytes)：通过使用平台的默认字符集解码指定的字节数组来构造新的String
- String(byte[] bytes, String charsetName)：通过指定的字符集解码指定的字节数组来构造新的String

**字符流中的编码解码问题**

字符流抽象基类

- Reader：字符输入流的抽象类
- Writer：字符输出流的抽象类

字符流中和编码解码问题相关的两个类：

- InputStreamReader
- OutputStreamWriter

**字符流写数据的5种方式**

|                  方法名                   |         说明         |
| :---------------------------------------: | :------------------: |
|             void write(int c)             |      写一个字符      |
|          void write(char[] cbuf)          |   写入一个字符数组   |
| void write(char[] cbuf, int off, int len) | 写入字符数组的一部分 |
|          void write(String str)           |     写一个字符串     |
| void write(String str, int off, int len)  | 写一个字符串的一部分 |

| 方法名  |                             说明                             |
| :-----: | :----------------------------------------------------------: |
| flush() |                   刷新流，还可以继续写数据                   |
| close() | 关闭流，释放资源，但是在关闭之前会先刷新流。一旦关闭，就不能再写数据 |

**字符流读数据的2种方式**

|        方法名         |          说明          |
| :-------------------: | :--------------------: |
|      int read()       |   一次读一个字符数据   |
| int read(char[] cbuf) | 一次读一个字符数组数据 |

**字符缓冲流**

字符缓冲流：

- BufferedWriter：将文本写入字符输出流，缓冲字符，以提供单个字符，数组和字符串的高效写入，可以指定缓冲区大小，或者可以接受默认大小。默认值足够大，可用于大多数用途
- BufferedReader：从字符输入流读取文本，缓冲字符，数组和行的高效读取，可以指定缓冲区大小，或者可以使用默认大小。默认值足够大，可用于大多数用途

构造方法：

- BufferedWriter(Writer out)
- BufferedReader(Reader in)

**字符缓冲流的特有功能**

BufferedWriter：

- void newLine()：写一行行分隔符，行分隔符字符串由系统属性定义

BufferedReader：

- public String readLine()：读一行文字。结果包含行的内容的字符串，不包括任何行终止字符，如果流的结尾已经到达，则为null

练习：使用字符缓冲流特有功能来复制Java文件。

```Java
import java.io.*;

public class BufferedStreamDemo1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new FileReader("F:\\JavaProjects\\Demo\\src\\com\\demo_01\\ForDemo.java"));
        BufferedWriter bw = new BufferedWriter(new FileWriter("copy.java"));

        String line;
        while ((line = br.readLine()) != null) {
            bw.write(line);
            bw.newLine();
            bw.flush();
        }

        bw.close();
        br.close();
    }
}
```

**IO流小结**

字节流：字节流可以复制任意文件数据，有4种方式。一般采用字节缓冲流一次读写一个字节数组的方式。

字符流：字符流只能复制文本数据，有5种方式，一般采用字符缓冲流的特有功能。

练习：把ArrayList集合中的字符串数据写入到文本文件。要求：每一个字符串元素作为文件中的一行数据。

```Java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;

public class BufferedStreamDemo1 {
    public static void main(String[] args) throws IOException {
        ArrayList<String> array = new ArrayList<String>();
        array.add("Hello");
        array.add("World");
        array.add("Java");

        BufferedWriter bw = new BufferedWriter(new FileWriter("fos.txt"));
        for (String s : array) {
            bw.write(s);
            bw.newLine();
            bw.flush();
        }

        bw.close();
    }
}
```

练习：把文本文件中的数据读取到集合中，并遍历集合。要求：文件中的每一行数据是一个集合元素。

```Java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;

public class BufferedStreamDemo1 {
    public static void main(String[] args) throws IOException {
        ArrayList<String> array = new ArrayList<String>();
        BufferedReader br = new BufferedReader(new FileReader("fos.txt"));
        
        String line;
        while ((line = br.readLine()) != null) {
            array.add(line);
        }
        br.close();

        for (String s : array) {
            System.out.println(s);
        }
    }
}
```

练习：点名器。有一个文件里面存储了班级同学的姓名，每一个姓名占一行，要求通过程序实现随机点名器。

```Java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.FileReader;
import java.util.ArrayList;
import java.util.Random;

public class FileIODemo {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new FileReader("fos.txt"));
        ArrayList<String> array = new ArrayList<String>();

        String line;
        while ((line = br.readLine()) != null) {
            array.add(line);
        }
        br.close();

        Random r = new Random();
        int index = r.nextInt(array.size());

        String name = array.get(index);
        System.out.println("幸运者是：" + name);
    }
}
```

练习：键盘录入5个学生信息(姓名，语文成绩，数学成绩，英语成绩)。要求按照成绩总分从高到低写入文本文件。

格式：姓名，语文成绩，数学成绩，英语成绩

举例：林青霞，98,99,100

```Java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Comparator;
import java.util.Scanner;
import java.util.TreeSet;

public class FileDemo1 {
    public static void main(String[] args) throws IOException {
        TreeSet<Student> ts = new TreeSet<Student>(new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                int num = o2.getSum() - o1.getSum();
                int num2 = num == 0 ? o1.getChinese() - o2.getChinese() : num;
                int num3 = num2 == 0 ? o1.getMath() - o2.getMath() : num2;
                int num4 = num3 == 0 ? o1.getName().compareTo(o2.getName()) : num3;
                return num4;
            }
        });

        for (int i = 0; i < 5; i++) {
            Scanner sc = new Scanner(System.in);
            System.out.println("请录入第" + (i + 1) + "个学生信息：");
            System.out.println("姓名：");
            String name = sc.nextLine();
            System.out.println("语文成绩：");
            int chinese = sc.nextInt();
            System.out.println("数学成绩：");
            int math = sc.nextInt();
            System.out.println("英语成绩：");
            int english = sc.nextInt();
            Student s = new Student(name, chinese, math, english);
            ts.add(s);
        }

        BufferedWriter bw = new BufferedWriter(new FileWriter("fos.txt"));
        for (Student s : ts) {
            StringBuilder sb = new StringBuilder();
            sb.append(s.getName()).append(",").append(s.getChinese()).append(",").append(s.getMath()).append(",").append(s.getEnglish()).append(",").append(s.getSum());
            bw.write(sb.toString());
            bw.newLine();
            bw.flush();
        }
        bw.close();

    }
}
```

练习：把某一单级文件夹复制到模块目录下。

```Java
import java.io.*;

public class FileDemo2 {
    public static void main(String[] args) throws IOException {
        File srcFolder = new File("C:\\Users\\Administrator\\Desktop\\论文材料");
        String srcFolderName = srcFolder.getName();
        File destFolder = new File(srcFolderName);

        if (!destFolder.exists()) {
            destFolder.mkdir();
        }

        File[] listFiles = srcFolder.listFiles();
        for (File srcFile : listFiles) {
            String srcFileName = srcFile.getName();
            File destFile = new File(destFolder,srcFileName);
            copyFile(srcFile,destFile);
        }

    }

    private static void copyFile(File srcFile, File destFile) throws IOException {
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream(srcFile));
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(destFile));
        byte[] bys = new byte[1024];
        int len;
        while ((len = bis.read(bys)) != -1) {
            bos.write(bys,0,len);
        }
        bos.close();
        bis.close();
    }
}
```

练习：复制多级文件夹。

```Java
import java.io.*;

public class FileDemo3 {
    public static void main(String[] args) throws IOException {
        File srcFile = new File("D:\\一些文档");
        File destFile = new File("F:\\");

        copyFolder(srcFile,destFile);
    }

    private static void copyFolder(File srcFile, File destFile) throws IOException {
        if (srcFile.isDirectory()) {
            String srcFileName = srcFile.getName();
            File newFolder = new File(destFile,srcFileName);
            if (!newFolder.exists()) {
                newFolder.mkdir();
            }

            File[] fileArray = srcFile.listFiles();
            for (File file : fileArray) {
                copyFolder(file,newFolder);
            }
        } else {
            File newFile = new File(destFile,srcFile.getName());
            copyFile(srcFile,newFile);
        }
    }

    private static void copyFile(File srcFile, File destFile) throws IOException {
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream(srcFile));
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(destFile));
        byte[] bys = new byte[1024];
        int len;
        while ((len = bis.read(bys)) != -1) {
            bos.write(bys,0,len);
        }
        bos.close();
        bis.close();
    }
}
```

**复制文件的异常处理**

try...catch...finally的做法是：

```Java
try{
    可能出现异常的代码;
}catch(异常类名 变量名){
    异常的处理代码;
}finally{
    执行所有清除操作;
}
```

JDK7改进方案：

```Java
try(定义流对象){
    可能出现异常的代码;
}catch(异常类名 变量名){
    异常的处理代码;
}

自动释放资源
```

JDK9改进方案：

```Java
定义输入流对象;
定义输出流对象;
try(输入流对象;输出流对象){
    可能出现异常的代码;
}catch(异常类名 变量名){
    异常的处理代码;
}

自动释放资源
```

### 24.5 特殊操作流

**标准输入输出流**

System类中有两个静态的成员变量：

- public static final InputStream in：标准输入流。通常该流对应于键盘输入或由主机环境或用户指定的另一个输入源
- public static final PrintStream out：标准输出流。通常该流对应于显示输出或由主机环境或用户指定的另一个输出目标

自己实现键盘录入数据：

- BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

写起来太麻烦，Java就提供了一个类实现键盘录入

- Scanner sc = new Scanner(System.in);

输出语句的本质：是一个标准的输出流

- PrintStream ps = System.out;
- PrintStream类有的方法，System.out都可以使用

**打印流**

打印流分类：

- 字节打印流：PrintStream
- 字符打印流：PrintWriter

打印流的特点：

- 只负责输出数据，不负责读取数据
- 有自己的特有方法

字节打印流

- PrintStream(String fileName)：使用指定的文件名创建新的打印流
- 使用继承父类的方法写数据，查看的时候会转码；使用自己的特有方法写数据，查看的数据原样输出

字符打印流PrintWriter的构造方法：

|                   方法名                   |                             说明                             |
| :----------------------------------------: | :----------------------------------------------------------: |
|        PrintWriter(String fileName)        | 使用指定的文件名创建一个新的PrintWriter，而不需要自动执行刷新 |
| PrintWriter(Writer out, boolean autoFlush) | 创建一个新的PrintWriter<br />out：字符输出流<br />autoFlush：一个布尔值，如果为真，则println，printf，或format方法将刷新输出缓冲区 |

练习：使用字符打印流来改进复制Java文件的程序。

```Java
import java.io.*;

public class CopyJavaDemo {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new FileReader("F:\\JavaProjects\\Demo\\src\\com\\demo_01\\ForDemo.java"));
        PrintWriter pw = new PrintWriter(new FileWriter("copy.java"),true);

        String line;
        while ((line = br.readLine()) != null) {
            pw.println(line);
        }

        pw.close();
        br.close();

    }
}
```

### 24.6 对象序列化流

对象序列化：就是将对象保存到磁盘中，或者在网络中传输对象。

这种机制就是使用一个字节序列表示一个对象，该字节序列包含：对象的类型、对象的数据和对象中存储的属性等信息。

字节序列写到文件之后，相当于文件中持久保存了一个对象的信息

反之，该字节序列还可以从文件中读取回来，重构对象，对它进行反序列化。

要实现序列化和反序列化就要使用对象序列化流和对象反序列化流：

- 对象序列化流：ObjectOutputStream
- 对象反序列化流：ObjectInputStream

**对象序列化流**

对象序列化流：ObjectOutputStream

- 将Java对象的原始数据类型和图形写入OutputStream。可以使用ObjectInputStream读取(重构)对象。可以通过使用流的文件来实现对象的持久存储。如果流是网络套接字流，则可以在另一个主机上或另一个进程中重构对象。

构造方法：

- ObjectOutputStream(OutputStream out)：创建一个写入指定的OutputStream的ObjectOutputStream

序列化对象的方法：

- void writeObject(Object obj)：将指定的对象写入ObjectOutputStream

注意：

- 一个对象要想被序列化，该对象所属的类必须必须实现Serializable接口
- Serializable是一个标记接口，实现该接口，不需要重写任何方法

对象反序列化流：ObjectInputStream

- ObjectInputStream反序列化先前使用ObjectOutputStream编写的原始数据和对象

构造方法：

- ObjectInputStream(InputStream in)：创建从指定的InputStream读取的ObjectInputStream

反序列化对象的方法：

- Object readObject()：从ObjectInputStream读取一个对象

**对象序列化流的一些问题**

用对象序列化流序列化了一个对象后，加入我们修改了对象所属的类文件，读取数据会不会出问题呢？

- 会出问题，抛出InvalidClassException异常

如果出问题了，如何解决呢？

- 给对象所属的类加一个serialVersionUID
  - public static final long serialVersionUID = 42L;

若果一个对象中的某个成员变量的值不想被序列化，又该如何实现呢？

- 给该成员变量加transient关键字修饰，该关键字标记的成员变量不参与序列化过程

### 24.7 Properties

**Properties概述**

- 是一个Map体系的集合类
- Properties可以保存到流中或从流中加载

**Properties作为集合的特有方法**

|                    方法名                    |                             说明                             |
| :------------------------------------------: | :----------------------------------------------------------: |
| Object setProperty(String key, String value) |  设置集合的键和值，都是String类型，底层调用Hashtable方法put  |
|        String getProperty(String key)        |               使用此属性列表中指定的键搜索属性               |
|      Set\<String> stringPropertyNames()      | 从该属性列表中返回一个不可修改的键集，其中键及其对应的值是字符串 |

**Properties和IO流结合的方法**

|                    方法名                     |                             说明                             |
| :-------------------------------------------: | :----------------------------------------------------------: |
|        void load(InputStream inStream)        |             从输入字节流读取属性列表(键和元素对)             |
|           void load(Reader reader)            |             从输入字符流读取属性列表(键和元素对)             |
| void store(OutputStream out, String comments) | 将此属性列表(键和元素对)写入此Properties表中，以适合于使用load(InputStream)方法的格式写入输出字节流 |
|  void store(Writer writer, String comments)   | 将此属性列表(键和元素对)写入此Properties表中，以适合于使用load(Reader)方法的格式写入输出字符流 |

```Java
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Properties;

public class PropertiesDemo1 {
    public static void main(String[] args) throws IOException {
        myStore();
        myLoad();
    }

    private static void myLoad() throws IOException {
        Properties prop = new Properties();

        FileReader fr = new FileReader("fos.txt");
        prop.load(fr);
        fr.close();
        System.out.println(prop);
    }

    private static void myStore() throws IOException {
        Properties prop = new Properties();
        prop.setProperty("itahu001","林青霞");
        prop.setProperty("itahu002","张曼玉");
        prop.setProperty("itahu003","王祖贤");

        FileWriter fw = new FileWriter("fos.txt");
        prop.store(fw,null);
        fw.close();
    }
}
```

练习：请写程序实现猜数字小游戏，只能玩三次，如果还想玩，提示：游戏试玩已结束，想玩请充值。

fos.txt文件初始内容为：count=0

```Java
// GuessNumber.java
import java.util.Random;
import java.util.Scanner;

public class GuessNumber {
    public GuessNumber() {
    }

    public static void start() {
        Random r = new Random();
        int number = r.nextInt(100) + 1;

        while (true) {
            Scanner sc = new Scanner(System.in);

            System.out.println("请输入你要猜的数字：");
            int guessNumber = sc.nextInt();

            if (guessNumber > number) {
                System.out.println("你猜的数字" + guessNumber + "大了");
            } else if (guessNumber < number) {
                System.out.println("你猜的数字" + guessNumber + "小了");
            } else {
                System.out.println("恭喜猜中了！");
                break;
            }
        }
    }
}
```

```Java
// Game.java
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Properties;

public class Game {
    public static void main(String[] args) throws IOException {
        Properties prop = new Properties();

        FileReader fr = new FileReader("fos.txt");
        prop.load(fr);
        fr.close();

        String count = prop.getProperty("count");
        int number = Integer.parseInt(count);

        if (number >= 3) {
            System.out.println("游戏已结束，想玩请充值(www.baidu.com)");
        } else {
            GuessNumber.start();
            number++;
            prop.setProperty("count",String.valueOf(number));
            FileWriter fw = new FileWriter("fos.txt");
            prop.store(fw,null);
            fw.close();
        }

    }
}
```

## 25. 多线程

### 25.1 实现多线程

**进程**

进程：是正在运行的程序

- 是系统进行资源分配和调用的独立单位
- 每一个进程都有它自己的内存空间和系统资源

**线程**

线程：是进程中的单个顺序控制流，是一条执行路径

- 单线程：一个进程如果只有一条执行路径，则称为单线程程序
- 多线程：一个进程如果有多条执行路径，则称为多线程程序

举例：

- 记事本程序
- 扫雷程序

**多线程的实现方式**

方式一：继承Thread类

- 定义一个类MyThread继承Thread类
- 在MyThread类中重写run()方法
- 创建MyThread类的对象
- 启动线程

两个小问题：

- 为什么要重写run()方法？
  - 因为run()是用来封装被线程执行的代码
- run()方法和start()方法的区别？
  - run()：封装线程执行的代码，直接调用，相当于普通方法的调用
  - start()：启动线程；然后由JVM调用此线程的run()方法

**设置和获取线程名称**

Thread类中设置和获取线程名称的方法

- void setName(String name)：将此线程的名称更改为等于参数name
- String getName()：返回此线程的名称
- 通过构造方法也可以设置线程名称

如何获取main()方法所在的线程名称？

- public static Thread currentThread()：返回对当前正在执行的线程对象的引用

**线程调度**

线程有两种调度模型

- 分时调度模型：所有线程轮流使用CPU的使用权，平均分配每个线程占用CPU的时间片
- 抢占式调度模型：优先让优先级高的线程使用CPU，如果线程的优先级相同，那么会随机选择一个，优先级高的线程获取的CPU时间片相对多一些

Java使用的是抢占式调度模型。

假如计算机只有一个CPU，那么CPU在某一时刻只能执行一条指令，线程只有得到CPU的时间片，也就是使用权，才可以执行指令。所以说多线程程序的执行是有随机性，因为谁抢到CPU的使用权是不一定的。

Thread类中设置和获取线程优先级的方法：

- public final int getPriority()：返回此线程的优先级
- public final void setPriority(int newPriority)：更改此线程的优先级

线程默认优先级是5；线程优先级的范围是：1-10。线程优先级高仅仅表示线程获取的CPU时间片的几率高，但是要在次数比较多，或者多次运行的时候才能看到你想要的效果。

**线程控制**

|             方法名             |                             说明                             |
| :----------------------------: | :----------------------------------------------------------: |
| static void sleep(long millis) |        使当前正在执行的线程停留(暂停执行)指定的毫秒数        |
|          void join()           |                       等待这个线程死亡                       |
|   void setDaemon(boolean on)   | 将此线程标记为守护线程，当运行的线程都是守护线程时，Java虚拟机将退出 |

**多线程的实现方式**

方式二：实现Runnable接口

- 定义一个类MyRunnable实现Runnable接口
- 在MyRunnable类中重写run()方法
- 创建MyRunnable类的对象
- 创建Thread类的对象，把MyRunnable对象作为构造方法的参数
- 启动线程

多线程的实现方案有两种

- 继承Thread类
- 实现Runnable接口

相比继承Thread类，实现Runnable接口的好处

- 避免了Java单继承的局限性
- 适合多个相同程序的代码去处理同一个资源的情况，把线程和程序的代码、数据有效分离，较好的体现了面向对象的设计思想

### 25.2 线程同步

练习：某电影院目前正在上映国产大片，共有100张票，而它有3个窗口卖票，请设计一个程序模拟该电影院卖票。

```Java
public class SellTicket implements Runnable {
    private int tickets = 100;
    @Override
    public void run() {
        while (true) {
            if (tickets > 0) {
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread().getName() + "正在出售第" + tickets + "张票");
                tickets--;
            }
        }
    }
}

public class SellTicketDemo {
    public static void main(String[] args) {
        SellTicket st = new SellTicket();

        Thread t1 = new Thread(st,"窗口1");
        Thread t2 = new Thread(st,"窗口2");
        Thread t3 = new Thread(st,"窗口3");

        t1.start();
        t2.start();
        t3.start();
    }
}
```

思考：在出售一张票的时候，需要一点时间的延迟，用sleep()方法实现。

卖票出现了问题

- 相同的票出现了多次
- 出现了负数的票

问题原因：

- 线程执行的随机性导致的

**卖票案例数据安全问题的解决**

为什么出现问题？(这也是我们判断多线程程序是否会有数据安全问题的标准)

- 是否是多线程环境
- 是否有共享数据
- 是否有多条语句提供共享数据

如何解决多线程安全问题呢？

- 基本思想：让程序没有安全问题的环境

怎么实现呢？

- 把多条语句操作共享数据的代码锁起来，让任意时刻只能有一个线程执行即可
- Java提供了同步代码块的方式来解决

**同步代码块**

锁多条语句操作共享数据，可以使用同步代码块实现

格式：

```Java
synchronized(任意对象){
    多条语句操作共享数据的代码
}
```

- synchronized(任意对象)：就相当于给代码加锁了，任意对象就可以看成是一把锁

同步的好处和弊端

- 好处：解决了多线程的数据安全问题
- 弊端：当线程很多时，因为每个线程都会去判断同步上的锁，这是很耗资源的，无形中会降低程序的运行效率

**同步方法**

同步方法：就是把synchronized关键字加到方法上

- 格式：
  - 修饰符 synchronized 返回值类型 方法名(方法参数){ }

同步方法的锁对象是什么呢？

- this

同步静态方法：就是把synchronized关键字加到静态方法上

- 格式：修饰符 static synchronized 返回值类型 方法名(方法参数){ }

同步静态方法的锁对象是什么呢？

- 类名.class

**线程安全的类**

StringBuffer

- 线程安全，可变的字符序列
- 从版本JDK5开始，被StringBuild替代。通常应该使用StringBuild类，因为它支持所有相同的操作，但它更快，因为它不执行同步

Vector

- 从Java 2平台v1.2 开始，该类改进了List接口，使其成为Java Collections Framework的成员。与新的集合实现不同，Vector被同步。如果不需要线程安全的实现，建议使用ArrayList代替Vector

Hashtable

- 该类实现了一个哈希表，它将键映射到值。任何非null对象都可以用作键或者值
- 从Java 2平台v1.2 开始，该类进行了改进，实现了Map接口，使其成为Java Collections Framework的成员。与新的集合实现不同，Hashtable被同步。如果不需要线程安全的实现，建议使用HashMap代替Hashtable

**Lock锁**

虽然我们可以理解同步代码块和同步方法的锁对象问题，但是我们并没有直接看到在哪里加上了锁，在哪里释放了锁，为了更清晰的表达如何加锁和释放锁，JDK5以后提供了一个新的锁对象Lock。

Lock实现提供比使用synchronized方法和语句可以获得更广泛的锁定操作。

Lock中提供了获得锁和释放锁的方法。

- void lock()：获得锁
- void unlock()：释放锁

Lock是接口，不能直接实例化，这里采用它的实现类ReentrantLock来实例化

ReentrantLock的构造方法

- ReentrantLock()：创建一个ReentrantLock的实例

**生产者消费者**

生产者消费者模式是一个十分经典的多线程协作的模式，弄懂生产者消费者问题就能够让我们对多线程编程的理解更加深刻。

所谓生产者消费者问题，实际上主要是包含了两类数据：

- 一类是生产者线程用于生产数据
- 一类是消费者线程用于消费数据

为了解耦生产者和消费者的关系，通常会采用共享的数据区域，就像是一个仓库

- 生产者生产数据之后直接放置在共享数据区中，并不需要关心消费者的行为
- 消费者只需要从共享数据区中获取数据，并不需要关心生产者的行为

为了体现生产和消费过程中的等待和唤醒，Java就提供了几个方法供我们使用，这几个方法在Object类中

Object类的等待和唤醒方法：

|      方法名      |                             说明                             |
| :--------------: | :----------------------------------------------------------: |
|   void wait()    | 导致当前线程等待，直到另一个线程调用该对象的notify()方法或notifyAll()方法 |
|  void notify()   |               唤醒正在等待对象监视器的单个线程               |
| void notifyAll() |               唤醒正在等待对象监视器的所有线程               |

生产者消费者案例中包含的类：

- 奶箱类(Box)：定义一个成员变量，表示第x瓶奶，提供存储牛奶和获取牛奶的操作
- 生产者类(Producer)：实现Runnable接口，重写run()方法，调用存储牛奶的操作
- 消费者类(Customer)：实现Runnable接口，重写run()方法，调用获取牛奶的操作
- 测试类(BoxDemo)：里面有main方法

```Java
public class Box {
    private int milk;
    private boolean state = false;

    public synchronized void put(int milk) {
        if (state) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }


        this.milk = milk;
        System.out.println("送奶工将第" + this.milk + "瓶奶放入奶箱");

        state = true;
        notifyAll();
    }

    public synchronized void get() {
        if (!state) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        System.out.println("用户拿到第" + this.milk + "瓶奶");

        state = false;
        notifyAll();
    }
}
```

```Java
public class Producer implements Runnable {
    private Box b;

    public Producer(Box b) {
        this.b = b;
    }

    @Override
    public void run() {
        for (int i = 1; i <= 30; i++) {
            b.put(i);
        }
    }
}
```

```Java
public class Customer implements Runnable {
    private Box b;

    public Customer(Box b) {
        this.b = b;
    }

    @Override
    public void run() {
        while (true) {
            b.get();
        }
    }
}
```

```Java
public class BoxDemo {
    public static void main(String[] args) {
        Box b = new Box();
        Producer p = new Producer(b);
        Customer c = new Customer(b);

        Thread t1 = new Thread(p);
        Thread t2 = new Thread(c);

        t1.start();
        t2.start();
    }
}
```

## 26. 网络编程

### 26.1 网络编程入门

**网络编程概述**

计算机网络

- 是指将地理位置不同的具有独立功能的多台计算机及其外部设备，通过通信线路连接起来，在网络操作系统，网络管理软件及网络通信协议的管理和协调下，实现资源共享和信息传递的计算机系统

网络编程

- 在网络通信协议下，实现网络互连的不同计算机上运行的程序间可以进行数据交换

**网络编程三要素**

IP地址

- 要想让网络中的计算机能够互相通信，必须为每台计算机指定一个标识号，通过这个标识号来指定要接收数据的计算机和识别发送的计算机，而IP地址就是这个标识号。也就是设备的标识

端口

- 网络的通信，本质上是两个应用程序的通信。每台计算机都有很多的应用程序，那么在网络通信时，如何区分这些应用程序呢？如果说IP地址可以唯一标识网络中的设备，那么端口号就可以唯一标识设备中的应用程序了。也就是应用程序的标识

协议

- 通过计算机网络可以使多台计算机实现连接，位于同一个网络中的计算机在进行连接和通信时需要遵守一定的规则，这就好比在道路中行驶的汽车一定要遵守交通规则一样。在计算机网络中，这些连接和通信的规则被称为网络通信协议，它对数据的传输格式、传输速率、传输步骤等做了统一规定，通信双方必须同时遵守才能完成数据交换，常见的协议有UDP协议和TCP协议

**IP地址**

IP地址：是网络中设备的唯一标识

IP地址分为两大类

- IPv4：是给每个连接在网络上的主机分配一个32bit地址。根据TCP/IP规定，IP地址用二进制表示，每个IP地址长32bit，也就是4个字节。例如一个采用二进制形式的IP地址是“11000000 10101000 00000001 01000010”，这么长的地址，处理起来也太费劲了。为了方便使用，IP地址经常被写成十进制的形式，中间使用符号“.”分隔不同的字节。于是，上面的IP地址可以表示为“192.168.1.66”。IP地址的这种表示法叫做“点分十进制表示法”，这显然比1和0容易记忆得多
- IPv6：由于互联网的蓬勃发展，IP地址的需求量越来越大，但是网络地址资源有限，使得IP的分配越发紧张。为了扩大地址空间，通过IPv6重新定义地址空间，采用128位地址长度，每16位一组，分成8组16进制数，这样就解决了网络地址资源数量不够的问题

常用命令：

- ipconfig：查看本机IP地址
- ping IP地址：检查网络是否连通

特殊IP地址：

- 127.0.0.1：是回送地址，可以代表本机地址，一般用来测试使用

**InetAddress的使用**

为了方便我们对IP地址的获取和操作，Java提供了一个类InetAddress供我们使用

InetAddress：此类表示Internet协议(IP)地址

|                  方法名                   |                             说明                             |
| :---------------------------------------: | :----------------------------------------------------------: |
| static InetAddress getByName(String host) | 确定主机名称的IP地址。主机名称可以是机器名称，也可以是IP地址 |
|           String getHostName()            |                     获取此IP地址的主机名                     |
|          String getHostAddress()          |                 返回文本显示中的IP地址字符串                 |

**端口**

端口：设备上应用程序的唯一标识

端口号：用两个字节标识的整数，它的取值范围是0 ~ 65535。其中，0 ~ 1023之间的端口号用于一些知名的网络服务和应用，普通的应用程序需要使用1024以上的端口号。如果端口号被另外一个服务或应用所占用，会导致当前程序启动失败

**协议**

协议：计算进网络中，连接和通信的规则被称为网络通信协议

UDP协议

- 用户数据报协议(User Datagram Protocol)

- UDP是无连接通信协议，即在数据传输时，数据的发送端和接收端不建立逻辑连接。简单来说，当一台计算机向另外一台计算机发送数据时，发送端不会确认接收端是否存在，就会发出数据，同样接收端在收到数据时，也不会向发送端反馈是否收到数据

  由于使用UDP协议消耗资源小，通信效率高，所以通常都会用于音频、视频和普通数据的传输

- 例如视频会议通常采用UDP协议，因为这种情况即使偶尔丢失一两个数据包，也不会对接收结果产生太大影响。但是在使用UDP协议传送数据时，由于UDP的面向无连接性，不能保证数据的完整性，因此在传输重要数据时不建议使用UDP协议

TCP协议

- 传输控制协议(Transmission Control Protocol)
- TCP协议是面向连接的通信协议，即传输数据之前，在发送端和接收端建立逻辑连接，然后再传输数据，它提供了两台计算机之间可靠无差错的数据传输。在TCP连接中必须要明确客户端和服务器端，由客户端向服务器端发出连接请求，每次连接的创建都需要经过“三次握手”
- 三次握手：TCP协议中，在发送数据的准备阶段，客户端和服务器之间的三次交互，以保证连接的可靠
  - 第一次握手，客户端向服务器端发出连接请求，等待服务器确认
  - 第二次握手，服务器端向客户端回送一个响应，通知客户端接收到了连接请求
  - 第三次握手，客户端再次向服务器端发送确认消息，确认连接
- 完成三次握手，连接建立后，客户端和服务器就可以开始进行数据传输了。由于这种面向连接的特性，TCP协议可以保证传输数据的安全，所以应用十分广泛。例如上传文件、下载文件、浏览网页等

### 26.2 UDP通信程序

**UDP通信原理**

UDP协议是一种不可靠的网络协议，它在通信的两端各建立一个Socket对象，但是这两个Socket只是发送，接收数据的对象

因此对于基于UDP协议的通信双方而言，没有所谓的客户端和服务器的概念

Java提供了DatagramSocket类作为基于UDP协议的Socket

**UDP发送数据**

发送数据的步骤

1. 创建发送端的Socket对象(DatagramSocket)

   DatagramSocket()

2. 创建数据，并把数据打包

   DatagramPacket(byte[] buf, int length, InetAddress address, int port)

3. 调用DatagramSocket对象的方法发送数据

   void send(DatagramPacket p)

4. 关闭发送端

   void close()

**UDP接收数据**

接收数据的步骤

1. 创建接收端的Socket对象(DatagramSocket)

   DatagramSocket(int port)

2. 创建一个数据包，用于接收数据

   DatagramPacket(byte[] buf, int length)

3. 调用DatagramSocket对象的方法接收数据

   void receive(DatagramPacket p)

4. 解析数据包，并把数据在控制台显示

   byte[] getData()

   int getLength()

5. 关闭接收端

   void close()

练习：按照下面的要求实现程序

- UDP发送数据：数据来自于键盘录入，直到输入的数据是886，发送数据结束
- UDP接收数据：因为接收端不知道发送端什么时候停止发送，故采用死循环接收

```Java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.*;

public class SendDemo {
    public static void main(String[] args) throws IOException {
        DatagramSocket ds = new DatagramSocket();

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String line;
        while ((line = br.readLine()) != null) {
            if ("886".equals(line)) {
                break;
            }

            byte[] bys = line.getBytes();
            DatagramPacket dp = new DatagramPacket(bys,bys.length, InetAddress.getByName("10.100.159.140"),12345);

            ds.send(dp);
        }
        ds.close();
    }
}
```

```Java
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;

public class ReceiveDemo {
    public static void main(String[] args) throws IOException {
        DatagramSocket ds = new DatagramSocket(12345);

        while (true) {
            byte[] bys = new byte[1024];
            DatagramPacket dp = new DatagramPacket(bys, bys.length);

            ds.receive(dp);

            System.out.println("数据是：" + new String(dp.getData(), 0, dp.getLength()));
        }
    }
}
```

### 26.3 TCP通信程序

**TCP通信原理**

TCP通信协议是一种可靠的网络协议，它在通信的两端各建立一个Socket对象，从而在通信的两端形成网络虚拟链路，一旦建立了虚拟的网络链路，两端的程序就可以通过虚拟链路进行通信

Java对基于TCP协议的网络提供了良好的封装，使用Socket对象来代表两端的通信端口，并通过Socket产生IO流来进行网络通信

Java为客户端提供了Socket类，为服务器端提供了ServerSocket类

**TCP发送数据**

发送数据的步骤

1. 创建客户端的Socket对象(Socket)

   Socket(String host, int port);

2. 获取输出流，写数据

   OutputStream getOutputStream()

3. 释放资源

   void close()

**TCP接受数据**

接收数据的步骤

1. 创建服务器端的Socket对象(ServerSocket)

   ServerSocket(int port)

2. 监听客户端连接，返回一个Socket对象

   Socket accept()

3. 获取输入流，读数据，并把数据显示在控制台

   InputStream getInputStream()

4. 释放资源

   void close()

练习1：

- 客户端：发送数据，接收服务器反馈
- 服务器：接收数据，给出反馈

```Java
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.Socket;

public class ClientDemo {
    public static void main(String[] args) throws IOException {
        Socket s = new Socket("10.100.159.140",10000);

        OutputStream os = s.getOutputStream();
        os.write("hello,tcp,我来了".getBytes());

        InputStream is = s.getInputStream();
        byte[] bys = new byte[1024];
        int len = is.read(bys);
        String data = new String(bys,0,len);
        System.out.println("客户端：" + data);

        s.close();
    }
}
```

```Java
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerDemo {
    public static void main(String[] args) throws IOException {
        ServerSocket ss = new ServerSocket(10000);

        Socket s = ss.accept();

        InputStream is = s.getInputStream();
        byte[] bys = new byte[1024];
        int len = is.read(bys);
        String data = new String(bys,0,len);
        System.out.println("服务器：" + data);

        OutputStream os = s.getOutputStream();
        os.write("数据已经收到".getBytes());

        ss.close();
    }
}
```

练习2：客户端接收数据来自于键盘录入

```Java
import java.io.*;
import java.net.Socket;

public class ClientDemo {
    public static void main(String[] args) throws IOException {
        Socket s = new Socket("10.100.159.140",10000);

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
        String line;
        while ((line = br.readLine()) != null) {
            if ("886".equals(line)) {
                break;
            }
            bw.write(line);
            bw.newLine();
            bw.flush();
        }
        s.close();
    }
}
```

```Java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerDemo {
    public static void main(String[] args) throws IOException {
        ServerSocket ss = new ServerSocket(10000);

        Socket s = ss.accept();

        BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
        String line;
        while ((line = br.readLine()) != null) {
            System.out.println(line);
        }
        ss.close();
    }
}
```

练习3：服务器端将接收数据写入文本文件(练习2基础上更改服务器端代码即可)

```Java
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerDemo {
    public static void main(String[] args) throws IOException {
        ServerSocket ss = new ServerSocket(10000);

        Socket s = ss.accept();

        BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
        BufferedWriter bw = new BufferedWriter(new FileWriter("fos.txt"));
        String line;
        while ((line = br.readLine()) != null) {
            bw.write(line);
            bw.newLine();
            bw.flush();
        }
        bw.close();
        ss.close();
    }
}
```

练习4：客户端数据来自于文本文件(在练习3基础上更改客户端代码即可)

```Java
import java.io.*;
import java.net.Socket;

public class ClientDemo {
    public static void main(String[] args) throws IOException {
        Socket s = new Socket("10.100.159.140",10000);

        BufferedReader br = new BufferedReader(new FileReader("C:\\Users\\Administrator\\Desktop\\窗里窗外.txt"));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
        String line;
        while ((line = br.readLine()) != null) {
            bw.write(line);
            bw.newLine();
            bw.flush();
        }
        br.close();
        s.close();
    }
}
```

练习5：上传文件后服务器给出相应反馈

```Java
import java.io.*;
import java.net.Socket;

public class ClientDemo {
    public static void main(String[] args) throws IOException {
        Socket s = new Socket("10.100.159.140",10000);

        BufferedReader br = new BufferedReader(new FileReader("C:\\Users\\Administrator\\Desktop\\窗里窗外.txt"));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
        String line;
        while ((line = br.readLine()) != null) {
            bw.write(line);
            bw.newLine();
            bw.flush();
        }

        s.shutdownOutput();

        BufferedReader brClient = new BufferedReader(new InputStreamReader(s.getInputStream()));
        String data = brClient.readLine();
        System.out.println("服务器的反馈：" + data);

        br.close();
        s.close();
    }
}
```

```Java
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerDemo {
    public static void main(String[] args) throws IOException {
        ServerSocket ss = new ServerSocket(10000);

        Socket s = ss.accept();

        BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
        BufferedWriter bw = new BufferedWriter(new FileWriter("fos.txt"));
        String line;
        while ((line = br.readLine()) != null) {
            bw.write(line);
            bw.newLine();
            bw.flush();
        }

        BufferedWriter bwServer = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
        bwServer.write("文件上传成功");
        bwServer.newLine();
        bwServer.flush();

        bw.close();
        ss.close();
    }
}
```

练习6：

- 客户端：数据来自于文本文件，接收服务器反馈
- 服务器：接收到的数据写入文本文件，给出反馈，代码用线程进行封装，为每一个客户端开启一个线程

客户端代码无需更改，需更改服务器端代码和增加多线程实现类

```Java
import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerDemo {
    public static void main(String[] args) throws IOException {
        ServerSocket ss = new ServerSocket(10000);

        while (true) {
            Socket s = ss.accept();
            new Thread(new ServerThread(s)).start();
        }
    }
}
```

```Java
import java.io.*;
import java.net.Socket;

public class ServerThread implements Runnable {
    private Socket s;

    public ServerThread(Socket s) {
        this.s = s;
    }

    @Override
    public void run() {
        try {
            BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
            int count = 0;
            File file = new File("fos[" + count + "].txt");
            while (file.exists()) {
                count++;
                file = new File("fos[" + count + "].txt");
            }
            BufferedWriter bw = new BufferedWriter(new FileWriter(file));

            String line;
            while ((line = br.readLine()) != null) {
                bw.write(line);
                bw.newLine();
                bw.flush();
            }

            BufferedWriter bwServer = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
            bwServer.write("文件上传成功");
            bwServer.newLine();
            bwServer.flush();

            s.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

注：启动多个客户端出现了Connection reset异常，暂不知道原因。

## 27. Lambda表达式

**函数式编程思想概述**

在数学中，函数就是有输入量、输出量的一套计算方案，也就是“拿数据做操作”

面向对象思想强调“必须通过对象的形式来做事情”

函数式思想则尽量忽略面向对象的复杂语法：“强调做什么，而不是以什么形式去做”

而我们要学习的Lambda表达式就是函数式思想的体现

**Lambda表达式的标准格式**

```Java
// 匿名内部类方式的代码分析
new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("多线程程序启动了");
            }
        }).start();
```

匿名内部类中重写run()方法的代码分析

- 方法形式参数为空，说明调用方法时不需要传递参数
- 方法返回值类型为void，说明方法执行没有结果返回
- 方法体中的内容，是我们具体要做的事

```Java
// Lambda表达式的代码分析
new Thread(() -> {
            System.out.println("多线程程序启动了");
        }).start();
```

Lambda表达式的代码分析

- ()：里面没有内容，可以看成是方法形式参数为空
- ->：用箭头指向后面要做的事情
- {}：包含一段代码，我们称之为代码块，可以看成是方法体中的内容

组成Lambda表达式的三要素：形式参数、箭头、代码块

Lambda表达式的格式

- 格式：(形式参数) -> {代码块}
- 形式参数：如果有多个参数，参数之间用逗号隔开；如果没有参数，留空即可
- ->：由英文中画线和大于符号组成，固定写法。代表指向动作
- 代码块：使我们具体要做的事情，也就是以前我们写的方法内容

练习：

- 定义一个接口(Addable)，里面定义一个抽象方法：int add(int x, int y);
- 定义一个测试类(AddableDemo)，在测试类中提供两个方法
  - 一个方法是：useAddable(Addable a)
  - 一个方法是主方法，在主方法中调用useAddable方法

```Java
public interface Addable {
    int add(int x, int y);
}
```

```Java
public class AddableDemo {
    public static void main(String[] args) {
        useAddable((int x, int y) -> {
            return x + y;
        });
    }

    private static void useAddable(Addable a) {
        int sum = a.add(10, 20);
        System.out.println(sum);
    }
}
```

**Lambda表达式的省略模式**

省略规则：

- 参数类型可以省略。但是有多个参数的情况下，不能只省略一个
- 如果参数有且仅有一个，那么小括号可以省略
- 如果代码块的语句只有一条，可以省略大括号和分号，甚至是return

**Lambda表达式的注意事项**

注意事项：

- 使用Lambda必须要有接口，并且要求接口中有且仅有一个抽象方法
- 必须有上下文环境，才能推导出Lambda对应的接口
  - 根据局部变量的赋值得知Lambda对应的接口：Runnable = () -> System.out.println("Lambda表达式");
  - 根据调用方法的参数得知Lambda对应的接口：new Thread(() -> System.out.println("Lambda表达式")).start()；

**Lambda表达式和匿名内部类的区别**

所需类型不同

-  匿名内部类：可以是接口，也可以是抽象类，还可以是具体类
- Lambda表达式：只能是接口

使用限制不同

- 如果接口中有且仅有一个抽象方法，可以使用Lambda表达式，也可以使用匿名内部类
- 如果接口中多于一个抽象方法，只能使用匿名内部类，而不能使用Lambda表达式

实现原理不同

- 匿名内部类：编译之后，产生一个单独的.class字节码文件
- Lambda表达式：编译之后，没有一个单独的.class字节码文件。对应的字节码会在运行的时候动态生成

## 28. 接口组成更新

### 28.1 接口组成更新概述

接口的组成

- 常量
  - public static final
- 抽象方法
  - public abstract
- 默认方法(Java 8)
- 静态方法(Java 8)
- 私有方法(Java 9)

**接口中默认方法**

接口中默认方法的定义格式：

- 格式：public default 返回值类型 方法名(参数列表){ }
- 范例：public default void show3(){ }

接口中默认方法的注意事项：

- 默认方法不是抽象方法，所以不强制被重写。但是可以被重写，重写的时候去掉default关键字
- public可以省略，default不能省略

**接口中静态方法**

接口中静态方法的定义格式：

- 格式：public static 返回值类型 方法名(参数列表){ }
- 范例：public static void show(){ }

接口中静态方法的注意事项：

- 静态方法只能通过接口名调用，不能通过实现类名或者对象名调用
- public可以省略，static不能省略

**接口中私有方法**

Java 9中新增了带方法体的私有方法，这其实在Java 8中就埋下了伏笔：Java 8允许在接口中定义带方法体的默认方法和静态方法。这样可能会引发一个问题：当两个默认方法或者静态方法中包含一段相同的代码实现时，程序必然考虑将这段实现代码抽取成一个共性方法，而这个共性方法是不需要让别人使用的，因此用私有给隐藏起来，这就是Java 9增加私有方法的必然性

接口中私有方法的定义格式：

- 格式1：private 返回值类型 方法名(参数列表){ }
- 范例1：private void show(){ }
- 格式2：private static 返回值类型 方法名(参数列表){ }
- 范例2：private static void method(){ }

接口中私有方法的注意事项：

- 默认方法可以调用私有的静态方法和非静态方法
- 静态方法只能调用私有的静态方法

### 28.2 函数式接口

**函数式接口概述**

函数式接口：有且仅有一个抽象方法的接口

Java中的函数式编程体现就是Lambda表达式，所以函数式接口即使可以适用于Lambda使用的接口

只有确保接口中有且仅有一个抽象方法，Java中的Lambda才能顺利地进行推导

如何检测一个接口是不是函数式接口呢？

- @FunctionalInterface
- 放在接口定义的上方：如果接口是函数式接口，编译通过；如果不是，编译失败

注意：我们自己定义函数式接口的时候，@FunctionalInterface是可选的，就算我不写这个注解，只要保证满足函数式接口定义的条件，也照样是函数式接口。但是，建议加上该注解

**函数式接口作为方法的参数**

如果方法的参数是一个函数式接口，我们可以使用Lambda表达式作为参数传递

- startThread(() -> System.out.println(Thread.currentThread().getName() + "线程启动了"))

**函数式方法作为方法的返回值**

如果方法的返回值是一个函数式接口，我们可以使用Lambda表达式作为结果返回

- private static Comparator<String> getComparator() {
          return (o1, o2) -> o1.length() - o2.length();
      }

**常用的函数式接口**

Java 8在java.util.function包下预定义了大量的函数式接口供我们使用，我们重点来学习下面的4个接口

- Supplier接口
- Consumer接口
- Predicate接口
- Function接口

**Supplier接口**

Supplier\<T>：包含一个无参的方法

- T get()：获得结果
- 该方法不需要参数，它会按照某种实现逻辑(由Lambda表达式实现)返回一个数据
- Supplier\<T>接口也被称为生产型接口，如果我们指定了接口的泛型是什么类型，那么接口中的get方法就会生产什么类型的数据供我门使用

练习：利用Supplier接口求数组中的最大值。

```Java
import java.util.function.Supplier;

public class SupplierTest {
    public static void main(String[] args) {
        int[] arr = {19,50,28,37,46};

        int maxValue = getMax(() -> {
            int max = arr[0];
            for (int i = 1; i < arr.length; i++) {
                if (arr[i] > max) {
                    max = arr[i];
                }
            }
            return max;
        });

        System.out.println(maxValue);
    }

    private static int getMax(Supplier<Integer> sup) {
        return sup.get();
    }
}
```

**Consumer接口**

Consumer\<T>：包含两个方法

- void accept(T t)：对给定的参数执行此操作
- default Consumer\<T> andThen(Consumer after)：返回一个组合的Consumer，依次执行此操作，然后执行after操作
- Consumer\<T>接口也被称为消费型接口，它消费的数据的数据类型由泛型指定

练习：利用Consumer按格式遍历打印数组

```Java
import java.util.function.Consumer;

public class ConsumerTest {
    public static void main(String[] args) {
        String[] strArray = {"林青霞，30", "张曼玉，35", "王祖贤，33"};

        printInfo(strArray,s -> System.out.print("姓名：" + s.split("，")[0]),s -> System.out.println("，年龄：" + s.split("，")[1]));
    }

    private static void printInfo(String[] strArray, Consumer<String> con1, Consumer<String> con2) {
        for (String str : strArray) {
            con1.andThen(con2).accept(str);
        }
    }
}
```

**Predicate接口**

Predicate\<T>：常用的四个方法

- boolean test(T t)：对给定的参数进行判断(判断逻辑是由Lambda表达式实现)，返回一个布尔值
- default Predicate\<T> negate()：返回一个逻辑的否定，对应逻辑非
- default Predicate\<T> and(Predicate other)：返回一个组合判断，对应短路与
- default Predicate\<T> or(Predicate other)：返回一个组合判断，对应短路或
- Predicate\<T>接口通常用于判断参数是否满足指定的条件

小练习

```Java
import java.util.function.Predicate;

public class PredicateDemo1 {
    public static void main(String[] args) {
        boolean b1 = checkString("hello",s -> s.length() > 8);
        System.out.println(b1);

        boolean b2 = checkString("helloworld",s -> s.length() > 8);
        System.out.println(b2);

        boolean b3 = checkString("hello",s -> s.length() > 8,s -> s.length() < 15);
        System.out.println(b3);

        boolean b4 = checkString("helloworld",s -> s.length() > 8,s -> s.length() < 15);
        System.out.println(b4);
    }

    private static boolean checkString(String s, Predicate<String> pre1, Predicate<String> pre2) {
//        boolean b1 = pre1.test(s);
//        boolean b2 = pre2.test(s);
//        boolean b = b1 && b2;
//        return b;
        
//        return pre1.and(pre2).test(s);
        
        return pre1.or(pre2).test(s);
    }

    private static boolean checkString(String s, Predicate<String> pre) {
        return pre.test(s);
    }
}
```

练习

-  String[] strArray = {"林青霞，30", "柳岩，34", "张曼玉，35", "貂蝉，31", "王祖贤，33"};
- 字符串数组中有多条信息，请通过Predicate接口的拼装将符合要求的字符串筛选到集合ArrayList中，并遍历ArrayList集合。
- 同时满足如下要求：姓名长度大于2；年龄大于33
- 分析
  - 有两个判断条件，所以需要使用两个Predicate接口，对条件进行判断
  - 必须同时满足两个条件，所以可以使用and方法连接两个判断条件

```Java
import java.util.ArrayList;
import java.util.function.Predicate;

public class PredicateTest {
    public static void main(String[] args) {
        String[] strArray = {"林青霞，30", "柳岩，34", "张曼玉，35", "貂蝉，31", "王祖贤，33"};

        ArrayList<String> array = myFilter(strArray, s -> s.split("，")[0].length() > 2, s -> Integer.parseInt(s.split("，")[1]) > 33);

        for (String str : array) {
            System.out.println(str);
        }
    }

    private static ArrayList<String> myFilter(String[] strArray, Predicate<String> pre1, Predicate<String> pre2) {
        ArrayList<String> array = new ArrayList<String>();

        for (String str : strArray) {
            if (pre1.and(pre2).test(str)) {
                array.add(str);
            }
        }

        return array;
    }
}
```

**Function接口**

Function<T,R>：常用的两个方法

- R apply(T t)：将此函数应用于给定的参数
- default \<V> Function andThen(Function after)：返回一个组合函数，首先将该函数应用于输入，然后将after函数应用于结果
- Function<T,R>接口通常用于对参数进行处理，转换(处理逻辑由Lambda表达式实现)，然后返回一个新的值

练习

- String s = "林青霞，30";
- 请按照指定的要求进行操作：
  - 将字符串截取得到数字年龄部分
  - 将上一步的年龄字符串转换成为int类型的数据
  - 将上一步的int数据加70，得到一个int结果，在控制台输出
- 请通过Function接口来实现函数拼接

```Java
import java.util.function.Function;

public class FunctionTest {
    public static void main(String[] args) {
        String s = "林青霞，30";

        convert(s, s1 -> s1.split("，")[1], s1 -> Integer.parseInt(s1), integer -> integer + 70);
        convert(s, s1 -> s1.split("，")[1], Integer::parseInt, integer -> integer + 70);
    }

    private static void convert(String s, Function<String, String> fun1, Function<String, Integer> fun2, Function<Integer, Integer> fun3) {
        int i = fun1.andThen(fun2).andThen(fun3).apply(s);
        System.out.println(i);
    }
}
```

## 29. 方法引用

在使用Lambda表达式的时候，我们实际上传递进去的代码就是一种解决方案：拿参数做操作

那么考虑一种情况：如果我们在Lambda中所指定的操作方法，已经有地方存在相同的方案，那是否还有必要再写重复逻辑呢？

答案肯定是没有必要的。我们是通过方法引用来使用已经存在的方案

**方法引用符**

方法引用符

- :: 改符号为引用运算符，而它所在的表达式被称为方法引用

回顾一下我们在体验方法引用中的代码

- Lambda表达式：usePrintable(s -> System.out.println(s));
  - 分析：拿到参数s之后通过Lambda表达式，传递给System.out.println方法去处理
- 方法引用：usePrintable(System.out::println);
  - 分析：直接使用System.out中的println方法来取代Lambda，代码更加简洁

推导与省略

- 如果用Lambda，那么根据“可推导就是可省略”的原则，无需指定参数类型，也无需指定的重载形式，它们都将被自动推导
- 如果使用方法引用，也是同样可以根据上下文进行推导
- 方法引用是Lambda的孪生兄弟

**Lambda表达式支持的方法引用**

常见的引用方式：

- 引用类方法
- 引用对象的实例方法
- 引用类的实例方法
- 引用构造器

**引用类方法**

引用类方法，其实就是引用类的静态方法

- 格式：类名::静态方法
- 范例：Integer::parseInt
  - Integer类的方法：public static int parseInt(String s)将此String转换为int类型数据

练习：

- 定义一个接口(Converter)，里面定义一个抽象方法
  - int convert(String s);
- 定义一个测试类(ConverterDemo)，在测试类中提供两个方法
  - 一个方法是：useConverter(Converter c)
  - 一个方法是主方法，在主方法中调用useConverter方法

**引用对象的实例方法**

引用对象的实例方法，其实就引用类中的成员方法

- 格式：对象::成员方法
- 范例："HelloWorld"::toUpperCase
  - String类中的方法：public String toUpperCase()将此String所有字符转换为大写

**引用类的实例方法**

引用类的实例方法，其实就是引用类中的成员方法

- 格式：类名::成员方法
- 范例：String::substring
  - String类中的方法：public String substring(int beginIndex, int endIndex)

**引用构造器**

引用构造器，其实就是引用构造方法

- 格式：类名::new
- 范例：Student::new

## 30. Stream流

**体验Stream流**

使用Stream的方式完成过滤操作：找出集合中以张姓开头，长度为3的人，并遍历

- list.stream().filter(s -> s.startsWith("张")).filter(s -> s.length() == 3).forEach(System.out::println);
- 直接阅读代码的字面意思即可完美展示无关逻辑方式的语义：生成流、过滤姓张、过滤长度为3、逐一打印
- Stream流把正在的函数式编程风格引入到Java中

**Stream流的生成方式**

Stream流的使用

- 生成流
  - 通过数据源(集合，数组等)生成流
  - list.stream()
- 中间操作
  - 一个流后面可以跟随零个或多个中间操作，其目的主要是打开流，做出某种程度的数据过滤/映射，然后返回一个新的流
  - 交给下一个操作使用
  - filter()
- 终结操作
  - 一个流只能有一个终结操作，当这个操作执行后，流就被使用“光”了，无法再被操作。所以这必定是流的最后一个操作
  - forEach()

Stream流的常见生成方式

- Collection体系和集合可以使用默认方法stream()生成流
  - default Stream\<E> stream()
- Map体系的集合间接的生成流
- 数组可以通过Stream接口的静态方法of(T... values)生成流

```Java
import java.util.*;
import java.util.stream.Stream;

public class StreamDemo1 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        Stream<String> listStream = list.stream();

        Set<String> set = new HashSet<String>();
        Stream<String> setStream = set.stream();

        Map<String,Integer> map = new HashMap<String,Integer>();
        Stream<String> keyStream = map.keySet().stream();
        Stream<Integer> valueStream = map.values().stream();
        Stream<Map.Entry<String, Integer>> entryStream = map.entrySet().stream();

        String[] strArray = {"hello","world","java"};
        Stream<String> stringStream = Stream.of(strArray);
        Stream<String> stringStream1 = Stream.of("hello", "world", "java");
        Stream<Integer> integerStream = Stream.of(10, 20, 30);
    }
}
```

**Stream流的常见中间操作方法**

- Stream\<T> filter(Predicate predicate)：用于对流中的数据进行过滤
  - Predicate接口中的方法
  - boolean test(T t)：对给定的参数进行判断，返回一个布尔值
- Stream\<T> limit(long maxSize)：返回此流中的元素组成的流，截取前指定参数个数的数据
- Stream\<T> skip(long n)：跳过指定参数个数的数据，返回由该流的剩余元素组成的流
- static\<T> Stream\<T> concat(Stream a, Stream b)：合并a和b两个流为一个流
- Stream\<T> distinct()：返回由该流的不同元素(根据Object.equals(Object))组成的流
- Stream\<T> sorted()：返回由此流的元素组成的流，根据自然顺序排序
- Stream\<T> sorted(Comparator comparator)：返回由该流的元素组成的流，根据提供的Comparator进行排序
- \<R> Stream\<R> map(Function mapper)：返回由给定函数应用于此流的元素的结果组成的流
  - Function接口中的方法：R apply(T t)
- IntStream mapToInt(ToIntFunction mapper)：返回一个IntStream其中包含将给定函数应用于此流的元素的结果
  - IntStream：表示原始int流
  - ToIntFunction接口中的方法：int applyAsInt(T value)

**Stream流的常见终结操作方法**

Stream流的常见终结操作方法

- void forEach(Consumer action)：对此流的每个元素执行操作
  - Consumer接口中的方法：void accept(T t)：对给定的参数执行此操作
- long count()：返回此流中的元素数

**Stream流的收集操作**

对数据使用Stream流的方式操作完毕后，我想把流中的数据收集到集合中，该怎么办呢？

Stream流的收集方法

- R collect(Collector collector)
- 但是这个收集方法的参数是一个Collector接口

工具类Collectors提供了具体的收集方式

- public static \<T> Collector toList()：把元素收集到List集合中
- public static \<T> Collector toSet()：把元素收集到Set集合中
- public static Collector toMap(Function keyMapper, Function valueMapper)：把元素收集到Map集合中

## 31. 反射

### 31.1 类加载器

**类加载**

当程序要使用某个类时，如果该类还未被加载到内存中，则系统会通过类的加载，类的连接，类的初始化这三个步骤来对类进行初始化。如果不出现意外情况，JVM将会连续完成这三个步骤，所以有时也把这三个步骤统称为类加载或者类初始化

类的加载

- 就是指将class文件读入内存，并为之创建一个java.lang.Class对象
- 任何类被使用时，系统都会为之建立一个java.lang.Class对象

类的连接

- 验证阶段：用于检验被加载的类是否有正确的内部结构，并和其他类协调一致
- 准备阶段：负责为类的类变量分配内存， 并设置默认初始化值
- 解析阶段：将类的二进制数据中的符号引用替换为直接引用

类的初始化

- 在该阶段，主要就是对类变量进行初始化

类的初始化步骤

- 假如类还未被加载和连接，则程序先加载并连接该类
- 假如该类的直接父类还未被初始化，则先初始化其直接父类
- 假如类中有初始化语句，则系统依次执行这些初始化语句

注意：在执行第2个步骤的时候，系统对直接父类的初始化步骤也遵循初始化步骤1-3。

类的初始化时机

- 创建类的实例
- 调用类的方法
- 访问类或者接口的类变量，或者为该类变量赋值
- 使用反射方式来强制创建某个类或接口对应的java.lang.Class对象
- 初始化某个类的子类
- 直接使用java.exe命令来运行某个主类

类加载器的作用

- 负责将.class文件加载到内存中，并为之生成对应的java.lang.Class对象
- 虽然我们不用过分关心类加载机制，但是了解这个机制我们就能更好的理解程序的运行

JVM的类加载机制

- 全盘负责：就是当一个类加载器负责加载某个Class时，该Class所依赖的引用的其他Class也将由该类加载器负责载入，除非显示使用另外一个类加载器来载入
- 父类委托：就是当一个类加载器负责加载某个Class时，先让父类加载器试图加载该Class，只有在父类加载器无法加载该类时才尝试从自己的类路径中加载该类
- 缓存机制：保证所有加载过的Class都会被缓存，当程序需要使用某个Class对象时，类加载器先从缓存区中搜索该Class，只有当缓存区中不存在该Class对象时，系统才会读取该类对应的二进制数据，并将其转换成Class对象，存储到缓存区

ClassLoader：是负责加载类的对象

Java运行时具有以下内置类加载器

- Bootstrap class loader：它是虚拟机的内置类加载器，通常表示为null，并且没有父null
- Platform class loader：平台类加载器可以看到所有平台类，平台类包括由平台类加载器或其祖先定义的Java SE平台API，其实现类和JDK特定的运行时类
- System class loader：它也被称为应用程序类加载器，与平台类加载器不同。系统类加载器通常用于定义应用程序类路径，模块路径和JDK特定工具上的类
- 类加载器的继承关系：System的父加载器为Platform，而Platform的父加载器为Bootstrap

ClassLoader中的两个方法

- static ClassLoader getSystemClassLoader()：返回用于委派的系统类加载器
- ClassLoader getParent()：返回父类加载器进行委派

### 31.2 反射

**反射概述**

Java反射机制：是指在运行时去获取一个类的变量和方法信息。然后通过获取到的信息来创建对象，调用方法的一种机制。由于这种动态性，可以极大的增强程序的灵活性，程序不用在编译期就完成确定，在运行期仍然可以扩展

**获取Class类的对象**

我们要想通过反射去使用一个类，首先我们要获取到该类的字节码文件对象，也就是类型为Class类型的对象

这里我们提供三种方式获取Class类型的对象

- 使用类的class属性来获取该类对应的Class对象。举例：Student.class将会返回Student类对应的Class对象
- 调用对象的getClass()方法，返回该对象所属类对应的Class对象
  - 该方法是Object类中的方法，所有的Java对象都可以调用该方法
- 使用Class类中的静态方法forName(String className)，该方法需要传入字符串参数，该字符串参数的值是某个类的全路径，也就是完整包名的路径

Class类中用于获取构造方法的方法

- Constructor<?>[] getConstructors()：返回所有公共构造方法对象的数组
- Constructor<?>[] getDeclaredConstructors()：返回所有构造方法对象的数组
- Constructor\<T> getConstructor(Class<?>... parameterTypes)：返回单个公共构造方法对象
- Constructor\<T> getDeclaredConstructor(Class<?>... parameterTypes)：返回单个构造方法对象

Constructor类中用于创建对象的方法

- T newInstance(Object... initargs)：根据指定的构造方法创建对象

练习：通过反射实现如下操作

- Studen s = new Studen("林青霞", 30, "西安");
- System.out.println(s);
- 基本数据类型也可以通过.class得到对应的Class类型
- public void setAccessible(boolean flag)：值为true，取消访问检查

```Java
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

public class ReflectDemo2 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException {
        Class<?> c = Class.forName("com.itahu2.demo1.Student");
        Constructor<?> con = c.getConstructor(String.class, int.class, String.class);
        Object obj = con.newInstance("林青霞", 30, "西安");
        System.out.println(obj);
    }
}
```

```Java
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

public class ReflectDemo2 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException {
        Class<?> c = Class.forName("com.itahu2.demo1.Student");
        Constructor<?> con = c.getDeclaredConstructor(String.class);
        con.setAccessible(true);
        Object obj = con.newInstance("林青霞");
        System.out.println(obj);
    }
}
```

**反射获取成员变量并使用**

Class类中用于获取成员变量的方法

- Field[] getFields()：返回所有公共成员变量对象的数组
- Field[] getDeclareFields()：返回所有成员变量对象的数组
- Field getField(String name)：返回单个公共成员变量的对象
- Field getDeclareField(String name)：返回单个成员变量对象

Field类中用于给成员变量赋值的方法

- void set(Object obj, Object value)：给obj对象的成员变量赋值为value

**反射获取成员方法并使用**

Class类中用于获取成员方法的方法

- Method[] getMethods()：返回所有公共成员方法对象的数组，包括继承的
- Method[] getDeclaredMethods()：返回所有成员方法对象的数组，不包括继承的
- Method getMethod(String name, Class<?>... parameterTypes)：返回单个公共成员方法对象
- Method getDeclareMethod(String name, Class<?>... parameterTypes)：返回单个成员方法对象

Method类中用于调用成员方法的方法

- Object invoke(Object obj, Object... args)：调用obj对象的成员方法，参数是args，返回值是Object类型

小练习

```Java
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class ReflectDemo3 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException {
        Class<?> c = Class.forName("com.itahu2.demo1.Student");
        Constructor<?> con = c.getConstructor();
        Object obj = con.newInstance();

        Method m1 = c.getMethod("method1");
        m1.invoke(obj);

        Method m2 = c.getMethod("method2", String.class);
        m2.invoke(obj,"林青霞");

        Method m3 = c.getMethod("method3", String.class, int.class);
        Object o = m3.invoke(obj, "林青霞", 30);
        System.out.println(o);

        Method m4 = c.getDeclaredMethod("function");
        m4.setAccessible(true);
        m4.invoke(obj);
    }
}
```

**反射练习**

练习1：有一个ArrayList\<Integer>集合，现在想在这个集合中添加一个字符串数据，如何实现？

```Java
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.util.ArrayList;

public class ReflectTest {
    public static void main(String[] args) throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {
        ArrayList<Integer> array = new ArrayList<Integer>();

        array.add(10);
        array.add(20);

        Class<? extends ArrayList> c = array.getClass();
        Method m = c.getMethod("add", Object.class);
        m.invoke(array,"Hello");
        m.invoke(array,"World");
        m.invoke(array,"Java");

        System.out.println(array);
    }
}
```

练习2：通过配置文件运行类中的方法

```Java
// Student类
public class Student {
    public void study() {
        System.out.println("好好学习天天向上");
    }
}

// Teacher类
public class Student {
    public void study() {
        System.out.println("好好学习天天向上");
    }
}

// class.txt文件内容
className=com.itahu2.demo2.Teacher    //类名路径
methodName=teach                      //方法名
```

```Java
import java.io.FileReader;
import java.io.IOException;
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.util.Properties;

public class ReflectTest1 {
    public static void main(String[] args) throws IOException, ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException {

        Properties prop = new Properties();
        FileReader fr = new FileReader("F:\\JavaProjects\\Demo2\\class.txt");
        prop.load(fr);
        fr.close();

        String className = prop.getProperty("className");
        String methodName = prop.getProperty("methodName");

        Class<?> c = Class.forName(className);
        Constructor<?> con = c.getConstructor();
        Object obj = con.newInstance();

        Method m = c.getMethod(methodName);
        m.invoke(obj);
    }
}
```

## 32. 模块化

Java语言随着这些年的发展已经成为了一门影响深远的编程语言，无数平台，系统都采用Java语言编写。但是，伴随着发展，Java也越来越庞大，逐渐发展成为一门“臃肿”的语言。而且，无论是运行一个大型的软件系统，还是运行一个小的程序，即使程序只需要使用Java的部分核心功能，JVM也要加载整个JRE环境。为了给Java“瘦身”，让Java实现轻量化，Java 9正式的推出了模块化系统。Java被拆分为N多个模块，并允许Java程序可以根据需要选择加载程序必须的Java模块，这样就可以让Java以轻量化的方式来运行

其实，Java 7的时候已经提出了模块化的概念，但由于其过于复杂，Java 7，Java 8都一直未能真正推出，直到Java 9才真正成熟起来。对于Java语言来说，模块化系统是一次真正的自我革新，这种革新使得“古老而庞大”的Java语言重新焕发年轻的活力

**模块的基本使用**

模块的基本使用步骤

- 创建模块(按照以前的讲解方式创建模块，创建包，创建类，定义方法)
  - 为了体现模块的使用，我们创建2个模块。一个是myOne，一个是myTwo
- 在模块的src目录下新建一个名为module-info.java的描述文件，该文件专门定义模块名，访问权限，模块依赖等信息
  - 描述性文件中使用模块导出和模块依赖来进行配置和使用
- 模块中所有未导出的包都是模块私有的，他们是不能在模块之外被访问的
  - 在myOne这个模块下的描述性文件中配置模块导出
  - 模块导出格式：exports 包名;
- 一个模块要访问其他的模块，必须明确指定依赖哪些模块，未明确指定依赖的模块不能访问
  - 在myTwo这个模块下的描述性文件中配置模块依赖
  - 模块依赖格式：requires 模块名;
  - 注意：写模块名报错，需要按下Alt+Enter提示，然后选择模块依赖
- 在myTwo这个模块的类中使用依赖模块下的内容

**模块服务的使用**

服务：从Java 6开始，Java提供了一种服务机制，允许服务提供者和服务使用者之间完成解耦

简单的说，就是服务使用者只面向接口编程，但不清楚服务提供者的实现类

Java 9的模块化系统则进一步的简化了Java的服务机制。Java 9允许将服务接口定义在一个模块中，并使用users语句来声明该服务接口，然后针对该服务接口提供不同的服务实现类，这些服务实现类可以分布在不同的模块，服务实现模块则使用provides语句为服务接口指定实现类

服务使用者只需要面向接口编程即可

模块服务的使用步骤

- 在myOne模块下创建一个包com.itahu_03，在该包下提供一个接口，接口中定义一个抽象方法

  ```Java
  public interface MyService {
      void service();
  }
  ```

- 在com.itahu_03包下创建一个包impl，在该包下提供接口的两个实现类itahu和ustc

- 在myOne这个模块下的描述文件中添加如下配置

  - 模块导出：exports com.itahu_03;
  - 服务提供：provides MyService with itahu;
  - 上一句指定MyService的服务实现类是itahu

- 在myTwo这个模块的类中使用MyService接口提供的服务

  - ServiceLoader：一种加载服务实现的工具
