# hermes-bot-crawler（网页爬取 Bot）

这是一个打包为 **Hermes Profile Distribution** 的网页爬取与结构化整理助手。它能够自动访问公开网页、处理动态渲染页面、提取正文与列表数据，并将结果整理为清晰的 Markdown 文档、对比表格或 CSV 文件，同时支持定时抓取任务。

## 功能特性

- **静态与动态网页抓取**：内置 `web`（`web_search` / `web_extract`）与 `browser` 工具集，并挂载官方 `@playwright/mcp` 无头浏览器服务，兼顾速度与复杂 DOM 渲染。
- **结构化整理与落盘**：自动将散乱网页信息清洗为 Markdown 表格或 CSV 文件，附带来源 URL 与抓取时间戳。
- **定时采集调度**：启用 `cronjob` 工具集，支持通过自然语言设定周期性网页监测与增量汇总。
- **内存友好**：为 Playwright MCP 配置了 15 分钟空闲自动回收（`idle_timeout_seconds: 900`），避免 Chromium 进程长期驻留消耗内存。
- **合规边界**：严格遵守 `robots.txt`，不抓取需要登录的隐私数据，不绕过付费墙。

## 本机前置依赖

在安装和使用本 Bot 前，请确保本机已安装：

1. **Node.js（含 `npx`）**：用于启动 `@playwright/mcp@latest` 服务（建议 Node.js 18+）。
   ```bash
   node --version
   npx --version
   ```
2. **Playwright 浏览器内核**（首次运行 `npx @playwright/mcp@latest` 时会自动按需准备，也可提前执行 `npx playwright install chromium`）。

## 安装命令

使用 Hermes CLI 一键安装本 Bot：

```bash
hermes profile install https://github.com/zzyxiangnian-star/hermes-bot-crawler --yes --alias
```

安装完成后，可直接启动对话：

```bash
hermes -p crawler chat
# 若使用了 --alias，也可以直接运行：
crawler chat
```

后续如需拉取本仓库的最新配方更新（不会覆盖你的本地记忆和模型配置）：

```bash
hermes profile update crawler
```

## 推荐搭配的 Hermes 技能（Skills）

本仓库不包含自定义 Skill 代码。安装后，推荐直接使用或从 Hermes 内置/技能市场启用以下官方技能以获得更佳体验：

- `web/blocked-page-recovery`（内置）：当抓取遇到 403/429 或反爬拦截时，采用合规的恢复与替代信息源策略。
- `productivity/product-price-monitor`（内置）：监控商品、航班或列表价格变动并触发提醒。
- `research/competitor-news-monitor`（内置）：定期跟踪指定公司或站点的动态资讯并生成带引用的摘要。
- `research/grounded-citations`（内置）：确保输出的表格与报告附带可核查的原始链接引用。

可通过以下命令查看或管理技能：

```bash
hermes -p crawler skills list
```
