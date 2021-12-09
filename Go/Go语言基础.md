<center>
    <h1>
        Go语言基础
    </h1>
</center>

## 1. 基础语法

### 1.1 基本数据类型

- bool 布尔
- string 字符串
- (u)int, (u)int8, (u)int16, (u)int32, (u)int64 整数(u无符号，有符号)
- uintptr 指针
- float32，float64浮点数
- complex64，complex128复数

练习案例

```Go
package main

import (
	"fmt"
	"math"
)

func main() {
	var (
		a bool      = false
		b string    = "张三"
		c int       = -16
		d uint      = 100
		e float32   = 3.14
		f complex64 = 3 + 2i
	)
	fmt.Println(a, b, c, d, e, f)

	// 类型转换
	var var1 int32 = 100
	var var2 int64
	var2 = int64(var1)
	fmt.Println("var2 = ", var2)

	// sqrt(a*a + b*b) = c
	var aa, bb = 3, 4
	cc := math.Sqrt(float64(aa*aa + bb*bb))
	fmt.Println("cc = ", cc)
}
```

### 1.2 常量与枚举

```Go
package main

import (
	"fmt"
	"math"
)

func main() {
	fmt.Println("常量的定义")

	// 单个常量的定义
	const pi = 3.14
	const os_version string = "1.0.0"
	fmt.Println(pi, os_version)

	// 单行定义多个常量
	const a, b = 3, 4
	fmt.Println(a, b)

	const (
		c = 5
		d = 10
	)
	fmt.Println(c, d)

	cc := math.Sqrt(a*a + b*b)
	fmt.Println("三角函数", cc)

	// 枚举 enum
	// 首字母大写默认public其他包可见
	const (
		langC    = "C"
		langJava = "JAVA"
		langGo   = "GO"
	)
	fmt.Println(langC, langJava, langGo)

	// 自增类型的枚举
	// 每一次const iota初始化为0
	const (
		zz = iota
		zz1
	)
	const (
		tt = iota
		tt1
		tt2
		_
		tt4
	)
	fmt.Println(zz, zz1, tt, tt1, tt2, tt4)

	// 简洁语法_占位符
	name1, _ := "张三", "李四"
	fmt.Println(name1)
}
```

### 1.3 基本运算法则

```Go
package main

import "fmt"

func main() {
	// 1 + 1 = 2
	// 知识点
	// 1.运算符
	// 2.表达式
	// 3.双目运算符
	// 4.字面量 3.5
	// 5.表达式是可以求值的

	fmt.Println("1 + 1 =", 1+1)

	// 拓展变量的定义与常量的定义
	var a int = 5
	var b int = a * 4
	const c = 4
	var d int = c * a * b
	const e = c * 5
	fmt.Printf("a = %d, b = %d, d = %d, e = %d\n", a, b, d, e)

	// 算术运算符+ - * / %
	// 整数的除法结果还是整数
	fmt.Println(5/2, 5.0/2)
	fmt.Println(a % c)

	// 关系运算符== != > < >= <=
	// 逻辑运算符&& || !
	var age int = 20
	fmt.Println(age >= 20 && age < 100)
	fmt.Println(age >= 20 || age < 15)
	fmt.Println(!(age > 20))

	// 位运算符 & | ^ << >>
	// & 按位与 | 按位或 ^ 按位异或 << 左移运算符 >> 右移运算符
	fmt.Println(1 << 2)
	kb := 1 << (10 * 1)
	fmt.Println(kb)
	fmt.Println(4 >> 2)

	// 赋值运算符= += -= /= %= <<= >>= &= ^= |=
	var x int = 10
	x += 1
	fmt.Println(x)
}
```

### 1.4 流程控制

```Go
package main

import "fmt"

func main() {
	fmt.Println("条件语句")
	// 需求计算订单优惠价
	// 1.订单金额小于等于100打九折
	// 2.订单金额大于100小于等于300打八折
	// 3.大于300打五折

	total := 150.00
	discount := 0.0
	if total <= 100 {
		discount = total * 0.9
	} else if total > 100 && total <= 300 {
		discount = total * 0.8
	} else {
		discount = total * 0.5
	}
	fmt.Printf("订单优惠后的价格：%.2f\n", discount)

	switch {
	case total <= 100:
		discount = total * 0.9
	case total > 100 && total <= 300:
		discount = total * 0.8
	default:
		discount = total * 0.5
	}
	fmt.Printf("订单优惠后的价格：%.2f", discount)
}
```

### 1.5 循环

```Go
package main

import "fmt"

func main() {
	fmt.Println("循环")

	a := 5
	a++
	fmt.Println("a++", a)
	a--
	fmt.Println("a--", a)

	// 循环1
	for i := 1; i <= 10; i++ {
		if i%2 == 0 {
			continue
		}
		fmt.Println("循环1，i= ", i)
	}

	// 循环2
	for i := 1; i <= 10; {
		fmt.Println("循环2，i= ", i)
		i++
	}

	// 无限循环，死循环
	for {
		fmt.Println("死循环")
		break
	}
}
```

