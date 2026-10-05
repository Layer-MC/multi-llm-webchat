# multi-llm-webchat

**语言 / Language**: [English](README.md) · [中文](README.zh-CN.md)

---

单文件网页版 AI 对话工具，兼容任意 OpenAI API 规范的服务商。

输入 Base URL 和 API Key，自动获取可用模型列表，选一个即可开始对话。无需安装、无需构建、无需服务器，拿到就能用。

## 亮点

多服务商。支持 DeepSeek、Moonshot (Kimi)、通义千问、豆包、智谱 GLM、MiniMax、SenseNova、OpenRouter、OpenAI，或任意自定义端点。

工具调用。助手可以直接在浏览器里调用 web_search、web_browse、calculator、get_time。每次调用都会以内联块的方式可视化展示参数和结果。

自带 Key。Key 只会作为 Authorization Bearer 头，发到你选择的 Base URL。保存在你自己的浏览器 localStorage 里。本仓库不包含任何硬编码凭证。

单文件。整个应用就是一个 chat.html。可以托管到 GitHub Pages、Netlify Drop、Cloudflare Pages，也可以用本地 HTTP 服务器打开。

## 功能特性

自动获取模型列表。通过 GET /v1/models 端点。

每个模型独立测试。低成本的可用性验证按钮。

配置持久化。模型、Base URL、API Key 都会本地存储，老用户无需重复设置。

工具调用可视化。每次调用都展示参数和返回结果，内联展示。

对话历史保留。存在 localStorage 里，刷新页面不丢。

深色主题、移动端适配，整包约 36 KB。

## 支持的服务商

以下预设开箱即用。任何 OpenAI 兼容端点都可以走"自定义"预设。

| 服务商 | Base URL |
|---|---|
| SenseNova | https://token.sensenova.cn/v1 |
| DeepSeek | https://api.deepseek.com/v1 |
| Moonshot (Kimi) | https://api.moonshot.cn/v1 |
| 通义千问（阿里云） | https://dashscope.aliyuncs.com/compatible-mode/v1 |
| 智谱 GLM | https://open.bigmodel.cn/api/paas/v4 |
| 豆包（火山） | https://ark.cn-beijing.volces.com/api/v3 |
| MiniMax | https://api.minimax.chat/v1 |
| OpenRouter | https://openrouter.ai/api/v1 |
| OpenAI | https://api.openai.com/v1 |

添加新服务商只需要在脚本顶部的 PROVIDERS 数组里追加一项。

## 快速开始

没有构建步骤，两种方式运行：

### 托管到公网（推荐）

把 chat.html 上传到 GitHub Pages、Netlify Drop、Cloudflare Pages 之类的静态托管，然后把链接分享给别人。首次访问的人会自己填 API Key。

### 本地运行

任意静态文件服务器都行，例如：

Python 方式：在 chat.html 所在目录执行 python3 -m http.server 8000，然后浏览器打开 http://localhost:8000/chat.html

Node 方式：执行 npx serve，然后打开终端里显示的地址

PHP 方式：执行 php -S localhost:8000

不要用 file:// 协议直接双击打开。浏览器会拦截跨域请求，工具调用会全部报 Failed to fetch。

## 安全说明

无中间人。API Key 只会作为 Authorization Bearer 头，发到你选择的 Base URL。不会被记录日志，不会写到任何第三方服务。

Key 存储位置。Key 保存在浏览器 localStorage 里，键名 ai_web_chat_config，只在你自己的设备上。清浏览器缓存即可清除。

跨域限制。目标服务商的端点必须返回 Access-Control-Allow-Origin 匹配你的托管域名。少数服务商会限制 CORS，遇到这种情况可以用代理或者换托管方式。

工具结果来源。web_search 使用 DuckDuckGo Lite，web_browse 使用 r.jina.ai 作为阅读代理。两者都是第三方服务，也可以在 runTool 函数里替换实现。

## 参与贡献

欢迎 issue 和 PR。如果你添加了新的服务商预设，请顺便更新上面的表格，方便其他用户看到。

## 许可证

MIT。详见 LICENSE。