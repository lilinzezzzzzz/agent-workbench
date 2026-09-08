# OpenCode Config

本目录用于维护可复用的 OpenCode 配置。

后续新增配置时，请勿提交 API Key、token、cookie、真实服务凭证或其他机器私有信息。

## MCP 环境准备

- Playwright (`opencode.json` 中 `mcp.playwright`)：首次使用前需安装 Playwright 浏览器副本（macOS：`npx playwright install chromium`；Linux：`npx playwright install --with-deps chromium`）。Playwright 的浏览器二进制与系统 Chrome/Safari 相互独立，未安装时启动 MCP 会报 `Executable doesn't exist`。