### 1.6 函数

```Go
package main

import "fmt"

func main() {
	fmt.Println("函数")
	c := add(10, 20)
	fmt.Println("func add =", c)
	dec()

	bb := func(a int, b int) int {
		return a + b
	}
	fmt.Println("匿名函数调用", bb(1, 1))

	fmt.Println("匿名函数调用方式2", func(a int, b int) int {
		return a + b
	}(3, 3))

	opFunc := op("+")
	fmt.Println("匿名函数+", opFunc(1, 9))
	opFunc = op("-")
	fmt.Println("匿名函数-", opFunc(10, 1))

	t1, t2 := 5, 10
	r1, r2 := swap(t1, t2)
	fmt.Println(r1, r2)
	fmt.Println(t1, t2)
	// 闭包
	func() {
		t1, t2 = t2, t1
	}()
	fmt.Println("闭包", t1, t2)

	test(1, 2, 3, 4, 5, 6)
}

func add(a int, b int) (r int) {
	return a + b
}

func dec() {
	fmt.Println("func dec 被调用")
}

// func add2(a, b int, c int64) (r int) {
// 	return a + b
// }

func op(s string) func(int, int) int {
	switch {
	case s == "+":
		return func(a, b int) int {
			return a + b
		}
	case s == "-":
		return func(a, b int) int {
			return a - b
		}
	default:
		panic("操作不支持")
	}
}

func swap(a int, b int) (int, int) {
	return b, a
}

func test(params ...int) {
	fmt.Println(params)
	test2(params...)
}

func test2(params ...int) {
	fmt.Println(params)
}
```

### 1.7 指针

```Go
package main

import "fmt"

func main() {
	fmt.Println("指针")

	// 指针，是用来保存内存地址的一种特殊的变量类型
	var p *int
	var p1 *float32
	var c int
	fmt.Println(p)
	fmt.Println(p1)
	fmt.Println(c)

	fmt.Printf("p 类型 %T\n", p)
	fmt.Printf("p %p\n", p)
	// nil 指针，函数，管道，切片，interface，map

	// & 取地址
	name := 10
	p = &name
	fmt.Printf("p %p\n", p)
	fmt.Println(name)

	// * 解指针操作符
	fmt.Println(*p)
	*p = 100
	fmt.Println(*p)
	fmt.Println(name)

	var p3 *int
	p3 = new(int)
	fmt.Println(*p3)
	*p3 = 101
	fmt.Println(*p3)
}
```

### 1.8 字符与字符串

- byte字符
- rune unicode编码字符
- for range语法

```Go
package main

import (
	"fmt"
	"unicode/utf8"
)

func main() {
	fmt.Println("字符与字符串")

	s := "你好，hello"
	fmt.Println("s 长度", len(s))

	// 字符串底层使用字节来保存
	// len返回字符串字节数

	// byte 字符
	var c byte = 'h'
	fmt.Printf("c = %c\n", c)
	// rune unicode的字符
	var ch rune = '中'
	fmt.Printf("ch = %c\n", ch)

	fmt.Println("*s 长度", utf8.RuneCountInString(s))

	for _, r := range s {
		fmt.Printf("rune %T, %U, %c\n", r, r, r)
	}
}
```

## 2. 内建容器

### 2.1 数组

```Go
package main

import "fmt"

func main() {
	fmt.Println("数组")

	var arr [3]int
	fmt.Println(arr)

	var arr1 [3]int = [3]int{1, 3}
	fmt.Println(arr1)

	arr2 := [5]int{1, 3, 5, 7, 9}
	fmt.Println(arr2)

	arr3 := [...]int{2, 4, 6, 8, 10, 12, 14}
	fmt.Println(arr3)
	fmt.Println("arr3 length", len(arr3))

	// 多维数组的定义
	t2 := [3][5]int{{1}, {3}, {5, 4, 3, 2, 1}}
	fmt.Println("t2 length", t2)

	for i := 0; i < len(arr2); i++ {
		fmt.Println("i =", i, arr2[i])
	}

	fmt.Println("for range")
	for i, v := range arr2 {
		fmt.Println("i =", i, v)
	}

	// 数组是值类型
	var test [3]int = [3]int{1, 3, 5}
	printArray(&test)
	fmt.Println("循环后", test)
}

func printArray(arr *[3]int) {
	fmt.Println("循环开始")
	arr[0] = 101
	for _, v := range arr {
		fmt.Println("i =", v)
	}
}
```

### 2.2 切片

- 切片的定义
- 理解切片的长度与容量的概念
- 切片的基本操作

