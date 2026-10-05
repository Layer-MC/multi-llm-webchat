# multi-llm-webchat

**语言 / Language**: [English](README.md) · [中文](README.zh-CN.md)

---

A single-file web chat that works with any OpenAI-compatible API.

Type in a Base URL and an API Key, it auto-discovers the available models, and lets you pick one to chat with. No install, no build, no server. Just open the file.

## Highlights

- Multi-provider. Works with DeepSeek, Moonshot (Kimi), Qwen, Doubao, Zhipu GLM, MiniMax, SenseNova, OpenRouter, OpenAI, or any custom endpoint.
- Tool calling. The assistant can call web_search, web_browse, calculator, and get_time directly from the browser. Each call is visualized inline with its arguments and result.
- Bring your own Key. The Key is only sent to the Base URL you chose, in an Authorization Bearer header. It is stored in your own browser's localStorage. This repository contains no hardcoded credentials.
- One file. The entire app is a single chat.html. Host it on GitHub Pages, Netlify Drop, or Cloudflare Pages, or serve it from a local HTTP server.

## Features

- Auto-discovers models via GET /v1/models.
- Per-model "test" button to verify availability without burning context.
- Model choice, Base URL, and API Key are all persisted locally so returning users skip setup.
- Visualized tool-call trace. Every call shows arguments and result in an inline block.
- History persisted to localStorage across page reloads.
- Dark theme, mobile-responsive, about 36 KB total.

## Supported providers

The following presets ship with the app. Any additional OpenAI-compatible endpoint works through the "Custom" preset.

| Provider | Base URL |
|---|---|
| SenseNova | https://token.sensenova.cn/v1 |
| DeepSeek | https://api.deepseek.com/v1 |
| Moonshot (Kimi) | https://api.moonshot.cn/v1 |
| Qwen (Aliyun) | https://dashscope.aliyuncs.com/compatible-mode/v1 |
| Zhipu GLM | https://open.bigmodel.cn/api/paas/v4 |
| Doubao (Volc) | https://ark.cn-beijing.volces.com/api/v3 |
| MiniMax | https://api.minimax.chat/v1 |
| OpenRouter | https://openrouter.ai/api/v1 |
| OpenAI | https://api.openai.com/v1 |

Adding a new provider is as simple as appending an entry to the PROVIDERS array at the top of the script.

## Getting started

There is no build step. Two ways to run:

### Host it online (recommended)

Upload chat.html to a static host such as GitHub Pages, Netlify Drop, or Cloudflare Pages, then share the URL. The recipient types in their own API Key on first visit.

### Run locally

Any static file server works. Examples:

- Python: run python3 -m http.server 8000, then open http://localhost:8000/chat.html
- Node: run npx serve, then open the URL printed in the terminal
- PHP: run php -S localhost:8000

Do not open the file directly with the file:// scheme. The browser will block the cross-origin requests to the API provider and the app will fail with Failed to fetch.

## Security model

- No middleman. The API Key is only sent to the Base URL you chose, in an Authorization Bearer header. It is never logged, never written to any third-party service.
- Key storage. The Key lives in localStorage under the ai_web_chat_config key, on your own device only. Clearing the browser cache removes it.
- Cross-origin. The provider's endpoint must return Access-Control-Allow-Origin matching your hosting origin. A few providers restrict CORS. Use a proxy or a hosted setup if you hit issues.
- Tool results. web_search uses DuckDuckGo Lite and web_browse uses r.jina.ai as a reader proxy. Both are third-party services. You can inspect or replace their implementations in the runTool function.

## Contributing

Issues and pull requests are welcome. If you add a new provider preset, please also update the table above so users can find it.

## License

MIT. See LICENSE for details.