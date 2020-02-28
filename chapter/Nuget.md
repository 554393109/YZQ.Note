<b style="font-size: 2em">Nuget</b>

---

# 私有源服务器搭建

## 创建ASP.NET项目

在Visual Studio中，选择“文件”>“新建”>“项目”，搜索“ASP.NET”，选择适用于 C# 的“ASP.NET Web 应用程序(.NET Framework)”模板，然后将“Framework”设置为“.NET Framework 4.6”或以上。

## 为项目引入NuGet.Server包

在“包管理器 UI”中，选择“浏览器”选项卡，然后搜索并安装【NuGet.Server】包的最新版本。（也可以使用Install-Package NuGet.Server从包管理器控制台安装。）如果出现提示，请接受此许可条款。

安装NuGet.Server会将空Web 应用程序转换成包源。此操作会安装各种其他包，在应用程序中创建Packages文件夹，并修改web.config以包括其他设置

> **重要**  
> 在NuGet.Server包完成对该文件的修改后，仔细检查web.config。NuGet.Server可能不会覆盖现有元素，而会创建重复元素。稍后尝试运行该项目时，这些重复项会导致“内部服务器错误”。 例如，如果web.config在安装NuGet.Server之前包含&lt;compilation debug="true" targetFramework="4.6.1" /&gt;，则该包不会覆盖它，而是会插入另一个 &lt;compilation debug="true" targetFramework="4.6" /&gt;。在这种情况下，请删除具有较旧框架版本的元素。

## 配置包文件夹

对于NuGet.Server 1.5和更高版本，可通过web.config中的【appSetting/packagesPath】节点更具体地配置包文件夹：

```xml
<appSettings>
    <add key="packagesPath" value="C:\xx\MyPackages" />
</appSettings>
```

packagesPath 可以是绝对或虚拟路径。省略packagesPath或将其留空时，包文件夹是默认的【~/Packages】。

## 部署至IIS中

首次访问该站点时，NuGet.Server会重新构建Packages文件夹，以包含每个包的文件夹。这符合NuGet 3.3中引入的用于提高性能的本地存储布局。添加更多包时，请继续遵照此结构。若出现错误，请参考上一步。

## 为Visual Studio添加Nuget源

在Visual Studio中，选择“工具”>“选项”>“NuGet 包管理器”>程序包源”，添加包源，将URL设为http://{domain}/nuget

## 以外部方式向源添加包

NuGet.Server站点运行后，就可以使用nuget push命令添加包，前提是在web.config中设置了API密钥值。安装NuGet.Server包后，web.config包含一个空【appSetting/apiKey】值：

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

省略apiKey或将其留空时，会禁用向源推送包的功能。要启用此功能，请设置apiKey的值（理想情况下为强密码），并添加值为true名为【appSettings/requireApiKey】的密钥：

```xml
<appSettings>
    <add key="requireApiKey" value="true" />
    <add key="apiKey" value="xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" />
</appSettings>
```

## 从源中删除包

使用NuGet.Server时，nuget delete命令会从存储库中删除一个包，但前提是包含API密钥和注释。如果想要改变行为以从列表中删除包（将其保留为可用于包还原），请将web.config中的enableDelisting键更改为true。

---

# nuspec文件解析

```xml
<?xml version="1.0" encoding="utf-8"?>
<package>
  <metadata>
    <id>$id$</id>
    <version>1.0.0.200227</version>
    <title>UnifiedPay.SDK</title>
    <authors>尹自强</authors>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <license type="expression">MIT</license>
    <projectUrl>https://github.com/554393109/UnifiedPaySDK/</projectUrl>
    <iconUrl>https://qrpay.pos.cn/favicon.png</iconUrl>
    <icon>static\icon.png</icon>
    <description>描述</description>
    <releaseNotes>此版本包中所作更改的说明</releaseNotes>
    <copyright>Copyright 2020</copyright>
    <tags>聚合支付, SDK, UnifiedPay, API, .Net, C#</tags>
    <dependencies>
      <group>
        <dependency id="System.Net" version="4.0.0" />
        <dependency id="System.Net.Http" version="4.0.0" />
        <dependency id="Newtonsoft.Json" version="10.0.0" />
      </group>
    </dependencies>
  </metadata>
  <files>
    <file src="icon.png" target="static\icon.png" />
  </files>
</package>
```
---

# 常用命令

```text
// 创建nuspec文件
> nuget spec [csproj项目文件路径]
> nuget spec -AssemblyPath [dll程序集路径]

// 打包
> nuget pack [csproj项目文件路径] -Prop Configuration=Release

// 发布包到库
> nuget push -Source [nuget库的地址] -ApiKey [nuget库秘钥] [待发布的nuget包nupkg文件路径]
> dotnet nuget push [待发布的nuget包nupkg文件路径] -k [nuget库秘钥] -s [nuget库的地址]

// 查看本地nuget包源
> nuget sources list

// 查看特定库中包含的包
> nuget list -Source [nuget库名]

// 删除特定nuget库的包
> nuget delete [nuget库名] 1.0.0 -Source [包名] -ApiKey [nuget库秘钥]

// 清理本地nuget缓存
> dotnet nuget  locals all --clear
```

---

# 相关资源

> 官网  
> <https://www.nuget.org/>  
> <https://docs.microsoft.com/zh-cn/nuget/>
>
> 创建包  
> <https://docs.microsoft.com/zh-cn/nuget/create-packages/creating-a-package>
>
> NuGet CLI  
> <https://docs.microsoft.com/zh-cn/nuget/reference/nuget-exe-cli-reference>
>
> nuspec文件  
> <https://docs.microsoft.com/zh-cn/nuget/reference/nuspec>
>
> 支持多个.NET版本  
> <https://docs.microsoft.com/zh-cn/nuget/create-packages/supporting-multiple-target-frameworks>
>
> NuGet 常见问题  
> <https://docs.microsoft.com/zh-cn/nuget/resources/nuget-faq>
