<b style="font-size: 2em">Golang</b>

既然选择使用Golang开发，科学上网是前提

---

# 安装与配置

## 下载并安装Golang程序

> **Go官网**  
> <https://go.dev/>
>
> **Go国内镜像**  
> <https://goproxy.io/>
>
> **七牛**  
> <https://goproxy.cn/>

## 配置环境变量（国内镜像加速）

> **Windows**  
> 1.右键 我的电脑 -> 属性 -> 高级系统设置 -> 环境变量  
> 2.在“用户变量”或“系统变量”中点击”新建“按钮  
> 3.“变量名”分别为“GOROOT”、“GOPATH”、“GOPROXY”、“GO111MODULE”、“GOSUMDB”  
> 4.“变量值”分别为“Golang根目录”、“Golang工作目录”、“on”、“<https://goproxy.cn,direct>”、“sum.golang.google.cn”  
> 5.最后点击“确定”按钮保存设置
>
> **Mac/Linux**  
> // 设置你的 bash 环境变量  
> echo "export GOROOT=Golang根目录" >> ~/.profile && source ~/.profile  
> echo "export GOPATH=Golang工作目录" >> ~/.profile && source ~/.profile  
> echo "export GO111MODULE=on" >> ~/.profile && source ~/.profile  
> echo "export GOPROXY=<https://goproxy.cn,direct>" >> ~/.profile && source ~/.profile  
> echo "export GOSUMDB=sum.golang.google.cn" >> ~/.profile && source ~/.profile  
>
> // 如果终端是 zsh，使用以下命令  
> echo "export GOROOT=Golang根目录"" >> ~/.zshrc && source ~/.zshrc  
> echo "export GOPATH=Golang工作目录" >> ~/.zshrc && source ~/.zshrc  
> echo "export GO111MODULE=on" >> ~/.zshrc && source ~/.zshrc  
> echo "export GOPROXY=<https://goproxy.cn,direct>" >> ~/.zshrc && source ~/.zshrc
> echo "export GOSUMDB=sum.golang.google.cn" >> ~/.zshrc && source ~/.zshrc  

## 配置Visual Studio Code

> **安装扩展插件**  
> 1.Go或Go Nightly（Go Team at Google）  
> 2.Code Runner（Jun Han）
>
> **安装辅助工具（语法提醒等开发必要功能）**  
> 1.“Ctrl+Shift+P”打开“命令面板”，输入“go:Install/Update Tools”，全选并“确定”安装

---

# 语法

## 数据类型

布尔型：bool

有符号整型：  
 int  
 int8（-128~127）  
 int16（-32768~32767）  
 int32（-2147483648~2147483647）  
 int64（-9223372036854775808~9223372036854775807）

无符号整型：  
 uint  
 uint8（0~255）  
 uint16（0~65535）  
 uint32（0~4294967295）  
 uint64（0~18446744073709551615）  

浮点型：float32、float64、complex64、complex128

字符串型：string

其他：byte、rune、uintptr（无符号整型，用于存放一个指针）

## 关键字

<table class="table table-bordered table-striped table-condensed">
  <tr>
    <td>break</td>
    <td>default</td>
    <td>func</td>
    <td>interface</td>
    <td>select</td>
  </tr>
  <tr>
    <td>case</td>
    <td>defer</td>
    <td>go</td>
    <td>map</td>
    <td>struct</td>
  </tr>
  <tr>
    <td>chan</td>
    <td>else</td>
    <td>goto</td>
    <td>package</td>
    <td>switch</td>
  </tr>
  <tr>
    <td>const</td>
    <td>fallthrough</td>
    <td>if</td>
    <td>range</td>
    <td>type</td>
  </tr>
  <tr>
    <td>continue</td>
    <td>for</td>
    <td>import</td>
    <td>return</td>
    <td>var</td>
  </tr>
</table>

通过 **const** 关键字来进行常量的定义。  
通过在函数体外部使用 **var** 关键字来进行全局变量的声明和赋值。  
通过 **type** 关键字来进行结构（**struct**）和接口（**interface**）的声明。  
通过 **func** 关键字来进行函数的声明。  

