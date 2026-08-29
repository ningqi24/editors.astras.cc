# editors.astras.cc

> **⚠ 免责声明：本仓库为 AstraEditor 非官方镜像定制版，与 AstraEditor 官方团队无关。**
> **本项目仅供学习交流使用，严禁用于商业用途。AstraEditor 的所有版权归其原作者团队所有。**

## 项目简介

本仓库是 [AstraEditor](https://github.com/AstraEditor/astraeditor.github.io) 的非官方镜像定制版，部署于 [editors.astras.cc](https://editors.astras.cc)。

通过 CDN 加速、视频压缩、懒加载等技术优化访问速度。编辑器正式版自动跳转至官方网站，快照版由本站直接提供。

## 功能特性

- **镜像加速**：首页加载量从 ~16MB 降至 ~460KB（视频懒加载 + VP9 压缩，总体积降 91%）
- **CDN 回退**：更新日志通过 jsDelivr CDN 加载，5 秒超时后回退本地 `changelog.json`
- **移动端适配**：viewport meta + 响应式 CSS（768px / 480px 两档断点）
- **默认插件配置**：snapshot 编辑器内置 92 个插件的默认配置，首次访问自动初始化
- **全站非官方声明**：主页横幅 + 镜像加速描述区 + snapshot 页面右下角徽章 + online 重定向页说明
- **下载统一跳转**：所有下载入口直接跳转至 [download.astras.cc](https://download.astras.cc)
- **中英双语**：主页支持中文/英文切换

## 目录结构

| 路径 | 说明 | 访问地址 |
| --- | --- | --- |
| `index.html` | 主页（落地页、镜像加速描述、下载入口、更新日志） | [editors.astras.cc](https://editors.astras.cc/) |
| `online/` | 正式版编辑器（11 个页面，全部重定向至官方网站） | [editors.astras.cc/online](https://editors.astras.cc/online) |
| `snapshot/` | 快照版编辑器（完整复刻原版，690+ 文件） | [editors.astras.cc/snapshot](https://editors.astras.cc/snapshot) |
| `d.html` / `download.html` | 下载站跳转页 | [editors.astras.cc/d](https://editors.astras.cc/d) |
| `changelog.json` | 更新日志数据（CDN 回退备源） | — |
| `css/style.css` | 主页样式（含响应式媒体查询） | — |
| `js/main.js` | 主页脚本（下载跳转、更新日志、视频懒加载、3D 效果） | — |
| `snapshot/js/default-addon-settings.js` | snapshot 编辑器默认插件配置（92 个插件） | — |
| `CNAME` | 自定义域名配置 | — |
| `sitemap.xml` | 站点地图 | — |

### online/ 重定向页面

| 页面 | 跳转目标 |
| --- | --- |
| `editor.html` | editors.astras.top/online/editor |
| `index.html` | editors.astras.top/online |
| `addons.html` | editors.astras.top/online/addons |
| `credits.html` | editors.astras.top/online/credits |
| `embed.html` | editors.astras.top/online/embed |
| `fullscreen.html` | editors.astras.top/online/fullscreen |
| `privacy.html` | editors.astras.top/online/privacy |
| `upload.html` | editors.astras.top/online/upload |
| `why.html` | editors.astras.top/online/why |

### snapshot/ 编辑器

完整复刻原仓库 `AstraEditor/astraeditor.github.io` 的 snapshot 版本，包含：

- 完整编辑器（editor.html、player、fullscreen、embed 等）
- 全部插件脚本（60+ addon entry）
- Monaco Editor 多语言支持（70+ 语言模块）
- 17 种语言本地化文件
- 背景图库、造型库、声音库、角色库
- 自定义默认插件配置（`default-addon-settings.js`）
- 全页面非官方镜像声明徽章

## 技术优化详情

### 视频懒加载 + 压缩

| 视频 | 压缩前 | 压缩后 | 降幅 |
| --- | --- | --- | --- |
| addons.webm | 7.0 MB | 736 KB | 90% |
| custom.webm | 6.6 MB | 604 KB | 91% |
| paint.webm | 2.2 MB | 112 KB | 95% |

- `<video>` 标签使用 `data-src` + `preload="none"`，首屏不加载视频
- 滚动到视口时通过 `loadVideoSrc()` 按需加载
- VP9 + 720p 重编码，画质满足展示需求

### 更新日志加载

- 主源：`cdn.jsdelivr.net`（jsDelivr CDN，国内有节点）
- 备源：本地 `./changelog.json`（同源加载）
- 5 秒超时自动切换（AbortController）
- 兼容 `note` / `notes` 两种字段名

### 默认插件配置机制

`snapshot/js/default-addon-settings.js` 在编辑器加载前执行：

1. 检查 `localStorage['tw:addons']` 是否已存在
2. 若不存在，用配置文件初始化（92 个插件的启用状态 + 参数）
3. 用户在编辑器中修改的设置保存在 localStorage，不被覆盖
4. 清除浏览器数据后重新用配置文件初始化

## 权利声明

- 本项目为 **AstraEditor 非官方镜像定制版**，与 AstraEditor 官方团队及 TurboWarp 项目组均无关联。
- 本项目基于 TurboWarp 构建，仅用于学习交流目的，不用于任何商业用途。
- AstraEditor 及相关商标、版权的所有权归原作者团队所有。
- 如有侵权，请联系本仓库所有者删除。

## 致谢

- [AstraEditor](https://github.com/AstraEditor/astraeditor.github.io) — 原项目
- [TurboWarp](https://github.com/TurboWarp) — 编辑器内核
- [jsDelivr](https://www.jsdelivr.com/) — CDN 服务
