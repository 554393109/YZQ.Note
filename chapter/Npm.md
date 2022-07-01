<b style="font-size: 2em">Npm</b>

---

# 国内镜像加速

```bash
// 方式1：修改npm源地址【推荐这个，因为不用安装其他的，同时原汁原味】
> npm config set registry https://registry.npmmirror.com

// 方式2：使用阿里的cnpm命令行工具代替npm命令行
> npm install -g cnpm --registry=https://registry.npmmirror.com

// 设置好之后，查看是否配置成功
>  npm config ls
```

> ; "builtin" config from C:\Users\Administrator\AppData\Roaming\npm\node_modules\npm\npmrc  
>
> prefix = "C:\\Users\\Administrator\\AppData\\Roaming\\npm"  
> ; "user" config from C:\Users\Administrator\.npmrc  
> registry = "https://registry.npmmirror.com/"  
> ; node bin location = C:\PROGRA~1\nodejs\node.exe  
> ; cwd = C:\Users\Administrator  
> ; HOME = C:\Users\Administrator  
> ; Run `npm config ls -l` to show all defaults.

---

# 常用命令

```bash
// 查看基本配置，后面增加参数-l能查看所有配置
npm config ls [-l]

// 查看某个配置
npm config get {配置名}

// 设置某个配置
npm config set {配置名} "{配置值}"

// 安装依赖，没带任何参数会直接安装对应目录下，package.json中声明的依赖包
npm install

// 卸载依赖包
npm uninstall pkg

// 卸载pkg，但是不会从package.json、package-lock.json中删除，仍保留
npm uninstall pkg --no-save

// 查看当前目录下安装的所有安装包及其依赖包
npm ls

// 检查云端的版本信息，对比本地安装包的版本规则，然后更新到对应规则的最新版本
npm update

// 升级全局安装的依赖包
npm update -g

// 清除npm缓存
npm cache clean --force
```

---