可见性规则
Go语言中，使用大小写来决定该常量、变量、类型、接口、结构或函数是否可以被外部包所调用。
函数名首字母小写即为private，函数名首字母大写即为public。

```go
func getId()  { } // 私有
func Printf() { } // 公共
```

## 变量声明

```go
// 方式1
var a int       // 不初始化值，默认为：0
var a int = 123   // 初始化值

// 方式2（无需声明类型，根据初始化值自动推断）
var a = 123

// 方式3（无需var和声明类型，根据初始化值自动推断，不支持全局变量）
a := 123

// 方式4（多变量声明）
var a, b = 123, "abc"     // 自动推断类型
var a, b int = 123, 456   // 类型相同的参数

var {
  a int = 123
  b string = "abc"
}

var {
  a = 123
  b = "abc"
}
```

## const常量和iota实现枚举数值

> iota 必须跟随const使用

```go
// 和变量类似，用const代替var声明变量
const a = 123

// 通过const来实现枚举
const (
  BeiJing   = 0
  ShangHai  = 1
  GuangZhou = 2
)

// 通过const和iota来实现枚举值自动累加，首行iota默认为零，后续逐行+1
const (
  BeiJing   = iota // iota=0,
  ShangHai         // iota=1
  GuangZhou        // iota=2
)

// 奇葩用法
const (
  g, h = iota + 1, iota + 2 // iota=0, g=iota+1=1, h=iota+2=2
  i, j                      // iota=1, i=iota+1=2, j=iota+2=3
  k, l                      // iota=2, i=iota+1=3, j=iota+2=4

  m, n = iota * 2, iota * 3 // iota=3, i=iota*2=6, j=iota*3=9
  o, p                      // iota=4, i=iota*2=8, j=iota*3=12
)
```

## 函数

### 传参、返回

```go
func main() {
  ret0 := Method_1("yzq", "18")
  ret1, ret2 := Method_2("yzq", 18)
  ret3, ret4 := Method_3()
  fmt.Println("ret0 =", ret0)
  fmt.Println("ret1 =", ret1, "ret2 =", ret2)
  fmt.Println("ret3 =", ret3, "ret4 =", ret4)
}

// 同类型形参，单一返回值
func Method_1(name, age string) string {
  fmt.Println(age, "岁的", name, "你好")
  return "aaa"
}

// 不同类型形参，多个匿名返回值，类似DotNet Tuple元祖
func Method_2(name string, age int) (string, string) {
  fmt.Println(age, "岁的", name, "你好")
  return "bbb", "ccc"
}

// 无形参，多个命名返回值
func Method_3() (ret3 string, ret4 string) {
  //func Method_3() (ret3, ret4 string) { // 同类型参数合并声明
  ret3 = "ddd"
  ret4 = "eee"
  return
}

// 18 岁的 yzq 你好
// 18 岁的 yzq 你好
// ret0 = aaa
// ret1 = bbb ret2 = ccc
// ret3 = ddd ret4 = eee
```

### 作为参数传递

```go
// 声明一个函数类型
type cb func(int) int

func main() {
  testCallBack(1, callBack)
  testCallBack(2, func(x int) int {
    fmt.Printf("我是回调，x：%d\n", x)
    return x
  })
}

func testCallBack(x int, f cb) {
  f(x)
}

func callBack(x int) int {
  fmt.Printf("我是回调，x：%d\n", x)
  return x
}

// 我是回调，x：1
// 我是回调，x：2
```

### 闭包

```go
// 定义函数getSequence()返回值是匿名函数func()，该匿名函数的返回值是int
func getSequence() func() int {
  i := 0
  return func() int {
    i += 1
    return i
  }
}

func main() {
  /* nextNumber 为一个函数，函数 i 为 0 */
  nextNumber := getSequence()

  /* 调用 nextNumber 函数，i 变量自增 1 并返回 */
  fmt.Println(nextNumber())
  fmt.Println(nextNumber())
  fmt.Println(nextNumber())

  /* 创建新的函数 nextNumber1，并查看结果 */
  nextNumber1 := getSequence()
  fmt.Println(nextNumber1())
  fmt.Println(nextNumber1())
}
s
// 1
// 2
// 3
// 1
// 2
```

