# 小程序

## 小程序尺寸单位 rpx

尺寸单位 rpx（responsive pixel）: 可以根据屏幕宽度进行自适应。规定屏幕宽为 750rpx。如在 iPhone6 上，屏幕宽度为 375px，共有 750 个物理像素，则 750rpx = 375px = 750 物理像素，1rpx = 0.5px = 1 物理像素。

## 微信小程序获取用户信息

`wx.login(Object object)`。调用接口获取登录凭证（code）。通过凭证进而换取用户登录态信息，包括用户的唯一标识（openid）及本次登录的会话密钥（session_key）等。用户数据的加解密通讯需要依赖会话密钥完成。

`wx.getUserInfo(Object object)`。调用前需要用户授权 `scope.userInfo`。获取用户信息。

## 小程序的目录结构

微信小程序目录结构可以分为三个部分：框架全局文件、框架页面文件和工具类文件。

- 框架全局文件。一个小程序的主题部分由三个文件组成，作为全局文件，必须放在项目的根目录，分别是`app.js`小程序逻辑、`app.json`小程序公共设置和`app.wxss`小程序公共样式表。
  `app.js`文件用来定义全局数据和函数的使用，可以指定小程序的生命周期函数。`app.json`文件可以对五个功能进行设置：配置页面路径、配置窗口表现、配置标签导航、配置网络超时、配置 debug 模式。`app.wxss`文件对 CSS 样式进行了扩充和修改，定义在 app.wxss 中的样式为全局样式，作用于每一个页面。

- 框架页面文件。pages 文件夹主要存放小程序的页面文件，其中每个文件夹为一个页面，每个页面包含四个文件。小程序每个页面必须有.wxml 和.js 文件，其他两种类型的文件（.json和.wxss）可以不需要。注意：为了方便开发者减少配置项，描述页面的四个文件必须具有相同的路径与文件名。

- 工具类文件。在微信小程序框架目录里还有一个“utils”文件夹，它用来存放工具栏的 js 函数。定义这些函数后，要通过 module.exports 将定义的函数名称注册进来，在其他页面才可以使用。

## 小程序文件的作用域

在 JavaScript 文件中声明的变量和函数只在该文件中有效；不同的文件中可以声明相同名字的变量和函数，不会互相影响。通过全局函数 `getApp()` 可以获取全局的应用实例，如果需要全局的数据可以在 `App()` 中设置。也可以在 `App()`中创建自定义全局函数，在 App 全局中使用 `getApp()` 获取到的全局应用实例来调用此方法。

模块只有通过 `module.exports` 或者 `exports` 才能对外暴露接口。在需要使用这些模块的文件中，使用 `require(path)` 将公共代码引入，使用引用实例进行公共方法的调用。

## 小程序常用组件

- view 视图容器。
- scroll-view 可滚动视图区域。
- swiper 滑块视图容器。
- movable-view 可移动的视图容器，在页面中可以拖拽滑动
- cover-view 覆盖在原生组件之上的文本视图。
- cover-image 覆盖在原生组件之上的图片视图。

## WXML 语法

数据绑定。WXML 中的动态数据均来自对应 Page 的 data。数据绑定使用 Mustache 语法（双大括号）将变量包起来。

列表渲染。在组件上使用 `wx: for` 控制属性绑定一个数组，即可使用数组中各项的数据重复渲染该组件。默认数组的当前项的下标变量名默认为 index，数组当前项的变量名默认为 item。使用 wx:for-item 可以指定数组当前元素的变量名，使用 wx:for-index 可以指定数组当前下标的变量名。如果列表中项目的位置会动态改变或者有新的项目添加到列表中，并且希望列表中的项目保持自己的特征和状态（如 input 中的输入内容，switch 的选中状态），需要使用 wx:key 来指定列表中项目的唯一的标识符。

条件渲染。在框架中，使用 `wx: if=""` 来判断是否需要渲染该代码块，也可以用 `wx: elif` 和 `wx: else` 来添加一个 else 块。因为 wx:if 是一个控制属性，需要将它添加到一个标签上。如果要一次性判断多个组件标签，可以使用一个 `<block/>` 标签将多个组件包装起来，并在上边使用 wx:if 控制属性。

