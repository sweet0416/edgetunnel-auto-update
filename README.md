# edgetunnel 自动更新

这个仓库用于部署 Cloudflare Pages 版本的 edgetunnel：根目录的 `_worker.js` 是 Pages 的 Worker 入口。

`.github/workflows/sync-edgetunnel.yml` 每周一触发一次，但只会在固定的 21 天周期到达时下载上游 `cmliu/edgetunnel` 的 `_worker.js`。只有源码实际变化时才会创建提交，因此 Cloudflare Pages 也只会在有新版时重新部署。

## 连接 Cloudflare Pages

在 Cloudflare Pages 项目 `edison` 的“设置 → 构建”中连接这个 GitHub 仓库，生产分支选择 `main`；框架预设选“无”，构建命令留空，构建输出目录使用 `/`。保留现有 `ADMIN` 环境变量与 `KV` 绑定。

首次连接后，Cloudflare 会从 `main` 自动创建生产部署。以后更新由 GitHub Actions 提交后自动触发。
