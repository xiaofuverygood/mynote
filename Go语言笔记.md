

# 		小付的Go语言笔记

## GO语言介绍

​	Go语言（Golang）是Google开发的开源编程语言，诞生于2006年1月2日下午3点4分5秒，于2009年11月开源，2012年发布go稳定版。Go语言在多核并发上拥有原生的设计优势，Go语言从底层原生支持并发，无须第三方库。

​	Go语言的并发是基于 `goroutine` 的，`goroutine` 类似于线程，但并非线程。可以将 `goroutine` 理解为一种虚拟线程。Go 语言运行时会参与调度 `goroutine`，并将 `goroutine` 合理地分配到每个 CPU 中，最大限度地使用CPU性能。开启一个goroutine的消耗非常小（大约2KB的内存），你可以轻松创建数百万个`goroutine`。

​	Go 语言简单易学，学习曲线平缓，不需要像 C/C++ 语言动辄需要两到三年的学习期。Go 语言被称为“互联网时代的C语言”。Go 语言的风格类似于C语言。其语法在C语言的基础上进行了大幅的简化，去掉了不需要的表达式括号，循环也只有 for 一种表示方法，就可以实现数值、键值等各种遍历。 



### 来历

​	很久以前，有一个IT公司，这公司有个传统，允许员工拥有20%自由时间来开发实验性项目。在2007的某一天，公司的几个大牛，正在用c++开发一些比较繁琐但是核心的工作，主要包括庞大的分布式集群，大牛觉得很闹心，后来c++委员会来他们公司演讲，说c++将要添加大概35种新特性。这几个大牛的其中一个人，名为：Rob Pike，听后心中一万个🦙飘过，“c++特性还不够多吗？简化c++应该更有成就感吧”。于是乎，Rob Pike和其他几个大牛讨论了一下，怎么解决这个问题，过了一会，Rob Pike说要不我们自己搞个语言吧，名字叫“go”，非常简短，容易拼写。其他几位大牛就说好啊，然后他们找了块白板，在上面写下希望能有哪些功能。接下来的时间里，大牛们开心的讨论设计这门语言的特性，经过漫长的岁月，他们决定，以c语言为原型，以及借鉴其他语言的一些特性，来解放程序员，解放自己，然后在2009年，go语言诞生。



### 优点

​	自带gc。

​	静态编译，编译好后，扔服务器直接运行。

​	简单的思想，没有继承，多态，类等。

​	丰富的库和详细的开发文档。

​	语法层支持并发，和拥有同步并发的channel类型，使并发开发变得非常方便。

​	简洁的语法，提高开发效率，同时提高代码的阅读性和可维护性。

​	超级简单的交叉编译，仅需更改环境变量。



### Go语言的主要特征

 	1.自动立即回收。
 	2.更丰富的内置类型。
 	3.函数多返回值。
 	4.错误处理。
 	5.匿名函数和闭包。
 	6.类型和接口。
 	7.并发编程。
 	8.反射。
 	9.语言交互性。



### Go的25个关键字

```go
    break        default      func         interface    select
    case         defer        go           map          struct
    chan         else         goto         package      switch
    const        fallthrough  if           range        type
    continue     for          import       return       var
```

### Go的37个保留字

```go
   Constants:    true  false  iota  nil

    Types:    int  int8  int16  int32  int64  
              uint  uint8  uint16  uint32  uint64  uintptr
              float32  float64  complex128  complex64
              bool  byte  rune  string  error

    Functions:   make  len  cap  new  append  copy  close  delete
                 complex  real  imag
                 panic  recover
```

### 可见性

​	1.声明在函数内部，是函数的本地值，类似private

​	2.声明在函数外部，是对当前包可见(包内所有.go文件都可见)的全局值，类似protect

​	3.声明在函数外部且首字母大写是所有包可见的全局值,类似public



### Go语言声明

```go
var（声明变量）, const（声明常量）, type（声明类型）,func（声明函数）
```



## Go 语言环境安装

安装包下载地址：https://golang.google.cn/dl/

配置环境变量：

1.在~/.bash_profile 或 /etc/profile文件内添加环境变量：

​	export GO_HOME=/usr/local/go/bin

​	export PATH=$PATH:$GO_HOME

2.通过加载更新后的文件

​	source ~/.bash_profile

开发工具下载地址：https://www.jetbrains.com.cn/go/



## Go语言结构

- 
  包声明
- 引入包
- 函数
- 变量
- 语句 & 表达式
- 注释

```go
package main	// 包声明

import "fmt"	// 引入包

func main() {
  
    var val string = "Hello wrld!"	// 变量

    fmt.Println(val) // 函数
}
```

注意：

1. 必须在源文件中非注释的第一行指明这个文件属于哪个包；

2. 文件夹名与包名没有直接关系，并非需要一致；

3. 同一个文件夹下的文件只能有一个包名，否则编译报错；

4. 一个 Go 项目中只能有一个 main 包，并且一个 main 包只能有一个 main 函数；

5. main 函数是每一个可执行程序所必须包含的，是在启动后第一个执行的函数（如果有 init() 函数则会先执行该函数）

   ⚠️当程序任何位置都没有使用某个包，那么该包内的init函数不会执行（可以使用_ 空引用的方式使用包）；

6. 强制函数左花括号 `{` 的放置位置，左花括号 `{` 必须在函数定义行的末尾，不能另起一行；



## Go 语言命令

在 Go 语言中，可以使用命令行传递参数，可以在 `go run` 命令后面跟上一个或多个参数。这些参数可以在程序中通过 `os.Args` 来访问，`os.Args` 是一个字符串切片。

```shell
go env	# 用于打印Go语言的环境信息

go mod init <module_name>	# 初始化Go模块

go mod tidy	# 用于清理未使用的依赖项

go get <package>	# 获取和管理项目的依赖包添加到 go.mod 文件中
go get -u <package>	# 更新到最新的版本的依赖包
go get -u ./... # 更新所有依赖包

go run <name> <args...>	# 运行 go 文件

go build <name> # 生成二进制文件可直接运行
go build -o <路径/../文件名> <name> # 可以指定编译后的文件名

go fmt <文件名> # 格式化go语言源代码文件
```



## Go 语言基础语法

### 规范

1. Go 程序由多个标记组成，可以是关键字，标识符，常量，字符串，符号。
2. Go 语言一行代表一个语句结束，每行语句不需要像Java一样写 ; 号结束。
3. 在 Go 语言中，也可以使用分号来显式地将多个语句放在同一行上。

```go
var x int; x = 10; fmt.Println(x)
```



