<b style="font-size: 2em">GitBook</b>

---

# 项目结构

```text
.
├── book.json
├── README.md
├── SUMMARY.md
├── chapter-1/
|   ├── README.md
|   └── something.md
└── chapter-2/
    ├── README.md
    └── something.md
```

## 静态文件和图片
静态文件是在SUMMARY.md中未列出的文件。除非被忽略，否则所有静态文件都将复制到输出路径。

## 忽略文件和文件夹
GitBook将读取【.gitignore】、【.bookignore】和【.ignore】文件，以获取要过滤的文件和文件夹。这些文件中的格式遵循.gitignore的规则：
```text
# 通过井号注释
 
# 忽略test.md文件
test.md
 
# 忽略bin目录下全部文件
bin/*
```

**GitBookt特殊文件**
| 文件      | 功能              |
| :---      | :-------------------------------|
|book.json    |配置               |
|README.md    |前言或简介            |
|SUMMARY.md    |目录               |
|GLOSSARY.md   |词汇/注释术语列表         |
|LANGS.md   |多语言目录              |

## book.json
GitBook允许您使用灵活的配置自定义您的电子书。

这些选项在book.json文件中指定。对于不熟悉JSON语法的作者，您可以使用JSONlint等工具验证语法。

| 参数      | 功能                        |
| :---      | :---------------------------------------------------|
|root       |包含所有图书文件的根文件夹的路径，除了book.json    |
|structure     |指定自述文件，摘要，词汇表等的路径          |
|title       |您的书名，默认值是从README中提取出来的        |
|description    |您的书籍的描述，默认值是从README中提取出来的     |
|author      |作者名                        |
|isbn       |国际标准书号ISBN                   |
|language     |本书的语言类型     |
|direction    |文本阅读顺序。可以是 rtl （从右向左）或 ltr （从左向右），默认值依赖于 language 的值  |
|gitbook     |应该使用的GitBook版本。使用[SemVer](https://semver.org/)规范，并接受类似于【>=3.0.0】的条件  |
|links      |在左侧导航栏添加链接信息                |
|pdf       |可以使用book.json中的一组选项来定制PDF输出       |

**gitbook**  
应该使用的GitBook版本。使用[SemVer](https://semver.org/)规范，并接受类似于【>=3.0.0】的条件
```json
"gitbook" : "3.2.3",
"gitbook" : ">=3.0.0"
```

**language**  
Gitbook使用的语言, 版本2.6.4中可选的语言如下：
```text
en, ar, bn, cs, de, en, es, fa, fi, fr, he, it, ja, ko, no, pl, pt, ro, ru, sv, uk, vi, zh-hans, zh-tw
```

**links**  
在左侧导航栏添加链接信息
```json
{
    "links": {
        "sidebar": {
            "作者GitHub": "https://github.com/554393109"
        }
    }
}
```

**root**  
包含所有图书文件的根文件夹的路径， book.json 文件除外。
```json
{
    "root" : "./docs",
}
```

**structure**  
指定Readme、Summary、Glossary和Languages对应的文件名（而不是使用默认名称，如README.md）这些文件必须在项目的根目录下（或root的根目录，如果你在 book.json中配置了root属性）。不接受的路径，如：dir / MY_README.md。。

| 参数        | 描述                 |
| :---        | :-------------------------------------|
|structure.readme   |Readme文件名（默认值是README.md）    |
|structure.summary   |Summary文件名（默认值是SUMMARY.md）  |
|structure.glossary  |Glossary文件名（默认值是GLOSSARY.md）  |
|structure.languages  |Languages文件名（默认值是LANGS.md）  |

**pdf**  
可以使用book.json中的一组选项来定制PDF输出

| 参数        | 功能                 |
| :---        | :-------------------------------------|
|pdf.pageNumbers   |将页码添加到每个页面的底部（默认为true） |
|pdf.fontSize     |基本字体大小（默认是12）        |
|pdf.fontFamily    |基本字体样式（默认是Arial）       |
|pdf.paperSize    |页面尺寸，选项有：'a0','a1','a2','a3','a4','a5','a6','b0','b1','b2','b3','b4','b5','b6','legal','letter'（默认值是a4）  |
|pdf.margin.top    |上边界（默认值是56）          |
|pdf.margin.bottom  |下边界（默认值是56）           |
|pdf.margin.right   |右边界（默认值是62）          |
|pdf.margin.left   |左边界（默认值是 62）          |

## README.md
此文件是简单的电子书介绍，可以把您所制作的电子书做一下简单的描述.

## SUMMARY.md
GitBook 使用 SUMMARY.md 文件来定义本书的章节和子章节的结构。 SUMMARY.md 文件用于生成本书的目录。

SUMMARY.md 的格式是一个链接列表。链接的标题将作为章节的标题，链接的目标是该章节文件的路径。

```md
# SUMMARY.md
* [第一章](part1/README.md)
    * [Writing is nice](part1/writing.md)
    * [GitBook is nice](part1/gitbook.md)
* [第二章](part2/README.md)
    * [We love feedback](part2/feedback_please.md)
    * [Better tools for authors](part2/better_tools.md)
```
每章都有一个专用页面（part#/README.md），并分为子章节。

**锚点**  
目录中的章节可以使用锚点指向文件的特定部分。
```md
# SUMMARY.md
* [第一章](part1/README.md)
    * [Writing is nice](part1/README.md#writing)
    * [GitBook is nice](part1/README.md#gitbook)
* [第二章](part2/README.md)
    * [We love feedback](part2/README.md#feedback)
    * [Better tools for authors](part2/README.md#tools)
```

**部分**  
目录可以分为以标题或水平线 ---- 分隔的部分：
```md
# SUMMARY.md
* [第一章](part1/README.md)
    * [Writing is nice](part1/writing.md)
    * [GitBook is nice](part1/gitbook.md)
* [第二章](part2/README.md)
    * [We love feedback](part2/feedback_please.md)
    * [Better tools for authors](part2/better_tools.md)
----
* [Last part without title](part3/title.md)
```
Parts 只是章节组，没有专用页面，但根据主题，它将在导航中显示。

## GLOSSARY.md
允许您指定要显示为注释的术语及其各自的定义。根据这些术语，GitBook 将自动构建索引并突出显示这些术语。

GLOSSARY.md 的格式是 h2 标题的列表，以及描述段落：
```md
## Term
Definition for this term
 
## Another term
With it's definition, this can contain bold text
and all other kinds of inline markup ...
```

## LANGS.md
GitBook支持使用多语言来构建书本。

按照GitBook的标准格式，每个语言应该作为一个子目录，命名为LANGS.md的文件应该遵循下面的格式并出现在仓库的根目录下：
```md
* [英语](en/)
* [法语](fr/)
* [西班牙语](es/)
```

## 普通章节.md
**Markdown语法**  
默认情况下，GitBook的大多数文件都使用Markdown语法。GitBook推荐使用这种语法。所使用的语法类似于[GitHub Flavored Markdown syntax](https://guides.github.com/features/mastering-markdown/)。

此外，你还可以选择[AsciiDoc](https://toolchain.gitbook.com/syntax/asciidoc.html)语法。

每编写一个.md文件，不要忘了在【SUMMARY.md】文件中添加一条记录

*普通章节内容示例：*
```md
# Title of the chapter
This is a great introduction.
 
## 第一节
Markdown will dictates _most_ of your **book's structure**
 
## 第二节
Markdown will dictates _most_ of your **book's structure**
```

---

# 常用插件
以下插件本书中皆有用到

| 插件名          | 功能                                      |
|:---------------------------|:---------------------------------------------------------------------------------|
|[search-pro][01]      |支持中文搜索                                   |
|[anchor-navigation-ex][02] |页内标题锚点&跳转顶部                               |
|[splitter][03]       |左侧菜单宽度拖拽                                 |
|[github][04]        |github右上图标跳转                                |
|[sitemap][05]        |生成站点地图                                   |
|[tbfed-pagefooter][06]   |页脚显示版权和修订时间                              |
|[alerts][07]        |美化区块消息                                   |
|[donate][08]        |打赏                                       |
|[copy-code-button][09]   |代码栏复制按钮                                  |
|[advanced-emoji][10]    |Emoji表情                                     |
|[baidu-tongji][11]     |百度统计                                     |
|[expandable-chapters][12]  |左侧菜单一级节点折叠                               |
|[echarts][13]        |百度Echarts图表                                 |

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
[13]: https://plugins.gitbook.com/plugin/echarts

---

# 常见问题
**生成静态网页错误**
> 执行build命令时，Error: ENOENT: no such file or directory  
> 解决方案：cd C:\Users\\{Administrator}\\.gitbook\versions\3.2.3\lib\output\website\  
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