```Go
package main

import "fmt"

func main() {
	fmt.Println("Slice 切片")

	var arr [6]int = [6]int{1, 2, 3, 4, 5, 6} //数组
	var _ []int                               //切片，slice

	//切片只对数组的局部或全部的一种引用形式

	fmt.Println("[1:3]", arr[1:3]) //半开半闭区间
	fmt.Println("[:3]", arr[:3])
	fmt.Println("[1:]", arr[1:])
	fmt.Println("[:]", arr[:])

	s1 := arr[1:3]
	s2 := s1[2:5]
	fmt.Println("s1 =", s1)
	fmt.Println("s2 =", s2)

	//切片的长度 len()
	fmt.Println("len(s1)", len(s1))
	fmt.Println("len(s2)", len(s2))

	//切片的容量 cap()
	fmt.Println("cap(s1)", cap(s1))
	fmt.Println("cap(s2)", cap(s2))

	//切片的操作
	//1切片的拓展追加 append
	d := [...]int{1, 2, 3, 4, 5, 6}
	d1 := d[:3]
	d1 = append(d1, 101)
	fmt.Println("d1", d1)
	fmt.Println("d", d)

	d1 = append(d1, []int{102, 103}...)
	fmt.Println("d1", d1)
	fmt.Println("d", d)

	d1 = append(d1, []int{103, 104}...)
	fmt.Println("d", d)

	//复制 copy()
	f := [...]int{1, 2, 3, 4, 5, 6}
	f1 := f[1:3]
	f2 := f[3:]

	fmt.Println("f1", f1)
	fmt.Println("f2", f2)
	copy(f2, f1)
	fmt.Println("copy之后")
	fmt.Println("f1", f1)
	fmt.Println("f2", f2)
	fmt.Println("f", f)

	//切片 make()
	t1 := make([]int, 3, 6)
	t2 := make([]int, 3)
	fmt.Println("t1", t1, len(t1), cap(t1))
	fmt.Println("t2", t2, len(t2), cap(t2))
}
```

### 2.3 Map

```Go
package main

import (
	"fmt"
	"sort"
)

func main() {
	fmt.Println("Map")

	//map是一种key，value的数据结构
	//key的类型不支持map，slice，func
	// map2 := map[string]int{"a": 5, "b": 4}
	map1 := map[string]int{
		"a": 5,
		"b": 4,
		"c": 3,
		"d": 2,
		"e": 1,
	}
	//map取值
	fmt.Println(map1["a"])

	//数组取值
	arr := [3]int{1, 2, 3}
	fmt.Println(arr[0])

	for index, val := range arr {
		fmt.Println(index, val)
	}

	//Map 遍历
	//知识点 map的遍历是无序的
	for key, val := range map1 {
		fmt.Println(key, val)
	}

	s := []string{}
	for key := range map1 {
		s = append(s, key)
	}

	sort.Strings(s)
	fmt.Println("Map的正序遍历")
	for _, v := range s {
		fmt.Println(map1[v])
	}

	// make
	map3 := make(map[string]float32)
	fmt.Println("map3", map3)

	test := map[string]int{
		"a": 5,
		"b": 4,
		"c": 3,
		"d": 2,
		"e": 1,
	}
	fmt.Println(test["f"])

	val, ok := test["d"]
	fmt.Println(val, ok)

	if val, ok := test["f"]; ok {
		fmt.Println(val, ok)
	} else {
		fmt.Println("键不存在于map")
	}
}
```

## 3. 自定义类型与结构体

### 3.1 结构体struct

- 结构体的定义
- 结构体的嵌套

```Go
package main

import "fmt"

type user struct {
	id   int
	name string
	addr address
}

type address struct {
	mobile string
	city   string
}

//匿名成员的数据类型相同的只允许出现一次
type teacher struct {
	int
	string
	city string
}

func main() {
	fmt.Println("结构体")

	//方式1
	var u user
	fmt.Printf("%#v\n", u)

	//方式2
	u1 := user{id: 1, name: "小张"}
	fmt.Printf("u1 %T, %#v\n", u1, u1)

	//方式3
	u2 := &user{2, "小李", address{mobile: "123", city: "北京"}}
	fmt.Printf("u2 %T, %#v\n", u2, u2)

	//方式4 new()
	u3 := new(user)
	// (*user)(u3).id = 888
	u3.id = 999
	fmt.Printf("u3 %T, %#v\n", u3, u3)

	//匿名结构体
	var u4 struct {
		id   int
		name string
	}
	fmt.Printf("u4 %T, %#v\n", u4, u4)

	//结构体如何访问成员
	u4.id = 101
	u4.name = "刘德华"
	fmt.Printf("u4 %T, %#v\n", u4, u4)

	//结构体的嵌套
	u5 := user{}
	u5.id = 666
	u5.name = "小孙"
	u5.addr.mobile = "188"
	u5.addr.city = "广州"
	fmt.Printf("u5 %T, %#v\n", u5, u5)

	//很少用
	t := teacher{}
	t.int = 999
	t.string = "孙老师"
	t.city = "上海"
	fmt.Printf("t %T, %#v\n", t, t)
}
```

