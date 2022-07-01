<b style="font-size: 2em">网站Console</b>

---

# 微信开发文档

```javascript
// 移除左菜单，加大文档宽度
$('.sidebar, .Catalog-box').remove();$('#art-content').removeClass('content');$('.container').css('width','1100px');$('.content-hd .with-border').css({'font-size':'20px', 'font-weight':700});

// 移除左菜单，加大文档宽度[https://pay.weixin.qq.com/wiki/doc/apiv3_partner/apis/chapter10_1_8.shtml]
$('.pendant, .doc-box-right, .doc-side').remove();$('.doc-box-left').css({'padding-left':15,'padding-right':150});
```

# 中国天气

```javascript
// 在华南区块保留广东，移除其他省份[http://www.weather.com.cn/textFC/hn.shtml]
$('.conMidtab').find('.conMidtab2:eq(2),.conMidtab2:eq(0)').remove();$('.lqcontentBoxheader,.weather_li,.weather_li_head,.locationSearch,.footer').remove();

```
