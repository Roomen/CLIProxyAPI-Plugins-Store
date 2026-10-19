# Roomen CLIProxyAPI Plugins Store

自用的 CLIProxyAPI 插件来源，遵循[官方插件仓库](https://github.com/router-for-me/CLIProxyAPI-Plugins-Store)的 schema v1 格式，收录 [Live Routes](https://github.com/Roomen/cpa-live-routes) 与 [Harness Usage](https://github.com/Roomen/cpa-harness-usage)。

## 使用

来源地址（**registry.json 直链**）：

```text
https://raw.githubusercontent.com/Roomen/CLIProxyAPI-Plugins-Store/main/registry.json
```

在 CPA 的 `config.yaml` 中合并以下配置（已有 `plugins` 节点时不要重复创建）：

```yaml
plugins:
  enabled: true
  store-sources:
    - "https://raw.githubusercontent.com/Roomen/CLIProxyAPI-Plugins-Store/main/registry.json"
```

保存后刷新管理面板的插件商店，找到 **Live Routes** 或 **Harness Usage** 并安装、启用。手动修改配置后，若当前 CPA 未热加载配置，请重启 CPA。内置官方源始终保留，本来源作为附加源加载。使用支持 `plugins.store-sources` 的 CPA 版本。

## 收录插件

| ID | 插件 | 仓库 |
| --- | --- | --- |
| `live-routes` | Live Routes：实时请求路由看板 | [Roomen/cpa-live-routes](https://github.com/Roomen/cpa-live-routes) |
| `harness-usage` | Harness Usage：本地 Claude Code / Codex / OpenCode 按日用量与估算费用 | [Roomen/cpa-harness-usage](https://github.com/Roomen/cpa-harness-usage) |

本仓库只维护 `registry.json` 中的插件元数据，不托管二进制包。安装包与 `checksums.txt` 均从插件仓库的最新 GitHub Release 获取，无需在此固定 `version` 或填写 `install`。

## 发布更新

在对应插件仓库发布新的正式 Release 即可；只要插件 ID 与仓库地址不变，本来源无需修改。Release 标签应为 `vX.Y.Z`，附件命名为：

```text
<pluginID>_<version>_<goos>_<goarch>.zip
checksums.txt
```

其中 `<version>` 不含前导 `v`。每个平台 ZIP 的根目录须包含 `<pluginID>.dylib`、`<pluginID>.so` 或 `<pluginID>.dll`，`checksums.txt` 使用 SHA-256 校验格式。

注意：`harness-usage` 当前不提供 `darwin/amd64` 构建（Go 共享库在 darwin/amd64 宿主存在 TLS 冲突），该平台安装会因缺少资产而失败。

---

Personal CLIProxyAPI plugin registry containing Live Routes and Harness Usage. Add the raw registry URL above to `plugins.store-sources`; the built-in official source stays enabled. Plugin versions and downloads are resolved from the plugin repository’s latest GitHub Release.
