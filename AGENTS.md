# ShopXO UniApp 移动端架构文档

## 项目概述
基于 uni-app 的跨平台移动电商应用，支持微信小程序、支付宝小程序、H5、APP等多端。

## 技术栈
- uni-app 框架
- Vue 2.x
- i18n 国际化

## 目录结构

```
shopxo-uniapp/
├── pages/                      # 页面目录 ★核心
│   ├── index/                  # 首页
│   ├── goods-category/         # 商品分类
│   ├── cart/                   # 购物车
│   ├── user/                   # 用户中心
│   ├── login/                  # 登录
│   ├── goods-detail/           # 商品详情
│   ├── goods-search/           # 商品搜索
│   ├── buy/                    # 下单页
│   ├── cashier/                # 收银台
│   ├── order/                  # 订单相关
│   │
│   ├── diy/                    # DIY页面组件
│   │   ├── diy.vue             # DIY页面入口
│   │   └── components/diy/     # DIY模块组件
│   │       ├── goods-list.vue  # 商品列表
│   │       ├── carousel.vue    # 轮播图
│   │       ├── coupon.vue      # 优惠券
│   │       ├── nav-group.vue   # 导航组
│   │       └── ... (30+组件)
│   │
│   ├── form-input/             # 表单输入组件
│   │   └── components/
│   │       └── form-input/
│   │           ├── input.vue   # 输入框
│   │           ├── select.vue  # 下拉选择
│   │           ├── upload.vue  # 上传
│   │           └── ...
│   │
│   └── plugins/                # 插件页面
│       ├── coupon/             # 优惠券插件
│       ├── distribution/       # 分销插件
│       ├── blog/               # 博客插件
│       ├── ask/                # 问答插件
│       ├── coin/               # 积分/虚拟币
│       └── ...
│
├── components/                 # 公共组件
│   ├── goods-buy/              # 商品购买弹窗
│   ├── goods-spec-choice/      # 规格选择
│   ├── goods-list/             # 商品列表
│   ├── cart/                   # 购物车组件
│   ├── payment/                # 支付组件
│   ├── popup/                  # 弹窗组件
│   ├── search/                 # 搜索组件
│   ├── countdown/              # 倒计时
│   └── ...
│
├── common/                     # 公共资源
│   ├── css/                    # 样式文件
│   │   ├── business.css        # 业务样式
│   │   ├── lib.css             # 库样式
│   │   ├── page.css            # 页面样式
│   │   ├── plugins.css         # 插件样式
│   │   └── theme.css           # 主题样式
│   │
│   └── js/                     # JS工具
│       ├── lib/                # 第三方库
│       │   └── base64.js       # Base64编解码
│       └── common/             # 公共方法
│           ├── base.js         # 基础方法
│           ├── common.js       # 通用方法
│           └── share.js        # 分享功能
│
├── locale/                     # 国际化
│   ├── index.js                # i18n配置
│   ├── zh.json                 # 中文
│   └── en.json                 # 英文
│
├── App.vue                     # 应用入口
├── main.js                     # 主入口
├── pages.json                  # 页面路由配置 ★重要
├── manifest.json               # 应用配置
└── package.json                # 依赖配置
```

## 页面路由结构

```
pages.json 配置:
├── pages (主包)
│   ├── pages/index/index           # 首页
│   ├── pages/goods-category/       # 分类
│   ├── pages/cart/cart             # 购物车
│   └── pages/user/user             # 用户中心
│
└── subPackages (分包)
    ├── pages/diy                   # DIY页面
    ├── pages/goods-detail          # 商品详情
    ├── pages/goods-search          # 商品搜索
    ├── pages/buy                   # 下单
    ├── pages/cashier               # 收银台
    ├── pages/form-input            # 表单
    └── pages/plugins/*             # 插件页面
```

## 核心业务流程

### 购物流程
```
首页 → 商品列表 → 商品详情 → 购物车 → 下单 → 支付 → 订单详情
 │        │          │         │       │      │
 └─ diy/  └─ goods-  └─ goods- └─ cart/ └─ buy/ └─ cashier/
    组件     list      detail
```

### 用户流程
```
登录 → 用户中心 → 个人信息 → 地址管理 → 订单列表
 │        │          │          │          │
 └─ login/ └─ user/  └─ personal └─ address └─ order/
```

## DIY 组件与后端对应

| 前端组件 | 后端服务 | DIY编辑器组件 |
|---------|---------|--------------|
| diy/goods-list.vue | DiyService | model-goods-list |
| diy/carousel.vue | DiyService | model-carousel |
| diy/coupon.vue | CouponService | model-coupon |
| diy/nav-group.vue | DiyService | model-nav-group |
| diy/notice.vue | MessageService | model-notice |

## 插件模块结构

每个插件页面遵循统一结构：
```
plugins/xxx/
├── index/          # 插件首页
├── detail/         # 详情页
├── form/           # 表单页
└── user/           # 用户相关页
```

## 主要插件列表

| 插件目录 | 功能描述 |
|---------|---------|
| coupon | 优惠券系统 |
| distribution | 分销系统 |
| blog | 博客文章 |
| ask | 问答系统 |
| coin | 虚拟币/积分 |
| seckill | 秒杀活动 |
| activity | 营销活动 |
| delivery | 物流配送 |
| realstore | 门店管理 |
| shop | 多店铺 |

## 公共组件说明

| 组件 | 用途 |
|-----|------|
| goods-buy | 商品购买弹窗(规格选择、数量) |
| goods-spec-choice | 商品规格选择器 |
| payment | 支付方式选择 |
| popup | 通用弹窗 |
| countdown | 倒计时组件 |
| search | 搜索框组件 |
| no-data | 空数据占位 |

## 与后端 API 交互

- API 基础路径在 `common/js/common/base.js` 中配置
- 请求封装在 `common/js/common/common.js`
- 主要接口对应后端 `shopxo/app/api/controller/`