模板。WXML 提供模板（template），可以在模板中定义代码片段，然后在不同的地方调用。使用 name 属性，作为模板的名字。然后在`<template/>`内定义代码片段。使用 is 属性，声明需要的使用的模板，然后将模板所需要的 data 传入

引用。WXML 提供两种文件引用方式 import 和 include。import 可以在该文件中使用目标文件定义的 template。import 有作用域的概念，即只会 import 目标文件中定义的 template，而不会 import 目标文件 import 的 template。include 可以将目标文件除了 `<template/>` `<wxs/>` 外的整个代码引入，相当于是拷贝到 include 位置。

## 事件及事件绑定

在组件中绑定一个事件处理函数。如 bindtap，当用户点击该组件的时候会在该页面对应的 Page 中找到相应的事件处理函数。在相应的 Page 定义中写上相应的事件处理函数，参数是 event。

支持使用 WXS 函数绑定事件，WXS 函数接受 2 个参数，第一个是 event，在原有的 event 的基础上加了 event.instance 对象，第二个参数是 ownerInstance，和 event.instance 一样是一个 ComponentDescriptor 对象。在组件中绑定和注册事件处理的 WXS 函数。

事件分为冒泡事件和非冒泡事件：

- 冒泡事件：当一个组件上的事件被触发后，该事件会向父节点传递。
- 非冒泡事件：当一个组件上的事件被触发后，该事件不会向父节点传递。

事件绑定的写法同组件的属性，以 key、value 的形式。

- key 以bind或catch开头，然后跟上事件的类型，如bindtap、catchtouchstart。自基础库版本 1.5.0 起，在非原生组件中，bind和catch后可以紧跟一个冒号，其含义不变，如`bind:tap`、`catch:touchstart`。
- value 是一个字符串，需要在对应的 Page 中定义同名的函数。不然当触发事件的时候会报错。

bind事件绑定不会阻止冒泡事件向上冒泡，catch事件绑定可以阻止冒泡事件向上冒泡。

## 事件对象

如无特殊说明，当组件触发事件时，逻辑层绑定该事件的处理函数会收到一个事件对象。

`BaseEvent` 基础事件对象属性列表。`currentTarget`是代表事件绑定的当前组件，其中`id`表示当前组件的id，`dataset`表示当前组件上由`data-`开头的自定义属性组成的集合。特殊事件 canvas 中的触摸事件不可冒泡，所以没有`currentTarget`。

| 属性 | 类型 | 说明 |
|---|---|---|
| type | String | 事件类型 |
| timeStamp | Integer | 事件生成时的时间戳 |
| target | Object | 触发事件的组件的一些属性值集合 |
| currentTarget | Object | 当前组件的一些属性值集合 |
| mark | Object | 事件标记数据 |

`CustomEvent` 自定义事件对象属性列表（继承 BaseEvent）。自定义事件所携带的数据，如表单组件的提交事件会携带用户的输入，媒体的错误事件会携带错误信息。

| 属性 | 类型 | 说明 |
|---|---|---|
| detail | Object | 额外的信息 |

`TouchEvent` 触摸事件对象属性列表（继承 BaseEvent）：

| 属性 | 类型 | 说明 |
|---|---|---|
| touches | Array | 触摸事件，当前停留在屏幕中的触摸点信息的数组 |
| changedTouches | Array | 触摸事件，当前变化的触摸点信息的数组 |

## 页面跳转

- `wx.switchTab` 跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面
- `wx.reLaunch` 关闭所有页面，打开到应用内的某个页面
- `wx.redirectTo` 关闭当前页面，跳转到应用内的某个页面。但是不允许跳转到 tabbar 页面。
- `wx.navigateTo` 保留当前页面，跳转到应用内的某个页面。但是不能跳到 tabbar 页面。使用 wx.navigateBack 可以返回到原页面。小程序中页面栈最多十层。
- `wx.navigateBack` 关闭当前页面，返回上一页面或多级页面。可通过 getCurrentPages 获取当前的页面栈，决定需要返回几层。

通过`wx.navigateTo`推入一个新的页面，通过`getCurrentPages`获取当前页面栈的实例，以数组形式按栈的顺序给出，第一个元素为首页，最后一个元素为当前页面。

