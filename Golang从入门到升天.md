

# Golang从入门到升天

### 1.开发团队

![开发团队](/Users/brodyliao/Desktop/Screen Shot 2020-11-25 at 6.50.26 AM.png)

### 2.编译和解释性语言

![](/Users/brodyliao/Desktop/Screen Shot 2020-11-25 at 6.52.38 AM.png)

### 3. Go语言诞生

![](/Users/brodyliao/Desktop/Screen Shot 2020-11-25 at 6.54.52 AM.png)

### 4. 性能

![](/Users/brodyliao/Desktop/Screen Shot 2020-11-25 at 6.59.05 AM.png)

### 5.应用领域

![](/Users/brodyliao/Desktop/Screen Shot 2020-11-25 at 7.07.34 AM.png)

### 6.个人开发

![image-20201129194934252](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201129194934252.png)

###7.企业开发者

![image-20201129195023095](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201129195023095.png)

### 8.打包命令

  第一种:

* SET CGO_ENABLED=0  //禁用CGO
* SET GOOS=linux //目标平台是linux
* SET GOARCH=amd64 //目标处理器架构是amd64
* go build

 第二种:

CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go install -tags "consul jsoniter"

### 9. Golang中25个关键字

![image-20201130060822445](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201130060822445.png)

### 10. Golang中37个保留字

![image-20201130060918108](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201130060918108.png)

### 11.变量声明方式

* 批量变量声明

  var ( 

  ​	a int

  ​	b bool

  ​    c string

  ​	)

* 赋值声明

  var a int = 1

* 类型推导声明

  var a = true

* 短变量声明(在函数内部), 声明并初始化

  func main() {

  ​	n := 10

  ​	m := 100

  }

### 12.匿名变量声明("_" 用于接收不需要的变量值)

func foo() (string, int){

​	reutrn "Brody", 100

}	

aa, bb := foo()

aa, _ := foo()

### 13. 常量声明(定义时必须赋值)

* 分别声明

  const b = 1

  const c = 2 

* 批量声明

  const (

  ​	b int

  ​	c bool

  )

  const (

  ​	b = 1

  ​	c

  ​	d

  )

  b, c, d 都等于1

* iota(常量计数器, 只能在常量的表达式中使用, **每增加一行**变量声明将使iota计数一次)

  const (

  ​	n1 = iota // 0

  ​	n2            // 1

  ​	n3            // 2

  )

  const (

  ​	n1 = iota // 0

  ​	_              // 

  ​	n3            // 2

  )

  const (

  ​	n1 = iota // 0

  ​	n2 = 100 // 100

  ​	n3            // 2

  )

 const (

​	_ = iota

​	KB = 1 << (10 * iota) // 1 << 10

​	MB = 1 << (10 * iota) // 1 << 20

​	GB = 1 << (10 * iota) // 1 << 30

​	TB = 1 << (10 * iota) // 1 << 40

​	PB = 1 << (10 * iota) // 1 << 50

)

const (

​	a, b = iota + 1, iota + 2  // 1, 2

​	c, d // 2, 3

​	e, f // 3, 4

)

### 14. 数据类型

#### 14.1整型

* 按长度分int8, int 16, int 32, int 64对应无符号类型为uint8(byte), uint16(short), uint32, uint 64(long)
* %b 表示二进制
* %o 表示八进制
* %x 表示十六进制(%X,大写)
* %p 表示变量的内存地址

#### 14.2 浮点型

* float32(3.4e+38, math.MaxFloat32), float64(1.8e+308, math.MaxFloat64)
* 打印浮点格式化都用配合动词%f,如果 %.2f保留两小数

#### 14.3 复数

![image-20201130072735410](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201130072735410.png)

#### 14.4 布尔值

* Golang中不允许将整形强制转换成布尔型
* 布尔型无法参与数值运算,也无法与其它类型进行转换
* 默认值false

#### 14.5 字符串

![image-20201130073129565](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201130073129565.png)

![image-20201130073906930](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201130073906930.png)

 注: 启一个godoc服务,

```
godoc -http=:9000   
```

#### 14.6 byte和 rune类型

* uint8类型,或者叫byte类型,代表了ASSCI码的一个字符

* rune类型( int32), 代表一个 UTF-8字符,如中文,日文,或其它复合字符

* range可遍历rune + byte,如" hello,廖"

  * 修改字符串,需要先将其转换成[]rune或[]byte,然后再转换成[]byte,无论哪种转换,都会重新分配类存,并复制字节数组

     func changeString() {

    ​	s1 := "big"

    ​	byteS1 := []byte(s1)

    ​	byteS1[0] = 'p'

    ​	fmt.Println(string(byteS1));

    ​	s2 := "天鹅肉"

    ​	runeS2 := []rune(s2)

    ​	runeS2[0] = "地"

    ​	fmt.Println(string(runeS2)) 

    }

### 15.类型强制转换

 Golang中只有强制类型转换, 没有隐式类型转换

```
T(表达式)	
```

### 16.流程控制

#### 16.1  if
if表达式之前可以添加一个执行语句, 再根据变量进行判断

if score := 65; score >= 90 { } else if score > 75 {} else {}

#### 16.2 for

* 初始语句和结束语句都可以省略

* 无限循环

* for range(键值循环), 可遍历数组,切片,字符串, map及通道( channel) 

  通过**for range**返回值有以下规律

  * 数组,切片,字符串返回索引和值
  * map返回键和值
  * 通道( channel)只返回通道内的值

#### 16.3 switch

* 一个switch只有一个 default

* 一个分支可以有多个值

  switch n := 7; n {

  ​	case 1,2,7,9:

  }

* 分支还可以使用表达式,switch后面不用再跟判断变量

  age := 17

  switch {

  ​	case age < 18:

  }

*  fallthrough语法可以执行满足条件的case下的下一个case,是为了兼容 C语言中的case设计的

  s := "a"

  switch {

  ​	case s == "a":		

  ​		fmt.Println("a")

  ​		fallthrought

  ​	case s == "b": 

  ​		fmt.Println("b")

  }

  ```
  输出:  a, b
  ```

  

#### 16.4 goto

* 代码间进行无条件跳转, 快速跳出循环,避免重复
* 跳出两层以上的循环

#### 16.5  break

aa:

​	for () {

​		for () {

​			break aa //可跳出两层循环并结束		

​		}

​	}

#### 16.6  continue

aa:

​	for () {

​		for () {

​			continue aa //可跳出两层循环,进行下次两层循环, 循环迭代过程

​		}

​	}

### 17 运行符

* ++ -- 为独立执行语句

* 位运行算, 二进制在内存中的运算

  ![image-20201202050000426](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201202050000426.png)

  13 & 3 = 1

  ![image-20201202045055878](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201202045055878.png)

### 18 格式化打印的占位符介绍

fmt.Printf

![image-20201202050403879](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201202050403879.png)

![image-20201202050837534](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201202050837534.png)

![image-20201202050941791](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201202050941791.png)

![image-20201202051028879](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201202051028879.png)

![image-20201202051334995](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201202051334995.png)

![image-20201202051530245](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201202051530245.png)

![image-20201202051622387](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201202051622387.png)

![image-20201202051705958](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201202051705958.png)

![image-20201202051735526](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201202051735526.png)

### 19 数组声明和初始化

#### 19.1 定义

同一种数据类型元素的集合

#### 19.2 特性

数组大小不可变,但可以修改成员, 数组的类型由长度和类型组成

```
var a [5]int
var b [10]int
a = [5]int{1, 2, 3, 4, 5}
b = [10]int{9, 10}
var c = [3]string{"天", "地", "人"}
```

#### 19.3 特殊符号"..."

表示让编译器去数一下有多少个初始值, 然后给变量赋值类型

```
var d = [...]init{1, 2, 3, 9}
```

#### 19.4 根据索引值初始化

```
var e [20]int
e = [20]int{19: 1}
```

#### 19.5 遍历数组

```
var a = [10]int{1, 2, 3}
第一种:
for i := 0; i < len(a); i++ {
	
}
第二种:
  for index, value := range a {
  	fmt.Println(index, a[index], value)
  }

```

#### 19.6 多维数组

```
var b [3][2]int
b = [3][2]int {
	[2]int{1, 3},
	[2]int{3, 4},
	[2]int{5, 6 }
}
var c = [3][2]int{
	{1, 2},
	{3, 5},
	{5, 6},
}
```

注: 多维数组除了第一层能用"...", 其它层不能使用

#### 19.7 数组是值类型

### 20 切片(slice)

#### 20.0 定义

一个拥有相同元素的可变长度的序列

基于数组类型的一层封装

支持扩容

是一个引用类型

```
var name []T
```

* name: 表示名称
* T: 表示切片中的元素类型

#### 20. 1 切片三要素

​	地址(切片中第一个元素指向的内存空间)

​	大小(切片中目前元素的个数)  						len()

​	容量(底层数组最大能存放的元素的个数) 	  cap()	

#### 20.2 从数组得到切片

```
var a = [3]int{1, 2, 3}
var c []int
c := a[0:2] // a[:] 从开头到结尾
```

#### 20.3 切片大小获取

```
len(切片名)
```

#### 20.4 切片的容量大小获取

```
cap(切片名)
```

#### 20.5 切片追加

```
append(切片名, 数据)
```

例子:

```
var a = []int{}
a = append(a, 1)
```

注容: 扩容策略是每次是上一次的2倍

#### 20.6 复制

```
copy(切片名) // 深复制
```

例子

```
 var a = [3]int{1, 2, 3}
 var b []int // 没有申请内存
 b = make([]int, 3, 3)
 copy(b, a)
```

#### 20.7 删除

```
var a = []string{"上海", "北京", "广州", "成都"}
a = append(a[:1], a[2:]...)
```

#### 20.8 扩容策略

可以通过查看`$GOROOT/src/runtime/slice.go`源码，其中扩容相关代码如下：

```
newcap := old.cap
doublecap := newcap + newcap
if cap > doublecap {
	newcap = cap
} else {
	if old.len < 1024 {
		newcap = doublecap
	} else {
		// Check 0 < newcap to detect overflow
		// and prevent an infinite loop.
		for 0 < newcap && newcap < cap {
			newcap += newcap / 4
		}
		// Set newcap to the requested cap when
		// the newcap calculation overflowed.
		if newcap <= 0 {
			newcap = cap
		}
	}
}
```

- 首先判断，如果新申请容量（cap）大于2倍的旧容量（old.cap），最终容量（newcap）就是新申请的容量（cap）
- 否则判断，如果旧切片的长度小于1024，则最终容量(newcap)就是旧容量(old.cap)的两倍，即（newcap=doublecap）
- 否则判断，如果旧切片长度大于等于1024，则最终容量（newcap）从旧容量（old.cap）开始循环增加原来的1/4，即（newcap=old.cap,for {newcap += newcap/4}）直到最终容量（newcap）大于等于新申请的容量(cap)，即（newcap >= cap）
- 如果最终容量（cap）计算值溢出，则最终容量（cap）就是新申请容量（cap）

#### 20.9  make

用来引用类型做初始化(申请内存空间)

```
 var s1 []int // 切片声明了,但没有初始化
 s1[0] = 100 // 不能这样使用
 s1 = make([]int, 3, 3)
 
```

#### 20.10 nil

引用类型的默认值, 底层是没有申请内存空间

### 21 Map

#### 21.1 定义

一种无序的基于key-value的数据结构, 

引用类型,必须初始化才能使用,默认为nil

```
 map[keyType]valueType
```

#### 21.2 初始化

```
 var a map[string]int
 a = make(map[string]int, 10)
```

#### 21.3 取值

```
 var a map[string]int
 a = make(map[string]int, 10)
 a["liao"] = 18
 value, ok := a["liao"]
 if !ok {
 
 } else {
 
 }
```



#### 21.4 遍历

```
 var a map[string]int
 a = make(map[string]int, 10)
 for k, v := range a {// 遍历key, value
 	
 }
 for k := range a { // 只遍历key
 	
 }
 for _, v := range a { // 只遍历value
 	
 }
```

#### 21.5 删除

```
 var a map[string]int
 a = make(map[string]int, 10)
 a["liao"] = 18
 a["brody"] = 20
 delete(a, "brody")
 delete(a, 'bbliao') // 删除不存在的
```

#### 21.6 按照指定顺序遍历

```
func main() {
	rand.Seed(time.Now().UnixNano()) //初始化随机数种子

	var scoreMap = make(map[string]int, 200)

	for i := 0; i < 100; i++ {
		key := fmt.Sprintf("stu%02d", i) //生成stu开头的字符串
		value := rand.Intn(100)          //生成0~99的随机整数
		scoreMap[key] = value
	}
	//取出map中的所有key存入切片keys
	var keys = make([]string, 0, 200)
	for key := range scoreMap {
		keys = append(keys, key)
	}
	//对切片进行排序
	sort.Strings(keys)
	//按照排序后的key遍历map
	for _, key := range keys {
		fmt.Println(key, scoreMap[key])
	}
}
```

sort.Strings 字符串排序

#### 21.7 元素为map类型的切片

```
var a = make([]map[int]string, 0, 10)
a[0] = make(map[int]string, 1)
a[0][10] = "brody"
```

#### 21.8 值为切片类型的map

```
var a = make(map[string][]int, 10)
a['brody'] = []int{10, 20, 30}
```

### 22 函数

#### 22.1 定义 

Golang中支持函数, 匿名函数和闭包, 函数是"一等公民"

```
func 函数名(参数)(返回值) {
	函数体
}
```

#### 22.2 defer

将其后面的语句进行延迟处理, 在defer归属的函数即将返回时,将延迟处理的语句按defer定义的逆序进行执行, 也就是说,先被defer的语句最后执行,是后被defer的语句,最后被执行

Golang中函数的return不是原子操作,在底层分为两步来执行

第一步: 返回值赋值

第二步: 真正的RET返回

函数中如果存在defer,那么defer执行时机在是第一步和第二步之间

#### ![image-20201206130658538](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201206130658538.png)

```go
func f1() int{
  x := 5
  defer func(){
    x++
  }()
  return x
}

func f2() (x int) {
  defer func(){
    x++
  }()
  return 5
}

func f3() (y int) {
  x := 5
  defer func() {
    x++
  }()
  return x
}

func f4() (x int) {
  defer func(x int) {
    x++
  }()
  return 5
}
```



#### 22.3 进阶

##### 22.3.1 全局变量

##### 22.3.2  局部变量 

##### 22.3.3 函数类型与变量

* 定义函数类型

  ```
  type calculation func(int, int)int
  ```

* 函数可以作为参数

  ```
   func a(x func() int) {
   		x()
   }
  ```

* 函数也可为返回值

  ``` go
   func a (x func() int) func(int, int) int {
   	 ret := func(a, b int) int {
   	 		return a + b
   	 }
   	 return ret 
   } 
  ```

##### 22.3.4 匿名函数

没有名字的函数, 一般用于函数内部

如果只调用一次,可以直接写成立即执行函数

##### 22.3.5 闭包

一个函数和相关引用环境组合而成的实体, 简单来说: 闭包 = 函数 + 引用环境

##### 22.3.6 内置函数

| 内置函数       | 介绍                                                         |
| :------------- | :----------------------------------------------------------- |
| close          | 主要用来关闭channel                                          |
| len            | 用来求长度，比如string、array、slice、map、channel           |
| new            | 用来分配内存，主要用来分配值类型，比如int、struct。返回的是指针 |
| make           | 用来分配内存，主要用来分配引用类型，比如chan、map、slice     |
| append         | 用来追加元素到数组、slice中                                  |
| panic和recover | 用来做错误处理                                               |

##### 22.3.7 panic/recover

* panic 可以在任何地方引发

*  recover只能在defer调用函数中有效

  注意:

  * `recover()`必须搭配``defer`使用

  * `defer`一定要在可能引发`panic`的语句之前定义

```go
func funcA() {
	fmt.Println("func A")
}

func funcB() {
	defer func() {
		err := recover()
		//如果程序出出现了panic错误,可以通过recover恢复过来
		if err != nil {
			fmt.Println("recover in B")
		}
	}()
	panic("panic in B")
}