- 结构体的方法
- 结构体的可见性
- 包与导入

```Go
package main

import (
	"fmt"

	"github.com/Mark-Clinton/Demo05/bird"
)

type (
	bird1 struct {
		name string
	}

	bird2 struct {
		name string
	}
)

// 结构体方法 接收者
// 值接收者
func (b bird1) fly() {
	fmt.Printf("传入时：%p\n", &b)
	b.name = "豆豆"
	fmt.Printf("%s 飞\n", b.name)
}

//指针接收者
func (b *bird1) fly2() {
	fmt.Printf("传入时：%p\n", b)
	b.name = "花花"
	fmt.Printf("%s 飞\n", b.name)
}

func (b bird2) fly() {
	fmt.Printf("%s 飞\n", b.name)
}

func main() {
	fmt.Println("结构体")

	b1 := bird1{name: "毛毛"}
	fmt.Printf("传入前：%p\n", &b1)
	b1.fly()
	fmt.Printf("%#v\n", b1)
	fmt.Println("fly2之后")
	b1.fly2()
	fmt.Printf("%#v\n", b1)

	b2 := bird2{name: "豆豆"}
	b2.fly()

	//结构体的可见性
	b := bird.Bird1{Name: "花花"}
	b.Fly2()
	fmt.Println(b)
}
```

- 结构体的标签
- 结构体的序列化与反序列化

```Go
package main

import (
	"encoding/json"
	"fmt"
)

type User struct {
	Id     int    `json:"id"`
	Name   string `json:"name"`
	Avatar string `json:"avatar"`
}

func main() {
	fmt.Println("结构体")

	//序列化
	user := new(User)
	user.Id = 999
	user.Name = "小李"
	user.Avatar = "https://www.baidu.com"

	bytes, err := json.Marshal(user)
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Printf("%s\n", bytes)

	//反序列化
	fmt.Println("反序列化")
	jsonStr := `{"id":888,"name":"小孙","avatar":"https://www.bilibili.com"}`
	user2 := User{}
	err = json.Unmarshal([]byte(jsonStr), &user2)
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Printf("%#v\n%d,%s,%s\n", user2, user2.Id, user2.Name, user2.Avatar)
}
```

### 3.2 自定义类型

- 自定义类型
- 类型别名
- 自定义类型拓展

```Go
package main

import "fmt"

type MyInt int    //自定义类型
type MyInt2 = int //类型别名

type Logger struct {
	Desc string
}

func (logger Logger) PrintLog() {
	fmt.Println("我是日志：", logger.Desc)
}

type MyLogger Logger

func (logger MyLogger) PrintPrettyLog() {
	fmt.Printf("我是日志：\t %s \t!!!\n", logger.Desc)
}

func main() {
	fmt.Println("自定义类型与类型别名")

	//自定义类型
	var a MyInt
	var b MyInt2

	fmt.Printf("%T\n", a)
	fmt.Printf("%T\n", b)

	//旧Logger
	logger := Logger{}
	logger.Desc = "哈哈哈"
	logger.PrintLog()

	fmt.Println("自定义类型拓展后的Logger")
	var myLogger MyLogger
	myLogger.Desc = "哈哈哈"
	myLogger.PrintPrettyLog()
}
```

## 4. 依赖管理与包初始化

### 4.1 依赖管理

- 依赖管理的概念
- 使用go mod管理依赖

初始化依赖管理：go mod init gostudy

下载依赖：go get -u github.com/wechatpay-apiv3/wechatpay-go@v0.2.8

删除未引用依赖：go mod tidy

### 4.2 包初始化

```Go
package test

import "fmt"

type User struct {
	Id int
}

var UserInfo *User

func init() {
	fmt.Println("init3")
	UserInfo = &User{
		Id: 888,
	}
}

func init() {
	fmt.Println("init1")
	UserInfo = &User{
		Id: 999,
	}
}

func init() {
	fmt.Println("init2")
	UserInfo = &User{
		Id: 666,
	}
}
```

```Go
package abc

import "fmt"

func init() {
	fmt.Println("abc init")
}
```

```Go
package main

import (
	"fmt"
	_ "gostudy/abc"
	"gostudy/test"
)

func main() {
	fmt.Println("包初始化")
	fmt.Printf("%#v", test.UserInfo)
}
```

## 5. 接口

### 5.1 接口的概念与定义