| 路由方式 | 触发时机 | 页面栈表现 | 进入方式 |
|---|---|---|---|
| 初始化 | 小程序打开的第一个页面 | 新页面入栈 | 从下往上升起 |
| 打开新页面 | 调用 API wx.navigateTo | 新页面入栈 | 从右往左切入 |
| 页面重定向 | 调用 API wx.redirectTo | 当前页面出栈，新页面入栈 | 页面重新加载 |
| 页面返回 | 返回/调用 API wx.navigateBack | 页面不断出栈，直到目标返回页 | 从右往左切回 |
| Tab 切换 | 切换/调用 API wx.switchTab | 页面全部出栈，只留下新的 Tab 页面 | 页面重新加载 |
| 重加载 | 调用 API wx.reLaunch | 页面全部出栈，只留下新的页面 | 页面重新加载 |

`wx.navigateTo`和`wx.redirectTo`只能打开非 TabBar 页面，`wx.switchTab`只能打开 Tabbar 页面，`wx.reLaunch`可以打开任意页面。跳转到 TabBar 页面，路径后不能带参数（注意，Tabbar 页面初始化之后不会被销毁），调用页面路由带的参数可以在目标页面的onLoad中获取。

页面的跳转存在哪些问题呢？
- 与接口的调用一样面临url的管理问题；
- 传递参数的方式不太友好，只能拼装url；
- 参数类型单一，只支持string。

第一个问题很好解决，我们做一个集中管理，比如新建一个router/routes.js文件来实现alias：
```js
// routes.js
module.exports = {
  home: '/pages/index/index',
  uc: '/pages/user_center/index',
};

// page
const routes = require('../../router/routes.js');
Page({
  onReady() {
    wx.navigateTo({
      url: routes.uc,
    });
  },
});
```


第二个问题，实现一个navigateTo函数，接受url参数和query参数，再自动拼接成需要的跳转参数。
```js
const routes = require('../../router/routes.js');

function navigateTo({ url, query }) {
  const queryStr = Object.keys(query).map(k => `${k}=${query[k]}`).join('&');
  wx.navigateTo({
    url: `${url}?${queryStr}`,
  });
}

Page({
  onReady() {
    const userId = '123456';
    navigateTo({
      url: routes.uc,
      query: {
        userId,
      },
    });
  },
});
```

第三个问题，参数保真。把要传的数据转成json字符串（JSON.stringify），然后在下个页面把它转回json数据（JSON.parse）。
```js
// routes.js
function navigateTo({ url, data }) {
  const dataStr = encodeURIComponent(JSON.stringify(data));
  wx.navigateTo({
    url: `${url}?encodedData=${dataStr}`,
  });
}

function extract(options) {
  return JSON.parse(decodeURIComponent(options.encodedData));
}

module.exports = {
  routes,
  navigateTo,
  extract,
};

// page home
const router = require('../../router/index.js');
Page({
  onLoad(options) {
    router.navigateTo({
      url: router.routes.uc,
      data: {
        isActive: true,
      },
    });
  },
});

// page uc
const router = require('../../router/index.js');
Page({
  onLoad(options) {
    const json = router.extract(options);
    console.log(json.isActive); // => true
    console.log(typeof json.isActive); // => "boolean"
    console.log(json.isActive === true); // => true
  },
});
```

## 设置 tabBar

tabBar 就是微信小程序下方的导航栏。

小程序开发过程中，当接受新的消息时，需要给出右上角的红点的提示，只需要调用函数`wx.showTabBarRedDot(Object object)`。

在微信小程序开发过程中，我们有时候需要界面全屏显示，比如调用地图API时，这样才能给用户更好的人机体验，这是后就需要动态的显示和隐藏微信小程序中的tabbar导航栏，关于显示tabbar，我们只需要调用函数：`wx.showTabBar(Object object)`。

在微信小程序开发过程中，我们有时候需要设置更为个性的tabbar，或者由于主题颜色的需求，我们需要保持与主题颜色一样，就需要调整tabbar的整体样式，我们只需要调用函数：`wx.setTabBarStyle(Object object)`。