### 格式化字符串

- %d 表示整型数字
- %s 表示字符串

Go 语言中使用 **fmt.Sprintf** 或 **fmt.Printf** 格式化字符串并赋值给新串：

```go
package main

import "fmt"

func main() {

  // Sprintf 根据格式化参数生成格式化的字符串并返回该字符串
	var code = 123
	var date = "2020-12-31"
	var urlTemplate = "Code=%dDate=%s"
	var url= fmt.Sprintf(urlTemplate, code, date)
  
	fmt.Println(target_url)

}
```

输出:

```
Code=123&Date=2020-12-31
```

```go
package main

import "fmt"

func main() {

	// Printf 根据格式化参数生成格式化的字符串并写入标准输出。
	var code = 123
	var date = "2020-12-31"
	var url = "Code=%d&Date=%s"

	fmt.Printf(url, code, date)

}
```

输出：

```
Code=123&Date=2020-12-31%
```

## Go语言数据类型

### 标准数据类型

```go
   bool	// 布尔型，值只可以是常量 true 或者 false
   
	 int(32 or 64), int8, int16, int32, int64 // 数值型，
	 
	 uint(32 or 64), uint8(byte), uint16, uint32, uint64 // 无符号数值型
   
	 float32, float64	// 浮点型

   string // Go 的字符串是由单个字节连接起来的。Go 语言的字符串的字节使用 UTF-8 编码标识 Unicode 文本

   complex64, complex128 // 复数类型，表示实数和虚数

	 uintptr // 无符号整型，用于存放一个指针


```

### 派生类型

```
指针类型(Pointer)
数组类型(array) 
结构化类型(struct)
管道类型(chan)
函数类型(func)
切片类型(slice)
接口类型(interface)
映射类型(map)
```



### 自定义数据类型

我们定义了一个自定义别名 MyString，它是 string 类型的别名。通过使用这个自定义别名，我们可以创 MyString 类型的变量并对它进行操作，就像使用普通的 string 类型一样。

```go
package main

import "fmt"

// 自定义别名
type MyString string

func main() {
    var message MyString
    message = "Hello, World!"
    fmt.Println(message) // 输出: Hello, World!

    // 使用自定义别名进行字符串拼接
    greeting := message + " Welcome!"
    fmt.Println(greeting) // 输出: Hello, World! Welcome!
}
	
```



⚠️Go语言中只有强制类型转换，没有隐式类型转换。



## 变量

​	Go 语言变量名由字母、数字、下划线组成，其中首个字符不能为数字，声明变量的一般形式是使用 var 关键字，局部变量定义后未使用编译会报错。

​	Go语言在声明变量的时候，会自动对变量对应的内存区域进行初始化操作。每个变量会被初始化成其类型的默认值，例如： 整型和浮点型变量的默认值为0。 字符串变量的默认值为空字符串。 布尔型变量默认为`false`。 切片、函数、指针变量的默认为`nil`。

### 格式

```go
var identifier type
```

声明多个变量

```go
var identifier1, identifier2, type
```



### 变量声明

第一种：声明变量指定类型不赋值，初始化时系统默认设置值。

- 数值类型（包括complex64/128）为 **0**

- 布尔类型为 **false**

- 字符串为 **""**（空字符串）

- 以下几种类型为 **nil**：

  ```go
  var a *int	// 指针	
  var a []int	// 切片
  var a map[string] int	// map集合
  var a chan int	// 通道
  var a func(string) int	// 方法
  var a error // error 接口
  ```



第二种：声明是不需要添加类型，可根据值类型自行判断（隐式类型定义）。

```go
var name = "jerry"
var age = 10

var str = "name:%s, age:%d"
fmt.Printf(str, name, age)
```



第三种：声明 + 赋值 只能被用在函数体内（如果变量已经使用 var 声明过了，再使用 := 声明变量，就产生编译错误）

```go
identifier := value
```

```go
name := "tom"
fmt.Printf(name)
```



### 多变量声明

```go
// 类型相同的多个变量
var name1, name2, name3 string = "tom", "jerry", "spike"
fmt.Println(name1, name2, name3)
```

```go
// 类型不同的多个变量
var name, age, sex = "tom", 18, "男"
fmt.Println(name, age, sex)
```



### 全局变量

这种因式分解关键字的写法一般用于声明全局变量，全局变量未使用编译不会报错。

局部变量可以和全局变量可以同时定义，就近原则会使用局部变量的值。

```go
// 这种因式分解关键字的写法一般用于声明全局变量
var (
    vname1 v_type1
    vname2 v_type2
)
```



## 常量

常量是一个简单值的标识符，在程序运行时，不会被修改的量，常量中的数据类型只可以是布尔型、数字型（整数型、浮点型和复数）和字符串型。

### 格式

显示类型定义

```
const identifier [type] = value
```

隐式类型定义

```
const identifier = value
```

多个相同类型

```
const c_name1, c_name2 = value1, value2
```



### 枚举

常量还可以用作枚举，如果没有显式为常量赋值，Go 语言会根据前一个常量的值自动推导后续常量的值。

```go
const (
    name1 = value1
    name2 = value2
    name3 = value3
)
```



### 内置函数

常量可以用**len(), cap(), unsafe.Sizeof()**函数计算表达式的值。常量表达式中，函数必须是内置函数，否则编译不过。

```go
package main

import "unsafe"

const (
    a = "abc"
    b = len(a)	// 计算a的长度
    c = unsafe.Sizeof(a)	计算变量a所占用的内存空间大小
)

func main(){
    println(a, b, c)
}
// cap()用于获取切片（slice）或数组（array）的容量。
```



### iota

iota，特殊常量，可以认为是一个可以被编译器修改的常量，iota 在 const关键字出现时将被重置为 0(const 内部的第一行之前)，const 中每新增一行常量声明将使 iota 计数一次。

```go
const (
		i0 = iota
		i1 = iota
		i2 = iota
	)

	fmt.Println(i0, i1, i2)
```

```
输出：0 1 2
```

第一个 iota 等于 0，每当 iota 在新的一行被使用时，它的值都会自动加1；所以 a=0, b=1, c=2 可以简写

```go
const (
		i0 = iota
		i1
		i2
	)

fmt.Println(i0, i1, i2)
```



## 运算符

Go语言的运算符与Java类似，以下简举几个：

### 位运算符

位运算符对整数在内存中的二进制位进行操作。

