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

## 配置环境变量

> **Windows**  
> 1.右键 我的电脑 -> 属性 -> 高级系统设置 -> 环境变量  
> 2.在“用户变量”或“系统变量”中点击”新建“按钮  
> 3.“变量名”分别为“GOROOT”、“GOPATH”、“GOPROXY”、“GO111MODULE”、“GOSUMDB”  
> 4.“变量值”分别为“Golang根目录”、“Golang工作目录”、“on”、“<https://goproxy.cn,direct>”、“sum.golang.google.cn”  
> 5.最后点击“确定”按钮保存设置
>
> **Mac/Linux**  
> // 设置你的 bash 环境变量  
> echo "export GO111MODULE=on" >> ~/.profile && source ~/.profile  
> echo "export GOPROXY=<https://goproxy.cn,direct>" >> ~/.profile && source ~/.profile  
> // 如果终端是 zsh，使用以下命令  
> echo "export GO111MODULE=on" >> ~/.zshrc && source ~/.zshrc  
> echo "export GOPROXY=<https://goproxy.cn,direct>" >> ~/.zshrc && source ~/.zshrc

## 配置Visual Studio Code

> **安装扩展插件**  
> 1.Go或Go Nightly（Go Team at Google）  
> 2.Code Runner（Jun Han）
>
> **安装辅助工具（语法提醒等开发必要功能）**  
> 1.“Ctrl+Shift+P”打开“命令面板”，输入“go:Install/Update Tools”，全选并“确定”安装

---

# 语法

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

## const常量和iota

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
  //func Method_3() (ret3, ret4 string) {	// 同类型参数合并声明
  ret3 = "ddd"
  ret4 = "eee"
  return
}
```

## import和init方法

```go

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
