# TraeWork 绿皮书

**AI 原生工作台 · 从入门到精通完全指南**

> v1.0 · 2026.08 · 7 大部分 · 30 章 · 3 附录

## 这是什么

TraeWork 绿皮书是一本**单文件 HTML 电子书**，系统梳理字节跳动 AI 原生工作台 **TraeWork** 的产品定位、界面入门、三种模式、核心能力与真实用法，覆盖从新手入门到进阶实战的完整路径。

内容整理自 TraeWork 官方知识库（飞书 Wiki）与官方公众号公开资料，包含：产品定位、界面入门、三种模式、20 个核心理由、8 个入门技巧、核心能力（Skill / MCP / 自动化 / 规则记忆 / 多模态 / 浏览器控制）、100+ 真实用法分类与最新「我的文件」功能解读。

## 快速访问

**https://traework-green-book.wangjn.site**

## 内容概览

- **认识 TraeWork** — 产品定位、vs Chatbot、三种模式（Work / Code / Design）
- **界面与上手** — 三栏布局、云端/本地、第一个任务、8 个入门技巧
- **20 个理由** — 门槛、体验、能力、本土生态、复用自动化、安全六大维度
- **核心能力详解** — Skill、Rules/Memory、MCP、自动化、多模态、浏览器控制、模板库、三端协同
- **100+ 真实用法** — 12 大场景分类、按人群推荐路径
- **社区与生态** — 社区、交流群、直播、官方账号矩阵
- **最新动态** — 「我的文件」功能上线解读

## 部署说明

本项目支持两种部署方式：

### A. GitHub Pages（当前生效）

仓库已配置 CNAME → `traework-green-book.wangjn.site`，GitHub Pages 自动构建。

### B. CNB + EdgeOne 全球加速（推荐）

1. 登录 [cnb.cool](https://cnb.cool) → 新建仓库 → **导入外部仓库**
2. 填入：`https://github.com/GoodTimeGGB/traework-green-book`
3. 导入后 CNB 自动识别 `.cnb.yml` 流水线，一键部署至 EdgeOne Pages
4. 到 DNSPod 将 `traework-green-book.wangjn.site` 的 CNAME 改为 EdgeOne 提供的加速域名

详细步骤见仓库内 [`CNB-EDGEONE-部署说明.md`](./CNB-EDGEONE-部署说明.md)

## 文件结构

```
├── index.html          # 主文件（单文件电子书，含全部章节 + 内联样式）
├── assets/             # 正文配图（27 张官方截图 / 动图）
├── .cnb.yml            # CNB EdgeOne 部署流水线配置
├── CNAME               # GitHub Pages 自定义域名
├── CNB-EDGEONE-部署说明.md
├── LICENSE             # MIT
└── README.md           # 本文件
```

## 关于作者

**王总（GoodTime）** — 全栈开发者 · AI 科普创作者

- 微信公众号「宁的AI小站」
- GitHub: [@GoodTimeGGB](https://github.com/GoodTimeGGB)

## License

[MIT](LICENSE)