| 运算符 | 描述                                                         | 实例                                   |
| :----- | :----------------------------------------------------------- | :------------------------------------- |
| &      | 按位与运算符"&"是双目运算符。 其功能是参与运算的两数各对应的二进位相与。 | (A & B) 结果为 12, 二进制为 0000 1100  |
| \|     | 按位或运算符"\|"是双目运算符。 其功能是参与运算的两数各对应的二进位相或 | (A \| B) 结果为 61, 二进制为 0011 1101 |
| ^      | 按位异或运算符"^"是双目运算符。 其功能是参与运算的两数各对应的二进位相异或，当两对应的二进位相异时，结果为1。 | (A ^ B) 结果为 49, 二进制为 0011 0001  |
| <<     | 左移运算符"<<"是双目运算符。左移n位就是乘以2的n次方。 其功能把"<<"左边的运算数的各二进位全部左移若干位，由"<<"右边的数指定移动的位数，高位丢弃，低位补0。 | A << 2 结果为 240 ，二进制为 1111 0000 |
| >>     | 右移运算符">>"是双目运算符。右移n位就是除以2的n次方。 其功能是把">>"左边的运算数的各二进位全部右移若干位，">>"右边的数指定移动的位数。 | A >> 2 结果为 15 ，二进制为 0000 1111  |

### 其他运算符

下表列出了Go语言的其他运算符。

| 运算符 | 描述             | 实例                       |
| :----- | :--------------- | :------------------------- |
| &      | 返回变量存储地址 | &a; 将给出变量的实际地址。 |
| *      | 指针变量。       | *a; 是一个指针变量         |

### 运算符优先级

有些运算符拥有较高的优先级，二元运算符的运算方向均是从左至右。下表列出了所有运算符以及它们的优先级，由上至下代表优先级由高到低：

| 优先级 | 运算符           |
| :----- | :--------------- |
| 5      | * / % << >> & &^ |
| 4      | + - \| ^         |
| 3      | == != < <= > >=  |
| 2      | &&               |
| 1      | \|\|             |

当然，你可以通过使用括号来临时提升某个表达式的整体运算优先级。



## 字符串

### 转义符

Go 语言的字符串常见转义符包含回车、换行、单双引号、制表符等，如下表所示。

| 转义 | 含义                               |
| ---- | ---------------------------------- |
| \r   | 回车符（返回行首）                 |
| \n   | 换行符（直接跳到下一行的同列位置） |
| \t   | 制表符                             |
| \'   | 单引号                             |
| \"   | 双引号                             |
| \    | 反斜杠                             |

### 多行字符串

Go语言中要定义一个多行字符串时，就必须使用`反引号`字符

```go
    s1 := 
		`第一行
   	 第二行
   	 第三行
    `
    fmt.Println(s1)
```

反引号间换行将被作为字符串中的换行，但是所有的转义字符均无效，文本将会原样输出。

### 字符串的常用操作

| 方法                                | 介绍           |
| ----------------------------------- | -------------- |
| len(str)                            | 求长度         |
| +或fmt.Sprintf                      | 拼接字符串     |
| strings.Split                       | 分割           |
| strings.Contains                    | 判断是否包含   |
| strings.HasPrefix,strings.HasSuffix | 前缀/后缀判断  |
| strings.Index(),strings.LastIndex() | 子串出现的位置 |
| strings.Join(a[]string, sep string) | join操作       |



## 下划线



zai go语言中 `"_" ` 是特殊标识符，用来忽略结果。

1. import 下划线的作用：当导入一个包时，该包下的文件里所有init()函数都会被执行，然而，有些时候我们并不需要把整个包都导入进来，仅是希望它执行init()函数。这个时候就可以使用 import _ "./package"引用该包。

   ```go
   package main
   
   import _ "./hello"
   
   func main() {
     
     // code
     
   }
   ```

2. 下划线意思是忽略这个变量，比如os.Open，返回值为*os.File，error，普通写法是f,err := os.Open("xxxxxxx")，如果此时不需要知道返回的错误值就可以用f, _ := os.Open("xxxxxx")如此则忽略了error变量。



## Go 语言条件语句

条件语句需要开发者通过指定一个或多个条件，并通过测试条件是否为 true 来决定是否执行指定语句，并在条件为 false 的情况在执行另外的语句。

### if语句

格式

```go
if 布尔表达式 {
   /* 在布尔表达式为 true 时执行 */
}
```

示例

```go
num := 20

// if表达式不用加括号
if num == 20 {
	fmt.Println("num等于20", num)
}
```

### switch 语句

switch 默认情况下 case 最后自带 break 语句，匹配成功后就不会执行其他 case，如果我们需要执行后面的 case，可以使用 **fallthrough** 。

格式

```go
switch var1 {
    case val1:
        ...
    case val2:
        ...
    default:
        ...
}
```

示例

```go
/* 
	switch 语句不需要加 break 
	表达式不需要加括号
	case支持多条件匹配
*/
score := 50

	switch score {
	case 90:
		fmt.Println("优秀")
	case 80:
		fmt.Println("良好")
	// switch 支持多条件匹配
	case 70, 60:
		fmt.Println("及格")
	default:
		fmt.Println("不及格")
	}
```

#### Type Switch

switch 语句还可以被用于 type-switch 来判断某个 interface 变量中实际存储的变量类型。

格式

```go
switch x.(type){
    case type:
       statement(s);      
    case type:
       statement(s); 
    /* 你可以定义任意个数的case */
    default: /* 可选 */
       statement(s);
}
```

示例

```go
var x interface{}

	// type-switch 来判断某个 interface 变量中实际存储的变量类型
	switch i := x.(type) {
	case nil:
		fmt.Printf(" x 的类型 :%T", i)
	case int:
		fmt.Printf("x 是 int 型")
	case float64:
		fmt.Printf("x 是 float64 型")
	case func(int) float64:
		fmt.Printf("x 是 func(int) 型")
	case bool, string:
		fmt.Printf("x 是 bool 或 string 型")
	default:
		fmt.Printf("未知型")
	}
```

#### fallthrough

使用 fallthrough 会强制执行后面的 case 语句，fallthrough 不会判断下一条 case 的表达式结果是否为 true。

示例

```go
// switch 没有表达式默认 true
switch {
    case false:
            fmt.Println("1、case 条件语句为 false")
            fallthrough
    case true:
            fmt.Println("2、case 条件语句为 true")
            fallthrough
    case false:
            fmt.Println("3、case 条件语句为 false")
            fallthrough
    case true:
            fmt.Println("4、case 条件语句为 true")
    case false:
            fmt.Println("5、case 条件语句为 false")
            fallthrough
    default:
            fmt.Println("6、默认 case")
    }
```

