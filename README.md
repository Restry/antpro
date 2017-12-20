---
order: 0
title: 开始使用
type: 入门
---

# 架构介绍

## 写在前面

此架构提供了以下的典型模板，并据此构建了一套基于 React 的中后台管理控制台的脚手架，可以快速搭建企业级中后台产品。

```
- Dashboard
  - 分析页
  - 监控页
  - 工作台
- 表单页
  - 基础表单页
  - 分步表单页
  - 高级表单页
- 列表页
  - 查询表格
  - 标准列表
  - 卡片列表
  - 搜索列表（项目/应用/文章）
- 详情页
  - 基础详情页
  - 高级详情页
- 结果
  - 成功页
  - 失败页
- 异常
  - 403 无权限
  - 404 找不到
  - 500 服务器出错
- 帐户
  - 登录
  - 注册
  - 注册成功
```

## 谁在使用

目前蚂蚁金服和阿里巴巴内部多个项目使用了这个架构, 以下是使用React技术开发的网站 .

[微软VS文档介绍](https://www.visualstudio.com/zh-cn/news/releasenotes/vs2017-relnotes)

[微软outlook邮箱](https://outlook.live.com/owa/?authRedirect=true)

[Pluralsight培训](https://app.pluralsight.com/paths/skill/react)

[知乎](https://www.zhihu.com)



### For 设计者

设计师，可以找到和此架构 一一配套的 [Axure/Sketch 设计资源] ，大幅度提升设计效率和沟通效率。

### For 开发者

如果你是工程师，在接下来的文档中，我们将具体介绍如何使用这个脚手架。

## 前序准备

本地环境需要安装 [node](http://nodejs.org/) 和 [git](https://git-scm.com/)。我们的技术栈基于 [ES2015+](http://es6.ruanyifeng.com/)、[React](http://facebook.github.io/react/)、 和 [antd](https://ant.design/docs/react/introduce-cn):前端UI库

## 安装


### 直接 clone git 仓库

```bash
$ git clone --depth=1 https://github.com/restry/antpro.git my-project
$ cd my-project
```
  
## 目录结构

完整的开发框架，提供了涵盖中后台开发的各类功能和坑位，下面是整个项目的目录结构。

```bash
├── mock                     # 本地模拟数据
├── public
│   └── favicon.ico          # Favicon
├── src
│   ├── assets               # 本地静态资源
│   ├── common               # 应用公用配置，如导航信息
│   ├── components           # 业务通用组件
│   ├── layouts              # 通用布局
│   ├── models               # 数据模型 model
│   ├── routes               # 业务页面入口和常用模板
│   ├── services             # 后台接口服务
│   ├── utils                # 工具库
│   ├── g2.js                # 可视化图形配置
│   ├── theme.js             # 主题配置
│   ├── index.ejs            # HTML 入口模板
│   ├── index.js             # 应用入口
│   ├── index.less           # 全局样式
│   └── router.js            # 路由入口
├── tests                    # 测试工具
├── README.md
└── package.json
```

## 本地开发

安装依赖。

```bash
$ npm install
```

> 如果网络状况不佳，可以使用 [cnpm](https://cnpmjs.org/) 进行加速。

```bash
$ npm start
```

<img src="https://gw.alipayobjects.com/zos/rmsportal/DaIsSQRbNkwOXbMDhqEx.png" width="700" />

启动完成后会自动打开浏览器访问 [http://localhost:8000](http://localhost:8000)，你看到下面的页面就代表成功了。

<img src="https://gw.alipayobjects.com/zos/rmsportal/psqyFTiRoXQeaNZdjppA.png" width="700" alt="首页截图" />

接下来就可以修改代码进行业务开发了，内建了典型业务模板、常用业务组件、模拟数据、实时预览、状态管理、全局路由等等各种实用的功能辅助开发。




# 添加路由和菜单
路由和菜单是组织起一个应用的关键骨架，脚手架提供了一些基本的工具及模板，帮助更方便的搭建路由/菜单。

---

## 前序知识

在此架构中, 根据实现方式的区别，通常对于导航和路由相关的需求，可以分为以下两种：

- **可以利用现有布局及导航展示规则，只是新增页面**。

   这种情况下，你只需要对导航数据进行增删，就能完成路由和导航的配置。

- **新增页面有不同的布局**。

   这种情况会稍微麻烦一些，修改数据的同时，还需要你新建布局文件，还可能需要自己生成相应的导航，或对现有规则进行调整。


下面简单介绍两种情况下如何添加路由/菜单。

## 添加页面/路由/菜单

### 添加页面

这里的『页面』指配置了路由，能够通过链接直接访问的模块，要新建一个页面，通常只需要在脚手架的基础上进行简单的配置。

---

#### 一、新增 js、less 文件

在 `src/routes` 下新建页面的 js 及 less 文件，如果相关页面有多个，可以新建一个文件夹来放置相关文件。

<img width="300" alt="新增页面" src="https://gw.alipayobjects.com/zos/rmsportal/hjDyFTVOgRwDzAIHApMO.png" />

<br />

样式文件默认使用 [CSS Modules](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)，如果需要，你可以在样式文件的头部引入 [antd 样式变量文件](https://github.com/ant-design/ant-design/blob/master/components/style/themes/default.less)：

```css
@import "~antd/lib/style/themes/default.less";
```

这样可以很方便地获取 antd 样式变量并在文件里使用，有利于保持页面的一致性，也方便实现定制主题。

  

#### 三、新增 model

布局及路由都配置好之后，回到之前新建的 `NewPage.js`，可以开始写业务代码了！如果需要用到 [dva](https://github.com/dvajs/dva/) 中的数据流，还需要在 `src/models` 中建立相应的 model，具体可以参考脚手架内置页面的写法。

#### 添加菜单和路由

脚手架默认提供了两种布局模板：`基础布局 - BasicLayout` 以及 `账户相关布局 - UserLayout`：

<img alt="基础布局" src="https://gw.alipayobjects.com/zos/rmsportal/oXmyfmffJVvdbmDoGvuF.png" />

<img alt="账户相关布局" src="https://gw.alipayobjects.com/zos/rmsportal/mXsydBXvLqBVEZLMssEy.png" />

如果页面可以利用这两种布局，那么只需要在导航数据中增加一条即可。打开文件 `src/common/nav.js`，添加页面信息：

```js
{
  name: '新页面',             // 页面名称，会展示在菜单栏中
  path: 'new',               // 匹配的路由
  icon: 'file',              // 页面图标，会展示在菜单栏中
  component: dynamicWrapper(app, ['NewPageModel'], () => import('/routes/NewPage')),   // 动态引入NewPage页面和所需的Models
}
```

加好后，会默认生成相关的路由及导航。访问 `http://localhost:8000/#/new` 就可以看到新增的页面了。

<img alt="新增页面" src="https://gw.alipayobjects.com/zos/rmsportal/xZIqExWKhdnzDBjajnZg.png" />

 
到这一步，路由和页面就建好了。

### 带参数的路由配置

在 `src/common/nav.js` 中这样配置即可：

```js
{
  name: '详情页',
  path: 'profile',
  icon: 'profile',
  children: [{
    name: '基础详情页',
    path: 'basic',
    component: dynamicWrapper(app, ['profile'], () => import('../routes/Profile/BasicProfile')),
  }, {
    name: '高级详情页',
    path: 'advanced',
    children: [{
      name: '高级详情页',
      path: ':id',                      // id 为参数名
      component: dynamicWrapper(app, ['profile'], () => import('../routes/Profile/AdvancedProfile')),
    }]
  }],
}
```

 
# 添加组件


对于一些可能被多处引用的功能模块，建议提炼成业务组件统一管理。这些组件一般有以下特征：

- 只负责一块相对独立，稳定的功能；
- 没有单独的路由配置；
- 可能是纯静态的，也可能包含自己的 state，但不涉及数据流，仅受父组件（通常是一个页面）传递的参数控制。

---


下面以一个简单的静态组件为例进行介绍。假设你的应用中经常需要展现图片，这些图片宽度固定，有一个灰色的背景和一定的内边距，有文字介绍，就像下图这样：

<img src="https://gw.alipayobjects.com/zos/rmsportal/vcRltFiKfHBHFrUcsTtW.png" width="400" />

你可以用一个组件来实现这一功能，它有默认的样式，同时可以接收父组件传递的参数进行展示。

## 新建文件

在 `src/components` 下新建一个以组件名命名的文件夹，注意首字母大写，命名尽量体现组件的功能，这里就叫 `ImageWrapper`。在此文件夹下新增 js 文件及样式文件（如果需要），命名为 `index.js` 和 `index.less`。

> 在使用组件时，默认会在 `index.js` 中寻找 export 的对象，如果你的组件比较复杂，可以分为多个文件，最后在 `index.js` 中统一 export，就像这样：

 ```js
// MainComponent.js
export default ({ ... }) => (...);

// SubComponent1.js
export default ({ ... }) => (...);

// SubComponent2.js
export default ({ ... }) => (...);

// index.js
import MainComponent from './MainComponent';
import SubComponent1 from './SubComponent1';
import SubComponent2 from './SubComponent2';

MainComponent.SubComponent1 = SubComponent1;
MainComponent.SubComponent2 = SubComponent2;
export default MainComponent;
```

你的代码大概是这个样子：

```jsx
// index.js
import React from 'react';
import styles from './index.less';    // 按照 CSS Modules 的方式引入样式文件。

export default ({ src, desc, style }) => (
  <div style={style} className={styles.imageWrapper}>
    <img className={styles.img} src={src} alt={desc} />
    {desc && <div className={styles.desc}>{desc}</div>}
  </div>
);
```

```css
// index.less
.imageWrapper {
  padding: 0 20px 8px;
  background: #f2f4f5;
  width: 400px;
  margin: 0 auto;
  text-align: center;
}

.img {
  vertical-align: middle;
  max-width: calc(100% - 32px);
  margin: 2.4em 1em;
  box-shadow: 0 8px 20px rgba(143, 168, 191, 0.35);
}
```

到这儿组件就建好了。

## 使用

在要使用这个组件的地方，按照组件定义的 API 传入参数，直接使用就好，不过别忘了先引入：

```js
import React from 'react';
import ImageWrapper from '../../components/ImageWrapper';  // 注意保证引用路径的正确

export default () => (
  <ImageWrapper
    src="https://os.alipayobjects.com/rmsportal/mgesTPFxodmIwpi.png"
    desc="示意图"
  />;
)

```

# 和服务器端交互


前后端分离开发,提供本地模拟数据给前端代码调用的开发模式，
通过 Restful API 的形式和任何技术栈的服务端应用一起工作。下面将简单介绍和服务端交互的基本写法。

## 前端请求流程

一个完整的前端 UI 交互到服务端处理流程是这样的：

1. UI 组件交互操作；
2. 调用 model 的 effect；  // 类似vuex或者redux的dispatch
3. 使用封装的 request.js 发送请求；
4. 获取服务端返回；
5. 然后调用 reducer 改变 state；
6. 更新 model。


其中，`utils/request.js` 是基于 [fetch](https://developer.mozilla.org/es/docs/Web/API/Fetch_API/Using_Fetch) 的封装，便于统一处理 POST，GET 等请求参数，请求头，以及错误提示信息等。具体可以参看 [request.js](https://github.com/ant-design/ant-design-pro/blob/master/src/utils/request.js)。

### Effect 处理异步请求

在处理复杂的异步请求的时候，很容易让逻辑混乱，陷入嵌套陷阱，所以底层基础框架使用 `effect` 的方式来管理同步化异步请求：

```js
effects: {
  *fetch({ payload }, { call, put }) {
    yield put({
      type: 'changeLoading',
      payload: true,
    });
    // 异步请求 1
    const response = yield call(queryFakeList, payload);
    yield put({
      type: 'save',
      payload: response,
    });
    // 异步请求 2
    const response2 = yield call(queryFakeList2, payload);
    yield put({
      type: 'save2',
      payload: response2,
    });
    yield put({
      type: 'changeLoading',
      payload: false,
    });
  },
},
```

通过 前面加星号 [generator](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/function*) 和 [yield](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/yield) 使得异步调用的逻辑处理跟同步一样


# API 文档自动生成

在日常开发中，往往是前后端分离的，这个时候约定好一套接口标准，前后端各自独立开发，就不会被对方的技术难点给阻塞住，从而保证项目进度。

在此架构中已经有了一套比较完善的 mock 功能，而 [roadhog-api-doc](https://github.com/nikogu/roadhog-api-doc) 工具，则能够从项目的 mock 数据中读取接口信息生成对应的文档，这样就能够更加清晰明了的展现项目的接口情况。
 
## 如何使用

```bash
$ npm install roadhog-api-doc -g
```

### 本地服务

进入到项目根目录，运行：

```bash
$ roadhog-api-doc start [port]
```
 

### 书写文档

通常来讲，你无需额外加入任何依赖就可以生成文档，但是如果你需要对接口做出说明，需要按照以下格式对 `roadhog mock` 文件进行修改：

```bash
$ npm install roadhog-api-doc --save-dev // 将 roadhog-api-doc 作为本地工具依赖安装
```

```js
import { format } from 'roadhog-api-doc';

const proxy = {
  'GET /api/currentUser': {
    $desc: "获取当前用户接口",
    $params: {
      pageSize: {
        desc: '分页',
        exp: 2,
      },
    },
    $body: {
      name: 'momo.zxy',
      avatar: imgMap.user,
      userid: '00000001',
      notifyCount: 12,
    },
  },
};

export default format(proxy);
```

其中：

- $desc: 接口说明
- $params: 接口参数说明，对象描述各个参数的意义
- $body: 数据返回结果，通常就是 mock 的数据

<img width="600" src="https://gw.alipayobjects.com/zos/rmsportal/PVfsHataJahAwAVaKDtp.png" />

### 本地测试 mock 数据和真实端口

当启动本地的 API Docs 站点以后，可以点击 `send` 按钮发送 `POST` 或者 `GET` 请求，并且返回值会在弹出框中显示：

<img width="600" src="https://gw.alipayobjects.com/zos/rmsportal/mkgrIEbmhXZFbSOWvTCz.png" />

其中需要注意的是，如果启动 API Docs 站点时，没有加端口号，那么这里的返回数据是静态数据，如果加了端口号并且本地也同时跑起了项目，那么就会直接返回实际数据。
 

