# Codex 网络配置与连接命令

## 全局网络与沙箱参数

- `codex --sandbox <SANDBOX_MODE>`：挑选运行会话时的沙箱策略。`read-only` 和 `workspace-write` 会禁用出站网络（默认策略），`danger-full-access` 解除网路与磁盘限制，适合在外部已经隔离的环境使用。
- `codex -a <APPROVAL_POLICY>`：控制命令执行审批模式。`untrusted` 仅允许白名单命令，`on-request` 由代理自行决定是否请求放权，`on-failure` 在沙箱失败时才请求，`never` 完全不请求人工批准。
- `codex --full-auto`：快捷方式，相当于 `-a on-failure --sandbox workspace-write`。通常用于需要快速自动化但仍接受默认的“禁用网络+工作区可写”沙箱配置。
- `codex --dangerously-bypass-approvals-and-sandbox`：完全关闭沙箱与审批，直接在本机执行（含网络访问），仅在明确受控环境下启用。
- `codex --search`：为代理开启原生联网搜索工具，允许在任务中发起 HTTP 搜索请求。
- `codex -c sandbox_permissions=["disk-full-read-access"]`：通过配置覆盖为沙箱添加额外权限；配置项保存在 `~/.codex/config.toml`，复杂场景可直接编辑该文件或用多个 `-c` 覆盖项组合。

示例：

```bash
codex --sandbox read-only --search "检查线上 API 状态"
codex -a on-request --sandbox danger-full-access -c shell_environment_policy.inherit=all
```

## 认证与凭据管理

- `codex login`：启动交互式登录流程；支持浏览器弹窗或设备码。
- `codex login --with-api-key`：通过标准输入读取密钥，适合 CI/CD 环境或脚本。
- `codex login --device-auth`：在无法打开浏览器时使用设备码登录。
- `codex login status`：查看当前账户、模型配额和登录有效期，排查鉴权失败。
- `codex logout`：删除本地凭据文件（通常位于 `~/.codex/credentials.json`），断开与 Codex 云服务的连接。

## 云端任务与远程服务

- `codex cloud`：列出 Codex Cloud 任务并应用到本地仓库。结合 `-c model="o3"` 等参数可以在云侧切换模型或沙箱策略。
- `codex exec --sandbox danger-full-access <PROMPT>`：在无沙箱场景下运行一次性任务（谨慎使用），适合需要访问内网或公网的非交互式脚本。
- `codex resume --last --sandbox workspace-write`：延续最近一次会话，保持原有网络限制；配合 `--search` 控制是否允许联网。
- `codex apply <TASK_ID>`：从 Codex Cloud 下载最新 diff 并应用，需要保持登录。

## MCP 与实验性服务

- `codex mcp list|get|add|remove`：管理注册的 MCP（Model Context Protocol）服务器条目，用于与外部工具或服务建立连接。
- `codex mcp login <SERVER>`：通过 OAuth 与指定 MCP 服务器建立授权会话，成功后 Codex 可以调用该服务器提供的联网能力。
- `codex mcp logout <SERVER>`：撤销存储的 OAuth 凭据，阻止后续接入。
- `codex mcp-server`：运行 Codex 自带的 MCP 服务器（stdio 传输），在本地暴露工具供其他客户端调用。
- `codex app-server`：启动实验性应用服务器，便于在局域网内共享 Codex 交互（注意检查操作系统防火墙与端口策略）。

示例：

```bash
codex mcp add my-search --url https://example.com/mcp --api-key $MCP_KEY
codex mcp login my-search
codex exec -c experimental_use_rmcp_client=true --search "Gather latest release notes"
```

## 沙箱调试与诊断

- `codex sandbox linux --full-auto "<COMMAND>"`：在 Landlock+seccomp 沙箱中执行命令，默认禁用网络，仅允许写入 `cwd` 与 `TMPDIR`。
- `codex sandbox macos "<COMMAND>"`：在 Seatbelt 沙箱里运行命令，适合验证 macOS 环境的权限限制。
- `codex sandbox --help`：快速查看各平台沙箱的权限说明和自定义参数。
- `codex completion bash`：生成补全脚本，可在 shell 中一键补齐网络/沙箱参数，减少误配。
- `codex --version`：确认 CLI 版本，排查因版本差异导致的沙箱策略不兼容问题。

## 常见排查步骤

1. 使用 `codex login status` 确认凭据有效；若失效，重新执行 `codex login`。
2. 检查全局配置：`cat ~/.codex/config.toml` 或通过 `codex -c key=value` 临时覆盖后重试。
3. 在沙箱中复现场景：`codex sandbox linux "<COMMAND>"`，验证是否触发网络拦截。
4. 必要时启用 `--search` 或 `--dangerously-bypass-approvals-and-sandbox`（仅在可信环境）来判断是否为沙箱限制所致。