```
输出：	2、case 条件语句为 true
			3、case 条件语句为 false
			4、case 条件语句为 true
```

### select 语句

select 是 Go 中的一个控制结构，类似于 switch 语句。

1. select 语句只能用于通道操作，每个 case 必须是一个通道操作，要么是发送要么是接收。
2. select 语句会监听所有指定的通道上的操作，一旦其中一个通道准备好就会执行相应的代码块。
3. 如果多个通道都准备好，那么 select 语句会随机选择一个通道执行。如果所有通道都没有准备好，那么执行 default 块中的代码。
4. 如果没有  default 子句 select 将阻塞，直到某个通道可以运行；Go 不会重新对 channel 或值进行求值。

示例

```go
// 创建两个无缓冲通道	无缓冲通道的容量为 0，因此它只能用于同步通信
	c1 := make(chan string)
	c2 := make(chan string)

	/*
		goroutine 是在后台异步运行
		如果需要等待这些 goroutine 执行完成后再继续执行主程序，可以使用通道阻塞等待的方式
		当向无缓冲通道发送数据时，发送者会阻塞，直到接收者从通道中接收了这个数据。类似地，当从无缓冲通道接收数据时，接收者会阻塞，直到发送者向通道中发送了这个数据
	*/

	// 创建了两个新的 goroutine
	go func() {
		time.Sleep(1 * time.Second)
		c1 <- "one"
	}()

	go func() {
		time.Sleep(2 * time.Second)
		c2 <- "two"
	}()

	for i := 0; i < 2; i++ {
		select {
		case msg1 := <-c1:
			fmt.Println("received", msg1)
		case msg2 := <-c2:
			fmt.Println("received", msg2)
		}
	}
```

```
输出：received one
		 received two
```



## 循环语句

Go 语言的 For 循环有 3 种形式，只有其中的一种使用分号。

### 写法格式

```go
// 方式一
	sum := 0
	for i := 0; i <= 10; i++ {
		sum += i
	}
	fmt.Println(sum
```

```go
// 方式二(类似于wehile循环)
	sum2 := 1
	for ; sum2 <= 10 ; {
		sum2 += sum2
	}
	fmt.Println(sum2)
```

```go
	// 方式三 这样写也可以，更像 While 语句形式
	sum3 := 1
	for sum3 <= 10 {
		sum3 += sum3
	}
	fmt.Println(sum3)
```

```go
	// 无限循环
	sum4 := 0
	for {
		sum4++
	}
	fmt.Println(sum4)
```

### For-each range 循环

For-each range 循环，这种格式的循环可以对字符串、数组、切片等进行迭代输出元素。

示例

```go
// 切片
strs := []string{"google", "runoob"}
for index, value := range strs {
	fmt.Println(index, value)
}

// 数组
nums := [6]int{1, 2, 3}
for i, v := range nums {
	fmt.Printf("第 %d 位 x 的值 = %d\n", i, v)
}

```

```
输出：0 google
		 1 runoob
		 第 0 位 x 的值 = 1
		 第 1 位 x 的值 = 2
		 第 2 位 x 的值 = 3
```

```go
// 注意：range 是 Go 语言中的一个关键字，用于在 for 循环中迭代数组、切片、映射、字符串等数据结构中的元素。range 迭代映射时，返回的键值对的顺序是随机的。

// for 循环的 range 格式可以省略 key 和 value
	map1 := make(map[int]float32)	// 定义一个map集合
	map1[1] = 1.0
	map1[2] = 2.0
	map1[3] = 3.0
	map1[4] = 4.0

	// 读取 key 和 value
	for key, value := range map1 {
		fmt.Printf("key is: %d - value is: %f\n", key, value)
	}

	// 读取 key(range一个参数默认返回key)
	for key := range map1 {
		fmt.Printf("key is: %d\n", key)
	}

	// 读取 value	(_（下划线）作为占位符，用于表示一个不需要使用的变量或值)
	for _, value := range map1 {
		fmt.Printf("value is: %f\n", value)
	}
```

### break语句

Go 语言中 break 语句用于以下两方面：

- ​	用于循环语句中跳出循环，并开始执行循环之后的语句
- ​	在多重循环中，可以用标号 label 标出想 break 的循环

示例

```go
// 用标号 label 标出想 break 的循环
re:
	for i := 1; i <= 3; i++ {
		fmt.Printf("i: %d\n", i)
    
		for i2 := 11; i2 <= 13; i2++ {
			fmt.Printf("i2: %d\n", i2)
			break re
		}
    
	}
```

```
输出：i: 1
		 i2: 11    
```



### continue语句

- continue 语句不是跳出循环，而是跳过当前循环执行下一次循环语句。
- 在多重循环中，可以用标号 label 标出想 continue 的循环。

```go
re:
	for i := 1; i <= 3; i++ {
		fmt.Printf("i: %d\n", i)

		for i2 := 11; i2 <= 13; i2++ {
			fmt.Printf("i2: %d\n", i2)
			continue re
		}

	}
```

```
输出：i: 1
		 i2: 11
		 i: 2
		 i2: 11
		 i: 3
		 i2: 11
```



### goto语句

- Go 语言的 goto 语句可以无条件地转移到过程中指定的行。
- goto 语句通常与条件语句配合使用。可用来实现条件转移， 构成循环，跳出循环体等功能。

```go
var b = 10

LOOP:
	for b < 14 {
    
		if b == 12 {
			/* 跳过迭代 */
			b = b + 1
			goto LOOP
		}
    
		fmt.Printf("b的值为 : %d\n", b)
		b++
	}
```

```
输出：b的值为 : 10
		 b的值为 : 11
		 b的值为 : 13
```



## Go语言函数

你可以通过函数来划分不同功能，逻辑上每个函数执行的是指定的任务，函数声明告诉了编译器函数的名称，返回类型，和参数。

- 函数开头一定要大写**, go**约定大写开头的标识符才能被**import**使用。
- 调用本包内的函数，函数首字母不需要大写。
- 一个函数可以有多个返回值。



### go语言常见的内置函数

```go
    append         -- 用来追加元素到数组、slice中,返回修改后的数组、slice
    close          -- 主要用来关闭channel和释放资源
    delete         -- 从map中删除key对应的value
		panic          -- 停止常规的goroutine(panic和recover：用来做错误处理)
    recover        -- 允许程序定义goroutine的panic动作
    imag           -- 返回complex的实部   （complex、real imag：用于创建和操作复数）
    real           -- 返回complex的虚部
    make           -- 用来分配内存，返回Type本身(只能应用于slice, map, channel)
    new            -- 用来分配内存，主要用来分配值类型，比如int、struct。返回指向Type的指针
    cap            -- capacity是容量的意思，用于返回某个类型的最大容量（只能用于切片和 map）
    copy           -- 用于复制和连接slice，返回复制的数目
    len            -- 来求长度，比如string、array、slice、map、channel ，返回长度

    print
		println    		 -- 底层打印函数，在部署环境中建议使用 fmt 包
```



