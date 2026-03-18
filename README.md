
# 校园导航系统

## 项目介绍

校园导航系统是一个基于 uni-app 开发的跨平台应用，旨在为校园师生提供便捷的导航、信息查询和服务获取平台。本系统集成了校园地图导航、校园指南、失物招领等多种功能，帮助用户快速了解校园信息，提高校园生活质量。

## 功能特点

- **首页信息流**：展示天气信息、热门地点和近期活动
- **导览服务**：校园地图导航，帮助用户快速找到目的地
- **校园指南**：提供水院导航、作息时间、快递收发、教学楼等校园生活指南
- **失物招领**：发布和查询校园内的失物招领信息
- **相关链接**：快速访问学校官网、教务系统等相关网站

## 技术栈

- 前端框架：Vue 3 + uni-app
- 构建工具：Vite
- 开发语言：JavaScript
- 样式处理：CSS

## 项目结构

```
campus-system-demo/
├── forefront/
│   ├── uni-preset-vue-vite/
│   │   ├── src/
│   │   │   ├── pages/
│   │   │   │   ├── index/        # 首页
│   │   │   │   ├── guide/        # 导览服务
│   │   │   │   ├── campus/       # 校园指南
│   │   │   │   ├── lost/         # 失物招领
│   │   │   │   ├── links/        # 相关链接
│   │   │   │   └── webview/      # 网页浏览
│   │   │   ├── static/           # 静态资源
│   │   │   ├── App.vue           # 应用入口
│   │   │   ├── main.js           # 主文件
│   │   │   ├── manifest.json     # 应用配置
│   │   │   └── pages.json        # 页面路由配置
│   │   └── ...
│   └── ...
└── ...
```

## 安装与运行

### 环境要求

- Node.js 14.0+
- npm 或 yarn

### 安装依赖

```bash
# 进入项目目录
cd campus-system-demo/forefront/uni-preset-vue-vite

# 安装依赖
npm install
# 或
yarn install
```

### 运行项目

```bash
# 运行到H5
npm run dev:h5
# 或
yarn dev:h5

# 运行到微信小程序
npm run dev:mp-weixin
# 或
yarn dev:mp-weixin
```

### 打包项目

```bash
# 打包H5
npm run build:h5
# 或
yarn build:h5

# 打包微信小程序
npm run build:mp-weixin
# 或
yarn build:mp-weixin
```

## 项目预览

![首页预览](./screenshots/home.png)
![校园指南](./screenshots/guide.png)
![失物招领](./screenshots/lost.png)

## 贡献指南

1. Fork 本仓库
2. 创建您的特性分支 (`git checkout -b feature/amazing-feature`)
3. 提交您的更改 (`git commit -m 'Add some amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 打开一个 Pull Request

## 许可证

本项目采用 MIT 许可证 - 详情请参阅 [LICENSE](LICENSE) 文件