```Go
package main

import (
	"encoding/json"
	"encoding/xml"
	"fmt"
)

type User struct {
	Id   int    `json:"id" xml:"id,attr"`
	Name string `json:"name" xml:"name,attr"`
}

type JsonParser string

func (p JsonParser) Serialize(v interface{}) {
	if bytes, err := json.Marshal(v); err != nil {
		panic(err)
	} else {
		fmt.Printf("%s\n", bytes)
	}
}

type XmlParser string

func (p XmlParser) Serialize(v interface{}) {
	if bytes, err := xml.Marshal(v); err != nil {
		panic(err)
	} else {
		fmt.Printf("%s\n", bytes)
	}
}

func main() {
	fmt.Println("接口")

	user := User{
		Id:   101,
		Name: "小李",
	}

	var p1 JsonParser
	p1.Serialize(user)

	var p2 XmlParser
	p2.Serialize(user)

	fmt.Println("接口之后")
	printAny(user, p1)
	printAny(user, p2)
}

type TokenParse interface {
	Serialize(v interface{})
}

func printAny(v interface{}, p TokenParse) {
	p.Serialize(v)
}
```

### 5.2 接口的组合使用

```Go
package discount

import "fmt"

type Order struct {
	Id    int
	Total float64
}

//免费会员
type FreeUser struct {
	Order *Order
}

func (u FreeUser) ComputeOrder() {
	fmt.Printf("订单编号：%d，订单金额：%.2f\n", u.Order.Id, u.Order.Total*0.9)
}
```

```Go
package discount

import "fmt"

//VIP会员
type VipUser struct {
	Order *Order
}

func (u VipUser) ComputeOrder() {
	fmt.Printf("订单编号：%d，订单金额：%.2f\n", u.Order.Id, u.Order.Total*0.8)
}

```

```Go
package main

import (
	"fmt"

	"github.com/Mark-Clinton01/Demo03/discount"
)

type CommonUser struct {
	Order *discount.Order
}

func (c CommonUser) ComputeOrder() {
	fmt.Println(c.Order.Id)
}

func (c *CommonUser) PrintCode() {
	fmt.Println("打印二维码", c.Order.Id)
}

func main() {
	fmt.Println("接口")

	order := &discount.Order{
		Id:    999,
		Total: 300.0,
	}

	PrintOrderDiscount(discount.FreeUser{Order: order})
	PrintOrderDiscount(discount.VipUser{Order: order})

	//接口组合
	fmt.Println("接口组合")
	var dc DiscounterAndCoder = &CommonUser{
		Order: order,
	}
	dc.ComputeOrder()
	dc.PrintCode()
}

type Discounter interface {
	ComputeOrder()
}

type Coder interface {
	PrintCode()
}

type DiscounterAndCoder interface {
	Discounter
	Coder
}

func PrintOrderDiscount(d Discounter) {
	if _, ok := d.(discount.FreeUser); ok {
		fmt.Println("您享受的是免费会员折扣")
	} else {
		fmt.Println("您享受的是VIP会员折扣")
	}
	d.ComputeOrder()
}
```

### 5.3 空接口

```Go
package main

import "fmt"

type Printer interface {
	PrintOrder() //方法的签名或原型
}

type Qr interface {
	Printer
	PrintQr()
}

type Order struct {
	Id    int
	Total float64
}

func (o Order) PrintOrder() {
	fmt.Println(o.Id)
}

type OrderQr struct {
	Order
}

func (o OrderQr) PrintQr() {
	fmt.Println("打印二维码", o.Order.Id)
}

type Empty interface{}

func main() {
	fmt.Println("接口")

	var p Printer = Order{Id: 999, Total: 100}
	p.PrintOrder()

	var q Qr = OrderQr{Order{Id: 666, Total: 350.0}}
	q.PrintOrder()
	q.PrintQr()

	//空接口
	var empty Empty = 456
	empty = false
	fmt.Println(empty)

	var s bool = empty.(bool)
	fmt.Println(s)

	//空接口应用场景
	map1 := map[string]interface{}{
		"id":   1,
		"name": "小李",
		"sex":  true,
	}
	fmt.Printf("%#v\n", map1)
}
```

## 6. 错误处理

### 6.1 延迟执行函数

- defer

```Go
package main

import (
	"fmt"
	"os"
)

func Test() {
	defer fmt.Println(1)
	defer fmt.Println(2)
	fmt.Println(3)
	fmt.Println(4)
	panic("error")
	// fmt.Println(5)
}

// defer 延迟执行函数是在函数返回之前或错误发生之前能够执行的函数
// defer 调用次序是一种先进后出也可以说是后进先出来执行的
// defer 参数是在defer定义时就已经计算好的

func main() {
	fmt.Println("defer延迟调用")

	// Test()
	// for i := 1; i <= 5; i++ {
	// 	defer fmt.Println(i)
	// }

	// defer fmt.Println("hello world")
	// os.Exit(0)

	WriterFile("test.txt", "Hello World")
}

func WriterFile(fileName string, content string) {
	file, err := os.OpenFile(fileName, os.O_CREATE|os.O_APPEND, 0666)
	if err != nil {
		panic(err)
	}
	defer file.Close()

	file.WriteString(content)
}
```