###  Init函数

​	go语言中`init`函数用于包`(package)`的初始化，该函数是go语言的一个重要特性。

```
    1 init函数是用于程序执行前做包的初始化的函数，比如初始化包里的变量等

    2 每个包可以拥有多个init函数

    3 包的每个源文件也可以拥有多个init函数

    4 同一个包中多个init函数的执行顺序go语言没有明确的定义(说明)

    5 不同包的init函数按照包导入的依赖关系决定该初始化函数的执行顺序

    6 init函数不能被其他函数调用，而是在main函数执行之前，自动被调用
```

###  main函数

```
    Go语言程序的默认入口函数(主函数)：func main()
    函数体用｛｝一对括号包裹。

    func main(){
        //函数体
    }
```

### init函数和main函数的异同

```go
   相同点：
        两个函数在定义时不能有任何的参数和返回值，且Go程序自动调用。
    不同点：
        init可以应用于任意包中，且可以重复定义多个。
        main函数只能用于main包中，且只能定义一个。
```

两个函数的执行顺序：

对同一个go文件的`init()`调用顺序是从上到下的。

对同一个package中不同文件是按文件名字符串比较“从小到大”顺序调用各文件中的`init()`函数。

对于不同的`package`，如果不相互依赖的话，按照main包中"先`import`的后调用"的顺序调用其包中的`init()`，如果`package`存在依赖，则先调用最早被依赖的`package`中的`init()`，最后调用`main`函数。

如果`init`函数中使用了`println()`或者`print()`你会发现在执行过程中这两个不会按照你想象中的顺序执行。这两个函数官方只推荐在测试环境中使用，对于正式环境不要使用。



### 函数定义

```go
func function_name( [parameter list] ) [return_types] {
   // 函数体
}
```

示例

```go
func Add(x, y int) int {
  
	return x + y
}
```

### 函数返回多个值

示例

```go
func swap(x, y string) (string, string) {
   return y, x
}
```



### 函数参数

#### 值传递

传递是指在调用函数时将实际参数复制一份传递到函数中，这样在函数中如果对参数进行修改，将不会影响到实际参数。

默认情况下，Go 语言使用的是值传递，即在调用过程中不会影响到实际参数。

```go
/* 定义相互交换值的函数 */
func swap(x, y int) int {
   var temp int

   temp = x
   x = y
   y = temp

   return temp;
}
```

#### 引用传递

引用传递是指在调用函数时将实际参数的地址传递到函数中，那么在函数中对参数所进行的修改，将影响到实际参数。

引用传递指针参数传递到函数内，以下是交换函数 swap() 使用了引用传递：

```go
/* 定义交换值函数*/
func swap(x *int, y *int) {
   var temp int
   temp = *x
   *x = *y
   *y = temp
}
```



### 函数用法

#### 函数作为另外一个函数的实参

Go 语言可以很灵活的创建函数，并作为另外一个函数的实参。以下实例中我们在定义的函数中初始化一个变量，该函数仅仅是为了使用内置函数

```go
// 函数作为实参(高阶函数)
func printResult(callback func(int)) {
    result := 42
    callback(result)
}

// 回调函数
func printValue(value int) {
    fmt.Println("Value:", value)
}

func main() {
    // 调用函数，并传递回调函数作为实参
    printResult(printValue)
}
```



### 匿名函数

```go
// 定义并调用匿名函数
func(a, b int) {
	fmt.Println("Hello, World!")
}(1, 2)

// 将匿名函数赋值给变量
greeting := func() {
	fmt.Println("Hello, Go!")
}

// 调用变量中存储的匿名函数
greeting()
```



### 闭包

闭包（Closure）是指在一个函数内部定义的函数，该内部函数可以访问外部函数的变量。

```go
func main() {
	// 外部函数返回一个闭包函数
	generator := generateCounter()

	// 使用闭包函数进行计数
	fmt.Println(generator()) // 输出: 1
	fmt.Println(generator()) // 输出: 2
	fmt.Println(generator()) // 输出: 3
}

func generateCounter() func() int {
	// 外部函数中定义的变量 count
	count := 0

	// 返回一个闭包函数，该闭包函数可以访问外部函数中的变量 count
	return func() int {
		count++
		return count
	}
}
```



### 方法

Go 语言中同时有函数和方法。一个方法就是一个包含了接受者的函数，接受者可以是命名类型或者结构体类型的一个值或者是一个指针。所有给定类型的方法属于该类型的方法集。

```go
func (variable_name variable_data_type) function_name() [return_type]{
   /* 函数体*/
}
```

⚠️如果 接收者 是一个指针类型，那么在方法内部对该类型的字段做出的修改将会被保留，而如果 接收者 是一个值类型，那么方法内部对该类型的字段的修改仅仅是对该值的拷贝做出的修改，并不会影响原始值。

⚠️方法只能由该类型的实例调用。



## Go语言数组

数组：是同一种数据类型的固定长度的序列。

### 声明数组

```go
var name [SIZE] type
```

### 初始化数组

- 初始化数组中 **{}** 中的元素个数不能大于 **[]** 中的数字。
- 如果忽略 **[]** 中的数字不设置数组大小，Go 语言会根据元素的个数来设置数组的大小
- 数组一旦定义，长度不能变

```go
numbers := [5] int {1, 2, 3, 4, 5}

// 如果数组长度不确定，可以使用 ... 代替数组的长度，编译器会根据元素个数自行推断数组的长度
numbers := [...] int {1, 2, 3, 4, 5}

// 初始化指定索引元素
numbers := [...] int {0 : 1， 1 : 2}
```



### 多维数组   

在多维数组中，第 2 纬度不能用 "..."

Go 语言支持多维数组，以下为常用的多维数组声明方式：

```go
var name [SIZE1][SIZE2]...[SIZEN] type
```

示例

