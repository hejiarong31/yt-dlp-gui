# 本地运行说明（Local Development Guide）

> 本文件由 `hejiarong31` 在 Fork 后补充，用于记录本机跑通原版的完整过程。
> 环境：Windows 11 · Python 3.13.17 · 无 Node.js / 无 Visual Studio / 无全局 Git

## 1. 环境要求

| 依赖 | 版本 | 说明 |
|---|---|---|
| Windows | 10 / 11 | 项目只支持 Windows |
| Python | 3.9 以上 | 本机实测 3.13.17 |
| customtkinter | ≥ 5.3.0 | GUI 框架 |
| pillow | ≥ 11.0.0 | 图标与缩略图处理 |
| requests | ≥ 2.32.0 | 更新检查 |
| packaging | ≥ 24.0 | 版本号比较 |
| pyinstaller | ≥ 6.0 | 仅打包时需要 |

`requirements.txt` 内容：

```
customtkinter>=5.3.0
pillow>=11.0.0
requests>=2.32.0
packaging>=24.0
```

## 2. 安装依赖

```bash
python -m pip install -r requirements.txt
```

国内网络可加清华镜像加速：

```bash
python -m pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## 3. 启动原版

```bash
python main.py
```

首次启动会弹出一个深色启动窗口，自动下载 `yt-dlp.exe` 和 `ffmpeg.exe`，存入：

- 打包后：`%LOCALAPPDATA%\yt-dlp-gui\bin\`
- 源码运行：项目根目录下的 `bin_dev\`

下载完成后进入主界面：粘贴视频链接 → 选择画质 → 开始下载。

## 4. 本机实测记录

| 检查项 | 结果 |
|---|---|
| `python main.py` 能否启动 | ✅ 启动画面正常弹出 |
| 依赖是否全部可安装 | ✅ 清华镜像可装齐 |
| 首次启动自动下载 yt-dlp | ⚠️ 本机访问 GitHub 失败（SSL 握手被中断），下载环节未通过 |
| 首次启动自动下载 ffmpeg | ✅ gyan.dev 源可达，文件约 114 MB |

> 结论：**程序本身可以正常启动**，卡点只在「首次启动需连 GitHub 下载 yt-dlp」。
> 这点在后续 `feature/my-mod` 分支中已通过增加镜像回退处理。

## 5. 日志位置

```
%APPDATA%\yt-dlp-gui\logs\app.log
```

启动异常时先看这里。

## 6. 目录结构

```
yt-dlp-gui/
├─ main.py                  入口，负责路径设置与启动
├─ build.py                 打包脚本（生成 .spec 并调用 PyInstaller）
├─ requirements.txt         运行依赖
├─ assets/                  图标与 logo（打包时嵌入）
└─ src/ytdlp_gui/
   ├─ gui/                  界面（主窗口 + 各组件）
   ├─ core/                 下载、设置、二进制管理、更新检查
   └─ utils/                日志、通知、错误翻译
```