> 闭包示例

```go
// 闭包使用方法，函数声明中的返回值(闭包函数)不用写具体的形参名称
func add(x1, x2 int) func(int, int) (int, int, int) {
  i := 0
  return func(x3, x4 int) (int, int, int) {
    i += 1
    return i, x1 + x2, x3 + x4
  }
}

func main() {
  add_func := add(1, 2)
  fmt.Println(add_func(4, 5))
  fmt.Println(add_func(1, 3))
  fmt.Println(add_func(2, 2))
}

//1 3 9
//2 3 4
//3 3 4
```

## import包和init方法

```go
package Lib1

import "fmt"

func init() {
  fmt.Println("执行 Lib1.init()") // init方法在调用方import时执行，参考DotNet构造函数
}

func Method() {
  fmt.Println("执行 Lib1.Method()")
}
```

```go
package Lib2

import "fmt"

func init() {
  fmt.Println("执行 Lib2.init()") // init方法在调用方import时执行，参考DotNet构造函数
}

func Method() {
  fmt.Println("执行 Lib2.Method()")
}
```

```go
package main

// 导入Lib1，并声名为MyLib，后续通过MyLib.Method()进行调用
// import "HelloGo/TestImport/Lib1" MyLib

import (
  "HelloGo/TestImport/Lib1" // 导入Lib1（源码根目录为%GOPATH%，HelloGo为项目文件夹）
  "HelloGo/TestImport/Lib2" // 导入Lib2（源码根目录为%GOPATH%，HelloGo为项目文件夹）

  _ "HelloGo/TestImport/Lib1" // 导入Lib1，仅在import时执行init函数，无法调用包内函数
  . "HelloGo/TestImport/Lib1" // 导入Lib1，合并当前包，后续调用省略包名
  MyLib "HelloGo/TestImport/Lib1" // 导入Lib1，并声名为MyLib，后续通过MyLib.Method()进行调用
)

func main() {
  Lib1.Method() // 调用Lib1.Method()
  Lib2.Method() // 调用Lib2.Method()
}
```

## 指针

```go
func main() {
  a := 1
  sub_1(a)
  fmt.Println("main.a =", a) // main.a == 1

  b := 1
  fmt.Println("main.&b =", &b) // main.&b == 0xc000016098（&b为参数b的地址）
  sub_2(&b)                    // 传递参数b的地址
  fmt.Println("main.b =", b)   // main.b == 3
}

// 参数传值，在子函数内改变，不影响主函数中的值
func sub_1(a int) {
  a = 2
  fmt.Println("sub_1.a =", a) // sub_1.a == 2
}

// 参数传址，在子函数内改变，影响主函数中的值
func sub_2(b *int) { // 此处b为参数b的地址
  *b = 3
  fmt.Println("sub_2.*b =", *b) // sub_2.*b == 3（*b获取参数b的值）
  fmt.Println("sub_2.b =", b)   // sub_2.b == 0xc000016098
}

// 输出：
// sub_1.a = 2
// main.a = 1
// main.&b = 0xc000016098
// sub_2.*b = 3
// sub_2.b = 0xc000016098
// main.b = 3
```

传址方式，交换变量值，示例：

```go
func main() {
  a := 1
  b := 2

  fmt.Println("main.a =", a, "main.b =", b)
  fmt.Println("main.&a =", &a, "main.&b =", &b)
  swap(&a, &b)
  fmt.Println("main.a =", a, "main.b =", b)
  fmt.Println("main.&a =", &a, "main.&b =", &b)
}

// 交换换值
func swap(a *int, b *int) {
  fmt.Println("swap.*a =", *a, "swap.*b =", *b)

  tmp := *a
  *a = *b
  *b = tmp
}

// 输出：
// main.a = 1 main.b = 2
// main.&a = 0xc000016098 main.&b = 0xc0000160b0
// swap.*a = 1 swap.*b = 2
// main.a = 2 main.b = 1
// main.&a = 0xc000016098 main.&b = 0xc0000160b0

```

