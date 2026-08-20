# TraeWork 绿皮书 · CNB + EdgeOne 部署清单

目标：把绿皮书（静态站点）托管到 **CNB（cnb.cool）** 作为代码源与 CI，前面套 **EdgeOne** 做免费全球加速 —— 国内直连、零流量分发费。

---

## 架构（你要的方案）

```
读者浏览器
   │  https://traework-green-book.wangjn.site/
   ▼
腾讯云 DNSPod（CNAME: traework → EdgeOne 加速域名）
   ▼
EdgeOne（免费版：国内节点 + 全球加速 + 自动 HTTPS + DDoS/WAF）  ← 加速层
   ▼
CNB 仓库（cnb.cool）+ EdgeOne Pages（托管绿皮书静态文件）  ← 源站
```

两种方式任选其一：

### 方式 A（推荐，最省事）：CNB 流水线 → EdgeOne Pages

代码进 CNB，CNB 的 `.cnb.yml` 流水线一键 `npx edgeone pages deploy` 把站点推到 EdgeOne 网络，托管 + 加速都在 EdgeOne 上，免费、国内快。

- 本目录已备好 `.cnb.yml`（指向 EdgeOne Pages 项目 `traework-green-book`）。

### 方式 B（最贴合原话：CNB 托管 + EdgeOne 仅加速）

CNB Pages 作为源站，EdgeOne 仅做 CDN 加速（CNAME 接入）。

- CNB 仓库开 Pages（控制台一键），拿到 `*.pages.cnb.run` 默认站点域名；
- EdgeOne 加站点 `traework-green-book.wangjn.site`，源站填 CNB Pages 域名，CNAME 接入；
- DNS：`traework` CNAME → EdgeOne 分配的加速域名。

---

## 操作步骤（方式 A）

1. **建 CNB 仓库**
   - 登录 cnb.cool，新建仓库（如 `traework-green-book`），把本目录内容（index.html + assets/ + .cnb.yml）推上去。
   - 或用「从 GitHub 导入」直接导入 `github.com/GoodTimeGGB/traework-green-book`。

2. **建 EdgeOne Pages 项目**
   - 腾讯云 EdgeOne 控制台 → Pages → 新建项目 `traework-green-book`（类型：直接上传）。
   - 记下项目名（与 `.cnb.yml` 里的 `-n` 一致）。

3. **配 EDGEONE_API_TOKEN**
   - EdgeOne Pages 控制台生成 API Token；
   - 在 CNB 仓库「变量/密钥」里新增 `EDGEONE_API_TOKEN`，值填该 Token。

4. **绑定自定义域名**
   - EdgeOne Pages 项目里添加自定义域名 `traework-green-book.wangjn.site`，按提示验证；
   - 拿到 EdgeOne 分配的 CNAME（如 `traework-green-book.wangjn.site.eo.dnse*.com`）。

5. **改 DNS（关键）**
   - 去腾讯云 DNSPod，把 `traework` 的 CNAME 值从 `goodtimeggb.github.io` 改成第 4 步 EdgeOne 给的加速域名；
   - 等 5–30 分钟传播，访问 `https://traework-green-book.wangjn.site/` 即上线；
   - 生效后 EdgeOne 自动签发 HTTPS，控制台勾选 Enforce HTTPS。

6. **自动部署**
   - 以后绿皮书升版：更新 `index.html` + `assets/` → `git push` 到 CNB main → 流水线自动重新部署到 EdgeOne Pages，无需手动操作。

---

## 手动增量更新（GitHub + CNB 双推送）

当前 CNB 仓库是**普通仓库**（不是「从 GitHub 导入」的镜像，页面**没有「同步」按钮**），更新靠双推送：

1. **改内容**：在本地 `edgeone-site/` 修改 `index.html` 或 `assets/`；
2. **推 GitHub**：运行 `node edgeone-upload.js`（增量脚本，只上传变化的文件、保留提交历史）；
3. **直推 CNB**：将 `edgeone-site/` 内容复制到本地 CNB 克隆目录 `cnb-traework-sync/`，执行 `git add . && git commit -m "说明" && git push origin main` → 流水线自动部署到 EdgeOne，无需手动点「同步」。

> 两个源都推送后，GitHub 与 CNB 内容一致；CNB 侧只要 `git push` 成功即自动触发 EdgeOne 部署。

---

## 本地已完成的准备

- [x] `index.html` 已移除 Google Fonts 等外部依赖（系统字体栈，国内秒开）
- [x] 全部配图本地化到 `assets/`（30 张官方截图 / 动图）
- [x] `.cnb.yml` 流水线配置（方式 A）
- [x] `edgeone-upload.js` 增量上传脚本（保留历史、只传变更、快进更新）

## 待你操作

- [ ] 连接 WorkBuddy 里的 **CNB** 与 **EdgeOne / EdgeOne Pages** 连接器（或网页端手动完成上面 1–5 步）
- [ ] 改 DNS 指向 EdgeOne
