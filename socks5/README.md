# QPlayer + SOCKS5（Windows 自动构建）

这个 fork 的 `master` 分支跟随上游 [TIMER-err/qplayer](https://github.com/TIMER-err/qplayer)，额外只有两样东西：

- `socks5/patches/*.patch`：给 QPlayer 加 GitHub 专用的 SOCKS5 代理（设置 → 关于 → 网络 → SOCKS5 代理）。
- `.github/workflows/socks5-release.yml`：每 6 小时检查上游是否有新的正式发布；有的话在上游源码上打补丁、编译 Windows 版，并在本仓库发布 `<版本>-socks5`（安装包 + 便携 zip）。

编出来的程序会到**本仓库**检查更新，所以在应用里点"更新"装上的仍是带补丁的版本。

## SOCKS5 设置

- 写法：`127.0.0.1:7890`、`[::1]:1080`、`用户名:密码@主机:端口`，可带 `socks5://` / `socks5h://` 前缀；留空关闭。
- 只代理 GitHub（github.com、*.githubusercontent.com）：检查更新、下载更新、插件目录与安装。听歌等其他请求不经过它。
- 域名由代理解析；代理不可用时回退到内置的下载加速镜像。

## 维护

- 补丁打不上（上游改了同一处代码）时，工作流会在本仓库开一个 Issue，附上失败日志。
- 手动重编：Actions → SOCKS5 Windows build → Run workflow（可指定上游标签、强制重建）。
- 修改 `socks5/` 下的文件并推送到 `master` 会自动重编当前版本。