## defer 延后执行

```go
func main() {
  // defer在调用函数执行完（return后），栈式处理当前函数内定义的每个defer对象（后进先出）
  fmt.Println("main begin")
  defer fun_1()     // 延后函数fun_1进栈
  defer fun_2()     // 延后函数fun_2进栈
  result := fun_3() // 同步执行函数fun_3
  fmt.Println("fun_3 =", result)
  fmt.Println("main end")
}

func fun_1() {
  fmt.Println("fun_1 run")
}

func fun_2() {
  fmt.Println("fun_2 run")
}

func fun_3() bool {
  fmt.Println("fun_3 run")
  defer fun_3_1()  // 延后函数fun_3_1进栈
  return fun_3_2() // 同步执行函数fun_3_2，并返回结果
}

func fun_3_1() {
  fmt.Println("fun_3_1 run")
}

func fun_3_2() bool {
  fmt.Println("fun_3_2 run")
  return true
}

// main begin
// fun_3 run
// fun_3_2 run
// fun_3_1 run
// fun_3 = true
// main end
// fun_2 run
// fun_1 run
```

## 定长数组

```go
func main() {
  const arrLen = 3      // 数组长度只能是const不能是val
  var arr_1 [arrLen]int // 定长数组
  // var arr_2 = [arrLen]int{10, 20, 30}  // 定长数组（初始化部分值）
  //arr_2 := [arrLen + 1]int{10, 20, 30} // 定长数组（初始化部分值）
  arr_2 := [...]int{10, 20, 30, 0} // 定长数组（初始化数组长度全部值，可用...代替长度值，初始化长度为数组实际长度）

  fmt.Printf("arr_1 Type:%T\n", arr_1) // 类型为长度是3的int数组
  fmt.Printf("arr_2 Type:%T\n", arr_2) // 类型为长度是4的int数组（长度不同视为不同类型，函数传参区分长度）
  fmt.Println("-------------")

  for i := 0; i < arrLen; i++ {
    fmt.Printf("arr_1[%v] = %v\n", i, arr_1[i])
  }
  fmt.Println("-------------")

  for i := 0; i < len(arr_2); i++ { // 循环方式一
    fmt.Printf("arr_2[%v] = %v\n", i, arr_2[i])
  }
  fmt.Println("-------------")

  for index, item := range arr_2 { // 循环方式二range（index：下标，item：项）
    fmt.Printf("arr_2[%v] = %v\n", index, item)
  }
  fmt.Println("-------------")

  // Foreach(arr_1) // 此传值会报错，[3]int和[4]int为不同类型
  Foreach(arr_2)
}

// 定长数组为传值（形参需指定数组长度），在子函数内改变，不影响主函数中的值
func Foreach(arr [4]int) {
  for _, item := range arr { // forr
    fmt.Println(item)
  }
}

// arr_1 Type:[3]int
// arr_2 Type:[4]int
// -------------
// arr_1[0] = 0
// arr_1[1] = 0
// arr_1[2] = 0
// -------------
// arr_2[0] = 10
// arr_2[1] = 20
// arr_2[2] = 30
// arr_2[3] = 0
// -------------
// arr_2[0] = 10
// arr_2[1] = 20
// arr_2[2] = 30
// arr_2[3] = 0
// -------------
// 10
// 20
// 30
// 0
```

## slice（切片、动态数组）

