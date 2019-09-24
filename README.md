# mina-page-patch

微信小程序 Page 叠加包，让 wxml 可以直接使用 wx 下的 api，并通过 `data-*` 传递参数

## 使用

下载 `page-patch.js` 到小程序项目目录，在 `app.js` **顶部**调用

```js
import pagePatch from './page-patch.js';
pagePatch();
```

`pagePatch` 默认叠加了大部分不需要用户授权的 api，如果需要叠加更多的 api，可以传入一个数组

```js
pagePatch(['vibrateShort']);
```

接下来就可以在 wxml 中直接使用 wx 下的 api，不需要在页面 js 文件中声明处理函数，例如实现点击图片进入预览

index.wxml

```xml
<image src="{{img_url}}" bindtap="$wx.previewImage" data-urls="{{[img_url]}}" />
```

### 需要用到 success, fail, complete 回调？

index.js

```js
Page({
  previewSuccess(res) {
    console.log('previewImage success', res);
  }
});
```

index.wxml

```xml
<image src="{{img_url}}" bindtap="$wx.previewImage" data-urls="{{[img_url]}}" data-success="previewSuccess" />
```

### 需要驼峰参数名？

index.wxml

```xml
<button bindtap="$wx.makePhoneCall" data-phone-number="13800138000">打电话</button>
```

## 注意

- `pagePatch` 必须在 `app.js` 顶部调用，确保页面初始化之前成功叠加