```go
// Step 1: 创建数组
    values := [][]int{}

    // Step 2: 使用 append() 函数向空的二维数组添加两行一维数组
    row1 := []int{1, 2, 3}
    row2 := []int{4, 5, 6}
    values = append(values, row1)
    values = append(values, row2)

    // Step 3: 显示两行数据
    fmt.Println("Row 1")
    fmt.Println(values[0])
    fmt.Println("Row 2")
    fmt.Println(values[1])

    // Step 4: 访问第一个元素
    fmt.Println("第一个元素为：")
    fmt.Println(values[0][0])
```



## Go语言指针

变量是一种使用方便的占位符，用于引用计算机内存地址，Go 语言的取地址符是 &，放到一个变量前使用就会返回相应变量的内存地址。

示例

```go
 var a int = 10   

 fmt.Printf("变量的地址: %x\n", &a  )
```

```
输出：20818a220
```

一个指针变量指向了一个值的内存地址，在使用指针前你需要声明指针，指针本身只能指向内存地址，而不能指向其他类型的值，例如常量、表达式、函数等。

### 声明格式

```go
var name *type
```

### 指针的使用

指针使用流程：

- 定义指针变量。
- 为指针变量赋值。
- 访问指针变量中指向地址的值。
- 当一个指针被定义后没有分配到任何变量时，它的值为 nil，也称为空指针。

```go
var a int= 20
var ip *int	// 声明指针

ip = &a	// 将指针指向a的内存地址

fmt.Printf("a 变量的地址是: %x\n", &a  )			 // a的内存地址
fmt.Printf("ip 变量储存的指针地址: %x\n", ip )	 // 指针指向的内存地址
fmt.Printf("*ip 变量的值: %d\n", *ip )				// 指针指向的内容
```

```
输出：a 变量的地址是: 20818a220
		 ip 变量储存的指针地址: 20818a220
		 *ip 变量的值: 20
```

### 指针数组

示例

```go
var max = 3
a := [max]int{10,100,200}
 var i int
 var ptr [3]*int;

 for  i = 0; i < max i++ {
    ptr[i] = &a[i] /* 整数地址赋值给指针数组 */
 }

 for  i = 0; i < MAX; i++ {
    fmt.Printf("a[%d] = %d\n", i,*ptr[i] )
 }
```

### 指向指针的指针

如果一个指针变量存放的又是另一个指针变量的地址，则称这个指针变量为指向指针的指针变量，当定义一个指向指针的指针变量时，第一个指针存放第二个指针的地址，第二个指针存放变量的地址。

#### 声明格式

```go
var name **type
```

示例

```go
var a ：= 3000
var ptr *int		// 指针变量
var pptr **int	// 指向指针的指针变量

ptr = &a
pptr = &ptr

fmt.Printf("变量 a = %d\n", a )
fmt.Printf("指针变量 *ptr = %d\n", *ptr )
fmt.Printf("指向指针的指针变量 **pptr = %d\n", **pptr)
```

```
输出：变量 a = 3000
		 指针变量 *ptr = 3000
		 指向指针的指针变量 **pptr = 3000
```



### Go 语言指针作为函数参数

- Go 语言允许向函数传递指针，只需要在函数定义的参数上设置为指针类型即可。
- 使用指针传递参数可以在函数内部修改原始变量的值，而使用值传递参数则不能修改原始变量的值，只能在函数内部操作参数的拷贝。

示例

```go
func swap(x *int, y *int) {
   var temp int
   temp = *x
   *x = *y
   *y = temp
}
```



## Go 语言结构体

Go 语言中结构体我们可以定义不同的数据类型。

结构体定义需要使用 type 和 struct 语句。struct语句定义一个新的数据类型，结构体中有一个或多个成员。

### 定义结构体

```go
// 首字母大写可以被其他包访问 小写值只可以在本包访问
type Persion struct {
   member type
   member type
   ...
   member type
}
```

### 声明结构体

```go
Persion1 := Persion {value1, value2...valuen}

Persion1 := Persion { member1: value1, member2: value2..., membern: valuen}
```

### 访问结构体成员

```go
var Persion1 Persion

Persion1.member
```

### 结构体指针

```go
var struct_pointer *Persion	// 定义指向结构体类型的指针

struct_pointer = &Persion1	// 存储结构体变量的地址	
```



## Go 语言切片(Slice)

- Go语言切片是对数组的抽象。
  Go数组的长度不可改变，在特定场景中这样的集合就不太适用，Go中提供了一种灵活，功能强悍的内置类型切片**("**动态数组**")**，
  与数组相比切片的长度是不固定的，可以追加元素，在追加时可能使切片的容量增大。
- 切片不需要说明长度。

### 定义切片

```go
var identifier []type
```

使用 **make()** 函数来创建切片:

```go
var slice1 []type = make([]type, len)

// 也可以简写为
slice1 := make([]type, len)

// 指定容量
make([]T, length, capacity)
```

### 切片初始化

```go
// 直接初始化切片，[] 表示是切片类型，{1,2,3} 初始化值依次是 1,2,3，其 cap=len=3。
s := []int {1,2,3} 

/*
	通过数组初始化切片

	初始化切片 s，是数组 arr 的引用。
	s := arr[startIndex:endIndex]
	将 arr 中从下标 startIndex 到 endIndex-1 下的元素创建为一个新的切片。
	默认 endIndex 时将表示一直到arr的最后一个元素。
	默认 startIndex 时将表示从 arr 的第一个元素开始。
*/
arr := [4]int{1, 2, 3, 4} // 定义并初始化一个长度为 4 的数组
s := arr[:]

	for i, v := range s {
		fmt.Println(v)
	}

/*
	通过内置函数 make() 初始化切片s，[]int 标识为其元素类型为 int 的切片。
	len() 和 cap() 函数
	切片是可索引的，并且可以由 len() 方法获取长度。
	切片提供了计算容量的方法 cap() 可以测量切片最长可以达到多少。
*/
s1 := make([]int, 3, 5)
fmt.Printf("len=%d cap=%d slice=%v\n", len(s1), cap(s1), s)
```

### append()和 copy()函数

```go
/*
	append() 和 copy() 函数
	append 函数不仅会在切片容量不足时自动扩展切片，还会在切片为 nil 时自动初始化一个空切片。
	如果想增加切片的容量，我们必须创建一个新的更大的切片并把原分片的内容都拷贝过来。
	下面的代码描述了从拷贝切片的 copy 方法和向切片追加新元素的 append 方法。
*/
var numbers []int
printSlice(numbers)

/* 允许追加空切片 */
numbers = append(numbers, 0)
printSlice(numbers)

/* 向切片添加一个元素 */
numbers = append(numbers, 1)
printSlice(numbers)

/* 同时添加多个元素 */
numbers = append(numbers, 2, 3, 4)
printSlice(numbers)

/* 创建切片 numbers1 是之前切片的两倍容量*/
numbers1 := make([]int, len(numbers), (cap(numbers))*2)

/* 拷贝 numbers 的内容到 numbers1 */
copy(numbers1, numbers)
printSlice(numbers1)

func printSlice(x []int){
   fmt.Printf("len=%d cap=%d slice=%v\n",len(x),cap(x),x)
}
```

