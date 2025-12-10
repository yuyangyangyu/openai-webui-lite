# OpenAI WebUI Lite - 自部署的 OpenAI API 代理服务

[![Deploy to Deno Deploy](https://img.shields.io/badge/Deploy%20to-Deno%20Deploy-00ADD8?style=flat-square&logo=deno)](https://dash.deno.com/)
[![Deploy to Cloudflare Workers](https://img.shields.io/badge/Deploy%20to-Cloudflare%20Workers-orange?style=flat-square&logo=cloudflare)](https://workers.cloudflare.com/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](#license)
[![OpenAI API](https://img.shields.io/badge/Powered%20by-OpenAI%20API-412991?style=flat-square&logo=openai)](https://platform.openai.com/)

一个简单、轻量且功能强大的 OpenAI API 代理服务。基于 Deno Deploy / Cloudflare Workers 构建，无需服务器，只需一个域名和 API Key，即可免费部署属于你自己的 AI 助手。

---

## ✨ 核心特性

本项目致力于提供“养老级”的稳定体验，功能丰富且不失简洁：

- 🚀 **一键部署**：基于 Serverless 架构，免费、快速，无需维护服务器。
- 🔐 **安全访问**：支持**共享密码**（长期使用）和**演示密码**（限制频率），保护 API Key 不泄露。
- 💬 **流畅对话**：支持打字机流式响应 (Streaming)，体验丝滑。
- 🌐 **多模型支持**：兼容 OpenAI (GPT-4o/5)、Google (Gemini)、Claude、以及各类国产大模型（Qwen/DeepSeek等）。
- 🔍 **联网搜索**：集成 Tavily Search API，让 AI 能够获取实时网络信息作为回答依据。
- 🖥️ **全端适配**：精心设计的响应式 UI，完美适配桌面端和移动端。
- 📱 **PWA 支持**：支持渐进式 Web 应用 (PWA) 标准，移动端可将网页添加到桌面，获得原生 App 般的沉浸体验。
- 🛡️ **隐私优先**：聊天记录仅存储在浏览器本地 (IndexedDB)，不上传服务器。
- 📸 **一键分享**：自动生成精美的问答长图，方便社交分享。
- 🏷️ **智能管理**：根据对话内容自动生成标题，支持两轮对话（一问一答+追问），保持界面清爽。
- 🎨 **高度定制**：支持自定义网站标题、Favicon 图标以及模型列表。

## 🖼️ 界面预览

![openai_webui_lite](https://lsky.useforall.com/pixel/2025/11/03/690882cd3229a.png)
![openai_webui_lite-m](https://lsky.useforall.com/pixel/2025/11/03/690882cced092.png)

## 🚀 部署指南

### 准备工作
1. **API Key**: 准备好 OpenAI 或其他兼容服务的 API Key。
2. **域名**: 一个用于绑定的域名（推荐，可避免官方域名被墙）。

### ⚡ 一键部署

点击下方按钮，即可快速部署：

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/icheer/openai-webui-lite)

[![Deploy to Deno Deploy](https://img.shields.io/badge/Deploy%20to-Deno%20Deploy-000?style=for-the-badge&logo=deno)](https://dash.deno.com/new?url=https://github.com/icheer/openai-webui-lite&entrypoint=worker.js)

> 首次部署需要授权访问您的 GitHub 账户，系统会自动 Fork 本仓库并完成部署。

### 部署方式 A：GitHub 集成部署 (推荐)
> **特点**：支持自动更新，当您同步了上游代码后，服务会自动重新部署。
> **支持平台**：Deno Deploy / Cloudflare Workers

1. **Fork 项目**：将本项目 Fork 到您的 GitHub 仓库。
2. **创建项目**：
   - **Deno Deploy**: 登录 [Deno Dash](https://dash.deno.com/) -> New Project -> 选择 Fork 的仓库 -> Entry Point 选 `worker.js` -> Deploy。
   - **Cloudflare Workers**: 登录 [Cloudflare Dash](https://dash.cloudflare.com/) -> Workers & Pages -> Create application -> Connect to Git -> 选择仓库 -> Deploy。

### 部署方式 B：手动复制部署 (Playground)
> **特点**：最简单，无需 GitHub 账号，直接复制粘贴代码即可。
> **支持平台**：Deno Deploy / Cloudflare Workers

1. **复制代码**：复制本项目 `worker.js` 的全部内容。
2. **创建项目**：
   - **Deno Deploy**: 登录 [Deno Dash](https://dash.deno.com/) -> New Playground -> 粘贴代码 -> Save & Deploy。
   - **Cloudflare Workers**: 登录 [Cloudflare Dash](https://dash.cloudflare.com/) -> Workers & Pages -> Create Worker -> Edit code -> 粘贴代码 -> Deploy。

### 后续配置 (通用)
1. **绑定域名**：在项目设置中绑定您的自定义域名（自动申请 SSL）。
   - *Deno Deploy*: Settings -> Domains
   - *Cloudflare Workers*: Settings -> Triggers -> Custom Domains
2. **配置变量**：在项目设置中添加环境变量（见下文配置章节）。
   - *Deno Deploy*: Settings -> Environment Variables
   - *Cloudflare Workers*: Settings -> Variables

> **⚠️ 平台选择建议**：
> - **Deno Deploy**: 部署最简单，且节点 IP 通常未被 OpenAI/Google 封锁，可直接调用官方 API。
> - **Cloudflare Workers**: 全球节点更多，连接速度可能更快，但调用官方 API 可能需要自备代理或使用中转。
> 
> **⚠️ 中国大陆访问提示**：无论选择哪个平台，原生域名 (`*.deno.dev`, `*.workers.dev`) 在国内通常无法访问。请务必绑定自定义域名，并将域名托管在 Cloudflare，开启“小黄云”代理模式（CDN），即可在国内正常访问。

---

## ⚙️ 配置说明 (环境变量)

本项目主要通过环境变量进行配置，优先级高于代码中的默认值。

| 变量名 | 必填 | 说明 | 示例 |
| :--- | :---: | :--- | :--- |
| `SECRET_PASSWORD` | 否 | **共享密码**。设置后，用户需输入此密码才能使用您配置的 API Key。适合家人朋友共享。 | `my-secret-pwd` |
| `API_KEYS` | 否 | **API Key 池**。多个 Key 用英文逗号 `,` 分隔，系统会自动轮询使用，实现简单的负载均衡。 | `sk-key1,sk-key2` |
| `MODEL_IDS` | **是** | **模型列表**。定义前端下拉框显示的模型。支持 `ID=显示名称` 格式。 | `gpt-4o,gemini-2.5-pro` |
| `API_BASE` | 否 | **接口地址**。默认为 `https://api.openai.com`。如使用中转服务需修改此项。 | `https://api.openai.com` |
| `TAVILY_KEYS` | 否 | **联网搜索 Key**。配置后前端会出现“联网搜索”选项。获取地址：[tavily.com](https://tavily.com/) | `tvly-xxxx` |
| `TITLE` | 否 | **网站标题**。自定义浏览器标签页标题。 | `我的 AI 助手` |
| `DEMO_PASSWORD` | 否 | **演示密码**。用于公开演示，有频率限制。 | `demo123` |
| `DEMO_MAX_TIMES_PER_HOUR` | 否 | 演示密码每小时最大调用次数，默认 15。 | `20` |

### 🔌 常见服务商配置参考

| 服务商 | API_BASE | API_KEYS 示例 | MODEL_IDS 示例 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenAI** | `https://api.openai.com` | `sk-proj-xxx` | `gpt-4o,gpt-4o-mini,o1-preview` | 推荐 Deno 部署 |
| **Gemini** | `https://generativelanguage.googleapis.com` | `AIzaSyxxx` | `gemini-2.5-pro,gemini-2.5-flash` | 推荐 Deno 部署 |
| **心流 AI** | `https://apis.iflow.cn` | `sk-xxx` | `qwen3-max,deepseek-v3` | 国产模型聚合，Cloudflare 部署即可 |
| **OpenRouter** | `https://openrouter.ai/api` | `sk-or-xxx` | `anthropic/claude-sonnet-4.5` | 聚合平台 |
| **DeepSeek** | `https://api.deepseek.com` | `sk-xxx` | `deepseek-chat,deepseek-coder` | 国产之光 |

> **💡 资源推荐**：如果您需要免费且稳定的国产大模型 API（如 Qwen, DeepSeek），推荐尝试 [心流 AI](https://iflow.cn/?invite_code=vNEjKzbSTbhgWooCw15Bsw%3D%3D&open=setting)，官方宣称 API 永久免费（但 API Key 有效期为7天，过期后需手动重置新 Key），支持 Cloudflare Workers 稳定调用。

---

## 📚 使用指南

### Web 界面使用
1. **访问**：打开您部署的域名。
2. **认证**：
   - 如果配置了 `SECRET_PASSWORD`，输入密码即可使用服务器端的 API Key。
   - 如果未配置密码，您可以直接输入自己的 OpenAI API Key 使用。
3. **对话**：选择模型，输入问题。支持 Markdown、代码高亮。
4. **功能**：
   - **联网搜索**：勾选后，AI 会先搜索网络信息再回答。
   - **追问**：一问一答后，支持一次追问，保持上下文。
   - **分享**：点击右上角分享按钮，生成长图。

### API 代理使用
本项目也完全兼容 OpenAI API 格式，可作为 API 网关使用。

- **Endpoint**: `https://your-domain.com/v1/chat/completions`
- **Authorization**: `Bearer YOUR_SECRET_PASSWORD` (如果设置了密码) 或 `Bearer sk-xxx` (直接透传)

**curl 示例：**
```bash
curl https://your-domain.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-password" \
  -d '{
    "model": "gpt-4o",
    "messages": [{"role": "user", "content": "Hello!"}],
    "stream": true
  }'
```

---

## 🙋‍♂️ 常见问题 (FAQ)

**Q: 部署需要付费吗？**  
A: Deno Deploy 和 Cloudflare Workers 都有免费额度，一般个人使用完全够用。

**Q: 为什么我的自定义域名在国内无法访问？**  
A: Deno Deploy 和 Cloudflare Workers 的默认域名 (`*.deno.dev`, `*.workers.dev`) 在国内通常是被墙的。您必须绑定自己的域名。如果是 Deno Deploy，建议将域名 DNS 托管在 Cloudflare 并开启 CDN（橙色云朵），这样国内用户可以通过 Cloudflare 的节点访问。

**Q: 为什么只支持两轮对话（提问+追问）？**  
A: 这是一个设计选择。为了保持界面极简和 token 消耗可控，我们限制了上下文长度。对于大多数日常查询，两轮对话已经足够。如果需要长对话，建议在“角色设定”中输入背景信息。

**Q: 历史记录保存在哪里？会泄露吗？**  
A: 所有聊天记录仅存储在您浏览器的 **IndexedDB** 中，**绝不会**上传到任何服务器。这意味着如果您清除浏览器缓存或更换设备/浏览器，历史记录会丢失。

**Q: 为什么推荐 Deno Deploy 而不是 Cloudflare Workers？**  
A: 虽然两者都支持，但 Deno Deploy 的出口 IP 质量目前更好，很少被 OpenAI 或 Google 封锁，因此可以直接调用官方 API 而不需要额外的代理层。

**Q: 如何配置多个 API Key？**  
A: 在环境变量 `API_KEYS` 中填入多个 Key，用逗号分隔（如 `key1,key2,key3`）。程序会在每次请求时随机选择一个 Key，实现简单的负载均衡和防封号。

**Q: 演示密码 (Demo Password) 有什么用？**  
A: 如果你想把网站分享给陌生人体验，但又怕 API 被刷爆，可以设置 `DEMO_PASSWORD`。使用该密码登录的用户，每小时只能进行有限次（默认15次）对话。

**Q: 支持哪些模型？**  
A: 理论上支持所有兼容 OpenAI Chat Completion 接口的模型。您只需在 `MODEL_IDS` 环境变量中添加模型 ID 即可。

**Q: 如何开启联网搜索功能？**  
A: 在环境变量中配置 `TAVILY_KEYS`，然后在 Web 界面勾选"联网搜索"选项即可。联网搜索会为 AI 提供实时的网络信息作为上下文，提升回答的时效性和准确性。

**Q: Tavily API Key 如何获取？**  
A: 访问 [Tavily](https://tavily.com/) 注册账号并获取 API Key。可以配置多个 Key 用逗号分隔，系统会自动轮换使用。

**Q: 如何自定义界面标题和 Favicon？**  
A: 通过环境变量 `TITLE` 设置自定义标题，如 `TITLE=My AI Assistant`。标题会同时影响网页标题和 Favicon 的显示样式。

**Q: TITLE 环境变量是如何影响 Favicon 的？**  
A: `TITLE` 中包含 Gemini 或 Qwen 字样时（忽略大小写），网站 Favicon 会自动变为相应的模型 Logo，否则 Logo 默认为 ChatBot 的样式。

## 📄 许可证

本项目采用 [MIT License](LICENSE) 开源。欢迎 Fork 和 Star！