当有好友发送消息过来时，tabbar右上角会有消息文本提示，这时只需要调用函数：`wx.setTabBarBadge(Object object)`。

## 页面生命周期

在app.js文件中，定义了一些生命周期方法：

- `onLaunch` 监听小程序初始化 当小程序初始化完成时，会触发 onLaunch（全局只触发一次）
- `onShow` 监听小程序显示 当小程序启动，或从后台进入前台显示，会触发 onShow
- `onHide` 监听小程序隐藏 当小程序从前台进入后台，会触发 onHide
- `onError` 错误监听函数 当小程序发生脚本错误，或者 api 调用失败时，会触发 onError 并带上错误信息
- 其他 开发者可以添加任意的函数或数据到 Object 参数中，用 this 可以访问

在page页面中定义的生命周期方法：

- `onLoad` 监听页面加载
- `onReady` 监听页面初次渲染完成
- `onShow` 监听页面显示
- `onHide` 监听页面隐藏
- `onUnload` 监听页面卸载

## 转发分享

页面内发起转发。通过给 button 组件设置属性 `open-type="share"`，可以在用户点击按钮后触发 `Page.onShareAppMessage` 事件，如果当前页面没有定义此事件，则点击后无效果。

`onShareAppMessage(Object object)` 监听用户点击页面内转发按钮（button 组件 `open-type="share"`）或右上角菜单“转发”按钮的行为，并自定义转发内容。注意：只有定义了此事件处理函数，右上角菜单才会显示“转发”按钮。

## request 请求后台接口



## http-promise 封装



## webview



## 获取用户收货地址

`wx.chooseAddress(Object object)`。获取用户收货地址。调起用户编辑收货地址原生界面，并在编辑完成后返回用户选择的地址。

参数 `Object object`

| 属性 | 类型 | 必填 | 说明 |
|---|---|---|---|
| success | function | 否 | 接口调用成功的回调函数 |
| fail | function | 否 | 接口调用失败的回调函数 |
| complete | function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行） |

object.success 回调函数的参数 `Object res`

| 属性 | 类型 | 说明 |  |
|---|---|---|---|
| userName | string | 收货人姓名 |  |
| postalCode | string | 邮编 |  |
| provinceName | string | 国标收货地址第一级地址 |  |
| cityName | string | 国标收货地址第二级地址 |  |
| countyName | string | 国标收货地址第三级地址 |  |
| detailInfo | string | 详细收货地址信息 |  |
| nationalCode | string | 收货地址国家码 |  |
| telNumber | string | 收货人手机号码 |  |
| errMsg | string | 错误信息 |  |

## 获取地理位置

`wx.getLocation(Object object)`。获取当前的地理位置、速度。当用户离开小程序后，此接口无法调用。调用前需要 用户授权 `scope.userLocation`。

```js
wx.getLocation({
 type: 'wgs84',
 success (res) {
   const latitude = res.latitude
   const longitude = res.longitude
   const speed = res.speed
   const accuracy = res.accuracy
 }
})
```

## 自定义组件

类似于页面，一个自定义组件由 json wxml wxss js 4个文件组成。要编写一个自定义组件，首先需要在 json 文件中进行自定义组件声明（将 component 字段设为 true 可这一组文件设为自定义组件）。

注意：在组件wxss中不应使用ID选择器、属性选择器和标签名选择器。

在自定义组件的 js 文件中，需要使用 `Component()` 来注册组件，并提供组件的属性定义、内部数据和自定义方法。

组件的属性值和内部数据将被用于组件 wxml 的渲染，其中，属性值是可由组件外部传入的。

```js
Component({
  properties: {
    // 这里定义了innerText属性，属性值可以在组件使用时指定
    innerText: {
      type: String,
      value: 'default value',
    }
  },
  data: {
    // 这里是一些组件内部数据
    someData: {}
  },
  methods: {
    // 这里是一个自定义方法
    customMethod: function(){}
  }
})
```

使用已注册的自定义组件前，首先要在页面的 json 文件中进行引用声明。此时需要提供每个自定义组件的标签名和对应的自定义组件文件路径。这样，在页面的 wxml 中就可以像使用基础组件一样使用自定义组件。节点名即自定义组件的标签名，节点属性即传递给组件的属性值。