func funcC() {
	fmt.Println("func C")
}
func main() {
	funcA()
	funcB()
	funcC()
}
```

###  

### 23 指针

#### 23.1 指针和地址的区别

* 指针: 指针是带类型的
* 地址: 就是内存地址(用字节来描述内存地址)
* &: 取地址
* *: 根据地址取值

### 24 new和make

* new是用来初始化值类型数组
* make是用来初始化slice, map, chan

### 25 结构体( struct)和方法

#### 25.1 自定义类型和别名

* 自定义类型

  ``` go
  type NewInt int
  ```

* 类型别名(只存在代码编写过程中,代码编译后根本不存在)

  ``` go
  type MyInt = int
  ```

#### 25.2 结构体

##### 25.2.1 定义

结构体是值类型

``` go
type typeName struct {
   field1 fieldType
   field2 fieldType
}
```

##### 25.2.2 实例化

* 基本实例化

  ``` go
  type student struct {
    name string
    age int
    gender string
    hobby []string
  }
  var brody = student {
    name: "Brody",
    age: 18,
    gender: "男",
    hobby []string{"骑行", "爬山"},
  }
  // 只填值初始化,必须初始化所有字段
  var bbliao = student {
    "Brody",
    18,
    "男",
    []string{"骑行", "爬山"},
  }
  // 键值对初始化
  var bb = &student {
    name: "Brody",
    age: 18,
  }
  ```

*  new(T)

  ```go
  type student struct {
    name string
    age int
    gender string
    hobby []string
  }
  var liao = new(student)
  liao.name = "brodyliao"
  liao.age = 18
  ```

* &

  ```go
  type student struct {
    name string
    age int
    gender string
    hobby []string
  }
  var liao = &student{}
  liao.name = "brodyliao"
  liao.age = 18
  ```

##### 25.3.3 结构体的匿名字段

结构体允许其成员字段在声明时没有字段而只有类型， 这种没有名字的字段就称为匿名字段

```go
type Person struct{
  name string
  string
  int
}
func main() {
  p1 := Person{
    name: "tt"
    "bb",
    18
  }
  fmt.Pringln(p1.name, p1.string, p1.int)
}
```

注：匿名字段默认采用类型名作为字段名， 结构体要求字段名称必须唯一，因此一个结构体中同种类型的匿名字段只能有一个

##### 25.3.4 嵌套结构体

一个结构体可以嵌套包含另一个结构体或结构体指针

```go
type Address struct {
  Province string
  City string
}
type User struct {
  Name string
  Gender string
  Address Address
}
func main() {
  user1 := User{
    Name: "bb",
    Gender: "boy"
    Adderss: Address {
      Province: "上海"
      City: "上海"
    }
  }
}
```

##### 25.3.5 嵌套匿名结构体

```go
type Address struct {
  Province string
  City string
}
type User struct {
  Name string
  Gender string
  Address
}
func main() {
  var user2 user
  user2.Name = "bb"
  user2.Gender = "boy"
  user2.Address.Province = "上海"
  user2.Address.City = "上海"
  // 匿名字段支持简写， 当没有命名冲突的时候， 也可以使用 user2.Province, user2.City获取
}
```

##### 25.3.6 结构体的继承

```go
type Animal struct {
  name string
}
func (a *Animal) move() {
  
}
type Dog struct {
  Feet int8
  *Animal
}
func (d *Dog) wang() {
  
}
func main() {
  d1 := &Dog{
    Feet: 4,
    Animal: &Animal{
      name: "dd"
    }
  }
  d1.wang()
  d1.move()
}
```

##### 25.2.7 结构体字段的可见性

* 大写开头表示可以公开访问
* 小写开头表示私有（仅在定义当前结构体的包中可以访问）

##### 25.2.8 结构体与JSON序列化

```go
type Student struct{
  ID int 	`json:"id"` // 定义元信息， json tag
  Gender string `json:"gender"`
  Name string	`json:"name"`
}
func main() {
  var stu = Student{
    ID: 1,
    Gender: "boy",
    Name: "bb",
  }
  // 序列化
  v, err := JSON.Marshal(stu)
  if err != nil {
    
  }
  fmt.Printf('%#v', string(v))
  // 反序列化
  str := string(v)
  var stu2 = &student{}
  json.Unmarshal([]byte(str), stu2)
}
```

* 序列化：把编程语言里的数据转化成JSON格式的字符串
* 反序列化：把满足JSON格式的字符串转换成当前编程语言里的对象

#### 25.3 方法

##### 25.3.1 定义 

Golang中`方法[method]` 是一种作用于特定类型变量的函数, 这种特定类型变量收做`接受者(receiver)` 。接受者的概念就类似于其他语言中的`this` 或则`self`

```go
func (接受者变量 接受者类型) 方法名（参数列表）（返回参数）{
  函数体
}
```

##### 25.3.2 指针类型接受者

使用条件：

* 需要修改接收者中的值

* 接收者是拷贝代价比较大的大对象

* 保证一致性，如果有某个方法使用了指针接收者，那么其他的方法也应该使用指针接收者。

##### 25.3.3 值类型接受者

##### 25.3.4 任意类型添加方法

```go
type MyInt int
func (m *MyInt)sayHi() {
  
}
func main() {
  var m MyInt
  m.sayHi()
}
```

注：不能给别的包定义类型添加方法

### 26 包（package）

#### 26.1 定义

是多个Go源码的集合，是一种高级代码复用方案

```go
package 包名
```

注意事项：

- 一个文件夹下面直接包含的文件只能归属一个`package`，同样一个`package`的文件不能在多个文件夹下
- 包名可以不和文件夹的名字一样，包名不能包含 `-` 符号
- 包名为`main`的包为应用程序的入口包，这种包编译后会得到一个可执行文件，而编译不包含`main`包的源代码则不会得到可执行文件

 #### 26.2 导入(import)

```go
// 单行导入
import 包的路径("github.com/xx") 
// 多行导入
import (
	"fmt"
  "os"
) 
// 自定义包名
import 别名 "包的路径"

// 匿名导入包
import _ "包的路径"

```

- import导入语句通常放在文件开头包声明语句的下面
- 导入的包名需要使用双引号包裹起来
- 包名是从`$GOPATH/src/`后开始计算的，使用`/`进行路径分隔
- Go语言中禁止循环导入包

#### 26.3  init()初始化函数

 Golang中程序执行时导入语句包会自动触发包内部`init()`函数的调用。需要注意的是: `init()`没有参数, 也没有返回值。`init()`在程序运行时自动被调用执行，不能在代码中主动调用它，其执行顺序如下：

![image-20201206162702020](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201206162702020.png)

![image-20201206163059506](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201206163059506.png)

#### 26.4  time包

##### 26.4.1  time.Now 

// time.Time return struct

```go
now := time.Now()
year := now.Year()
month := now.Month()
day := now.Day()
hour := now.Hour()
minute := now.Minute()
second := now.Second()
nanosecond := now.Nanosecond()

```

##### 26.4.2  时间戳

 自1970年1月1号(08:00:00GMT)至当前时间的总毫秒数。它也被称为Unix时间戳(UnixTimestamp )

``` go
func timestampDemo() {
  now := time.Now()
  timestamp1 = now.Unix() // 时间戳
  timestamp2 = now.UnixNano() // 纳秒时间戳
}
```

使用time.Unix()函数将时间戳转为时间格式

``` go
func timestampDemo2(timestamp int64) {
  timeObj := time.Unix(timestamp, 0) // 0表示时间偏移量
  year := now.Year()
  month := now.Month()
  day := now.Day()
  hour := now.Hour()
  minute := now.Minute()
  second := now.Second()
  nanosecond := now.Nanosecond()
}
```

##### 26.4.3  定时器

使用 time.Tick(时间间隔)来设置定时器

``` go
func tickDemo(){
	ticker := time.Tick(time.Second)
  for i := range ticker{
    // 每秒执行的任务
  }
}
```

##### 26.4.4 时间间隔

``` go
const (
	Nanosecond Duration = 1
  Microsecond					= 1000 * Nanosecond
  Millisecond					= 1000 * Microsecond
  Second							= 1000 * Millisecond
  Minute							= 60 * second
  Hour								= 50 * Minute
)
```

例如：time.Duration 表示1纳秒， time.Second表示一秒

##### 26.4.5 时间格式化

时间类型有一个自带的方法Format进行格式化， 需要注意的是Go语言中格式化时间模板不是常见的`Y-m-d H:M:S`而是使用Go的诞生时间2006年1月2号15点04分（记忆口诀20061234）

```go
func formatDemo() {
  now := time.Now()
  fmt.Println(now.Format("2006-01-02 15:04:05.000"))
  fmt.Println(now.Format("2006/01/02 15:04"))
  fmt.Println(now.Format("15:04 2006/01/02"))
  fmt.Println(now.Format("2006/01/02"))
}
```

### 27 接口(interface)

#### 27.1 定义

定义了一个行为规范， 只定义规范不实现，由具体的对象来实现规范的细节

在Golang中接口是一种类型，一种抽象类型

` interface` 是一组` method`的集合，是`duck-type programing`的一种体现。接口做的事情就像定义一个协议（规则），不关心属性（数据），只关心行为（方法）

Golang提倡面向接口编程

```go
type 接口类型名 interface {
  方法名1（参数列表1）返回值列表1
  方法名2（参数列表2）返回值列表2
}
```

```go
type writer interface{
  Write([]byte) error
}
```

Golang的接口在命名时，一般会在单词后加er

#### 27.2 实现

 ``` go
type Liao struct {
  name string
}

func (l Liao) Write() {
  
}
type Brody struct {
  age string
}
func (b Brody) Write() {
  
}

 ```

#### 27.3 类型与接口的关系

##### 27.3.1 一个类型实现多个接口

##### 27.3.2 多个类型实现同一接口

##### 27.3.3 接口类型变量

##### 27.3.4 接口嵌套

``` go
type speaker interface {
  speak()
}
type mover interface {
  move()
}
type animal interface {
  speaker
  mover
}
type cat struct {
  name string
}
func (c cat) speak() {
  
}
func (c cat) move() {
  
}
func main() {
  var x animal
  x = cat{name: "hh"}
  x.move()
  x.speak()
}
```

#### 27.4 空接口

##### 27.4.1 定义

空接口是指没有定义任何方法的接口，因些任何类型都实现了空接口

空接口类型的变量可以存储任意类型的变量

```go
func main() {
  var x interface{}
  s := "bb"
  x = s
  b := true
  x = b
}
```

##### 27.4.2 应用

* 作为函数的参数

  ```go
  func show(c interface{}) {
    
  }
  ```

  

* 空接口作为map的值

  ```go
  var studentInfo = make(map[string]interface{})
  studentInfo["name"] = "BBliao"
  studentInfo["age"] = 18
  studentInfo["married"] = false
  ```

  

##### 27.4.3 类型断言

空接口可以存储任意类型的的值， 那我们如何获取其存储的具体数据呢？

语法格式：` x.(T) `其中：

* x: 表示类型为interface{}的变量

* T: 表示断言x可能是的类型

  该语法返回两个参数， 第一个参数是`x`转化为`T`类型后的变量，第二个是布尔值， 若为`true`则表示断言成功，`false`则表示断言失败

  ```go
  func main() {
    var x interface{}
    x = "brodyliao"
    v, ok := x.(string)
    if (ok) {
      fmt.Println("断言成功")
    } else {
      fmt.Println("断言失败")
    }
  }
  ```

  ```go
  func justifyType(x interface{}) {
    switch v := x.(type) {
      case string:
      case int:
      case bool:
      default:
    }
  }
  // 类型断言简化版
  ```

  ##### 27.4.4 接口值 
  
  接口是由`一个具体类型`和`具体类型值`组成
  
  我们来看一个具体的例子：
  
  ```go
  var w io.Writer // <nil, nil>
  w = os.Stdout
  w = new(bytes.Buffer)
  w = nil
  ```
  
  请看下图分解：![接口值图解](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/interface.png)



### 28 文件操作

#### 28.1 打开和关闭文件

```go
func main() {
  file: err := os.Open("xx.go")
  defer file.close()
  if err != nil {
    fmt.Println(err)
  }
}
```

#### 28.2 读取文件

##### 28.2.1 file.Read()

```go
func (f *File) Read(b []byte)(n int, err error) 
```

Demo:

```go
func main() {
  file: err := os.Open("xx.go")
  defer file.close()
  if err != nil {
    fmt.Println(err)
  }
  var tmp = make([]byte, 128)
  n, err := file.Read(tmp)
  if err == io.EOF {
    fmt.Prinln("文件读完了")
    return
  }
  if err != nil {
    fmt.Println(err)
  }
  fmt.Println(string(tmp[:n]))
}
```

##### 28.2.2  bufio

`bufio`在 `file`的基础上封装了一层API，支持更多的功能

Demo:

```go
func main() {
  file: err := os.Open("xx.go")
  defer file.close()
  if err != nil {
    fmt.Println(err)
  }
  reader := bufio.NewReader(file)
  for {
    line, err := reader.ReadString('\n') // 注意是字符
    if err == io.EOF {
      fmt.Prinln("文件读完了")
      break;
    }
    if err != nil {
      fmt.Println(err)
    }
    fmt.Println(line)
  }
}
```

##### 28.2.3 ioutil

```go
func main() {
  content, err := ioutil.ReadFile("../main.go")
  if err != nil {
   	return 
  }
  fmt.Println(string(content))
}
```

#### 28.3 文件写入操作

` os.OpenFile()`函数能够以指模式打开文件，从而实现文件写入相关功能

```go
func OpenFile(nam string, flag int, perm FileMode) (*File, error){
  
}
```

![image-20201206203046602](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201206203046602.png)

##### 28.3.1 Write和 WriteString

```go
func main() {
  file, err := os.OpenFile("xx.txt", os.O_CREATE|os.O_TRUNC|os.O_WRONLY, 0666)
  if err != nil {
    fmt.Prinln(err)
    return 
  }
  defer file.Close()
  str := "hello"
  file.Write([]byte(str))					// 写入字节切片数据
  file.WriteString("hello buddy") // 直接写入字符串
}
```

##### 28.3.2 buffo.NewWriter

```go
func main() {
  file, err := os.OpenFile("xx.txt", os.O_CREATE|os.O_TRUNC|os.O_WRONLY, 0666)
  if err != nil {
    fmt.Prinln(err)
    return 
  }
  defer file.Close()
  writer := bufio.NewWriter(file)
  for i := 0; i < 10; i++ {
    writer.WriteString("haha")  // 将数据写入缓存
    writer.Flush() // 将缓存中的内容写入文件
  }
}
```

##### 28.3.3 ioutil.WriteFile

```go
func main() {
  str := "brody liao"
  err := ioutil.WriteFile("xx.go", []byte(str), 0755)
  if err != nil {
    fmt.Println(err)
    return
  }
}
```

##### 28.3.4 copyFile

```go
// CopyFile 拷贝文件函数
func CopyFile(dstName, srcName string) (written int64, err error) {
	// 以读方式打开源文件
	src, err := os.Open(srcName)
	if err != nil {
		fmt.Printf("open %s failed, err:%v.\n", srcName, err)
		return
	}
	defer src.Close()
	// 以写|创建的方式打开目标文件
	dst, err := os.OpenFile(dstName, os.O_WRONLY|os.O_CREATE, 0644)
	if err != nil {
		fmt.Printf("open %s failed, err:%v.\n", dstName, err)
		return
	}
	defer dst.Close()
	return io.Copy(dst, src) //调用io.Copy()拷贝内容
}
func main() {
	_, err := CopyFile("dst.txt", "src.txt")
	if err != nil {
		fmt.Println("copy file failed, err:", err)
		return
	}
	fmt.Println("copy done!")
}
```

##### 28.3.5 实现一个cat命令

``` go
package main

import (
	"bufio"
	"flag"
	"fmt"
	"io"
	"os"
)

// cat命令实现
func cat(r *bufio.Reader) {
	for {
		buf, err := r.ReadBytes('\n') //注意是字符
		if err == io.EOF {
			break
		}
		fmt.Fprintf(os.Stdout, "%s", buf)
	}
}

