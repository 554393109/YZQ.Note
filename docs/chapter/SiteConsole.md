<b style="font-size: 2em">网站Console</b>

---

# 微信开发文档

```javascript
// 移除左菜单，加大文档宽度
$('.sidebar, .Catalog-box').remove();$('#art-content').removeClass('content');$('.container').css('width','1100px');$('.content-hd .with-border').css({'font-size':'20px', 'font-weight':700});

```

# 中国天气

```javascript
// 在华南区块保留广东，移除其他省份
$('.conMidtab').find('.conMidtab2:eq(2),.conMidtab2:eq(0)').remove();$('.lqcontentBoxheader,.weather_li,.weather_li_head,.locationSearch,.footer').remove();

```
