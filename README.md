# 🎯 Competitor Radar

> AI 驱动的竞品监控系统 —— 每天 9 点自动推送洞察报告

[![Demo](https://img.shields.io/badge/🚀_在线预览-创作过程-red?style=flat-square)](https://matrix-wong-ai.github.io/competitor-radar/)
[![OpenClaw](https://img.shields.io/badge/🦞_Powered_by-OpenClaw-black?style=flat-square)](https://openclaw.ai)
[![License](https://img.shields.io/badge/📄_License-MIT-blue?style=flat-square)](LICENSE)

---

## 📖 这是什么？

**竞品雷达**是一个 [OpenClaw](https://openclaw.ai) Skill，自动监控 AI Agent 领域的核心竞品动态。

**核心场景：**
- 产品经理每天需要追踪竞品更新
- 手动查看多个官网、博客、Release Notes 太耗时
- 容易遗漏关键信息，且难以形成系统性洞察

**解决方案：**
让 AI 代理自动完成搜索、分析、总结，每天早上 9 点推送结构化简报到你手中。

**[👉 点击查看完整创作过程](https://matrix-wong-ai.github.io/competitor-radar/)**

---

## ✨ 核心能力

```
┌─────────────────────────────────────────┐
│         每天早上 9:00 自动执行           │
└─────────────────────────────────────────┘
                    ↓
┌─────────────┐  ┌─────────────┐  ┌─────────────┐
│  动态监控    │  │  商业洞察    │  │  产品机会    │
│  (发生了什么) │  │  (意味着什么) │  │  (应该怎么做) │
└─────────────┘  └─────────────┘  └─────────────┘
        ↓                ↓                ↓
┌─────────────────────────────────────────┐
│     📬 推送到飞书 / 其他 IM 平台          │
└─────────────────────────────────────────┘
```

### 三层信息架构

| 层级 | 内容 | 价值 |
|:---|:---|:---|
| **🔍 动态监控** | 竞品最新更新、发布、功能变更<br/>附带原文链接，来源可验证 | 信息不遗漏<br/>权威可信 |
| **💡 商业洞察** | 竞品战略意图、市场定位变化<br/>竞争格局影响分析 | 理解背后的逻辑<br/>把握趋势 |
| **🎯 产品机会** | 基于竞品动态的可执行建议<br/>短期跟进 + 中期策略 | 知道如何应对<br/>actionable |

---

## 🎯 监控对象（可配置）

### 默认监控

| 竞品 | 重点 | 信息源 |
|:---|:---|:---|
| **智谱 AI** | GLM 系列模型、API 能力、定价策略 | 官方文档、Release Notes |
| **OpenClaw** | 版本更新、技能生态、安全策略 | GitHub、官方博客 |
| **Claude** | 新模型发布、企业功能、Constitution | Anthropic 官方渠道 |

### 可扩展

支持添加任意竞品，只需配置：
- 搜索关键词
- 重点监控页面
- 信息源优先级

---

## 🚀 快速开始

### 1. 安装

```bash
# 下载本仓库的 competitor-radar.skill 文件
# 然后安装
openclaw skills install ./competitor-radar.skill
```

### 2. 配置环境变量

```bash
# Tavily API Key 用于搜索
export TAVILY_API_KEY="tvly-your-api-key"
```

### 3. 运行测试

```bash
# 生成今日简报
openclaw agent --message "运行竞品雷达"

# 或监控特定竞品
openclaw agent --message "监控智谱的最新动态"
```

### 4. 配置定时任务（自动推送）

```bash
openclaw cron add \
  --name "竞品雷达日报" \
  --cron "0 9 * * 1-5" \
  --message "运行竞品雷达生成简报并发送到飞书" \
  --channel feishu \
  --to "your-user-id" \
  --announce
```

---

## 📋 输出示例

```markdown
📊 竞品动态雷达 - 2026-03-25

## 一、动态监控

**智谱 GLM-5-Turbo 发布**
- 来源：[智谱官方文档](https://docs.bigmodel.cn/...)
- 时间：2026-03-15
- 核心：面向 OpenClaw 场景优化的基座模型

**OpenClaw 重大更新**
- 来源：[机器之心](https://news.qq.com/...)
- 时间：2026-03-24
- 核心：ClawHub 成为默认插件入口

## 二、商业洞察

**趋势：模型厂商向下游延伸**
智谱不再只卖 API，而是深度绑定 Agent 框架...

## 三、产品机会

**短期**：评估 GLM-5-Turbo 在内部任务中的效果
**中期**：关注生态合作机会，申请早期接入
```

---

## 🛠 技术架构

```
OpenClaw Skill Framework
│
├── Tavily Search API          # AI 优化搜索，高质量信源
├── LLM (Claude/Kimi/etc)      # 内容理解、洞察生成
├── Cron Scheduler             # 定时任务调度
└── Feishu/IM Bot              # 消息推送
```

### 工作流程

```
每天 09:00 (工作日)
    ↓
触发定时任务
    ↓
Tavily 搜索 "智谱/OpenClaw/Claude 最新动态"
    ↓
LLM 分析搜索结果
    ↓
生成结构化简报（动态+洞察+机会）
    ↓
推送到飞书私聊
```

---

## 📁 文件结构

```
competitor-radar/
├── README.md                    # 本文件
├── index.html                   # 创作过程展示页 ⭐
├── competitor-radar.skill       # 可安装的技能包
├── SKILL.md                     # Skill 定义文档
├── scripts/
│   ├── search_competitor.sh     # 搜索脚本
│   └── generate_report.sh       # 报告生成
└── references/
    └── competitors.md           # 竞品配置
```

---

## 🔄 迭代历程

本项目采用敏捷迭代方式，三轮打磨：

| 轮次 | 反馈 | 改进 |
|:---|:---|:---|
| **v0.1** | — | MVP：基础搜索 + 简单汇总 |
| **v0.2** | 「每条动态必须有网站来源」 | ➕ 添加来源链接验证 |
| **v0.3** | 「要有商业洞察」 | ➕ 添加策略分析层 |
| **v1.0** | 「要有产品机会」 | ➕ 添加 actionable 建议 |

**完整创作过程记录：** [在线可视化展示](https://matrix-wong-ai.github.io/competitor-radar/)

---

## 💡 设计理念

```
把重复的工作交给 AI
把时间留给思考
```

### 核心原则

1. **来源可验证** — 每条动态必须附原文链接
2. **洞察有支撑** — 商业分析必须基于事实数据
3. **建议可执行** — 产品机会必须具体 actionable
4. **交付自动化** — 定时推送，无需人工干预

---

## ⚙️ 高级配置

### 自定义监控竞品

编辑 `references/competitors.md`：

```markdown
### 新品名
**关键词**：关键词1、关键词2、关键词3
**重点页面**：
- https://example.com/changelog
- https://example.com/blog
**监控重点**：新功能发布、API变更、定价调整
```

### 修改定时频率

```bash
# 查看现有任务
openclaw cron list

# 编辑任务（修改时间、输出渠道等）
openclaw cron edit <task-id>
```

### 更换输出渠道

支持：飞书、Telegram、Discord、Slack 等

```bash
# Telegram 示例
openclaw cron add \
  --channel telegram \
  --to "@your_channel" \
  ...
```

---

## 🤝 贡献指南

欢迎提交 Issue 和 PR：

- **新竞品** — 添加行业相关竞品监控
- **分析模板** — 改进洞察和机会的生成逻辑
- **输出格式** — 优化简报结构和可读性
- **Bug 修复** — 报告和修复问题

### 开发流程

```bash
# 1. 克隆仓库
git clone https://github.com/Matrix-WONG-AI/competitor-radar.git

# 2. 修改 SKILL.md 或脚本

# 3. 打包测试
openclaw skills package ./competitor-radar

# 4. 本地安装测试
openclaw skills install ./competitor-radar.skill

# 5. 提交 PR
```

---

## 📄 License

[MIT](LICENSE) © Matrix WONG

---

## 🙏 致谢

- [OpenClaw](https://openclaw.ai) — 强大的开源 AI Agent 框架
- [Tavily](https://tavily.com) — AI 优化的搜索 API
- Matrix — 提出需求并参与全程打磨

---

> **Less, but better.** — Dieter Rams