## Go 语言Map(集合)

- Map 是一种无序的键值对的集合。
- Map 最重要的一点是通过 key 来快速检索数据，key 类似于索引，指向数据的值。
- Map 是一种集合，所以我们可以像迭代数组和切片那样迭代它。不过，Map 是无序的，遍历 Map 时返回的键值对的顺序是不确定的。
- 在获取 Map 的值时，如果键不存在，返回该类型的零值，例如 int 类型的零值是 0，string 类型的零值是 ""。
- Map 是引用类型，如果将一个 Map 传递给一个函数或赋值给另一个变量，它们都指向同一个底层数据结构，因此对 Map 的修改会影响到所有引用它的变量。

### 定义 Map

```go
/* 使用 make 函数 */
map_variable := make(map[KeyType]ValueType, initialCapacity)
```

### 操作Map

```go
// 使用字面量创建 Map
m := map[string]int{
    "apple": 1,
    "banana": 2,
    "orange": 3,
}

// 获取键值对
v1 := m["apple"]
v2, ok := m["pear"]  // 如果键不存在，ok 的值为 false，v2 的值为该类型的零值

// 修改键值对
m["apple"] = 5

// 获取 Map 的长度
len := len(m)

// 删除键值对
delete(m, "banana")
```

## Go 语言类型转换



### Go 语言类型转换基本格式

Go不支持隐式的类型转换

```go
type_name(expression)
```

### 示例

```go
var a int = 10
var b float64 = float64(a)
```

### 字符串类型转换

```go
strconv.Atoi(str)	// 字符串转换其他类型
strconv.Itoa(num)	// 整型转换成字符串
strconv.ParseFloat(str, 64)	// 字符串转浮点型
strconv.FormatFloat(num, 'f', 2, 64) // 浮点型转字符串
```

### 接口类型转换

接口类型转换有两种情况**：类型断言**和类型转换。

#### 类型断言

```go
//	类型断言用于将接口类型转换为指定类型
str, ok := value.(type)	// 类型断言成功，它将返回转换后的值和一个布尔值，表示转换是否成功
```

#### 类型转换

```go
// 类型转换用于将一个接口类型的值转换为另一个接口类型
type(value)
```

## Go 语言接口

- Go 语言提供了另外一种数据类型即接口，它把所有的具有共性的方法定义在一起，任何其他类型只要实现了这些方法就是实现了这个接口。
- 接口可以让我们将不同的类型绑定到一组公共的方法上，从而实现多态和灵活的设计。
- Go 语言中的接口是隐式实现的，也就是说，如果一个类型实现了一个接口定义的所有方法，那么它就自动地实现了该接口。因此，我们可以通过将接口作为参数来实现对不同类型的调用，从而实现多态。

接口格式

```go
/* 定义接口 */
type interface_name interface {
   method_name1 [return_type]
   method_name2 [return_type]
   method_name3 [return_type]
   ...
   method_namen [return_type]
}

/* 定义结构体 */
type struct_name struct {
   /* variables */
}

/* 实现接口方法 */
func (struct_name_variable struct_name) method_name1() [return_type] {
   /* 方法实现 */
}
...
func (struct_name_variable struct_name) method_namen() [return_type] {
   /* 方法实现*/
}
```

示例

```go
type Phone interface {
    call()
}

type NokiaPhone struct {
}

func (nokiaPhone NokiaPhone) call() {
    fmt.Println("I am Nokia, I can call you!")
}

type IPhone struct {
}

func (iPhone IPhone) call() {
    fmt.Println("I am iPhone, I can call you!")
}

func main() {
    var phone Phone

  	// new 是一个内建函数，用于创建某种类型的指针，并返回该指针的地址
    phone = new(NokiaPhone)
    phone.call()

    phone = new(IPhone)
    phone.call()

}
```

### any

any是interface{}的别名，在所有方面都等同于interface{}。

```go
var value any

// 等同于

var value interface{}
```



## Go 错误处理

error 类型是一个接口类型

### 定义

```go
type error interface {
    Error() string
}
```

我们可以在编码中通过实现 error 接口类型来生成错误信息。

函数通常在最后的返回值中返回错误信息。使用 errors.New 可返回一个错误信息。

```go
func Sqrt(f float64) (float64, error) {
    if f < 0 {
        return 0, errors.New("math: square root of negative number")
    }
    // 实现
}
```



## Go 并发

### Goroutine（协程）

- Go 语言支持并发，我们只需要通过 go 关键字来开启 goroutine 即可，它是轻量级线程，goroutine 的调度是由 Golang 运行时进行管理的。
- 同一个程序中的所有 goroutine 共享同一个地址空间。

goroutine的特点：

1. `goroutine`具有可增长的分段堆栈。这意味着它们只在需要时才会使用更多内存。

2. `goroutine`的启动时间比线程快。

3. `goroutine`原生支持利用channel安全地进行通信。

4. `goroutine`共享数据结构时无需使用互斥锁

   

#### 语法格式

```go
go 函数名( 参数列表 )	// 只需要在函数前加上go， 此函数就变成异步函数
```



### Channel（通道）

- 通道是一种用于在多个goroutine之间进行通信和同步的机制。通道本身可以被看作一个阻塞队列，可以用于将数据从一个goroutine传递到另一个goroutine。通道的使用可以保证并发安全，避免了多个goroutine之间的竞争条件和数据访问冲突。（等同于java中的同步锁，保证线程安全。）
- 通道可以是带缓冲或非缓冲的。
- 带缓冲的通道允许在发送数据时缓存一定量的数据，带缓冲区的通道允许发送端的数据发送和接收端的数据获取处于异步状态，就是说发送端发送的数据可以放在缓冲区里面，不需要接收方立刻接收（缓冲区满之前不会进入阻塞状态）。
- 而非缓冲的通道则需要等待接收者就绪才能发送数据，发送方会阻塞直到接收方从通道中接收了值。
- 通道也可以有不同的方向，即只能用于发送或只能用于接收，channel <- data表示向通道发送数据，data = <-channel表示从通道接收数据。
- 通道在阻塞状态下，后续操作将不再执行。

#### 语法格式