### 6.2 异常与恢复

- panic
- recover

```Go
package main

import (
	"fmt"
	"os"
)

func main() {
	fmt.Println("错误处理")
	defer func() {
		err := recover()
		if myErr, ok := err.(MyError); ok {
			fmt.Println("main函数捕获错误", myErr.Code, myErr.Reason)
		} else {
			fmt.Println(err)
		}
	}()
	WriterFile("file.txt", "你好，Go")
}

type MyError struct {
	Code   uint
	Reason string
}

func (e MyError) Error() string {
	return fmt.Sprintf("自定义错误码：%d 错误原因：%s\n", e.Code, e.Reason)
}

func WriterFile(fileName string, content string) {
	file, err := os.Open(fileName)
	defer func() {
		err := recover()
		switch err.(type) {
		case *os.PathError:
			fmt.Println("WriteFile捕获错误：文件不存在")
			panic(err)
		default:
			// fmt.Printf("%#v", MyError{Code: 1001, Reason: "文件不存在"})
			panic(MyError{Code: 1001, Reason: "文件不存在"})
		}
	}()
	if err != nil {
		panic(err) //"出错了"
	}
	defer file.Close()
	file.WriteString(content)
}
```

## 7. 并发编程

### 7.1 初识goroutine

- go
- 协程同步

```Go
package main

import (
	"fmt"
	"sync"
)

// 轻量级线程，Go语言运行时调度的

func Test(n int) {
	defer wg.Done()
	fmt.Println(n)
}

var wg sync.WaitGroup

func main() {
	fmt.Println("并发编程")

	for i := 0; i < 1000; i++ {
		wg.Add(1)
		go Test(i)
	}

	wg.Wait()
}
```

### 7.2 channel

```Go
package main

import (
	"fmt"
	"math/rand"
	"strconv"
	"strings"
	"sync"
	"time"
)

var wg sync.WaitGroup

func main() {
	fmt.Println("channel")

	// 1.无缓冲的通道，同步通道
	// var ch chan int
	// fmt.Println("未初始化", ch)
	// ch = make(chan int)
	// fmt.Println("初始化完成", ch)

	ch := make(chan int)
	go func() {
		//从通道接收数据
		fmt.Println("从通道中接收数据", <-ch)
	}()
	//向通道发送数据
	ch <- 100

	// 2.有缓冲通道，不是同步通道
	ch2 := make(chan int, 3)
	ch2 <- 1
	ch2 <- 2
	ch2 <- 3
	// ch2 <- 4 // 缓冲区满的时候不能发送数据

	fmt.Println("从ch2中接收数据", <-ch2)
	fmt.Println("从ch2中接收数据", <-ch2)
	fmt.Println("从ch2中接收数据", <-ch2)
	// fmt.Println("从ch2中接收数据", <-ch2) // 缓冲区为空时不能读取数据

	close(ch2)
	// ch2 <- 1 // 不能向已关闭的通道发送数据
	fmt.Println("从ch2中接收数据", <-ch2) // 从关闭通道中缓冲区为0的通道返回数据会返回通道元素类型的默认0值
	// close(ch2) // 不能再次关闭已经关闭的通道

	// 模拟比特币挖矿
	blockChain := make(chan string)

	rand.Seed(time.Now().UnixNano())
	for i := 0; i < 10000; i++ {
		wg.Add(1)
		go Miner(i, blockChain)
	}
	go func(ch chan string) {
		for c := range ch {
			fmt.Println(c)
		}
	}(blockChain)
	wg.Wait()
}

const MagicNum = "88"

func Miner(n int, ch chan string) {
	defer wg.Done()
	num := rand.Int()
	numStr := strconv.Itoa(num)
	if strings.HasPrefix(numStr, MagicNum) {
		ch <- fmt.Sprintf("矿工编号 %d, 挖矿成功 %d", n, num)
	}
	// } else {
	// 	fmt.Printf("矿工编号 %d, 计算hash %d\n", n, num)
	// }
}
```

### 7.3 数据竞争与锁

```Go
package main

import (
	"fmt"
	"sync"
)

var wg sync.WaitGroup

var lock sync.Mutex

func main() {
	fmt.Println("数据竞争与锁")

	var x int

	// 自增+1
	for i := 0; i < 1000; i++ {
		wg.Add(1)
		go func() {
			defer wg.Done()
			lock.Lock()
			x++
			lock.Unlock()
		}()
	}

	// 自增-1
	for i := 0; i < 1000; i++ {
		wg.Add(1)
		go func() {
			defer wg.Done()
			lock.Lock()
			x--
			lock.Unlock()
		}()
	}

	wg.Wait()
	fmt.Println("计算后 x =", x)
}

// go run -race .\race.go
// atomic.AddInt32(&x, 1)
```

