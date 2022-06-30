<b style="font-size: 2em">Npm</b>

---

# 国内镜像加速

```text
// 1.使用阿里的cnpm命令行工具代替npm命令行
> npm install -g cnpm --registry=https://registry.npmmirror.com

// 2.修改npm源地址（个人非常推荐这个，因为不用安装其他的，同时原汁原味）
> npm config set registry https://registry.npmmirror.com

// 3.设置好之后，查看是否配置成功
>  npm config list

; cli configs
metrics-registry = "https://registry.npmmirror.com/"
scope = ""
user-agent = "npm/6.14.4 node/v13.14.0 win32 x64"

; userconfig C:\Users\Administrator\.npmrc
registry = "https://registry.npmmirror.com/"

; builtin config undefined
prefix = "C:\\Users\\Administrator\\AppData\\Roaming\\npm"

; node bin location = C:\Program Files\nodejs\node.exe
; cwd = D:\wenhsing
; HOME = C:\Users\Administrator
; "npm config ls -l" to show all defaults.
```

---

# 常用命令

```text
// 
```

---