```go
func main() {
  // make(切片类型, 切片初始化长度, 切片容量)
  arr_1 := make([]int, 3, 6)    // 定义方式一：创建一个整型切片，其初始化长度为3，容量为6
  arr_2 := make([]int, 4)       // 定义方式二：创建一个整型切片，其初始化长度为4。若不传入容量的大小，则容量和初始化长度相同
  arr_3 := []int{1, 2, 3, 4, 5} // 定义方式三：创建一个整型切片，长度和容量为初始化值的数量5

  fmt.Printf("arr_1 Len:%v, Type:%T\n", len(arr_1), arr_1)
  fmt.Printf("arr_2 Len:%v, Type:%T\n", len(arr_2), arr_2)
  fmt.Printf("arr_3 Len:%v, Type:%T\n", len(arr_3), arr_3)

  Foreach(arr_1)
  fmt.Println("-------------")

  Foreach(arr_2)
  fmt.Println("-------------")

  Foreach(arr_3)
}

// 切片slice为传址（形参无需指定数组长度），在子函数内改变，影响主函数中的值
func Foreach(arr []int) {
  for _, item := range arr { // forr
    fmt.Println(item)
  }
}

// arr_1 Len:3, Type:[]int
// arr_2 Len:4, Type:[]int
// arr_3 Len:5, Type:[]int
// 0
// 0
// 0
// -------------
// 0
// 0
// 0
// 0
// -------------
// 1
// 2
// 3
// 4
// 5
```

## map 集合

```go
// 声明变量，默认 map 是 nil
// var map_variable map[key_type]value_type

// 使用 make 函数
// map_variable := make(map[key_type]value_type)

// 使用 delete 函数
// delete(map, key)

func main() {
  map_1 := Mode_1()
  fmt.Println(map_1)
  fmt.Println("----------------------------------")
  map_2 := Mode_2()
  fmt.Println(map_2)
  fmt.Println("----------------------------------")
  map_3 := Mode_3()
  fmt.Println(map_3)
  fmt.Println("----------------------------------")
  for k, v := range map_3 { // 遍历map
    fmt.Println("Key =", k, "Value =", v)
  }
  fmt.Println("----------------------------------")

  exists_two := map_1["two"]   // 从map_1获取two的值
  exists_five := map_1["five"] // 从map_1获取five的值
  fmt.Println("map_1 exists 'two'：", exists_two)
  fmt.Println("map_1 exists 'five'：", exists_five)

  delete(map_1, "two") // 删除two的值
  exists_two = map_1["two"]
  fmt.Println("map_1 exists 'two'：", exists_two)
}

// 创建方式一
func Mode_1() map[string]string {
  var map_1 map[string]string // 声明
  if map_1 == nil {           // 判断为nil
    fmt.Println("Type_1.map_1 is nil")
    map_1 = make(map[string]string, 3) // 创建初始长度为5的map
    map_1["one"] = "Golang"            // 赋值
    map_1["two"] = "C#"                // 赋值
    map_1["three"] = "javascript"      // 赋值
    map_1["ten"] = "java"              // 赋值（超出容量会动态增加长度）
  }

  fmt.Printf("map_1 长度：%v\n", len(map_1))
  return map_1
}

// 创建方式二
func Mode_2() map[int]string {
  map_2 := make(map[int]string) // 通过make声明并创建初始长度为0的map
  map_2[1] = "Golang"
  map_2[2] = "C#"
  map_2[3] = "javascript"
  map_2[10] = "java"

  fmt.Printf("map_2 长度：%v\n", len(map_2))
  return map_2
}

// 声明和创建方式二
func Mode_3() map[int]string {
  map_3 := map[int]string{
    1:  "Golang",
    2:  "C#",
    3:  "javascript",
    10: "java",
  }

  fmt.Printf("map_3 长度：%v\n", len(map_3))
  return map_3
}

// Type_1.map_1 is nil
// map_1 长度：4
// map[one:Golang ten:java three:javascript two:C#]
// ----------------------------------
// map_2 长度：4
// map[1:Golang 2:C# 3:javascript 10:java]
// ----------------------------------
// map_3 长度：4
// map[1:Golang 2:C# 3:javascript 10:java]
// ----------------------------------
// Key = 1 Value = Golang
// Key = 2 Value = C#
// Key = 3 Value = javascript
// Key = 10 Value = java
// ----------------------------------
// map_1 exists 'two'： C#
// map_1 exists 'five'： 
// map_1 exists 'two'： 
```

## struct 结构体