func main() {
	flag.Parse() // 解析命令行参数
	if flag.NArg() == 0 {
		// 如果没有参数默认从标准输入读取内容
		cat(bufio.NewReader(os.Stdin))
	}
	// 依次读取每个指定文件的内容并打印到终端
	for i := 0; i < flag.NArg(); i++ {
		f, err := os.Open(flag.Arg(i))
		if err != nil {
			fmt.Fprintf(os.Stdout, "reading from %s failed, err:%v\n", flag.Arg(i), err)
			continue
		}
		cat(bufio.NewReader(f))
	}
}
```

### 29 反射

#### 29.1 为什么要用反射

类型太多了， 类型断言判断不全，使用反射就能直接拿到接口值的动因类型和动态值

#### 29.2 反射的应用

各种web框架，配置文件解析库， ORM框架

#### 29.3 反射的优缺点

* 优点：让代码更灵活
* 缺点：运行效率低

#### 29.4 reflect包

##### 29.4.1 TypeOf

```go
func reflectType(x interface{}) {
  v := reflect.TypeOf(x)
  //fmt.Printf("type: %v\n", v)
  fmt.Printf("type:%v kind:%v\n", t.Name(), t.Kind()
}
func main() {
  reflectType(100)
}
```

Go语言的反射中像数组、切片、Map、指针等类型的变量，它们的`.Name()`都是返回`空`。

在`reflect`包中定义的Kind类型如下：

```go
type Kind uint
const (
    Invalid Kind = iota  // 非法类型
    Bool                 // 布尔型
    Int                  // 有符号整型
    Int8                 // 有符号8位整型
    Int16                // 有符号16位整型
    Int32                // 有符号32位整型
    Int64                // 有符号64位整型
    Uint                 // 无符号整型
    Uint8                // 无符号8位整型
    Uint16               // 无符号16位整型
    Uint32               // 无符号32位整型
    Uint64               // 无符号64位整型
    Uintptr              // 指针
    Float32              // 单精度浮点数
    Float64              // 双精度浮点数
    Complex64            // 64位复数类型
    Complex128           // 128位复数类型
    Array                // 数组
    Chan                 // 通道
    Func                 // 函数
    Interface            // 接口
    Map                  // 映射
    Ptr                  // 指针
    Slice                // 切片
    String               // 字符串
    Struct               // 结构体
    UnsafePointer        // 底层指针
)
```

##### 29.4.2 ValueOf

  `reflect.ValueOf()`返回的是`reflect.Value`类型，其中包含了原始值的值信息。`reflect.Value`与原始值之间可以互相转换。

`reflect.Value`类型提供的获取原始值的方法如下：

|           方法           |                             说明                             |
| :----------------------: | :----------------------------------------------------------: |
| Interface() interface {} | 将值以 interface{} 类型返回，可以通过类型断言转换为指定类型  |
|       Int() int64        |     将值以 int 类型返回，所有有符号整型均可以此方式返回      |
|      Uint() uint64       |     将值以 uint 类型返回，所有无符号整型均可以此方式返回     |
|     Float() float64      | 将值以双精度（float64）类型返回，所有浮点数（float32、float64）均可以此方式返回 |
|       Bool() bool        |                     将值以 bool 类型返回                     |
|     Bytes() []bytes      |               将值以字节数组 []bytes 类型返回                |
|     String() string      |                     将值以字符串类型返回                     |

* 通过反射获取值

```go
func reflectValue(x interface{}) {
	v := reflect.ValueOf(x)
	k := v.Kind()
	switch k {
	case reflect.Int64:
		// v.Int()从反射中获取整型的原始值，然后通过int64()强制类型转换
		fmt.Printf("type is int64, value is %d\n", int64(v.Int()))
	case reflect.Float32:
		// v.Float()从反射中获取浮点型的原始值，然后通过float32()强制类型转换
		fmt.Printf("type is float32, value is %f\n", float32(v.Float()))
	case reflect.Float64:
		// v.Float()从反射中获取浮点型的原始值，然后通过float64()强制类型转换
		fmt.Printf("type is float64, value is %f\n", float64(v.Float()))
	}
}
func main() {
	var a float32 = 3.14
	var b int64 = 100
	reflectValue(a) // type is float32, value is 3.140000
	reflectValue(b) // type is int64, value is 100
	// 将int类型的原始值转换为reflect.Value类型
	c := reflect.ValueOf(10)
	fmt.Printf("type c :%T\n", c) // type c :reflect.Value
}
```

* 通过反射设置值

想要在函数中通过反射修改变量的值，需要注意函数参数传递的是值拷贝，必须传递变量地址才能修改变量值。而反射中使用专有的`Elem()`方法来获取指针对应的值。

```go
package main

import (
	"fmt"
	"reflect"
)

func reflectSetValue1(x interface{}) {
	v := reflect.ValueOf(x)
	if v.Kind() == reflect.Int64 {
		v.SetInt(200) //修改的是副本，reflect包会引发panic
	}
}
func reflectSetValue2(x interface{}) {
	v := reflect.ValueOf(x)
	// 反射中使用 Elem()方法获取指针对应的值
	if v.Elem().Kind() == reflect.Int64 {
		v.Elem().SetInt(200)
	}
}
func main() {
	var a int64 = 100
	// reflectSetValue1(a) //panic: reflect: reflect.Value.SetInt using unaddressable value
	reflectSetValue2(&a)
	fmt.Println(a)
}
```

#### 29.4 isNil()和isValid()

##### 29.4.1 isNil()

```go
func (v Value) IsNil() bool
```

`IsNil()`报告v持有的值是否为nil。v持有的值的分类必须是通道、函数、接口、映射、指针、切片之一；否则IsNil函数会导致panic。

##### 29.4.2 isValid()

```go
func (v Value) IsValid() bool
```

`IsValid()`返回v是否持有一个值。如果v是Value零值会返回假，此时v除了IsValid、String、Kind之外的方法都会导致panic。

Demo:

```go
func main() {
	// *int类型空指针
	var a *int
	fmt.Println("var a *int IsNil:", reflect.ValueOf(a).IsNil())
	// nil值
	fmt.Println("nil IsValid:", reflect.ValueOf(nil).IsValid())
	// 实例化一个匿名结构体
	b := struct{}{}
	// 尝试从结构体中查找"abc"字段
	fmt.Println("不存在的结构体成员:", reflect.ValueOf(b).FieldByName("abc").IsValid())
	// 尝试从结构体中查找"abc"方法
	fmt.Println("不存在的结构体方法:", reflect.ValueOf(b).MethodByName("abc").IsValid())
	// map
	c := map[string]int{}
	// 尝试从map中查找一个不存在的键
	fmt.Println("map中不存在的键：", reflect.ValueOf(c).MapIndex(reflect.ValueOf("娜扎")).IsValid())
}
```

#### 29.5 结构体反射

##### 29.5.1 与结构体相关的方法

任意值通过`reflect.TypeOf()`获得反射对象信息后，如果它的类型是结构体，可以通过反射值对象（`reflect.Type`）的`NumField()`和`Field()`方法获得结构体成员的详细信息。

`reflect.Type`中与获取结构体成员相关的的方法如下表所示。

|                            方法                             |                             说明                             |
| :---------------------------------------------------------: | :----------------------------------------------------------: |
|                  Field(i int) StructField                   |          根据索引，返回索引对应的结构体字段的信息。          |
|                       NumField() int                        |                   返回结构体成员字段数量。                   |
|        FieldByName(name string) (StructField, bool)         |       根据给定字符串返回字符串对应的结构体字段的信息。       |
|            FieldByIndex(index []int) StructField            | 多层成员访问时，根据 []int 提供的每个结构体的字段索引，返回字段的信息。 |
| FieldByNameFunc(match func(string) bool) (StructField,bool) |              根据传入的匹配函数匹配需要的字段。              |
|                       NumMethod() int                       |                返回该类型的方法集中方法的数目                |
|                     Method(int) Method                      |                返回该类型方法集中的第i个方法                 |
|             MethodByName(string)(Method, bool)              |              根据方法名返回该类型方法集中的方法              |

##### 29.5.2 StructField类型

`StructField`类型用来描述结构体中的一个字段的信息。

`StructField`的定义如下：

```go
type StructField struct {
    // Name是字段的名字。PkgPath是非导出字段的包路径，对导出字段该字段为""。
    // 参见http://golang.org/ref/spec#Uniqueness_of_identifiers
    Name    string
    PkgPath string
    Type      Type      // 字段的类型
    Tag       StructTag // 字段的标签
    Offset    uintptr   // 字段在结构体中的字节偏移量
    Index     []int     // 用于Type.FieldByIndex时的索引切片
    Anonymous bool      // 是否匿名字段
}
```

Demo:

```go
type Student struct {
	Name  string `json:"name"`
	Score int    `json:"score"`
}

func main() {
	stu1 := Student{
		Name:  "小王子",
		Score: 90,
	}

	t := reflect.TypeOf(stu1)
	fmt.Println(t.Name(), t.Kind()) // student struct
	// 通过for循环遍历结构体的所有字段信息
	for i := 0; i < t.NumField(); i++ {
		field := t.Field(i)
		fmt.Printf("name:%s index:%d type:%v json tag:%v\n", field.Name, field.Index, field.Type, field.Tag.Get("json"))
	}

	// 通过字段名获取指定结构体字段信息
	if scoreField, ok := t.FieldByName("Score"); ok {
		fmt.Printf("name:%s index:%d type:%v json tag:%v\n", scoreField.Name, scoreField.Index, scoreField.Type, scoreField.Tag.Get("json"))
	}
}
```

#### 29.6 总结

反射是一个强大并富有表现力的工具，能让我们写出更灵活的代码。但是反射不应该被滥用，原因有以下三个：

* 基于反射的代码是极其脆弱的，反射中的类型错误会在真正运行的时候才会引发panic，那很可能是在代码写完的很长时间之后
* 大量使用反射的代码通常难以理解
* 反射的性能低下，基于反射实现的代码通常比正常代码运行速度慢一到两个数量级



### 30 并发

#### 30.1 并发与并行的区别

* 并发：同一时间段同时在做很多事情
* 并行：同一时刻同时做做很多事情

#### 30. 2进程，线程，协程

* 进程： 一个程序启动后就启动了一个进程
* 线程：操作系统调度的最小单位
* 协程：用户态的线程

#### 30.3goroutine

 golang运行时执行

一个gorouting对应一个任务（函数）

##### 30.3.1 sync.WaitGroup

* Add(i) : 计数器 + 1
* Done(): 计数器 -1， 最好用defer注册
*  Wait(): 等待

```go
var wg sync.WaitGroup
func hello() {
  defer sync.Done() // 计数器-1
  fmt.Println("Hello world")
}
func main() {
  wg.Add(2) // 2代表启动几个goroutine
  go hello()
  go hello()
  fmt.Println("Hello main")
  wg.Wait() // 阻塞，一直等待所有的goroutine结束
}
// 结果如下

```

##### 30.3.2 goroutine与线程的区别

* 可增长的栈
* goroutine调度，Go运行时（runtime）自己的调试器调度的， 采用m:n调度技术（复用/调度m到n个 goroutine OS线程）
* GOMAXPROCS, runtime.GOMAXPROCS(1)，可用来修改当前程序并发时占用CPU逻辑个数，默认在go1.5版本后是全部占用

#### 30.3 channel

##### 30.3.1定义

channel是引用类型

```go
var ch1 chan int
var ch2 chan string
// make分配内存， slice, map, channel
ch3 := make(chan int, 1)
// 通道的操作：发送、接收、关闭
// 发送和接收 <-
ch3 <- 10 // 把10发送到ch3中
ret := <-ch3 // 从 ch3中接收值，保存到变量ret中
// 关闭
// 1. 如果再接收值能取到对应的零值
// 2. 往关闭的channel中发送值会引发panic
// 3. 关闭一个已经关闭的channel也会引发panic
close(ch3)
```

##### 30.3.2 无缓冲通道和缓冲通道

``` go
fun recv(ch chan bool) {
  <- ch
}
func main() {
  ch := make(chan bool)
  go recv(ch)
  ch <- true
}
```

* 取值时通道是否关闭

  ```go
  func send(ch chan int) {
    for i:= 0; i < 10; i++ {
      ch <- i
    }
    close(ch)
  }
  func main () {
    var ch1 = make(chan int, 100)
    go send()
    //第一种
    for {
      ret, ok := <- ch1
      if !ok {
        break
      }
    }
   	// 第二种
    for ret := range ch1 {
      fmt.Println(ret)
    }
  }
  ```

  

#### 30.4 select多路复用

同一时间点从多个通道操作数据

```go
select {
  case <-ch1:
	case data := <-ch2:
  case ch3 := <-data:
  default:
}
```

#### 30.5 单向通道

参数带`<-`

chan<- :只能发送的一个队列（单向通道）

<-chan:只能接收的一个队列（单向通道）

```go
func producer(ch chan<- *item) {
	// 1: 生成随要数
	var id int64
	for {
		id++
		number := rand.Int63()
		tmp := &item{
			id:  id,
			num: number,
		}
		ch <- tmp
	}
}

```

#### 30.6 并发控制与锁

##### 30.6.1 数据竞争

``` go
var x int64
var wg sync.WaitGroup
func add() {
  for i:= 0; i < 5000; i++ {
    x = x + 1
  }
  wg.done()
}
func main() {
  wg.Add(2)
  go add()
  go add()
  wg.Wait()
  fmt.Println(x) // 结果随机
}
```

##### 30.6.2 互斥锁

```go
var x int64
var wg sync.WaitGroup
var lock sync.Mutex
func add() {
  for i:= 0; i < 5000; i++ {
    lock.Lock()
    x = x + 1
    lock.Unlock()
  }
  wg.done()
}
func main() {
  wg.Add(2)
  go add()
  go add()
  wg.Wait()
  fmt.Println(x) // 结果随机
}
```

##### 30.6.3 读写互斥锁

``` go
var x int64
var wg sync.WaitGroup
var lock sync.Mutex
var rwlock sync.RWMutex
func read() {
  defer wg.Done()
  //lock.Lock()
  rwlock.RLock()
  time.Sleep(time.Millisecond * 10)
  //lock.Unlock()
  rwlock.URLock()
}
func write() {
  defer wg.Done()
  //lock.Lock()
  rwlock.Lock()
  x = x + 1
  time.Sleep(time.Millisecond * 50)
  //lock.Unlock()
  rwlock.Unlock()
}
func main() {
  start := time.Now()
  for i:= 0; i < 10; i++ {
    wg.Add(1)
    go write()
  }
  for i:= 0; i < 1000; i++ {
    wg.Add(1)
    go read()
  }
  end := time.Now()
  fmt.Println("耗时%v.", end.Sub(start))
}
```

注：只有读的时候多于写的时候，读写锁才会有意义

##### 30.6.3  sync.Once

```go
var icons map[string]image.Image
var loadIconsOnce sync.Once
func loadIcons() {
  icons = map[string]image.Image{
    "left": loadIcon("left.png"),
    "right": loadIcon("right.png")
  }
}
//  Icon是并发安全的
func Icon(nam string) image.Image {
  loadIconsOnce.Do(loadIcons)
  return icons[name]
}
```

##### 30.6.4  sync.Map

Map并不是并发安全的，`sync.Map`适用于并发

``` go
var m = make(map[string]int)
func get(key string) int {
  return m[key]
}
func set(key string, value int) {
  m[key] = value
}
func main() {
  wg := wg.WaitGroup
  for i:= 0; i < 20; i++ {
    wg.Add(1)
    go func(n int) {
      key := strconv.Itoa(n)
      set(key, n)
      wg.Done()
    }(i)
  }
  wg.Wait()
}
```

改良版

```go
var m = sync.Map{}
func main{
  wg := wg.WaitGroup
  for i: = 0; i < 20; i++ {
    wg.Add(1)
    go func(n int) {
      key := strconv.Itoa(n)
      m.Store(key, n)
      value, _ := m.Load(key)
      wg.Done()
    }(i)
  }
  wg.Wait()
}
```

##### 30.6.5 原子操作

代码中的加锁操作因为涉及内核态的上下文切换会比较耗时、代价比较高。针对基本数据类型我们还可以使用原子操作来保证并发安全，因为原子操作是Golang提供的方法，它在用户态就可以完成，因些性能比加锁操作更好， Golang中的原子操作由内制的标准库sync/atomic提供（只支持int unit类型）

###  31单元测试

Go语言中的测试依赖`go test`命令。编写测试代码和编写普通的Go代码过程是类似的，并不需要学习新的语法、规则或工具。

go test命令是一个按照一定约定和组织的测试代码的驱动程序。在包目录内，所有以`_test.go`为后缀名的源代码文件都是`go test`测试的一部分，不会被`go build`编译到最终的可执行文件中。

在`*_test.go`文件中有三种类型的函数，单元测试函数、基准测试函数和示例函数。

|   类型   |         格式          |              作用              |
| :------: | :-------------------: | :----------------------------: |
| 测试函数 |   函数名前缀为Test    | 测试程序的一些逻辑行为是否正确 |
| 基准函数 | 函数名前缀为Benchmark |         测试函数的性能         |
| 示例函数 |  函数名前缀为Example  |       为文档提供示例文档       |

`go test`命令会遍历所有的`*_test.go`文件中符合上述命名规则的函数，然后生成一个临时的main包用于调用相应的测试函数，然后构建并运行、报告测试结果，最后清理测试中生成的临时文件。

```bash
go test
go test -v
go test -run="正则" -v
```

测试函数的名字必须以`Test`开头，可选的后缀名必须以大写字母开头，举几个例子：

```go
func TestAdd(t *testing.T){ ... }
func TestSum(t *testing.T){ ... }
func TestLog(t *testing.T){ ... }
```

其中参数`t`用于报告测试失败和附加的日志信息。 `testing.T`的拥有的方法如下：

```go
func (c *T) Error(args ...interface{})
func (c *T) Errorf(format string, args ...interface{})
func (c *T) Fail()
func (c *T) FailNow()
func (c *T) Failed() bool
func (c *T) Fatal(args ...interface{})
func (c *T) Fatalf(format string, args ...interface{})
func (c *T) Log(args ...interface{})
func (c *T) Logf(format string, args ...interface{})
func (c *T) Name() string
func (t *T) Parallel()
func (t *T) Run(name string, f func(t *T)) bool
func (c *T) Skip(args ...interface{})
func (c *T) SkipNow()
func (c *T) Skipf(format string, args ...interface{})
func (c *T) Skipped() bool
```

#### 31.1 组合测试

``` go
func TestGroupSplit(t *testing.T) {
	type test struct {
		str      string
		sep      string
		excepted []string
	}
	var tests = map[string]test{
		"normal": test{"a:b:c", ":", []string{"a", "b", "c"}},
		"none":   test{"a:b:c", "*", []string{"a:b:c"}},
		"multi":  test{"abcfbcdbce", "bc", []string{"a", "f", "d", "e"}},
	}
	for name, testcase := range tests {
		ret := Split(testcase.str, testcase.sep)
		if ok := reflect.DeepEqual(ret, testcase.excepted); !ok {
			t.Fatalf("Testcase:%v Failed, Excepted: %#v, got: %#v", name, testcase.excepted, ret)
		}
	}
}
```

```
go test -run /none -v // 运行指定的测试用例
```



#### 31.2 子测试

``` go
func TestGroupSplit(t *testing.T) {
	type test struct {
		str      string
		sep      string
		excepted []string
	}
	var tests = map[string]test{
		"normal": test{"a:b:c", ":", []string{"a", "b", "c"}},
		"none":   test{"a:b:c", "*", []string{"a:b:c"}},
		"multi":  test{"abcfbcdbce", "bc", []string{"a", "f", "d", "e"}},
	}
	for name, testcase := range tests {
		// ret := Split(testcase.str, testcase.sep)
		// if ok := reflect.DeepEqual(ret, testcase.excepted); !ok {
		// 	t.Fatalf("Testcase:%v Failed, Excepted: %#v, got: %#v", testcase.excepted, ret)
		// }
		t.Run(name, func(t *testing.T) {
			ret := Split(testcase.str, testcase.sep)
			if !reflect.DeepEqual(ret, testcase.excepted) {
				t.Fatalf("Excepted: %#v, got: %#v", testcase.excepted, ret)
			}
		})
	}
}
```

#### 31.2 测试覆盖率

测试覆盖率是你的代码被测试套件覆盖的百分比。通常我们使用的都是语句的覆盖率，也就是在测试中至少被运行一次的代码占总代码的比例。

Go提供内置功能来检查你的代码覆盖率。我们可以使用`go test -cover`来查看测试覆盖率。例如

```bash
split $ go test -cover
PASS
coverage: 100.0% of statements
ok      github.com/Q1mi/studygo/code_demo/test_demo/split       0.005s
```

Go还提供了一个额外的`-coverprofile`参数，用来将覆盖率相关的记录信息输出到一个文件。例如：

```go
split $ go test -cover -coverprofile=c.out
PASS
coverage: 100.0% of statements
ok      github.com/Q1mi/studygo/code_demo/test_demo/split       0.005s
```

上面的命令会将覆盖率相关的信息输出到当前文件夹下面的`c.out`文件中，然后我们执行`go tool cover -html=c.out`，使用`cover`工具来处理生成的记录信息，该命令会打开本地的浏览器窗口生成一个HTML报告。![Go test cover](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/cover.png)上图中每个用绿色标记的语句块表示被覆盖了，而红色的表示没有被覆盖。

#### 31.3基准测试

基准测试就是在一定的工作负载之下检测程序性能的一种方法。基准测试的基本格式如下：

```go
func BenchmarkName(b *testing.B){
    // ...
}
```

基准测试以`Benchmark`为前缀，需要一个`*testing.B`类型的参数b，基准测试必须要执行`b.N`次，这样的测试才有对照性，`b.N`的值是系统根据实际情况去调整的，从而保证测试的稳定性。 `testing.B`拥有的方法如下：

```go
func (c *B) Error(args ...interface{})
func (c *B) Errorf(format string, args ...interface{})
func (c *B) Fail()
func (c *B) FailNow()
func (c *B) Failed() bool
func (c *B) Fatal(args ...interface{})
func (c *B) Fatalf(format string, args ...interface{})
func (c *B) Log(args ...interface{})
func (c *B) Logf(format string, args ...interface{})
func (c *B) Name() string
func (b *B) ReportAllocs()
func (b *B) ResetTimer()
func (b *B) Run(name string, f func(b *B)) bool
func (b *B) RunParallel(body func(*PB))
func (b *B) SetBytes(n int64)
func (b *B) SetParallelism(p int)
func (c *B) Skip(args ...interface{})
func (c *B) SkipNow()
func (c *B) Skipf(format string, args ...interface{})
func (c *B) Skipped() bool
func (b *B) StartTimer()
func (b *B) StopTimer()
```

我们为split包中的`Split`函数编写基准测试如下：

```go
func BenchmarkSplit(b *testing.B) {
	for i := 0; i < b.N; i++ {
		Split("沙河有沙又有河", "沙")
	}
}
```

基准测试并不会默认执行，需要增加`-bench`参数，所以我们通过执行`go test -bench=Split`命令执行基准测试，输出结果如下：

```bash
split $ go test -bench=Split -cpu=8
goos: darwin
goarch: amd64
pkg: github.com/Q1mi/studygo/code_demo/test_demo/split
BenchmarkSplit-8        10000000               203 ns/op
PASS
ok      github.com/Q1mi/studygo/code_demo/test_demo/split       2.255s
```

其中`BenchmarkSplit-8`表示对Split函数进行基准测试，数字`8`表示`GOMAXPROCS`的值，这个对于并发基准测试很重要。`10000000`和`203ns/op`表示每次调用`Split`函数耗时`203ns`，这个结果是`10000000`次调用的平均值。

我们还可以为基准测试添加`-benchmem`参数，来获得内存分配的统计数据。

```bash
split $ go test -bench=Split -benchmem
goos: darwin
goarch: amd64
pkg: github.com/Q1mi/studygo/code_demo/test_demo/split
BenchmarkSplit-8        10000000               215 ns/op             112 B/op          3 allocs/op
PASS
ok      github.com/Q1mi/studygo/code_demo/test_demo/split       2.394s
```

其中，`112 B/op`表示每次操作内存分配了112字节，`3 allocs/op`则表示每次操作进行了3次内存分配。 我们将我们的`Split`函数优化如下：

```go
func Split(s, sep string) (result []string) {
	result = make([]string, 0, strings.Count(s, sep)+1)
	i := strings.Index(s, sep)
	for i > -1 {
		result = append(result, s[:i])
		s = s[i+len(sep):] // 这里使用len(sep)获取sep的长度
		i = strings.Index(s, sep)
	}
	result = append(result, s)
	return
}
```

这一次我们提前使用make函数将result初始化为一个容量足够大的切片，而不再像之前一样通过调用append函数来追加。我们来看一下这个改进会带来多大的性能提升：

```bash
split $ go test -bench=Split -benchmem
goos: darwin
goarch: amd64
pkg: github.com/Q1mi/studygo/code_demo/test_demo/split
BenchmarkSplit-8        10000000               127 ns/op              48 B/op          1 allocs/op
PASS
ok      github.com/Q1mi/studygo/code_demo/test_demo/split       1.423s
```

这个使用make函数提前分配内存的改动，减少了2/3的内存分配次数，并且减少了一半的内存分配。

#### 31.4 性能比较函数

上面的基准测试只能得到给定操作的绝对耗时，但是在很多性能问题是发生在两个不同操作之间的相对耗时，比如同一个函数处理1000个元素的耗时与处理1万甚至100万个元素的耗时的差别是多少？再或者对于同一个任务究竟使用哪种算法性能最佳？我们通常需要对两个不同算法的实现使用相同的输入来进行基准比较测试。

性能比较函数通常是一个带有参数的函数，被多个不同的Benchmark函数传入不同的值来调用。举个例子如下：

```go
func benchmark(b *testing.B, size int){/* ... */}
func Benchmark10(b *testing.B){ benchmark(b, 10) }
func Benchmark100(b *testing.B){ benchmark(b, 100) }
func Benchmark1000(b *testing.B){ benchmark(b, 1000) }
```

例如我们编写了一个计算斐波那契数列的函数如下：

```go
// fib.go

// Fib 是一个计算第n个斐波那契数的函数
func Fib(n int) int {
	if n < 2 {
		return n
	}
	return Fib(n-1) + Fib(n-2)
}
```

我们编写的性能比较函数如下：

```go
// fib_test.go

func benchmarkFib(b *testing.B, n int) {
	for i := 0; i < b.N; i++ {
		Fib(n)
	}
}

func BenchmarkFib1(b *testing.B)  { benchmarkFib(b, 1) }
func BenchmarkFib2(b *testing.B)  { benchmarkFib(b, 2) }
func BenchmarkFib3(b *testing.B)  { benchmarkFib(b, 3) }
func BenchmarkFib10(b *testing.B) { benchmarkFib(b, 10) }
func BenchmarkFib20(b *testing.B) { benchmarkFib(b, 20) }
func BenchmarkFib40(b *testing.B) { benchmarkFib(b, 40) }
```

运行基准测试：

```bash
split $ go test -bench=.
goos: darwin
goarch: amd64
pkg: github.com/Q1mi/studygo/code_demo/test_demo/fib
BenchmarkFib1-8         1000000000               2.03 ns/op
BenchmarkFib2-8         300000000                5.39 ns/op
BenchmarkFib3-8         200000000                9.71 ns/op
BenchmarkFib10-8         5000000               325 ns/op
BenchmarkFib20-8           30000             42460 ns/op
BenchmarkFib40-8               2         638524980 ns/op
PASS
ok      github.com/Q1mi/studygo/code_demo/test_demo/fib 12.944s
```

这里需要注意的是，默认情况下，每个基准测试至少运行1秒。如果在Benchmark函数返回时没有到1秒，则b.N的值会按1,2,5,10,20,50，…增加，并且函数再次运行。

最终的BenchmarkFib40只运行了两次，每次运行的平均值只有不到一秒。像这种情况下我们应该可以使用`-benchtime`标志增加最小基准时间，以产生更准确的结果。例如：

```bash
split $ go test -bench=Fib40 -benchtime=20s
goos: darwin
goarch: amd64
pkg: github.com/Q1mi/studygo/code_demo/test_demo/fib
BenchmarkFib40-8              50         663205114 ns/op
PASS
ok      github.com/Q1mi/studygo/code_demo/test_demo/fib 33.849s
```

这一次`BenchmarkFib40`函数运行了50次，结果就会更准确一些了。

使用性能比较函数做测试的时候一个容易犯的错误就是把`b.N`作为输入的大小，例如以下两个例子都是错误的示范：

```go
// 错误示范1
func BenchmarkFibWrong(b *testing.B) {
	for n := 0; n < b.N; n++ {
		Fib(n)
	}
}

// 错误示范2
func BenchmarkFibWrong2(b *testing.B) {
	Fib(b.N)
}
```

#### 31.5 重置时间

`b.ResetTimer`之前的处理不会放到执行时间里，也不会输出到报告中，所以可以在之前做一些不计划作为测试报告的操作。例如：

```go
func BenchmarkSplit(b *testing.B) {
	time.Sleep(5 * time.Second) // 假设需要做一些耗时的无关操作
	b.ResetTimer()              // 重置计时器
	for i := 0; i < b.N; i++ {
		Split("沙河有沙又有河", "沙")
	}
}
```

#### 31.6 并行测试

`func (b *B) RunParallel(body func(*PB))`会以并行的方式执行给定的基准测试。

`RunParallel`会创建出多个`goroutine`，并将`b.N`分配给这些`goroutine`执行， 其中`goroutine`数量的默认值为`GOMAXPROCS`。用户如果想要增加非CPU受限（non-CPU-bound）基准测试的并行性， 那么可以在`RunParallel`之前调用`SetParallelism` 。`RunParallel`通常会与`-cpu`标志一同使用。

```go
func BenchmarkSplitParallel(b *testing.B) {
	// b.SetParallelism(1) // 设置使用的CPU数
	b.RunParallel(func(pb *testing.PB) {
		for pb.Next() {
			Split("沙河有沙又有河", "沙")
		}
	})
}
```

执行一下基准测试：

```bash
split $ go test -bench=.
goos: darwin
goarch: amd64
pkg: github.com/Q1mi/studygo/code_demo/test_demo/split
BenchmarkSplit-8                10000000               131 ns/op
BenchmarkSplitParallel-8        50000000                36.1 ns/op
PASS
ok      github.com/Q1mi/studygo/code_demo/test_demo/split       3.308s
```

还可以通过在测试命令后添加`-cpu`参数如`go test -bench=. -cpu 1`来指定使用的CPU数量。

#### 31.7  Setup和TearDown

测试程序有时需要在测试之前进行额外的设置（setup）或在测试之后进行拆卸（teardown）。

##### 31.7.1 TestMain

通过在`*_test.go`文件中定义`TestMain`函数来可以在测试之前进行额外的设置（setup）或在测试之后进行拆卸（teardown）操作。

如果测试文件包含函数:`func TestMain(m *testing.M)`那么生成的测试会先调用 TestMain(m)，然后再运行具体测试。`TestMain`运行在主`goroutine`中, 可以在调用 `m.Run`前后做任何设置（setup）和拆卸（teardown）。退出测试的时候应该使用`m.Run`的返回值作为参数调用`os.Exit`。

一个使用`TestMain`来设置Setup和TearDown的示例如下：

```go
func TestMain(m *testing.M) {
	fmt.Println("write setup code here...") // 测试之前的做一些设置
	// 如果 TestMain 使用了 flags，这里应该加上flag.Parse()
	retCode := m.Run()                         // 执行测试
	fmt.Println("write teardown code here...") // 测试之后做一些拆卸工作
	os.Exit(retCode)                           // 退出测试
}
```

需要注意的是：在调用`TestMain`时, `flag.Parse`并没有被调用。所以如果`TestMain` 依赖于command-line标志 (包括 testing 包的标记), 则应该显示的调用`flag.Parse`。

##### 31.7.1 子测试的Setup与Teardown

有时候我们可能需要为每个测试集设置Setup与Teardown，也有可能需要为每个子测试设置Setup与Teardown。下面我们定义两个函数工具函数如下：

```go
// 测试集的Setup与Teardown
func setupTestCase(t *testing.T) func(t *testing.T) {
	t.Log("如有需要在此执行:测试之前的setup")
	return func(t *testing.T) {
		t.Log("如有需要在此执行:测试之后的teardown")
	}
}

// 子测试的Setup与Teardown
func setupSubTest(t *testing.T) func(t *testing.T) {
	t.Log("如有需要在此执行:子测试之前的setup")
	return func(t *testing.T) {
		t.Log("如有需要在此执行:子测试之后的teardown")
	}
}
```

使用方式如下：

```go
func TestSplit(t *testing.T) {
	type test struct { // 定义test结构体
		input string
		sep   string
		want  []string
	}
	tests := map[string]test{ // 测试用例使用map存储
		"simple":      {input: "a:b:c", sep: ":", want: []string{"a", "b", "c"}},
		"wrong sep":   {input: "a:b:c", sep: ",", want: []string{"a:b:c"}},
		"more sep":    {input: "abcd", sep: "bc", want: []string{"a", "d"}},
		"leading sep": {input: "沙河有沙又有河", sep: "沙", want: []string{"", "河有", "又有河"}},
	}
	teardownTestCase := setupTestCase(t) // 测试之前执行setup操作
	defer teardownTestCase(t)            // 测试之后执行testdoen操作

	for name, tc := range tests {
		t.Run(name, func(t *testing.T) { // 使用t.Run()执行子测试
			teardownSubTest := setupSubTest(t) // 子测试之前执行setup操作
			defer teardownSubTest(t)           // 测试之后执行testdoen操作
			got := Split(tc.input, tc.sep)
			if !reflect.DeepEqual(got, tc.want) {
				t.Errorf("excepted:%#v, got:%#v", tc.want, got)
			}
		})
	}
}
```

测试结果如下：

```bash
split $ go test -v
=== RUN   TestSplit
=== RUN   TestSplit/simple
=== RUN   TestSplit/wrong_sep
=== RUN   TestSplit/more_sep
=== RUN   TestSplit/leading_sep
--- PASS: TestSplit (0.00s)
    split_test.go:71: 如有需要在此执行:测试之前的setup
    --- PASS: TestSplit/simple (0.00s)
        split_test.go:79: 如有需要在此执行:子测试之前的setup
        split_test.go:81: 如有需要在此执行:子测试之后的teardown
    --- PASS: TestSplit/wrong_sep (0.00s)
        split_test.go:79: 如有需要在此执行:子测试之前的setup
        split_test.go:81: 如有需要在此执行:子测试之后的teardown
    --- PASS: TestSplit/more_sep (0.00s)
        split_test.go:79: 如有需要在此执行:子测试之前的setup
        split_test.go:81: 如有需要在此执行:子测试之后的teardown
    --- PASS: TestSplit/leading_sep (0.00s)
        split_test.go:79: 如有需要在此执行:子测试之前的setup
        split_test.go:81: 如有需要在此执行:子测试之后的teardown
    split_test.go:73: 如有需要在此执行:测试之后的teardown
=== RUN   ExampleSplit
--- PASS: ExampleSplit (0.00s)
PASS
ok      github.com/Q1mi/studygo/code_demo/test_demo/split       0.006s
```

##### 31.7.2 示例函数

被`go test`特殊对待的第三种函数就是示例函数，它们的函数名以`Example`为前缀。它们既没有参数也没有返回值。标准格式如下：

```go
func ExampleName() {
    // ...
}
```

### 32 TCP编辑

#### 32.1 七层协议

![osi七层模型](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/osi.png)

#### 32.2 Socket图解

![socket图解](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/socket.png)

#### 32.3 HTTP数据传输图解

![HTTP数据传输图解](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/httptcpip.png)

#### 32.3 unicode包

unicode.IsLetter():

unicode.ToLower():

unicode.ToUpper():

#### 32.4 粘包

主要原因：

就是tcp数据传递模式是流模式，在保持长连接的时候可以进行多次的收和发。

“粘包”可发生在发送端也可发生在接收端：

1. 由Nagle算法造成的发送端的粘包：Nagle算法是一种改善网络传输效率的算法。简单来说就是当我们提交一段数据给TCP发送时，TCP并不立刻发送此段数据，而是等待一小段时间看看在等待期间是否还有要发送的数据，若有则会一次把这两段数据发送出去。
2. 接收端接收不及时造成的接收端粘包：TCP会把接收到的数据存在自己的缓冲区中，然后通知应用层取数据。当应用层由于某些原因不能及时的把TCP的数据取出来，就会造成TCP缓冲区中存放了几段数据。

解决办法：

出现”粘包”的关键在于接收方不确定将要传输的数据包的大小，因此我们可以对数据包进行封包和拆包的操作。

封包：封包就是给一段数据加上包头，这样一来数据包就分为包头和包体两部分内容了(过滤非法包时封包会加入”包尾”内容)。包头部分的长度是固定的，并且它存储了包体的长度，根据包头长度固定以及包头中含有包体长度的变量就能正确的拆分出一个完整的数据包。

我们可以自己定义一个协议，比如数据包的前4个字节为包头，里面存储的是发送的数据的长度。

```go
// socket_stick/proto/proto.go
package proto

import (
	"bufio"
	"bytes"
	"encoding/binary"
)

// Encode 将消息编码
func Encode(message string) ([]byte, error) {
	// 读取消息的长度，转换成int32类型（占4个字节）
	var length = int32(len(message))
	var pkg = new(bytes.Buffer)
	// 写入消息头
  // 按照小端的方式写入pkg
	err := binary.Write(pkg, binary.LittleEndian, length)
	if err != nil {
		return nil, err
	}
	// 写入消息实体
	err = binary.Write(pkg, binary.LittleEndian, []byte(message))
	if err != nil {
		return nil, err
	}
	return pkg.Bytes(), nil
}

// Decode 解码消息
func Decode(reader *bufio.Reader) (string, error) {
	// 读取消息的长度
	lengthByte, _ := reader.Peek(4) // 读取前4个字节的数据
	lengthBuff := bytes.NewBuffer(lengthByte)
	var length int32
	err := binary.Read(lengthBuff, binary.LittleEndian, &length)
	if err != nil {
		return "", err
	}
	// Buffered返回缓冲中现有的可读取的字节数。
	if int32(reader.Buffered()) < length+4 {
		return "", err
	}

	// 读取真正的消息数据
	pack := make([]byte, int(4+length))
	_, err = reader.Read(pack)
	if err != nil {
		return "", err
	}
	return string(pack[4:]), nil
}
```

大端，小端

![image-20201224061058791](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201224061058791.png)

接下来在服务端和客户端分别使用上面定义的`proto`包的`Decode`和`Encode`函数处理数据。

服务端代码如下：

```go
// socket_stick/server2/main.go

func process(conn net.Conn) {
	defer conn.Close()
	reader := bufio.NewReader(conn)
	for {
		msg, err := proto.Decode(reader)
		if err == io.EOF {
			return
		}
		if err != nil {
			fmt.Println("decode msg failed, err:", err)
			return
		}
		fmt.Println("收到client发来的数据：", msg)
	}
}

func main() {

	listen, err := net.Listen("tcp", "127.0.0.1:30000")
	if err != nil {
		fmt.Println("listen failed, err:", err)
		return
	}
	defer listen.Close()
	for {
		conn, err := listen.Accept()
		if err != nil {
			fmt.Println("accept failed, err:", err)
			continue
		}
		go process(conn)
	}
}
```

客户端代码如下：

```go
// socket_stick/client2/main.go

func main() {
	conn, err := net.Dial("tcp", "127.0.0.1:30000")
	if err != nil {
		fmt.Println("dial failed, err", err)
		return
	}
	defer conn.Close()
	for i := 0; i < 20; i++ {
		msg := `Hello, Hello. How are you?`
		data, err := proto.Encode(msg)
		if err != nil {
			fmt.Println("encode msg failed, err:", err)
			return
		}
		conn.Write(data)
	}
}
```



### 33 HTML

```html
<ul type="circle">
  <li></li>
</ul>

<ol type="I"> <!--罗马数字-->
  <li></li>
</ol>
<dl>
  <dt></dt>
  <dd></dd>
</dl>
```

### 34  template

#### 34.1 Go语言的模板引擎

Go语言内置了文本模板引擎`text/template`和用于HTML文档的`html/template`。它们的作用机制可以简单归纳如下：

1. 模板文件通常定义为`.tmpl`和`.tpl`为后缀（也可以使用其他的后缀），必须使用`UTF8`编码。
2. 模板文件中使用`{{`和`}}`包裹和标识需要传入的数据。
3. 传给模板这样的数据就可以通过点号（`.`）来访问，如果数据是复杂类型的数据，可以通过{ { .FieldName }}来访问它的字段。
4. 除`{{`和`}}`包裹的内容外，其他内容均不做修改原样输出。

##### 34.1.1 定义模板文件

我们按照Go模板语法定义一个`hello.tmpl`的模板文件，内容如下：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Hello</title>
</head>
<body>
    <p>Hello {{.}}</p>
</body>
</html>
```

##### 34.1.2 解析和渲染模板文件

然后我们创建一个`main.go`文件，在其中写下HTTP server端代码如下：

```go
// main.go

func sayHello(w http.ResponseWriter, r *http.Request) {
	// 解析指定文件生成模板对象
	tmpl, err := template.ParseFiles("./hello.tmpl")
	if err != nil {
		fmt.Println("create template failed, err:", err)
		return
	}
	// 利用给定数据渲染模板，并将结果写入w
	tmpl.Execute(w, "沙河小王子")
}
func main() {
	http.HandleFunc("/", sayHello)
	err := http.ListenAndServe(":9090", nil)
	if err != nil {
		fmt.Println("HTTP server failed,err:", err)
		return
	}
}
```

将上面的`main.go`文件编译执行，然后使用浏览器访问`http://127.0.0.1:9090`就能看到页面上显示了“Hello 沙河小王子”。 这就是一个最简单的模板渲染的示例，Go语言模板引擎详细用法请往下阅读。

#### 34.2 模板语法

##### 34.2.1 {{.}}

模板语法都包含在`{{`和`}}`中间，其中`{{.}}`中的点表示当前对象。

当我们传入一个结构体对象时，我们可以根据`.`来访问结构体的对应字段。例如：

```go
// main.go

type UserInfo struct {
	Name   string
	Gender string
	Age    int
}

func sayHello(w http.ResponseWriter, r *http.Request) {
	// 解析指定文件生成模板对象
	tmpl, err := template.ParseFiles("./hello.tmpl")
	if err != nil {
		fmt.Println("create template failed, err:", err)
		return
	}
	// 利用给定数据渲染模板，并将结果写入w
	user := UserInfo{
		Name:   "小王子",
		Gender: "男",
		Age:    18,
	}
	tmpl.Execute(w, user)
}
```

模板文件`hello.tmpl`内容如下：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Hello</title>
</head>
<body>
    <p>Hello {{.Name}}</p>
    <p>性别：{{.Gender}}</p>
    <p>年龄：{{.Age}}</p>
</body>
</html>
```

同理，当我们传入的变量是map时，也可以在模板文件中通过`.`根据key来取值。

##### 34.2.2 注释

```template
{{/* a comment */}}
注释，执行时会忽略。可以多行。注释不能嵌套，并且必须紧贴分界符始止。
```

##### 34.2.3 pipeline

`pipeline`是指产生数据的操作。比如`{{.}}`、`{{.Name}}`等。Go的模板语法中支持使用管道符号`|`链接多个命令，用法和unix下的管道类似：`|`前面的命令会将运算结果(或返回值)传递给后一个命令的最后一个位置。

**注意：**并不是只有使用了`|`才是pipeline。Go的模板语法中，`pipeline的`概念是传递数据，只要能产生数据的，都是`pipeline`。

##### 34.2.4 变量

我们还可以在模板中声明变量，用来保存传入模板的数据或其他语句生成的结果。具体语法如下：

```template
$obj := {{.}}
```

其中`$obj`是变量的名字，在后续的代码中就可以使用该变量了。

##### 34.2.5 移除空格

有时候我们在使用模板语法的时候会不可避免的引入一下空格或者换行符，这样模板最终渲染出来的内容可能就和我们想的不一样，这个时候可以使用`{{-`语法去除模板内容左侧的所有空白符号， 使用`-}}`去除模板内容右侧的所有空白符号。

例如：

```template
{{- .Name -}}
```

**注意：**`-`要紧挨`{{`和`}}`，同时与模板值之间需要使用空格分隔。



##### 34.2.6 条件判断

Go模板语法中的条件判断有以下几种:

```template
{{if pipeline}} T1 {{end}}

{{if pipeline}} T1 {{else}} T0 {{end}}

{{if pipeline}} T1 {{else if pipeline}} T0 {{end}}
```



##### 34.2.7 range

Go的模板语法中使用`range`关键字进行遍历，有以下两种写法，其中`pipeline`的值必须是数组、切片、字典或者通道。

```template
{{range pipeline}} T1 {{end}}
如果pipeline的值其长度为0，不会有任何输出

{{range pipeline}} T1 {{else}} T0 {{end}}
如果pipeline的值其长度为0，则会执行T0。
```



##### 34.2.8 with

```template
{{with pipeline}} T1 {{end}}
如果pipeline为empty不产生输出，否则将dot设为pipeline的值并执行T1。不修改外面的dot。

{{with pipeline}} T1 {{else}} T0 {{end}}
如果pipeline为empty，不改变dot并执行T0，否则dot设为pipeline的值并执行T1。
```



##### 34.2.9 预定义函数

```template
and
    函数返回它的第一个empty参数或者最后一个参数；
    就是说"and x y"等价于"if x then y else x"；所有参数都会执行；
or
    返回第一个非empty参数或者最后一个参数；
    亦即"or x y"等价于"if x then x else y"；所有参数都会执行；
not
    返回它的单个参数的布尔值的否定
len
    返回它的参数的整数类型长度
index
    执行结果为第一个参数以剩下的参数为索引/键指向的值；
    如"index x 1 2 3"返回x[1][2][3]的值；每个被索引的主体必须是数组、切片或者字典。
print
    即fmt.Sprint
printf
    即fmt.Sprintf
println
    即fmt.Sprintln
html
    返回与其参数的文本表示形式等效的转义HTML。
    这个函数在html/template中不可用。
urlquery
    以适合嵌入到网址查询中的形式返回其参数的文本表示的转义值。
    这个函数在html/template中不可用。
js
    返回与其参数的文本表示形式等效的转义JavaScript。
call
    执行结果是调用第一个参数的返回值，该参数必须是函数类型，其余参数作为调用该函数的参数；
    如"call .X.Y 1 2"等价于go语言里的dot.X.Y(1, 2)；
    其中Y是函数类型的字段或者字典的值，或者其他类似情况；
    call的第一个参数的执行结果必须是函数类型的值（和预定义函数如print明显不同）；
    该函数类型值必须有1到2个返回值，如果有2个则后一个必须是error接口类型；
    如果有2个返回值的方法返回的error非nil，模板执行会中断并返回给调用模板执行者该错误；
```



##### 34.2.10 比较函数

布尔函数会将任何类型的零值视为假，其余视为真。

下面是定义为函数的二元比较运算的集合：

```template
eq      如果arg1 == arg2则返回真
ne      如果arg1 != arg2则返回真
lt      如果arg1 < arg2则返回真
le      如果arg1 <= arg2则返回真
gt      如果arg1 > arg2则返回真
ge      如果arg1 >= arg2则返回真
```

为了简化多参数相等检测，eq（只有eq）可以接受2个或更多个参数，它会将第一个参数和其余参数依次比较，返回下式的结果：

```template
{{eq arg1 arg2 arg3}}
```

比较函数只适用于基本类型（或重定义的基本类型，如”type Celsius float32”）。但是，整数和浮点数不能互相比较。



##### 34.2.11 自定义函数

Go的模板支持自定义函数。

```go
func sayHello(w http.ResponseWriter, r *http.Request) {
	htmlByte, err := ioutil.ReadFile("./hello.tmpl")
	if err != nil {
		fmt.Println("read html failed, err:", err)
		return
	}
	// 自定义一个夸人的模板函数
	kua := func(arg string) (string, error) {
		return arg + "真帅", nil
	}
	// 采用链式操作在Parse之前调用Funcs添加自定义的kua函数
	tmpl, err := template.New("hello").Funcs(template.FuncMap{"kua": kua}).Parse(string(htmlByte))
	if err != nil {
		fmt.Println("create template failed, err:", err)
		return
	}

	user := UserInfo{
		Name:   "小王子",
		Gender: "男",
		Age:    18,
	}
	// 使用user渲染模板，并将结果写入w
	tmpl.Execute(w, user)
}
```

我们可以在模板文件`hello.tmpl`中按照如下方式使用我们自定义的`kua`函数了。

```template
{{kua .Name}}
```



##### 34.2.12 嵌套template

我们可以在template中嵌套其他的template。这个template可以是单独的文件，也可以是通过`define`定义的template。

举个例子： `t.tmpl`文件内容如下：

```template
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>tmpl test</title>
</head>
<body>
    
    <h1>测试嵌套template语法</h1>
    <hr>
    {{template "ul.tmpl"}}
    <hr>
    {{template "ol.tmpl"}}
</body>
</html>

{{ define "ol.tmpl"}}
<ol>
    <li>吃饭</li>
    <li>睡觉</li>
    <li>打豆豆</li>
</ol>
{{end}}
```

`ul.tmpl`文件内容如下：

```template
<ul>
    <li>注释</li>
    <li>日志</li>
    <li>测试</li>
</ul>
```

我们注册一个`templDemo`路由处理函数.

```go
http.HandleFunc("/tmpl", tmplDemo)
```

`tmplDemo`函数的具体内容如下：

```go
func tmplDemo(w http.ResponseWriter, r *http.Request) {
	tmpl, err := template.ParseFiles("./t.tmpl", "./ul.tmpl")
	if err != nil {
		fmt.Println("create template failed, err:", err)
		return
	}
	user := UserInfo{
		Name:   "小王子",
		Gender: "男",
		Age:    18,
	}
	tmpl.Execute(w, user)
}
```

**注意**：在解析模板时，被嵌套的模板一定要在后面解析，例如上面的示例中`t.tmpl`模板中嵌套了`ul.tmpl`，所以`ul.tmpl`要在`t.tmpl`后进行解析。

##### 34.2.13 block

```template
{{block "name" pipeline}} T1 {{end}}
```

`block`是定义模板`{{define "name"}} T1 {{end}}`和执行`{{template "name" pipeline}}`缩写，典型的用法是定义一组根模板，然后通过在其中重新定义块模板进行自定义。

定义一个根模板`templates/base.tmpl`，内容如下：

```template
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <title>Go Templates</title>
</head>
<body>
<div class="container-fluid">
    {{block "content" . }}{{end}}
</div>
</body>
</html>
```

然后定义一个`templates/index.tmpl`，”继承”`base.tmpl`：

```tempalte
{{template "base.tmpl"}}

{{define "content"}}
    <div>Hello world!</div>
{{end}}
```

然后使用`template.ParseGlob`按照正则匹配规则解析模板文件，然后通过`ExecuteTemplate`渲染指定的模板：

```go
func index(w http.ResponseWriter, r *http.Request){
	tmpl, err := template.ParseGlob("templates/*.tmpl")
	if err != nil {
		fmt.Println("create template failed, err:", err)
		return
	}
	err = tmpl.ExecuteTemplate(w, "index.tmpl", nil)
	if err != nil {
		fmt.Println("render template failed, err:", err)
		return
	}
}
```

如果我们的模板名称冲突了，例如不同业务线下都定义了一个`index.tmpl`模板，我们可以通过下面两种方法来解决。

1. 在模板文件开头使用`{{define 模板名}}`语句显式的为模板命名。
2. 可以把模板文件存放在`templates`文件夹下面的不同目录中，然后使用`template.ParseGlob("templates/**/*.tmpl")`解析模板。



##### 34.2.14 修改默认的标识符

Go标准库的模板引擎使用的花括号`{{`和`}}`作为标识，而许多前端框架（如`Vue`和 `AngularJS`）也使用`{{`和`}}`作为标识符，所以当我们同时使用Go语言模板引擎和以上前端框架时就会出现冲突，这个时候我们需要修改标识符，修改前端的或者修改Go语言的。这里演示如何修改Go语言模板引擎默认的标识符：

```go
template.New("test").Delims("{[", "]}").ParseFiles("./t.tmpl")
```

#### 34.3 text/template与html/tempalte的区别

`html/template`针对的是需要返回HTML内容的场景，在模板渲染过程中会对一些有风险的内容进行转义，以此来防范跨站脚本攻击。

例如，我定义下面的模板文件：

```template
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Hello</title>
</head>
<body>
    {{.}}
</body>
</html>
```

这个时候传入一段JS代码并使用`html/template`去渲染该文件，会在页面上显示出转义后的JS内容。`<script>alert('嘿嘿嘿')</script>` 这就是`html/template`为我们做的事。

但是在某些场景下，我们如果相信用户输入的内容，不想转义的话，可以自行编写一个safe函数，手动返回一个`template.HTML`类型的内容。示例如下：

```go
func xss(w http.ResponseWriter, r *http.Request){
	tmpl,err := template.New("xss.tmpl").Funcs(template.FuncMap{
		"safe": func(s string)template.HTML {
			return template.HTML(s)
		},
	}).ParseFiles("./xss.tmpl")
	if err != nil {
		fmt.Println("create template failed, err:", err)
		return
	}
	jsStr := `<script>alert('嘿嘿嘿')</script>`
	err = tmpl.Execute(w, jsStr)
	if err != nil {
		fmt.Println(err)
	}
}
```

这样我们只需要在模板文件不需要转义的内容后面使用我们定义好的safe函数就可以了。

```template
{{ . | safe }}
```

### 35 数据库和消息对列

#### 35.1 mysql

驱动：import _ "github.com/go-sql-driver/mysql"

sqlx: 查询单条，查询多条，执行SQL，事务，预处理

![image-20201225073942103](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20201225073942103.png)

#### 35.2 redis

#### 35.3 NSQ(消息对列)

### 36 godep

#### 36.1 安装

```bash
go get github.com/tools/godep
```

#### 36.2 基本命令

```bash
godep save     将依赖项输出并复制到Godeps.json文件中
godep go       使用保存的依赖项运行go工具
godep get      下载并安装具有指定依赖项的包
godep path     打印依赖的GOPATH路径
godep restore  在GOPATH中拉取依赖的版本
godep update   更新选定的包或go版本
godep diff     显示当前和以前保存的依赖项集之间的差异
godep version  查看版本信息
```

### 37  go module

`go module`是Go1.11版本之后官方推出的版本管理工具，并且从Go1.13版本开始，`go module`将是Go语言默认的依赖管理工具。

#### 37.1 GO111MODULE

要启用`go module`支持首先要设置环境变量`GO111MODULE`，通过它可以开启或关闭模块支持，它有三个可选值：`off`、`on`、`auto`，默认值是`auto`。

1. `GO111MODULE=off`禁用模块支持，编译时会从`GOPATH`和`vendor`文件夹中查找包。
2. `GO111MODULE=on`启用模块支持，编译时会忽略`GOPATH`和`vendor`文件夹，只根据 `go.mod`下载依赖。
3. `GO111MODULE=auto`，当项目在`$GOPATH/src`外且项目根目录有`go.mod`文件时，开启模块支持。

简单来说，设置`GO111MODULE=on`之后就可以使用`go module`了，以后就没有必要在GOPATH中创建项目了，并且还能够很好的管理项目依赖的第三方包信息。

使用 go module 管理依赖后会在项目根目录下生成两个文件`go.mod`和`go.sum`。

#### 37.2 GOPROXY

Go1.11之后设置GOPROXY命令为：

```bash
export GOPROXY=https://goproxy.cn
```

Go1.13之后`GOPROXY`默认值为`https://proxy.golang.org`，在国内是无法访问的，所以十分建议大家设置GOPROXY，这里我推荐使用[goproxy.cn](https://studygolang.com/topics/10014)。

```bash
go env -w GOPROXY=https://goproxy.cn,direct
```

#### 37.3 go mod命令

常用的`go mod`命令如下：

```
go mod download    下载依赖的module到本地cache（默认为$GOPATH/pkg/mod目录）
go mod edit        编辑go.mod文件
go mod graph       打印模块依赖图
go mod init        初始化当前文件夹, 创建go.mod文件
go mod tidy        增加缺少的module，删除无用的module
go mod vendor      将依赖复制到vendor下
go mod verify      校验依赖
go mod why         解释为什么需要依赖
```

#### 37.4 go.mod

go.mod文件记录了项目所有的依赖信息，其结构大致如下：

```sh
module github.com/Q1mi/studygo/blogger

go 1.12

require (
	github.com/DeanThompson/ginpprof v0.0.0-20190408063150-3be636683586
	github.com/gin-gonic/gin v1.4.0
	github.com/go-sql-driver/mysql v1.4.1
	github.com/jmoiron/sqlx v1.2.0
	github.com/satori/go.uuid v1.2.0
	google.golang.org/appengine v1.6.1 // indirect
)
```

其中，

- `module`用来定义包名
- `require`用来定义依赖包及版本
- `indirect`表示间接引用

##### 37.4.1 依赖的版本

go mod支持语义化版本号，比如`go get foo@v1.2.3`，也可以跟git的分支或tag，比如`go get foo@master`，当然也可以跟git提交哈希，比如`go get foo@e3702bed2`。关于依赖的版本支持以下几种格式：

```go
gopkg.in/tomb.v1 v1.0.0-20141024135613-dd632973f1e7
gopkg.in/vmihailenco/msgpack.v2 v2.9.1
gopkg.in/yaml.v2 <=v2.2.1
github.com/tatsushid/go-fastping v0.0.0-20160109021039-d7bb493dee3e
latest
```

##### 37.4.2 replace

在国内访问golang.org/x的各个包都需要翻墙，你可以在go.mod中使用replace替换成github上对应的库。

```go
replace (
	golang.org/x/crypto v0.0.0-20180820150726-614d502a4dac => github.com/golang/crypto v0.0.0-20180820150726-614d502a4dac
	golang.org/x/net v0.0.0-20180821023952-922f4815f713 => github.com/golang/net v0.0.0-20180826012351-8a410e7b638d
	golang.org/x/text v0.3.0 => github.com/golang/text v0.3.0
)
```

#### 37.5 go get

在项目中执行`go get`命令可以下载依赖包，并且还可以指定下载的版本。

1. 运行`go get -u`将会升级到最新的次要版本或者修订版本(x.y.z, z是修订版本号， y是次要版本号)
2. 运行`go get -u=patch`将会升级到最新的修订版本
3. 运行`go get package@version`将会升级到指定的版本号version

如果下整理依赖载所有依赖可以使用`go mod download`命令。

#### 37.6 整理依赖

我们在代码中删除依赖代码后，相关的依赖库并不会在`go.mod`文件中自动移除。这种情况下我们可以使用`go mod tidy`命令更新`go.mod`中的依赖关系。

#### 37.7 go mod edit

##### 37.7.1 格式化

因为我们可以手动修改go.mod文件，所以有些时候需要格式化该文件。Go提供了一下命令：

```bash
go mod edit -fmt
```

##### 37.7.2 添加依赖项

```bash
go mod edit -require=golang.org/x/text
```

##### 37.7.3 移除依赖项

如果只是想修改`go.mod`文件中的内容，那么可以运行`go mod edit -droprequire=package path`，比如要在`go.mod`中移除`golang.org/x/text`包，可以使用如下命令：

```bash
go mod edit -droprequire=golang.org/x/text
```

关于`go mod edit`的更多用法可以通过`go help mod edit`查看。

#### 37.8 在项目中使用go module

##### 37.8.1 既有项目

如果需要对一个已经存在的项目启用`go module`，可以按照以下步骤操作：

1. 在项目目录下执行`go mod init`，生成一个`go.mod`文件。
2. 执行`go get`，查找并记录当前项目的依赖，同时生成一个`go.sum`记录每个依赖库的版本和哈希值。

##### 37.8.2 新项目

对于一个新创建的项目，我们可以在项目文件夹下按照以下步骤操作：

1. 执行`go mod init 项目名`命令，在当前项目文件夹下创建一个`go.mod`文件。
2. 手动编辑`go.mod`中的require依赖项或执行`go get`自动发现、维护依赖。

### 38 Gin框架

#### 38.1 安装

```bash
go get -u github.com/gin-gonic/gin
```

#### 38.2 示例

```golang 
package main

import "github.com/gin-gonic/gin"

func main() {
	r := gin.Default()
	r.GET("/ping", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "pong",
		})
	})
  r.Run(":8080") // listen and serve on 0.0.0.0:8080 (for windows "localhost:8080")
}
```

### 39 RESTful API

REST与技术无关，代表的是一种软件架构风格，REST是Representational State Transfer的简称，中文翻译为“表征状态转移”或“表现层状态转化”。

推荐阅读[阮一峰 理解RESTful架构](http://www.ruanyifeng.com/blog/2011/09/restful.html)

简单来说，REST的含义就是客户端与Web服务器之间进行交互的时候，使用HTTP协议中的4个请求方法代表不同的动作。

- `GET`用来获取资源
- `POST`用来新建资源
- `PUT`用来更新资源
- `DELETE`用来删除资源。

只要API程序遵循了REST风格，那就可以称其为RESTful API。目前在前后端分离的架构中，前后端基本都是通过RESTful API来进行交互。

例如，我们现在要编写一个管理书籍的系统，我们可以查询对一本书进行查询、创建、更新和删除等操作，我们在编写程序的时候就要设计客户端浏览器与我们Web服务端交互的方式和路径。按照经验我们通常会设计成如下模式：

| 请求方法 |     URL      |     含义     |
| :------: | :----------: | :----------: |
|   GET    |    /book     | 查询书籍信息 |
|   POST   | /create_book | 创建书籍记录 |
|   POST   | /update_book | 更新书籍信息 |
|   POST   | /delete_book | 删除书籍信息 |

同样的需求我们按照RESTful API设计如下：

| 请求方法 |  URL  |     含义     |
| :------: | :---: | :----------: |
|   GET    | /book | 查询书籍信息 |
|   POST   | /book | 创建书籍记录 |
|   PUT    | /book | 更新书籍信息 |
|  DELETE  | /book | 删除书籍信息 |

Gin框架支持开发RESTful API的开发。

```go
func main() {
	r := gin.Default()
	r.GET("/book", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "GET",
		})
	})

	r.POST("/book", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "POST",
		})
	})

	r.PUT("/book", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "PUT",
		})
	})

	r.DELETE("/book", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "DELETE",
		})
	})
}
```

开发RESTful API的时候我们通常使用[Postman](https://www.getpostman.com/)来作为客户端的测试工具。

#### 39.1 渲染

##### 39.1.1 JSON

```go
c.JSON(HTTP.StatusOK, func(c *gin.Context){ "message": "HELLO"})
```



##### 39.1.2  HTML

我们首先定义一个存放模板文件的`templates`文件夹，然后在其内部按照业务分别定义一个`posts`文件夹和一个`users`文件夹。 `posts/index.html`文件的内容如下：

```template
{{define "posts/index.html"}}
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>posts/index</title>
</head>
<body>
    {{.title}}
</body>
</html>
{{end}}
```

`users/index.html`文件的内容如下：

```template
{{define "users/index.html"}}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>users/index</title>
</head>
<body>
    {{.title}}
</body>
</html>
{{end}}
```

Gin框架中使用`LoadHTMLGlob()`或者`LoadHTMLFiles()`方法进行HTML模板渲染。

```go
func main() {
	r := gin.Default()
	r.LoadHTMLGlob("templates/**/*")
  //静态文件处理
  r.Static("/static", "./static")
	//r.LoadHTMLFiles("templates/posts/index.html", "templates/users/index.html")
	r.GET("/posts/index", func(c *gin.Context) {
		c.HTML(http.StatusOK, "posts/index.html", gin.H{
			"title": "posts/index",
		})
	})

	r.GET("users/index", func(c *gin.Context) {
		c.HTML(http.StatusOK, "users/index.html", gin.H{
			"title": "users/index",
		})
	})

	r.Run(":8080")
}
```

##### 39.1.3  XML

``` go
func main() {
	r := gin.Default()
	// gin.H 是map[string]interface{}的缩写
	r.GET("/someXML", func(c *gin.Context) {
		// 方式一：自己拼接JSON
		c.XML(http.StatusOK, gin.H{"message": "Hello world!"})
	})
	r.GET("/moreXML", func(c *gin.Context) {
		// 方法二：使用结构体
		type MessageRecord struct {
			Name    string
			Message string
			Age     int
		}
		var msg MessageRecord
		msg.Name = "小王子"
		msg.Message = "Hello world!"
		msg.Age = 18
		c.XML(http.StatusOK, msg)
	})
	r.Run(":8080")
}
```

##### 39.1.4  YMAL渲染

```go
r.GET("/someYAML", func(c *gin.Context) {
	c.YAML(http.StatusOK, gin.H{"message": "ok", "status": http.StatusOK})
})
```

##### 39.1.5 protobuf渲染

```go
r.GET("/someProtoBuf", func(c *gin.Context) {
	reps := []int64{int64(1), int64(2)}
	label := "test"
	// protobuf 的具体定义写在 testdata/protoexample 文件中。
	data := &protoexample.Test{
		Label: &label,
		Reps:  reps,
	}
	// 请注意，数据在响应中变为二进制数据
	// 将输出被 protoexample.Test protobuf 序列化了的数据
	c.ProtoBuf(http.StatusOK, data)
})
```

##### 39.1.6 使用模板继承

Gin框架默认都是使用单模板，如果需要使用`block template`功能，可以通过`"github.com/gin-contrib/multitemplate"`库实现，具体示例如下：

首先，假设我们项目目录下的templates文件夹下有以下模板文件，其中`home.tmpl`和`index.tmpl`继承了`base.tmpl`：

```bash
templates
├── includes
│   ├── home.tmpl
│   └── index.tmpl
├── layouts
│   └── base.tmpl
└── scripts.tmpl
```

然后我们定义一个`loadTemplates`函数如下：

```go
func loadTemplates(templatesDir string) multitemplate.Renderer {
	r := multitemplate.NewRenderer()
	layouts, err := filepath.Glob(templatesDir + "/layouts/*.tmpl")
	if err != nil {
		panic(err.Error())
	}
	includes, err := filepath.Glob(templatesDir + "/includes/*.tmpl")
	if err != nil {
		panic(err.Error())
	}
	// 为layouts/和includes/目录生成 templates map
	for _, include := range includes {
		layoutCopy := make([]string, len(layouts))
		copy(layoutCopy, layouts)
		files := append(layoutCopy, include)
		r.AddFromFiles(filepath.Base(include), files...)
	}
	return r
}
```

我们在`main`函数中

``` go
func indexFunc(c *gin.Context){
	c.HTML(http.StatusOK, "index.tmpl", nil)
}

func homeFunc(c *gin.Context){
	c.HTML(http.StatusOK, "home.tmpl", nil)
}

func main(){
	r := gin.Default()
	r.HTMLRender = loadTemplates("./templates")
	r.GET("/index", indexFunc)
	r.GET("/home", homeFunc)
	r.Run()
}
```

#### 39.2 获取参数

##### 39.2.1 query

`querystring`指的是URL中`?`后面携带的参数，例如：`/user/search?username=小王子&address=沙河`。 获取请求的querystring参数的方法如下：

```go
func main() {
	//Default返回一个默认的路由引擎
	r := gin.Default()
	r.GET("/user/search", func(c *gin.Context) {
		username := c.DefaultQuery("username", "小王子")
		//username := c.Query("username")
		address := c.Query("address")
		//输出json结果给调用方
		c.JSON(http.StatusOK, gin.H{
			"message":  "ok",
			"username": username,
			"address":  address,
		})
	})
	r.Run()
}
```

##### 39.2.2 form

请求的数据通过form表单来提交，例如向`/user/search`发送一个POST请求，获取请求数据的方式如下：

```go
func main() {
	//Default返回一个默认的路由引擎
	r := gin.Default()
	r.POST("/user/search", func(c *gin.Context) {
		// DefaultPostForm取不到值时会返回指定的默认值
		//username := c.DefaultPostForm("username", "小王子")
		username := c.PostForm("username")
		address := c.PostForm("address")
		//输出json结果给调用方
		c.JSON(http.StatusOK, gin.H{
			"message":  "ok",
			"username": username,
			"address":  address,
		})
	})
	r.Run(":8080")
}
```

##### 39.2.3 path

请求的参数通过URL路径传递，例如：`/user/search/小王子/沙河`。 获取请求URL路径中的参数的方式如下。

```go
func main() {
	//Default返回一个默认的路由引擎
	r := gin.Default()
	r.GET("/user/search/:username/:address", func(c *gin.Context) {
		username := c.Param("username")
		address := c.Param("address")
		//输出json结果给调用方
		c.JSON(http.StatusOK, gin.H{
			"message":  "ok",
			"username": username,
			"address":  address,
		})
	})

	r.Run(":8080")
}
```

##### 39.2.4 参数绑定

为了能够更方便的获取请求相关参数，提高开发效率，我们可以基于请求的`Content-Type`识别请求数据类型并利用反射机制自动提取请求中`QueryString`、`form表单`、`JSON`、`XML`等参数到结构体中。 下面的示例代码演示了`.ShouldBind()`强大的功能，它能够基于请求自动提取`JSON`、`form表单`和`QueryString`类型的数据，并把值绑定到指定的结构体对象。

```go
// Binding from JSON
type Login struct {
	User     string `form:"user" json:"user" binding:"required"`
	Password string `form:"password" json:"password" binding:"required"`
}

func main() {
	router := gin.Default()

	// 绑定JSON的示例 ({"user": "q1mi", "password": "123456"})
	router.POST("/loginJSON", func(c *gin.Context) {
		var login Login

		if err := c.ShouldBind(&login); err == nil {
			fmt.Printf("login info:%#v\n", login)
			c.JSON(http.StatusOK, gin.H{
				"user":     login.User,
				"password": login.Password,
			})
		} else {
			c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
		}
	})

	// 绑定form表单示例 (user=q1mi&password=123456)
	router.POST("/loginForm", func(c *gin.Context) {
		var login Login
		// ShouldBind()会根据请求的Content-Type自行选择绑定器
		if err := c.ShouldBind(&login); err == nil {
			c.JSON(http.StatusOK, gin.H{
				"user":     login.User,
				"password": login.Password,
			})
		} else {
			c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
		}
	})

	// 绑定QueryString示例 (/loginQuery?user=q1mi&password=123456)
	router.GET("/loginForm", func(c *gin.Context) {
		var login Login
		// ShouldBind()会根据请求的Content-Type自行选择绑定器
		if err := c.ShouldBind(&login); err == nil {
			c.JSON(http.StatusOK, gin.H{
				"user":     login.User,
				"password": login.Password,
			})
		} else {
			c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
		}
	})

	// Listen and serve on 0.0.0.0:8080
	router.Run(":8080")
}
```

`ShouldBind`会按照下面的顺序解析请求中的数据完成绑定：

1. 如果是 `GET` 请求，只使用 `Form` 绑定引擎（`query`）。
2. 如果是 `POST` 请求，首先检查 `content-type` 是否为 `JSON` 或 `XML`，然后再使用 `Form`（`form-data`）。

#### 39.3 文件上传

##### 39.3.1 单个文件上传

文件上传前端页面代码：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <title>上传文件示例</title>
</head>
<body>
<form action="/upload" method="post" enctype="multipart/form-data">
    <input type="file" name="f1">
    <input type="submit" value="上传">
</form>
</body>
</html>
```

后端gin框架部分代码：

```go
func main() {
	router := gin.Default()
	// 处理multipart forms提交文件时默认的内存限制是32 MiB
	// 可以通过下面的方式修改
	// router.MaxMultipartMemory = 8 << 20  // 8 MiB
	router.POST("/upload", func(c *gin.Context) {
		// 单个文件
		file, err := c.FormFile("f1")
		if err != nil {
			c.JSON(http.StatusInternalServerError, gin.H{
				"message": err.Error(),
			})
			return
		}

		log.Println(file.Filename)
		dst := fmt.Sprintf("C:/tmp/%s", file.Filename)
		// 上传文件到指定的目录
		c.SaveUploadedFile(file, dst)
		c.JSON(http.StatusOK, gin.H{
			"message": fmt.Sprintf("'%s' uploaded!", file.Filename),
		})
	})
	router.Run()
}
```

#### 

##### 39.3.2 多个文件上传

```go
func main() {
	router := gin.Default()
	// 处理multipart forms提交文件时默认的内存限制是32 MiB
	// 可以通过下面的方式修改
	// router.MaxMultipartMemory = 8 << 20  // 8 MiB
	router.POST("/upload", func(c *gin.Context) {
		// Multipart form
		form, _ := c.MultipartForm()
		files := form.File["file"]

		for index, file := range files {
			log.Println(file.Filename)
			dst := fmt.Sprintf("C:/tmp/%s_%d", file.Filename, index)
			// 上传文件到指定的目录
			c.SaveUploadedFile(file, dst)
		}
		c.JSON(http.StatusOK, gin.H{
			"message": fmt.Sprintf("%d files uploaded!", len(files)),
		})
	})
	router.Run()
```

#### 39.4 重定向

##### 39.4.1 HTTP重定向

HTTP 重定向很容易。 内部、外部重定向均支持。

```go
r.GET("/test", func(c *gin.Context) {
	c.Redirect(http.StatusMovedPermanently, "http://www.sogo.com/")
})
```

##### 39.4.2 路由重定向

路由重定向，使用`HandleContext`：

```go
r.GET("/test", func(c *gin.Context) {
    // 指定重定向的URL
    c.Request.URL.Path = "/test2"
    r.HandleContext(c)
})
r.GET("/test2", func(c *gin.Context) {
    c.JSON(http.StatusOK, gin.H{"hello": "world"})
})
```

#### 39.5 Gin路由

##### 39.5.1 普通路由

```go
r.GET("/index", func(c *gin.Context) {...})
r.GET("/login", func(c *gin.Context) {...})
r.POST("/login", func(c *gin.Context) {...})
```

此外，还有一个可以匹配所有请求方法的`Any`方法如下：

```go
r.Any("/test", func(c *gin.Context) {...})
```

为没有配置处理函数的路由添加处理程序，默认情况下它返回404代码，下面的代码为没有匹配到路由的请求都返回`views/404.html`页面。

```go
r.NoRoute(func(c *gin.Context) {
		c.HTML(http.StatusNotFound, "views/404.html", nil)
	})
```

#### 

##### 39.5.2 路由组

我们可以将拥有共同URL前缀的路由划分为一个路由组。习惯性一对`{}`包裹同组的路由，这只是为了看着清晰，你用不用`{}`包裹功能上没什么区别。

```go
func main() {
	r := gin.Default()
	userGroup := r.Group("/user")
	{
		userGroup.GET("/index", func(c *gin.Context) {...})
		userGroup.GET("/login", func(c *gin.Context) {...})
		userGroup.POST("/login", func(c *gin.Context) {...})

	}
	shopGroup := r.Group("/shop")
	{
		shopGroup.GET("/index", func(c *gin.Context) {...})
		shopGroup.GET("/cart", func(c *gin.Context) {...})
		shopGroup.POST("/checkout", func(c *gin.Context) {...})
	}
	r.Run()
}
```

路由组也是支持嵌套的，例如：

```go
shopGroup := r.Group("/shop")
	{
		shopGroup.GET("/index", func(c *gin.Context) {...})
		shopGroup.GET("/cart", func(c *gin.Context) {...})
		shopGroup.POST("/checkout", func(c *gin.Context) {...})
		// 嵌套路由组
		xx := shopGroup.Group("xx")
		xx.GET("/oo", func(c *gin.Context) {...})
	}
```

通常我们将路由分组用在划分业务逻辑或划分API版本时。

##### 39.5.2 路由原理

Gin框架中的路由使用的是[httprouter](https://github.com/julienschmidt/httprouter)这个库。

其基本原理就是构造一个路由地址的前缀树。

#### 39.6 Gin中间件

Gin框架允许开发者在处理请求的过程中，加入用户自己的钩子（Hook）函数。这个钩子函数就叫中间件，中间件适合处理一些公共的业务逻辑，比如登录认证、权限校验、数据分页、记录日志、耗时统计等。

##### 39.6.1 定义中间件

Gin中的中间件必须是一个`gin.HandlerFunc`类型。例如我们像下面的代码一样定义一个统计请求耗时的中间件。

```go
// StatCost 是一个统计耗时请求耗时的中间件
func StatCost() gin.HandlerFunc {
	return func(c *gin.Context) {
		start := time.Now()
		c.Set("name", "小王子") // 可以通过c.Set在请求上下文中设置值，后续的处理函数能够取到该值
		// 调用该请求的剩余处理程序
		c.Next()
		// 不调用该请求的剩余处理程序
		// c.Abort()
		// 计算耗时
		cost := time.Since(start)
		log.Println(cost)
	}
}
```

##### 39.6.2 注册中间件

在gin框架中，我们可以为每个路由添加任意数量的中间件。

###### 为全局路由注册

```go
func main() {
	// 新建一个没有任何默认中间件的路由
	r := gin.New()
	// 注册一个全局中间件
	r.Use(StatCost())
	
	r.GET("/test", func(c *gin.Context) {
		name := c.MustGet("name").(string) // 从上下文取值
		log.Println(name)
		c.JSON(http.StatusOK, gin.H{
			"message": "Hello world!",
		})
	})
	r.Run()
}
```

###### 为某个路由单独注册

```go
// 给/test2路由单独注册中间件（可注册多个）
	r.GET("/test2", StatCost(), func(c *gin.Context) {
		name := c.MustGet("name").(string) // 从上下文取值
		log.Println(name)
		c.JSON(http.StatusOK, gin.H{
			"message": "Hello world!",
		})
	})
```

###### 为路由组注册中间件

为路由组注册中间件有以下两种写法。

写法1：

```go
shopGroup := r.Group("/shop", StatCost())
{
    shopGroup.GET("/index", func(c *gin.Context) {...})
    ...
}
```

写法2：

```go
shopGroup := r.Group("/shop")
shopGroup.Use(StatCost())
{
    shopGroup.GET("/index", func(c *gin.Context) {...})
    ...
}
```

##### 39.6.3 中间件注意事项

###### gin默认中间件

`gin.Default()`默认使用了`Logger`和`Recovery`中间件，其中：

- `Logger`中间件将日志写入`gin.DefaultWriter`，即使配置了`GIN_MODE=release`。
- `Recovery`中间件会recover任何`panic`。如果有panic的话，会写入500响应码。

如果不想使用上面两个默认的中间件，可以使用`gin.New()`新建一个没有任何默认中间件的路由。

###### gin中间件中使用goroutine

当在中间件或`handler`中启动新的`goroutine`时，**不能使用**原始的上下文（c *gin.Context），必须使用其只读副本（`c.Copy()`）。

#### 39.7 运行多个服务

我们可以在多个端口启动服务，例如：

```go
package main

import (
	"log"
	"net/http"
	"time"

	"github.com/gin-gonic/gin"
	"golang.org/x/sync/errgroup"
)

var (
	g errgroup.Group
)

func router01() http.Handler {
	e := gin.New()
	e.Use(gin.Recovery())
	e.GET("/", func(c *gin.Context) {
		c.JSON(
			http.StatusOK,
			gin.H{
				"code":  http.StatusOK,
				"error": "Welcome server 01",
			},
		)
	})

	return e
}

func router02() http.Handler {
	e := gin.New()
	e.Use(gin.Recovery())
	e.GET("/", func(c *gin.Context) {
		c.JSON(
			http.StatusOK,
			gin.H{
				"code":  http.StatusOK,
				"error": "Welcome server 02",
			},
		)
	})

	return e
}

func main() {
	server01 := &http.Server{
		Addr:         ":8080",
		Handler:      router01(),
		ReadTimeout:  5 * time.Second,
		WriteTimeout: 10 * time.Second,
	}

	server02 := &http.Server{
		Addr:         ":8081",
		Handler:      router02(),
		ReadTimeout:  5 * time.Second,
		WriteTimeout: 10 * time.Second,
	}
   // 借助errgroup.Group或者自行开启两个goroutine分别启动两个服务
	g.Go(func() error {
		return server01.ListenAndServe()
	})

	g.Go(func() error {
		return server02.ListenAndServe()
	})

	if err := g.Wait(); err != nil {
		log.Fatal(err)
	}
}
```

#### 39.8 参数绑定

```go
type UesrInfo {
  Username string `form:"username" json:"username" binding:"required"`
  Password string `form:"password" json:"password" binding:"required"`
}
var u UserInfo
c.ShouldBind(&u) // 可以减少参数一个赋值, 会根据请求头中的Content-Type解析
c.ShouldBindBodyWidth(&u, binding.JSON | binding.XML | binding.Form)
```

#### 39.9 日志库logrus

##### 39.9.1 介绍

Logrus是Go（golang）的结构化logger，与标准库logger完全API兼容。

它有以下特点：

- 完全兼容标准日志库，拥有七种日志级别：`Trace`, `Debug`, `Info`, `Warning`, `Error`, `Fatal`and `Panic`。
- 可扩展的Hook机制，允许使用者通过Hook的方式将日志分发到任意地方，如本地文件系统，logstash，elasticsearch或者mq等，或者通过Hook定义日志内容和格式等
- 可选的日志输出格式，内置了两种日志格式JSONFormater和TextFormatter，还可以自定义日志格式
- Field机制，通过Filed机制进行结构化的日志记录
- 线程安全

##### 39.9.2 安装

```bash
go get github.com/sirupsen/logrus
```

##### 39.9.2 基本示例

```go
package main

import (
  log "github.com/sirupsen/logrus"
)

func main() {
  log.WithFields(log.Fields{
    "animal": "dog",
  }).Info("一条舔狗出现了。")
}
```

##### 39.9.3 进阶示例

```go
package main

import (
  "os"
  "github.com/sirupsen/logrus"
)

// 创建一个新的logger实例。可以创建任意多个。
var log = logrus.New()

func main() {
  // 设置日志输出为os.Stdout
  log.Out = os.Stdout

  // 可以设置像文件等任意`io.Writer`类型作为日志输出
  // file, err := os.OpenFile("logrus.log", os.O_CREATE|os.O_WRONLY|os.O_APPEND, 0666)
  // if err == nil {
  //  log.Out = file
  // } else {
  //  log.Info("Failed to log to file, using default stderr")
  // }

  log.WithFields(logrus.Fields{
    "animal": "dog",
    "size":   10,
  }).Info("一群舔狗出现了。")
}
```

##### 39.9.4 日志级别

Logrus有七个日志级别：`Trace`, `Debug`, `Info`, `Warning`, `Error`, `Fatal`and `Panic`。

```go
log.Trace("Something very low level.")
log.Debug("Useful debugging information.")
log.Info("Something noteworthy happened!")
log.Warn("You should probably take a look at this.")
log.Error("Something failed but I'm not quitting.")
// 记完日志后会调用os.Exit(1) 
log.Fatal("Bye.")
// 记完日志后会调用 panic() 
log.Panic("I'm bailing.")
```

你可以在Logger上设置日志记录级别，然后它只会记录具有该级别或以上级别任何内容的条目：

```go
// 会记录info及以上级别 (warn, error, fatal, panic)
log.SetLevel(log.InfoLevel)
```

如果你的程序支持debug或环境变量模式，设置`log.Level = logrus.DebugLevel`会很有帮助。

##### 39.9.5 字段

Logrus鼓励通过日志字段进行谨慎的结构化日志记录，而不是冗长的、不可解析的错误消息。

例如，区别于使用`log.Fatalf("Failed to send event %s to topic %s with key %d")`，你应该使用如下方式记录更容易发现的内容:

```go
log.WithFields(log.Fields{
  "event": event,
  "topic": topic,
  "key": key,
}).Fatal("Failed to send event")
```

`WithFields`的调用是可选的。

##### 39.9.6 默认字段

通常，将一些字段始终附加到应用程序的全部或部分的日志语句中会很有帮助。例如，你可能希望始终在请求的上下文中记录`request_id`和`user_ip`。

区别于在每一行日志中写上`log.WithFields(log.Fields{"request_id": request_id, "user_ip": user_ip})`，你可以向下面的示例代码一样创建一个`logrus.Entry`去传递这些字段。

```go
requestLogger := log.WithFields(log.Fields{"request_id": request_id, "user_ip": user_ip})
requestLogger.Info("something happened on that request") # will log request_id and user_ip
requestLogger.Warn("something not great happened")
```

##### 39.9.7 日志条目

除了使用`WithField`或`WithFields`添加的字段外，一些字段会自动添加到所有日志记录事中:

- time：记录日志时的时间戳
- msg：记录的日志信息
- level：记录的日志级别

##### 39.9.8 Hooks

你可以添加日志级别的钩子（Hook）。例如，向异常跟踪服务发送`Error`、`Fatal`和`Panic`、信息到StatsD或同时将日志发送到多个位置，例如syslog。

Logrus配有内置钩子。在`init`中添加这些内置钩子或你自定义的钩子：

```go
import (
  log "github.com/sirupsen/logrus"
  "gopkg.in/gemnasium/logrus-airbrake-hook.v2" // the package is named "airbrake"
  logrus_syslog "github.com/sirupsen/logrus/hooks/syslog"
  "log/syslog"
)

func init() {

  // Use the Airbrake hook to report errors that have Error severity or above to
  // an exception tracker. You can create custom hooks, see the Hooks section.
  log.AddHook(airbrake.NewHook(123, "xyz", "production"))

  hook, err := logrus_syslog.NewSyslogHook("udp", "localhost:514", syslog.LOG_INFO, "")
  if err != nil {
    log.Error("Unable to connect to local syslog daemon")
  } else {
    log.AddHook(hook)
  }
}
```

意：Syslog钩子还支持连接到本地syslog（例如. “/dev/log” or “/var/run/syslog” or “/var/run/log”)。有关详细信息，请查看[syslog hook README](https://github.com/sirupsen/logrus/blob/master/hooks/syslog/README.md)。

##### 39.9.9 格式化

logrus内置以下两种日志格式化程序：

```
logrus.TextFormatter` `logrus.JSONFormatter
```

还支持一些第三方的格式化程序，详见项目首页。

##### 39.9.10 记录函数名

如果你希望将调用的函数名添加为字段，请通过以下方式设置：

```go
log.SetReportCaller(true)
```

这会将调用者添加为”method”，如下所示：

```json
{"animal":"penguin","level":"fatal","method":"github.com/sirupsen/arcticcreatures.migrate","msg":"a penguin swims by",
"time":"2014-03-10 19:57:38.562543129 -0400 EDT"}
```

**注意：**，开启这个模式会增加性能开销。

##### 39.9.11 线程安全

默认的logger在并发写的时候是被mutex保护的，比如当同时调用hook和写log时mutex就会被请求，有另外一种情况，文件是以appending mode打开的， 此时的并发操作就是安全的，可以用`logger.SetNoLock()`来关闭它。

##### 39.9.12 gin框架使用logrus

```go
// a gin with logrus demo

var log = logrus.New()

func init() {
	// Log as JSON instead of the default ASCII formatter.
	log.Formatter = &logrus.JSONFormatter{}
	// Output to stdout instead of the default stderr
	// Can be any io.Writer, see below for File example
	f, _ := os.Create("./gin.log")
	log.Out = f
	gin.SetMode(gin.ReleaseMode)
	gin.DefaultWriter = log.Out
	// Only log the warning severity or above.
	log.Level = logrus.InfoLevel
}

func main() {
	// 创建一个默认的路由引擎
	r := gin.Default()
	// GET：请求方式；/hello：请求的路径
	// 当客户端以GET方法请求/hello路径时，会执行后面的匿名函数
	r.GET("/hello", func(c *gin.Context) {
		log.WithFields(logrus.Fields{
			"animal": "walrus",
			"size":   10,
		}).Warn("A group of walrus emerges from the ocean")
		// c.JSON：返回JSON格式的数据
		c.JSON(200, gin.H{
			"message": "Hello world!",
		})
	})
	// 启动HTTP服务，默认在0.0.0.0:8080启动服务
	r.Run()
}
```

##### 39.9.13 404处理

``` go
r := gin.Default()
r.NoRoute(func(c *gin.Context){
  c.HTML(http.StatusOk, '404.html', nil)
})
```

##### 39.9.14 Marshal 和UnMarshal序列化问题

序列化接口类型数据，传入 int类型值，反序列化则是float64类型，可用gob序列化解决

### 40 Context

在 Go http包的Server中，每一个请求在都有一个对应的 goroutine 去处理。请求处理函数通常会启动额外的 goroutine 用来访问后端服务，比如数据库和RPC服务。用来处理一个请求的 goroutine 通常需要访问一些与请求特定的数据，比如终端用户的身份认证信息、验证相关的token、请求的截止时间。 当一个请求被取消或超时时，所有用来处理该请求的 goroutine 都应该迅速退出，然后系统才能释放这些 goroutine 占用的资源。

#### 40.1 定义

Go1.7加入了一个新的标准库`context`，它定义了`Context`类型，专门用来简化 对于处理单个请求的多个 goroutine 之间与请求域的数据、取消信号、截止时间等相关操作，这些操作可能涉及多个 API 调用。

对服务器传入的请求应该创建上下文，而对服务器的传出调用应该接受上下文。它们之间的函数调用链必须传递上下文，或者可以使用`WithCancel`、`WithDeadline`、`WithTimeout`或`WithValue`创建的派生上下文。当一个上下文被取消时，它派生的所有上下文也被取消。

#### 40.2  Context接口

`context.Context`是一个接口，该接口定义了四个需要实现的方法。具体签名如下：

```go
type Context interface {
    Deadline() (deadline time.Time, ok bool)
    Done() <-chan struct{}
    Err() error
    Value(key interface{}) interface{}
}
```

其中：

- `Deadline`方法需要返回当前`Context`被取消的时间，也就是完成工作的截止时间（deadline）；

- `Done`方法需要返回一个`Channel`，这个Channel会在当前工作完成或者上下文被取消之后关闭，多次调用`Done`方法会返回同一个Channel；

- ```
  Err
  ```

  方法会返回当前

  ```
  Context
  ```

  结束的原因，它只会在

  ```
  Done
  ```

  返回的Channel被关闭时才会返回非空的值；

  - 如果当前`Context`被取消就会返回`Canceled`错误；
  - 如果当前`Context`超时就会返回`DeadlineExceeded`错误；

- `Value`方法会从`Context`中返回键对应的值，对于同一个上下文来说，多次调用`Value` 并传入相同的`Key`会返回相同的结果，该方法仅用于传递跨API和进程间跟请求域的数据；

#### 40.3 Background()和TODO()

Go内置两个函数：`Background()`和`TODO()`，这两个函数分别返回一个实现了`Context`接口的`background`和`todo`。我们代码中最开始都是以这两个内置的上下文对象作为最顶层的`partent context`，衍生出更多的子上下文对象。

`Background()`主要用于main函数、初始化以及测试代码中，作为Context这个树结构的最顶层的Context，也就是根Context。

`TODO()`，它目前还不知道具体的使用场景，如果我们不知道该使用什么Context的时候，可以使用这个。

`background`和`todo`本质上都是`emptyCtx`结构体类型，是一个不可取消，没有设置截止时间，没有携带任何值的Context。

#### 40.4 With系列函数

##### 40.4.1 WithCancel

`WithCancel`的函数签名如下：

```go
func WithCancel(parent Context) (ctx Context, cancel CancelFunc)
```

`WithCancel`返回带有新Done通道的父节点的副本。当调用返回的cancel函数或当关闭父上下文的Done通道时，将关闭返回上下文的Done通道，无论先发生什么情况。

取消此上下文将释放与其关联的资源，因此代码应该在此上下文中运行的操作完成后立即调用cancel。

```go
func gen(ctx context.Context) <-chan int {
		dst := make(chan int)
		n := 1
		go func() {
			for {
				select {
				case <-ctx.Done():
					return // return结束该goroutine，防止泄露
				case dst <- n:
					n++
				}
			}
		}()
		return dst
	}
func main() {
	ctx, cancel := context.WithCancel(context.Background())
	defer cancel() // 当我们取完需要的整数后调用cancel

	for n := range gen(ctx) {
		fmt.Println(n)
		if n == 5 {
			break
		}
	}
}
```

上面的示例代码中，`gen`函数在单独的goroutine中生成整数并将它们发送到返回的通道。 gen的调用者在使用生成的整数之后需要取消上下文，以免`gen`启动的内部goroutine发生泄漏。

##### 40.4.2 WithDeadline

`WithDeadline`的函数签名如下：

```go
func WithDeadline(parent Context, deadline time.Time) (Context, CancelFunc)
```

返回父上下文的副本，并将deadline调整为不迟于d。如果父上下文的deadline已经早于d，则WithDeadline(parent, d)在语义上等同于父上下文。当截止日过期时，当调用返回的cancel函数时，或者当父上下文的Done通道关闭时，返回上下文的Done通道将被关闭，以最先发生的情况为准。

取消此上下文将释放与其关联的资源，因此代码应该在此上下文中运行的操作完成后立即调用cancel。

```go
func main() {
	d := time.Now().Add(50 * time.Millisecond)
	ctx, cancel := context.WithDeadline(context.Background(), d)

	// 尽管ctx会过期，但在任何情况下调用它的cancel函数都是很好的实践。
	// 如果不这样做，可能会使上下文及其父类存活的时间超过必要的时间。
	defer cancel()

	select {
	case <-time.After(1 * time.Second):
		fmt.Println("overslept")
	case <-ctx.Done():
		fmt.Println(ctx.Err())
	}
}
```

上面的代码中，定义了一个50毫秒之后过期的deadline，然后我们调用`context.WithDeadline(context.Background(), d)`得到一个上下文（ctx）和一个取消函数（cancel），然后使用一个select让主程序陷入等待：等待1秒后打印`overslept`退出或者等待ctx过期后退出。 因为ctx50秒后就过期，所以`ctx.Done()`会先接收到值，上面的代码会打印ctx.Err()取消原因。

##### 40.4.3 WithTimeout

`WithTimeout`的函数签名如下：

```go
func WithTimeout(parent Context, timeout time.Duration) (Context, CancelFunc)
```

`WithTimeout`返回`WithDeadline(parent, time.Now().Add(timeout))`。

取消此上下文将释放与其相关的资源，因此代码应该在此上下文中运行的操作完成后立即调用cancel，通常用于数据库或者网络连接的超时控制。具体示例如下：

```go
package main

import (
	"context"
	"fmt"
	"sync"

	"time"
)

// context.WithTimeout

var wg sync.WaitGroup

func worker(ctx context.Context) {
LOOP:
	for {
		fmt.Println("db connecting ...")
		time.Sleep(time.Millisecond * 10) // 假设正常连接数据库耗时10毫秒
		select {
		case <-ctx.Done(): // 50毫秒后自动调用
			break LOOP
		default:
		}
	}
	fmt.Println("worker done!")
	wg.Done()
}

func main() {
	// 设置一个50毫秒的超时
	ctx, cancel := context.WithTimeout(context.Background(), time.Millisecond*50)
	wg.Add(1)
	go worker(ctx)
	time.Sleep(time.Second * 5)
	cancel() // 通知子goroutine结束
	wg.Wait()
	fmt.Println("over")
}
```

##### 40.4.4 WithValue

`WithValue`函数能够将请求作用域的数据与 Context 对象建立关系。声明如下：

```go
func WithValue(parent Context, key, val interface{}) Context
```

`WithValue`返回父节点的副本，其中与key关联的值为val。

仅对API和进程间传递请求域的数据使用上下文值，而不是使用它来传递可选参数给函数。

所提供的键必须是可比较的，并且不应该是`string`类型或任何其他内置类型，以避免使用上下文在包之间发生冲突。`WithValue`的用户应该为键定义自己的类型。为了避免在分配给interface{}时进行分配，上下文键通常具有具体类型`struct{}`。或者，导出的上下文关键变量的静态类型应该是指针或接口。

```go
package main

import (
	"context"
	"fmt"
	"sync"

	"time"
)

// context.WithValue

type TraceCode string

var wg sync.WaitGroup

func worker(ctx context.Context) {
	key := TraceCode("TRACE_CODE")
	traceCode, ok := ctx.Value(key).(string) // 在子goroutine中获取trace code
	if !ok {
		fmt.Println("invalid trace code")
	}
LOOP:
	for {
		fmt.Printf("worker, trace code:%s\n", traceCode)
		time.Sleep(time.Millisecond * 10) // 假设正常连接数据库耗时10毫秒
		select {
		case <-ctx.Done(): // 50毫秒后自动调用
			break LOOP
		default:
		}
	}
	fmt.Println("worker done!")
	wg.Done()
}

func main() {
	// 设置一个50毫秒的超时
	ctx, cancel := context.WithTimeout(context.Background(), time.Millisecond*50)
	// 在系统的入口中设置trace code传递给后续启动的goroutine实现日志数据聚合
	ctx = context.WithValue(ctx, TraceCode("TRACE_CODE"), "12512312234")
	wg.Add(1)
	go worker(ctx)
	time.Sleep(time.Second * 5)
	cancel() // 通知子goroutine结束
	wg.Wait()
	fmt.Println("over")
}
```

#### 40.5 使用Context的注意事项

- 推荐以参数的方式显示传递Context
- 以Context作为参数的函数方法，应该把Context作为第一个参数。
- 给一个函数方法传递Context的时候，不要传递nil，如果不知道传递什么，就使用context.TODO()
- Context的Value相关方法应该传递请求域的必要数据，不应该用于传递可选参数
- Context是线程安全的，可以放心的在多个goroutine中传递

#### 40.6 客户端超时取消示例

调用服务端API时如何在客户端实现超时控制？

server端

```go
// context_timeout/server/main.go
package main

import (
	"fmt"
	"math/rand"
	"net/http"

	"time"
)

// server端，随机出现慢响应

func indexHandler(w http.ResponseWriter, r *http.Request) {
	number := rand.Intn(2)
	if number == 0 {
		time.Sleep(time.Second * 10) // 耗时10秒的慢响应
		fmt.Fprintf(w, "slow response")
		return
	}
	fmt.Fprint(w, "quick response")
}

func main() {
	http.HandleFunc("/", indexHandler)
	err := http.ListenAndServe(":8000", nil)
	if err != nil {
		panic(err)
	}
}
```

client端

```go
// context_timeout/client/main.go
package main

import (
	"context"
	"fmt"
	"io/ioutil"
	"net/http"
	"sync"
	"time"
)

// 客户端

type respData struct {
	resp *http.Response
	err  error
}

func doCall(ctx context.Context) {
	transport := http.Transport{
	   // 请求频繁可定义全局的client对象并启用长链接
	   // 请求不频繁使用短链接
	   DisableKeepAlives: true, 	}
	client := http.Client{
		Transport: &transport,
	}

	respChan := make(chan *respData, 1)
	req, err := http.NewRequest("GET", "http://127.0.0.1:8000/", nil)
	if err != nil {
		fmt.Printf("new requestg failed, err:%v\n", err)
		return
	}
	req = req.WithContext(ctx) // 使用带超时的ctx创建一个新的client request
	var wg sync.WaitGroup
	wg.Add(1)
	defer wg.Wait()
	go func() {
		resp, err := client.Do(req)
		fmt.Printf("client.do resp:%v, err:%v\n", resp, err)
		rd := &respData{
			resp: resp,
			err:  err,
		}
		respChan <- rd
		wg.Done()
	}()

	select {
	case <-ctx.Done():
		//transport.CancelRequest(req)
		fmt.Println("call api timeout")
	case result := <-respChan:
		fmt.Println("call server api success")
		if result.err != nil {
			fmt.Printf("call server api failed, err:%v\n", result.err)
			return
		}
		defer result.resp.Body.Close()
		data, _ := ioutil.ReadAll(result.resp.Body)
		fmt.Printf("resp:%v\n", string(data))
	}
}

func main() {
	// 定义一个100毫秒的超时
	ctx, cancel := context.WithTimeout(context.Background(), time.Millisecond*100)
	defer cancel() // 调用cancel释放子goroutine资源
	doCall(ctx)
}
```

### 41  Flag

Go语言内置的`flag`包实现了命令行参数的解析，`flag`包使得开发命令行工具更为简单。

#### 41.1 os.Args

如果你只是简单的想要获取命令行参数，可以像下面的代码示例一样使用`os.Args`来获取命令行参数。

```go
package main

import (
	"fmt"
	"os"
)

//os.Args demo
func main() {
	//os.Args是一个[]string
	if len(os.Args) > 0 {
		for index, arg := range os.Args {
			fmt.Printf("args[%d]=%v\n", index, arg)
		}
	}
}
```

将上面的代码执行`go build -o "args_demo"`编译之后，执行：

```bash
$ ./args_demo a b c d
args[0]=./args_demo
args[1]=a
args[2]=b
args[3]=c
args[4]=d
```

`os.Args`是一个存储命令行参数的字符串切片，它的第一个元素是执行文件的名称。

#### 41.2 flag包基本使用

##### 41.2.1 导入flag包

```go
import flag
```

##### 41.2.2 flag参数类型

flag包支持的命令行参数类型有`bool`、`int`、`int64`、`uint`、`uint64`、`float``float64`、`string`、`duration`。

|   flag参数   |                            有效值                            |
| :----------: | :----------------------------------------------------------: |
|  字符串flag  |                          合法字符串                          |
|   整数flag   |           1234、0664、0x1234等类型，也可以是负数。           |
|  浮点数flag  |                          合法浮点数                          |
| bool类型flag |  1, 0, t, f, T, F, true, false, TRUE, FALSE, True, False。   |
|  时间段flag  | 任何合法的时间段字符串。如”300ms”、”-1.5h”、”2h45m”。 合法的单位有”ns”、”us” /“µs”、”ms”、”s”、”m”、”h”。 |

##### 41.2.3 定义命令行flag参数

有以下两种常用的定义命令行`flag`参数的方法。

* ### flag.Type()

  基本格式如下：

  `flag.Type(flag名, 默认值, 帮助信息)*Type` 例如我们要定义姓名、年龄、婚否三个命令行参数，我们可以按如下方式定义：

  ```go
  name := flag.String("name", "张三", "姓名")
  age := flag.Int("age", 18, "年龄")
  married := flag.Bool("married", false, "婚否")
  delay := flag.Duration("d", 0, "时间间隔")
  ```

  需要注意的是，此时`name`、`age`、`married`、`delay`均为对应类型的指针。

* ### flag.TypeVar()

  基本格式如下： `flag.TypeVar(Type指针, flag名, 默认值, 帮助信息)` 例如我们要定义姓名、年龄、婚否三个命令行参数，我们可以按如下方式定义：

  ```go
  var name string
  var age int
  var married bool
  var delay time.Duration
  flag.StringVar(&name, "name", "张三", "姓名")
  flag.IntVar(&age, "age", 18, "年龄")
  flag.BoolVar(&married, "married", false, "婚否")
  flag.DurationVar(&delay, "d", 0, "时间间隔")
  ```

* ### flag.Parse()

  通过以上两种方法定义好命令行flag参数后，需要通过调用`flag.Parse()`来对命令行参数进行解析。

  支持的命令行参数格式有以下几种：

  - `-flag xxx` （使用空格，一个`-`符号）
  - `--flag xxx` （使用空格，两个`-`符号）
  - `-flag=xxx` （使用等号，一个`-`符号）
  - `--flag=xxx` （使用等号，两个`-`符号）

  其中，布尔类型的参数必须使用等号的方式指定。

  Flag解析在第一个非flag参数（单个”-“不是flag参数）之前停止，或者在终止符”–“之后停止。

* ### flag其它函数

  ```go
  flag.Args()  ////返回命令行参数后的其他参数，以[]string类型
  flag.NArg()  //返回命令行参数后的其他参数个数
  flag.NFlag() //返回使用的命令行参数个数
  ```

* ### 完整示例

  ```go
  func main() {
  	//定义命令行参数方式1
  	var name string
  	var age int
  	var married bool
  	var delay time.Duration
  	flag.StringVar(&name, "name", "张三", "姓名")
  	flag.IntVar(&age, "age", 18, "年龄")
  	flag.BoolVar(&married, "married", false, "婚否")
  	flag.DurationVar(&delay, "d", 0, "延迟的时间间隔")
  
  	//解析命令行参数
  	flag.Parse()
  	fmt.Println(name, age, married, delay)
  	//返回命令行参数后的其他参数
  	fmt.Println(flag.Args())
  	//返回命令行参数后的其他参数个数
  	fmt.Println(flag.NArg())
  	//返回使用的命令行参数个数
  	fmt.Println(flag.NFlag())
  ```

命令行参数使用提示：

```bash
$ ./flag_demo -help
Usage of ./flag_demo:
  -age int
        年龄 (default 18)
  -d duration
        时间间隔
  -married
        婚否
  -name string
        姓名 (default "张三")
```

正常使用命令行flag参数：

```bash
$ ./flag_demo -name 沙河娜扎 --age 28 -married=false -d=1h30m
沙河娜扎 28 false 1h30m0s
[]
0
4
```

使用非flag命令行参数：

```bash
$ ./flag_demo a b c
张三 18 false 0s
[a b c]
3
0
```

### 42 性能调优

https://www.liwenzhou.com/posts/Go/performance_optimisation/

### 43 日志

#### 43.1 ELK

![image-20210109223911023](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20210109223911023.png)

![image-20210109223941993](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20210109223941993.png)

#### 43.2 架构设计

![image-20210109224217718](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20210109224217718.png)

#### 43.3 kafka

![image-20210109225147129](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20210109225147129.png)

##### 43.3.1 log agent 开发

下载安装

``` bash
go get github.com/Shopify/sarama
```

示例 

``` go
package main

import (
	"fmt"

	"github.com/Shopify/sarama"
)

func main() {
	// 1. 生产者配置
	config := sarama.NewConfig()
	// 发送数据leader与follower都需要确认 （ACK）
	config.Producer.RequiredAcks = sarama.WaitForAll
	// 新选出一个Partition
	config.Producer.Partitioner = sarama.NewRandomPartitioner
	// 确认
	config.Producer.Return.Successes = true

	// 2.连接kafka
	client, err := sarama.NewSyncProducer([]string{"127.0.0.1:9092"}, config)

	if err != nil {
		fmt.Println("Producer closed, err: ", err)
		return
	}
	defer client.Close()
	// 3. 封装消息
	msg := &sarama.ProducerMessage{}
	msg.Topic = "web_log"
	msg.Value = sarama.StringEncoder("this is a test log")

	// 4. 发送消息
	pid, offset, err := client.SendMessage(msg)
	if err != nil {
		fmt.Println("Send message failed, err: ", err)
		return
	}
	fmt.Printf("pid: %v offset: %v\n", pid, offset)
}

```

##### 43.3.1	tailf包

下载

```bash
go get github.com/hpcloud/tail
```

示例

```go
package main

import (
	"fmt"
	"time"

	"github.com/hpcloud/tail"
)

func main() {
	filename := `xx.log`
	config := tail.Config{
		ReOpen:    true,
		Follow:    true,
		Location:  &tail.SeekInfo{Offset: 0, Whence: 2},
		MustExist: false,
		Poll:      false,
	}
	tails, err := tail.TailFile(filename, config)
	if err != nil {
		fmt.Printf("tail %s failed, err: %v \n", filename, err)
		return
	}
	var (
		msg *tail.Line
		ok  bool
	)
	for {
		msg, ok = <-tails.Lines
		if !ok {
			fmt.Printf("tail file close reopen, filename: %s\n", tails.Filename)
			time.Sleep(time.Second)
			continue
		}
		fmt.Println("msg:", msg.Text)
	}
}

```

### 44 ETCD

#### 44.1 特点

* 完全复制：集群中的每个节点都可以使用完整的存档
* 高可复用性：etcd可用于避免于硬件的单点故障或网络问题
* 一致性：每次读取都会返回跨多主机的最新写入
* 简单：包括一个定义良好、面向用户的API(gRPC)
* 安全：实现了带有可选的客户端证书身份验证的自动化TLS
* 快速：每秒10000次写入的基准速度
* 可靠：使用Raft算法实现了强一致、高可用的服务存储目录

![image-20210110111922719](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20210110111922719.png)

![image-20210112063540728](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20210112063540728.png)

#### 44.2 架构

![image-20210112063827214](Golang%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%8D%87%E5%A4%A9.assets/image-20210112063827214.png)

#### 44.3 etcd启动

```bash
etcd --data-dir=data.etcd --name n30 \
	--initial-advertise--peer-urls http://10.88.22.111:2380 --listener-peer-urls http://10.88.22.111:2380 \
	--initial-client--peer-urls http://10.88.22.111:2379 --listener-client-urls http://10.88.22.111:2379 \
	--initial-cluster ${CLUSTER} \
	--initial-cluster-state ${CLUSTER_STATE} --initial-cluster-token ${TOKEN}
	
	
	client端调用
	etcdctl --endpoints=http://127.0.0.1:2379 put bbliao "dsb"
	etcdctl --endpoints=http://127.0.0.1:2379 get bbliao
	etcdctl --endpoints=http://127.0.0.1:2379 del bbliao
	
```

#### 44.4 import installer

```bash
go get go.etcd.io/etcd/clientv3
```

