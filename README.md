# health-reminder-dist

打工人健康助手发布仓库。**承载 Windows 安装包与自动更新 exe 资产（GitHub Releases 充当免费 CDN），不托管源码。**

## 结构

本仓库只放发布说明与更新记录；真正的二进制资产通过 **GitHub Releases** 上传，客户端自动更新从 `releases/download/v<版本>/health-reminder-windows.exe` 拉取。

| 仓库 | 托管 | 角色 |
|---|---|---|
| `health-reminder` | （开发） | 源码 + 治理文档 |
| `health-reminder-server` | Gitee | 服务器代码 + `server/version.json`（热配置） |
| `health-reminder-dist` | GitHub Releases | exe / 安装程序大文件（自动更新 CDN 源） |

## 发布操作（发版脚本 tools/publish.py 已半自动化）

1. 打包：`python tools/publish.py --version x.y.z --changelog "..."` → `dist/打工人健康助手.exe`
2. 上传资产：新建 Release `tag vx.y.z`，拖入二进制。**资产名必须英文**（如 `health-reminder-windows.exe`），中文名网页上传会被强制改成 `default.exe`。
3. 同步 `server/version.json` 到 `health-reminder-server` 并推 Gitee。
4. 服务器热生效：拉取 + 重启服务（version.json 为热配置）。

## 版本记录

- **v1.1.0**：体检站业务保护（方案B，业务编译进 _ws_core.pyd）；对应 `health-reminder-server` 的 `server/version.json`。