### 7.4 select

```Go
package main

import "fmt"

func main() {
	fmt.Println("select")

	ch := make(chan int)
	go func() {
		sum := 0
		for i := 0; i < 1000; i++ {
			sum += i
			ch <- sum
		}
		close(ch)
	}()

	ch1 := make(chan int)
	go func() {
		sum := 0
		for i := 0; i < 1000; i++ {
			sum += i
			ch1 <- sum
		}
		close(ch1)
	}()

	// 1.for
	// for {
	// 	value, ok := <-ch
	// 	if ok {
	// 		fmt.Println("ch =", value)
	// 	} else {
	// 		break
	// 	}
	// }

	// 2.for range
	// for c := range ch {
	// 	fmt.Println("range ch =", c)
	// }

	// switch类似
	// select 当多个分支条件满足时，会随机选择一个分支执行
	for {
		select {
		// 必须是一个channel的IO操作，要么读，要么写
		case value, ok := <-ch:
			if ok {
				fmt.Println("select ch =", value)
			}
		case value, ok := <-ch1:
			if ok {
				fmt.Println("select ch1 =", value)
			}
		}
	}

	// fmt.Println("main结束")
}
```

### 7.5 计时器和定时器

```Go
package main

import (
	"fmt"
	"time"
)

func main() {
	fmt.Println("计时器和定时器")

	// 计时器
	ticker := time.NewTicker(time.Second * 5)

	// 定时器，只会执行一次
	timer := time.NewTimer(time.Second * 3)
	timeout := make(chan bool)
	go func() {
		<-time.After(time.Second * 8)
		timeout <- true
	}()
	for {
		select {
		case <-ticker.C:
			fmt.Println("上报服务器数据...")
		case <-timer.C:
			fmt.Println("3s后执行...")
		case <-timeout:
			fmt.Println("8秒超时...")
		default:
			fmt.Println("服务器运行中...")
			time.Sleep(time.Second * 2)
		}
	}
}
```

### 7.6 context

```Go
package main

import (
	"context"
	"fmt"
	"time"
)

type MyKey string
type MyValue string

func main() {
	fmt.Println("context")

	// 1. runtime.Goexit()
	// 2. channel

	// ch := make(chan bool)
	// go func() {
	// 	go func ()  {}()
	// 	go func ()  {}()
	// 	for {
	// 		select {
	// 		case <-ch:
	// 			fmt.Println("我要结束了")
	// 			return
	// 		default:
	// 			fmt.Println("我是协程...")
	// 			time.Sleep(time.Second)
	// 			// runtime.Goexit()
	// 		}
	// 	}
	// }()
	// <-time.After(time.Second * 3)
	// ch <- true

	// 1 WithCancel
	// 2 WithDeadline
	// 3 WithTimeout
	// 4 WithValue

	// ctx, cancel := context.WithCancel(context.Background())
	// go TestCancel(ctx)

	// ctx, _ := context.WithDeadline(context.Background(), time.Now().Add(time.Second*5))
	// go TestDeadline(ctx)

	// ctx, _ := context.WithTimeout(context.Background(), time.Second*3)
	// go TestTimeout(ctx)

	var myKey MyKey = "key"
	var myValue MyValue = "我是值"
	ctx := context.WithValue(context.Background(), myKey, myValue)
	go TestValue(ctx, myKey)

	<-time.After(time.Second * 10)
	// cancel()
	// <-time.After(time.Second * 2)
	fmt.Println("main结束")
}

// 1
func TestCancel(ctx context.Context) {
	for {
		select {
		case <-ctx.Done():
			fmt.Println("主协程取消了，我是子协程也同时结束了...")
			return
		default:
			fmt.Println("TestCancel 我是子协程，我在运行中..")
			time.Sleep(time.Second)
		}
	}
}

// 2
func TestDeadline(ctx context.Context) {
	for {
		select {
		case <-ctx.Done():
			fmt.Println("我是子协程，我运行了5秒就结束了...")
			return
		default:
			fmt.Println("TestDeadline 我是子协程，我在运行中..")
			time.Sleep(time.Second)
		}
	}
}

// 3
func TestTimeout(ctx context.Context) {
	<-time.After(time.Second * 5)
	for {
		select {
		case <-ctx.Done():
			fmt.Println("我是子协程，我超时3秒就结束了...")
			return
		default:
			fmt.Println("TestTimeout 我是子协程，我在运行中..")
			time.Sleep(time.Second)
		}
	}
}

// 4
func TestValue(ctx context.Context, myKey MyKey) {
	for {
		select {
		default:
			fmt.Println("TestValue 我是子协程，我获取到了参数", ctx.Value(myKey))
			time.Sleep(time.Second)
		}
	}
}
```