```go
// struct结构体作参数时是传值
// 定义结构体（定义的结构体如果只在当前包内使用，结构体的属性不用区分大小写。如果想要被其他的包引用，那么结构体的属性的首字母需要大写。结构体小写开头的属性只能包内调用）
type People struct {
  Name     string  // 大写开头为public（当要将结构体对象转换为 JSON 时，对象中的属性首字母必须是大写，才能正常转换为 JSON）
  age      int     // 小写开头为private（JSON序列化时忽略private字段）
  Weight   float32 `json:"-"`    // [`json:"-"`]标记输出json时忽略该字段
  Birthday string  `json:"bday"` // [`json:"bday"`]标记输出的json名字为bday
}

func main() {
  yzq := People{
    Name:     "尹自强",
    age:      18,
    Weight:   130.5,
    Birthday: "2022-01-01",
  }

  zhangsan := People{"张三", 19, 150.8, "1999-12-31"} // 按结构体定义顺序赋值

  fmt.Println(yzq)
  fmt.Println(zhangsan)
  rename(yzq)
  fmt.Println(yzq)
  rename_2(&yzq)
  fmt.Println(yzq)

  if result, err := json.Marshal(yzq); err == nil {
    fmt.Println("JSON =", string(result))
  }
}

// 传值
func rename(people People) {
  people.Name = "今晚出嚟威"
}

// 传址
func rename_2(people *People) {
  people.Name = "今晚出嚟威"
}

// {尹自强 18 130.5 2022-01-01}
// {张三 19 150.8 1999-12-31}
// {尹自强 18 130.5 2022-01-01}
// {今晚出嚟威 18 130.5 2022-01-01}
// JSON = {"Name":"今晚出嚟威","bday":"2022-01-01"}
```

## OOP 面向对象

### 封装

```go
// 为结构体绑定方法
// func (variable_name variable_type) func_name() [return_type]{
//    /* 函数体*/
// }

// people类首字母小写，为private私有类
type people struct {
  Name     string
  age      uint8
  Weight   float32 `json:"-"`    // [`json:"-"`]标记输出json时忽略该字段
  Birthday string  `json:"bday"` // [`json:"bday"`]标记输出的json名字为bday
}

// 首字母大写，定义类的public公有方法
func (_people people) Show() {
  fmt.Printf("姓名：%v，年龄：%v，体重：%v\n", _people.Name, _people.age, _people.Weight)
}

// struct类型作参数时是传值，所以在方法内修改值，在外部主函数中不生效
func (_people people) rename_1(new_name string) {
  _people.Name = new_name // 此处编译器会有提示修改值无效
}

// 通过指针传址，在方法内修改值，在外部主函数中有效
func (_people *people) rename_2(new_name string) {
  _people.Name = new_name
}

func (_people *people) getname() string {
  return _people.Name
}

func main() {
  yzq := people{
    Name:     "尹自强",
    age:      18,
    Weight:   130.5,
    Birthday: "2022-01-01",
  }

  yzq.Show()
  yzq.rename_1("今晚出嚟威1")
  yzq.Show()
  yzq.rename_2("今晚出嚟威2")
  yzq.Show()

  name := yzq.getname()
  fmt.Println(name)

  if result, err := json.Marshal(yzq); err == nil {
    fmt.Println("JSON =", string(result))
  }
}

// 姓名：尹自强，年龄：18，体重：130.5
// 姓名：尹自强，年龄：18，体重：130.5
// 姓名：今晚出嚟威2，年龄：18，体重：130.5
// 今晚出嚟威2
// JSON = {"Name":"今晚出嚟威2","bday":"2022-01-01"}
```

### 继承

