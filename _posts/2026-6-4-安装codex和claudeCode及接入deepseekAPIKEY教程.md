---
tags: codex claudeCode deepseekAPI CCswitch
title: 安装codex和claudeCode及接入deepseekAPIKEY教程
author: fox
---

## 一、codex claudeCode deepseekAPI CCswitch解释

1. Codex：AI Agent工具，直接和用户对话、交互，内置许多插件，拥有操作浏览器、操作电脑的强大能力。

2. 终端里的 AI 编程助手，能直接读代码、改文件、跑命令，像 ChatGPT 但绑定在你的项目里干活。有命令行和客户端两种运行模式

2. DeepSeek API：API供应商，由于Codex费用较高，大量使用的话DeepSeek API更加实惠，因此才需要让Codex接入DeepSeek API。

3. CC Switch：虽然直接修改codex的配置文件也可以让Codex用上DeepSeek API，但是这样改来改去非常麻烦，CC Switch可以帮我们实现一键切换的便捷功能。

-  CC Switch还提供了路由转换的功能，需要升级到最新版本，由于codex和deepseek模型两者无法直接对接，根本原因是接口协议不一致，由CC Switch提供路由转换，将codex的API请求转换格式通过deepseek的官方APIKEY发送，充当中转站的作用。

- CC Switch下载 ：https://github.com/farion1231/cc-switch/releases

## 二、codex

###  2.1 codex下载

1. 下载并安装官方 Codex 客户端，完成账号登录。

2. 首次登录后，后台完全退出 Codex，避免配置冲突。

### 2.2 CC Switch配置

1. 打开后顶部选择OpenAI，选择+添加新的供应商，选择deepseek,需要填API-KEY和请求地址，要选开启本地路由

```
sk-proxy-local-61855f460d6b1bf9ac8ba19cc764e0b576c85483232b9f6f

https://platform.deepseek.com
```

2. 去获取 DeepSeek API Key，首先打开 DeepSeek 开放平台：https://www.deepseek.com/，充钱后进入 API Keys → 点击创建 API Key，命名后生成密钥。注：API Key 只显示一次，立即复制保存，丢失需重建。

3. 返回CC switch配置，模型选择deepseek pro(擅长深度思考)，deepseek flash v4(响应更快)配好点击保存，然后返回启动这个API-KEY

4. 再打开codex就能通过API-KEY进入了

## 三、Claude Code

### 3.2 安装前提

1. 需要 Node.js 18.0 及以上版本。（使电脑能够在本地运行javascript代码）
2. npm（一个可以自动下载依赖的包，相当于应用商店，能够下载该项目所需要的依赖）

```bash
node --version   # 确认版本
npm --version
```

### 3.3 安装 Claude Code


*指定目录安装

```bash
npm install @anthropic-ai/claude-code --prefix D:\Claude Code\npm-global
```

之后将 `D:\Claude Code\npm-global\node_modules\.bin` 添加到系统 PATH。

### 3.4 CC Switch配置（连接DeepSeek）

Claude Code 原生使用 Anthropic 的 API（Messages API 格式），而 DeepSeek 使用 OpenAI 兼容格式。CC Switch 作为中转翻译层解决了这个问题。

**架构流程：**

```
Claude Code (Anthropic格式)
    ↓ ANTHROPIC_BASE_URL 指向 CC Switch
CC Switch (路由转换)
    ↓ 翻译为 OpenAI 格式
DeepSeek API
```

**配置步骤：**

1. 打开 CC Switch，顶部选择 Claude Code，添加 DeepSeek 供应商（以后同第二章步骤）。


-  注：`ANTHROPIC_API_KEY` 填 CC Switch 提供的代理 key 即可，实际转发时 CC Switch 会用你配置的 DeepSeek API Key。

4. 启动 Claude Code：
- 在cmd输入
```bash
claude
```

### 3.5 基本用法

**交互模式（默认）：**

```bash
claude
```

进入对话界面，可以直接提问、让它改代码、执行命令。

**管道模式（非交互）：**

```bash
claude -p "解释一下这个项目的结构"
```

适合脚本调用或快速问答。

**指定模型：**

```bash
claude --model sonnet
```

### 3.6 模型选择建议

| DeepSeek 模型 | 特点 | 适用场景 |
|:---|:---|:---|
| deepseek-chat | 通用对话模型 | 日常编码辅助 |
| deepseek-reasoner | 深度推理模型 | 复杂问题分析 |

### 3.7 常用命令

1. /compact 压缩当前对话，将冗余细节总结为简短摘要，释放上下文空间。

2. /clear 完全清除对话

3. shift+Tab ，切换审查形式






