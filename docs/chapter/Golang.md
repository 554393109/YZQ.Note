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

// 方式3（无需var和声明类型，根据初始化值自动推断，仅支持func内使用）
a := 123
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