```go
make(chanName <type>, <capacity>)	// 使用make()函数创建
```

示例

```go
// Producer 数据生产者
func Producer(header string, channel chan<- string) {
	// 无限循环，不停的生产数据
	for {
		//每隔1秒钟将随机数和字符串格式化为字符串发送给通道
		channel <- fmt.Sprintf("%s: %v", header, rand.Int31()) // 阻塞状态 后边代码不执行
		time.Sleep(time.Second)

	}
}

// Customer 数据消费者
func Customer(channel <-chan string) {

	// 不停的获取数据
	for {
		// 从通道中取出数据, 此处会阻塞直到信道中返回数据
		message := <-channel
		fmt.Println(message)
	} 
}
```



## Go泛型

不应该去限定它的类型，应该让调用者自己去定义类型。

### 泛型函数格式

```go
// any 任意类型
// comparable 可对比类型
func 函数名 [T type1 ｜ type2 ](args []T) {
  
	for _, i := range strArr {
    
		fmt.Println(i)
	}
  
}
```

示例

```go 
// 类型
type MySlice[T int | float32] []T

// 类型的方法
func (s MySlice[T]) sum() T {
	var sum T

	for _, v := range s {
		sum += v
	}

	return sum
}
```



### 泛型定义类型

```go
// 泛型切片
type slice_name [type1 | type2] []T

// 泛型map
type map_name [KEY type1 | type2, VALUE type1 | type2] map[KEY]VALUE // KEY VALUE 是类型的形参

// 泛型结构体
type struct_name [T type1 | type2 ...] struct {
  id T 
  name T
}

// 泛型接口
type interface_name[T type1 | type2 ...] interface {
   method_name1 [data T]
   method_name2 [data T]
   method_name3 [data T]
   ...
   method_namen [data T]
}

// 泛型通道
type channel[T type1 | type2] chan T
```

### 自定义泛型约束

如果泛型类型过多，可以是铜自定义泛型约束来实现。

```go
type myInt interface {
  ~int | int16 | int32 | int64  // ~int 可以支持int下所有的衍生类型
}

func sum(a, b T) T {
  return a + b
}

```



## Go命名规范

包名要简短，有意义，全部小写。例如：`fmt`, `net`, `http`, `json`等。

文件名要描述文件内容，全部小写，使用下划线连接。例如：`user_controller.go`, `utils.go`等。

变量名、函数名和方法名使用驼峰式命名法，首字母小写。例如：`getUserInfo()`, `userList`等。

结构体名使用驼峰式命名法，首字母大写。例如：`type User struct{}`。

接口名使用 `er` 后缀，例如：`Reader`, `Writer`等。

常量名使用全部大写字母，使用下划线连接。例如：`MAX_USER_COUNT`, `VERSION_NUMBER`等。



## 单元测试

- Go语言提供了内置的单元测试框架testing，可以方便地对函数和方法进行单元测试。
- 在Go语言中，测试文件以_test.go结尾，测试函数名以Test开头，参数为testing.T类型的指针。

### 格式

```go
func TestFuncName(t *testing.T) {
    if result false {
        t.Errorf()	// 测试失败返回的信息
    }
}
```

### 测试

该命令会自动查找并运行所有以_test.go结尾的测试函数，并输出测试结果。

```
go test
```

可以通过添加参数来指定测试文件或测试函数。

```
go test -v	// 输出详细信息
```

```
go test -run 函数名	// 运行指定测试函数
```

还可以使用通配符来运行匹配特定模式的所有测试函数。

```
go test -run MyFunction	// 测试所有包含MyFunction的函数

go test -run Test*	// 测试所有以Test开头的函数
```



## 编码小技巧

#### 定义一个使用指南的函数

```go
// 定义一个使用指南的函数
var Usage = func() {
    fmt.Println("=======方法指南========")
    fmt.Println("method1")
  	fmt.Println("method1")
  	fmt.Println("method1")
  	fmt.Println("=======方法指南========")
}

// 如果满足条件调用提示信息
if args == nil {
  Usage()
}
```



## GoPath

GoPath是Golang的工作空间，所有的Go文件，都需要放在GoPath下的src目录下才能够编译运行。

在项目中使用第三方类库的时候，可以使用`go get`命令从网下直接拉去第三方类库的包，而拉取下来的包就会直接下载到我们的GoPath目录下的src包下。

如果给不同的项目设置不同的GoPath：

优点：

1.便于管理项目，每个项目都是不同的GoPath，这对于我们管理多个Golang项目而言，能够非常清晰的处理项目结构。

缺点：

1.第三方依赖的包和我们自己的Golang包混在一起，会给我们的项目文件管理带来一定的麻烦。
2.不同的GoPath都需要下载依赖，那么磁盘中重复的依赖就会非常多，会占用我们大量的磁盘空间。



## GoModule（go.mod）

为了解决GoPath的问题Golang最终引入了GoModule的概念，GoModule 是 golang 1.11 新加的特性，在1.12版本中正式开始使用。

Golang1.11和1.12版本虽然已经引入了GoModule的概念，但是GoModule是默认不开启的，如果需要开启，那么需要配置一个环境变量：`GO111MODULE=on`，默认是`off`。

而在Golang1.13及以上的版本中，GoModule的默认配置为auto，即GoModule会通过你的目录下是否有go.mod文件来判断是否开启GoModule。

### 什么是GoModule：

GoModule就是一个用来取代GoPath的Golang的工作空间，有了GoModule之后，那么我们就可以把文件放在GoModule目录下，而放在GoModule目录下的Golang文件，也可以正确地编译运行。

### 使用GoModule，GoPath是否可以被舍弃：

GoPath所引出的问题，就是因为第三方类库的包所导致的，所以我们在有了GoModule之后，GoPath和GoModule就分别负责不同的职责，共同为我们的Golang项目服务。

GoPath我们用来存放我们从网上拉取的第三方依赖包。
GoModule我们用来存放我们自己的Golang项目文件，当我们自己的项目需要依赖第三方的包的时候，我们通过GoModule目录下的一个go.mod文件来引用GoPath目录src包下的第三方依赖即可。

总而言之，在引入GoModule之后，我们不会直接在GoPath目录进行编程，而是把GoPath作为一个第三方依赖包的仓库，我们真正的工作空间在GoModule目录下。



## 推荐书籍

《Go 入门指南》



## web框架

### Gin

### Beego

### Iris



# 常用的API

sort.Slice 根据任意字段进行切片排序

```go
	sort.Slice(slice, func(i, j int) bool {
		return slice[i].fields > slice[j].fields
	})
```