## 8. 测试与文档

### 8.1 测试

- 单元测试
- 性能测试

定义方法

```Go
package demo

// Add
func Add(a, b int) int {
	return a + b
}

// Mul
func Mul(a, b int) int {
	return a * b
}
```

单元测试

```Go
package test

import (
	"testing"

	"github.com/Mark-Clinton02/Demo07/demo"
)

// 测试文件必须以_test.go结尾

// 测试用例

func TestAdd(t *testing.T) {
	// 准备要测试的数据
	// 表格驱动测试
	data := []struct{ a, b, expect int }{
		{1, 2, 3},
		{2, 2, 4},
		{100, 9, 109},
		{36, 51, 87},
		{55, 22, 77},
	}

	for _, row := range data {
		actual := demo.Add(row.a, row.b)
		if actual != row.expect {
			// t.Fail()
			t.Errorf("输入 a = %d, b = %d, 实际计算结果为 actual = %d, 期望值为 expect = %d", row.a, row.b, actual, row.expect)
		}
	}
}

func TestMul(t *testing.T) {
	// 准备要测试的数据
	// 表格驱动测试
	data := []struct{ a, b, expect int }{
		{3, 3, 9},
		{4, 5, 20},
		{11, 11, 121},
	}

	for _, row := range data {
		actual := demo.Mul(row.a, row.b)
		if actual != row.expect {
			// t.Fail()
			t.Errorf("输入 a = %d, b = %d, 实际计算结果为 actual = %d, 期望值为 expect = %d", row.a, row.b, actual, row.expect)
		}
	}
}
```

联合测试

```Go
package test

import (
	"testing"
	"time"

	"github.com/Mark-Clinton02/Demo07/demo"
)

// 测试文件必须以_test.go结尾

// 测试用例

func testAdd(t *testing.T) {
	t.Parallel()
	<-time.After(time.Second * 3)
	// 准备要测试的数据
	// 表格驱动测试
	data := []struct{ a, b, expect int }{
		{1, 2, 3},
		{2, 2, 4},
		{100, 9, 109},
		{36, 51, 87},
		{55, 22, 77},
	}

	for _, row := range data {
		actual := demo.Add(row.a, row.b)
		if actual != row.expect {
			// t.Fail()
			t.Errorf("输入 a = %d, b = %d, 实际计算结果为 actual = %d, 期望值为 expect = %d", row.a, row.b, actual, row.expect)
		}
	}
}

func testMul(t *testing.T) {
	t.Parallel()
	<-time.After(time.Second * 1)
	// 准备要测试的数据
	// 表格驱动测试
	data := []struct{ a, b, expect int }{
		{3, 3, 9},
		{4, 5, 20},
		{11, 11, 121},
	}

	for _, row := range data {
		actual := demo.Mul(row.a, row.b)
		if actual != row.expect {
			// t.Fail()
			t.Errorf("输入 a = %d, b = %d, 实际计算结果为 actual = %d, 期望值为 expect = %d", row.a, row.b, actual, row.expect)
		}
	}
}

func TestCombin(t *testing.T) {
	// 初始化工作
	t.Run("Add", testAdd)
	t.Run("Mul", testMul)
	// 收尾
}
```

性能测试

```Go
package test

import (
	"testing"

	"github.com/Mark-Clinton02/Demo07/demo"
)

// 性能测试用例名称必须以Benchmark开头，后面一般是测试的方法或函数名
func BenchmarkAdd(t *testing.B) {
	// 循环
	for i := 0; i < t.N; i++ {
		demo.Add(88, 11)
	}
}
```

### 8.2 文档与示例

```Go
// 包注释 - 我的包名demo
package demo

import "fmt"

// 常量注释 - 最大连接数
const (
	MaxConnections = 100
)

// 全局变量注释 - 数据库对象实例
var (
	Db *Database
)

// 数据库结构对象
type Database struct {
	Host string
	Port string
}

// 方法注释 - 连接到一个数据库
func (db *Database) Connect(dbName string) *Database {
	fmt.Println("模拟数据库连接...", dbName)
	return db
}

// 方法注释 - 执行SQL语句
func (db *Database) ExecuteSql(sql string) {
	fmt.Println("执行SQL语句...", sql)
}

// 函数注释 - 创建一个数据库对象实例
func NewDatabase(host, port string) *Database {
	return &Database{
		Host: host,
		Port: port,
	}
}
```

```Go
package demo

func ExampleDatabase() {
	db := NewDatabase("127.0.0.1", "3306")
	db.Connect("demo").ExecuteSql("select * from demo")

	// Output:
	// 模拟数据库连接... demo
	// 执行SQL语句... select * from demo
}
```

主要使用工具：godoc
