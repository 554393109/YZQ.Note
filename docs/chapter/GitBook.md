<b style="font-size: 2em">GitBook</b>

---

# 常用插件

| 插件名             | 功能           |
|:---------------------------------|:---------------------------|
|[search-pro][01]         |支持中文搜索        |
|[anchor-navigation-ex][02]    |页内标题锚点&跳转顶部    |
|[splitter][03]          |左侧菜单宽度拖拽      |
|[github][04]           |github右上图标跳转     |
|[sitemap][05]           |生成站点地图        |
|[tbfed-pagefooter][06]      |页脚显示版权和修订时间   |
|[alerts][07]           |美化区块消息        |
|[donate][08]           |打赏            |
|[copy-code-button][09]      |代码栏复制按钮       |
|[advanced-emoji][10]       |Emoji表情          |
|[baidu-tongji][11]        |百度统计          |
|[expandable-chapters][12]     |左侧菜单一级节点折叠    |

[01]: https://plugins.gitbook.com/plugin/search-pro
[02]: https://plugins.gitbook.com/plugin/anchor-navigation-ex
[03]: https://plugins.gitbook.com/plugin/splitter
[04]: https://plugins.gitbook.com/plugin/github
[05]: https://plugins.gitbook.com/plugin/sitemap
[06]: https://plugins.gitbook.com/plugin/tbfed-pagefooter
[07]: https://plugins.gitbook.com/plugin/alerts
[08]: https://plugins.gitbook.com/plugin/donate
[09]: https://plugins.gitbook.com/plugin/copy-code-button
[10]: https://plugins.gitbook.com/plugin/advanced-emoji
[11]: https://plugins.gitbook.com/plugin/baidu-tongji
[12]: https://plugins.gitbook.com/plugin/expandable-chapters

---

# 常见问题
**生成静态网页错误**
> 执行build命令时，Error: ENOENT: no such file or directory  
> 解决方案：cd C:\Users\{Administrator}\.gitbook\versions\3.2.3\lib\output\website\  
> 修改copyPluginAssets.js文件，fs.copyDir的参数，第112行【confirm: true】->【confirm: false】  

---

# 常用命令
```text
// 列出gitbook所有的命令
> gitbook help

// 列出gitbook-cli所有的命令
> gitbook --help

// 查看GitBook版本
> gitbook version

// 列出本地所有的gitbook版本
> gitbook ls

// 列出远程可用的gitbook版本
> gitbook ls-remote

// 更新到gitbook的最新版本
> gitbook update

// 卸载指定版本的gitbook
> gitbook uninstall 3.2.3

// 安装gitbook插件
> gitbook install

// 生成静态网页
> gitbook build ./ ./docs --debug

// 导出PDF、EPUB、MOBI
> gitbook pdf ./ ./{file_name}.pdf
> gitbook epub ./ ./{file_name}.epub
> gitbook mobi ./ ./{file_name}.mobi

```