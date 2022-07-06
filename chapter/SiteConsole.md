<b style="font-size: 2em">网站Console</b>

---

# 微信开发文档

```javascript
// 移除左菜单，加大文档宽度
$('.sidebar, .Catalog-box').remove();$('#art-content').removeClass('content');$('.container').css('width','1100px');$('.content-hd .with-border').css({'font-size':'20px', 'font-weight':700});

// 移除非必要元素，加大文档可视内容 [https://pay.weixin.qq.com/wiki/doc/apiv3_partner/apis/chapter10_1_8.shtml]
$('.pendant, .doc-box-right, .doc-side, .header-wrp, .header_segment, .bread-crumb, #we-feedback__panel').remove();$('.doc-box-left').css({'padding-top':'initial', 'padding-right':150, 'padding-left':15});$('#cnt-json, #cnt-normal').css({'max-height':'initial'});$('.wrap').css({'max-width':'initial', 'width':'initial'});
```

# 中国天气

```javascript
// 在华南区块保留广东，移除其他省份[http://www.weather.com.cn/textFC/hn.shtml]
$('.conMidtab').find('.conMidtab2:eq(2),.conMidtab2:eq(0)').remove();$('.lqcontentBoxheader,.weather_li,.weather_li_head,.locationSearch,.footer').remove();
```

# Gitbook

```javascript
// 加大文档宽度
$('.page-inner').css({'max-width':'initial','padding':'20px 20px 40px'})
```

# 富友支付接口文档

```javascript
// 加大文档宽度 [https://fundwx.fuiou.com/doc/]
$('#main').style.cssText+="max-width:initial; padding:30px 30px 40px 15px;";$('.content').style.cssText+="padding-top: initial"
```