```go
// Golang中继承类似于组合形式

// 定义父类Human
type Human struct {
  Name string
  Sex  uint8
}

// 父类方法Eat
func (_human *Human) Eat() {
  fmt.Println("Human Eat")
}

// 父类方法Talk
func (_human *Human) Talk() {
  fmt.Println("Human Talk")
}

// 定义子类
type Superman struct {
  Human // ★继承Human类
  Level uint
}

// 重写父类Eat方法
func (_superman *Superman) Eat() {
  fmt.Println("Superman Eat")
}

// 子类自有方法Fly
func (_superman *Superman) Fly() {
  fmt.Println("Superman Fly")
}

func main() {
  // 初始化方式一：需要通过先赋值父类再赋值子类，多层继承要遭罪
  // yzq := Superman{Human{Name: "尹自强", Sex: 1}, 99}

  // 初始化方式二：先声明子类，然后通过点号逐个赋值
  //var yzq Superman
  var yzq = new(Superman)
  yzq.Name = "尹自强"
  yzq.Sex = 1
  yzq.Level = 99

  yzq.Eat()  // Superman.Eat()
  yzq.Talk() // Human.Talk()
  yzq.Fly()  // Superman.Fly()

  if result, err := json.Marshal(yzq); err == nil {
    fmt.Println("Superman =", string(result))
  }
}

// Superman Eat
// Human Talk
// Superman Fly
// Superman = {"Name":"尹自强","Sex":1,"Level":99}
```

### 多态

```go
// interface 本质是一个指针
// 定义接口
// type interface_name interface {
//   method_name1 [return_type]
//   method_name2 [return_type]
//   // ...
//   method_nameX [return_type]
// }

// 定义动物接口IAnimal
type IAnimal interface {
  Sleep()          // 定义接口方法Sleep()
  GetName() string // 定义接口方法GetName()获取名称
  GetKind() string // 定义接口方法GetKind()获取种类
}

// -----------------------------------------------------------------

// 定义猫类（必须实现接口全部方法）
type Cat struct {
  Name string
}

// 实现接口方法Sleep()
func (_animal *Cat) Sleep() {
  fmt.Printf("%v Sleep\r", _animal.Name)
}

// 实现接口方法GetName()
func (_animal *Cat) GetName() string {
  return _animal.Name
}

// 实现接口方法GetKind()
func (_animal *Cat) GetKind() string {
  return fmt.Sprintf("Animal Kind %T\r", _animal)
}

// -----------------------------------------------------------------

// 定义老鼠类（必须实现接口全部方法）
type Mouse struct {
  Name string
}

// 实现接口方法Sleep()
func (_animal *Mouse) Sleep() {
  fmt.Printf("%v Sleep\r", _animal.Name)
}

// 实现接口方法GetName()
func (_animal *Mouse) GetName() string {
  return _animal.Name
}

// 实现接口方法GetKind()
func (_animal *Mouse) GetKind() string {
  return fmt.Sprintf("Animal Kind %T\r", _animal)
}

// -----------------------------------------------------------------

// 接口作为参数传递
func ShowAnimal(_animal IAnimal) {
  _animal.Sleep()
  fmt.Println("名称：", _animal.GetName())
  fmt.Println(_animal.GetKind())
}

func main() {
  cat := Cat{Name: "汤姆"}
  ShowAnimal(&cat)

  fmt.Println("-------------------------")

  var mouse = new(Mouse) // 通过new创建的对象为指针
  mouse.Name = "杰瑞"
  ShowAnimal(mouse) // 所以传入该方法时，不需要加前缀&
}

// 汤姆 Sleep
// 名称： 汤姆
// Animal Kind *main.Cat
// -------------------------
// 杰瑞 Sleep
// 名称： 杰瑞
// Animal Kind *main.Mouse
```

> 组合接口

```go
// 定义读接口
type reader interface {
  read() string
}

// 定义写接口
type writer interface {
  write() string
}

// 定义读写接口
type reader_writer interface {
  reader
  writer
}

// 定义实现类（必须实现接口全部方法）
type mouse struct{}

// 实现读接口
func (m mouse) read() string {
  return "mouse reading..."
}

// 实现写接口
func (m *mouse) write() string {
  return "mouse writing..."
}

func main() {
  var rw = new(mouse)

  fmt.Println(rw.read())
  fmt.Println(rw.write())
}

// mouse reading...
// mouse writing...
```

---

# 常用命令

```text
// 查看Golang版本
> go version

// 查看环境配置
> go env

// GO111MODULE=on 以后，下载的模块内容会缓存在 $GOPATH/pkg/mod 目录中。使用以下命令可清空缓存：
> go clean --modcache

---

// xxx
> xxx
```
