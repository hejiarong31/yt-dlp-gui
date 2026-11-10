<h1>
  <img src="assets/logo.png?v=2" width="32" height="32" style="vertical-align: text-bottom; margin-right: 8px;" />
  <sup>视频下载器 · hejiarong31</sup>
</h1>

基于 [vokrob/yt-dlp-gui](https://github.com/vokrob/yt-dlp-gui) 改造的桌面视频下载器：粘贴链接、选择画质、开始下载。

> **本仓库是 Fork 后的改造版**，用于课程作业。原作者为 `vokrob`，遵循 MIT 协议。
> Fork 自：https://github.com/vokrob/yt-dlp-gui

## 我的改动

| 项目 | 原版 | 改造版 |
|---|---|---|
| 应用名 | `yt-dlp GUI` | `视频下载器` |
| 图标 | 原项目图标 | 自制墨绿播放键图标（`assets/icon.ico`） |
| 界面语言 | 英文 | **全中文**（34 处文案） |
| 主题色 | 红/白灰 | **墨绿 `#16A34A`**，字体换成微软雅黑 |
| 二进制下载 | 仅 GitHub 直连 | 增加镜像回退 + PyPI 兜底 |

具体的界面文案包括"继续""开始下载""下载队列""清空""保存到："等。

## 描述

把视频保存为 MP4（144p 到 8K），或把音频保存为 MP3，支持 YouTube 及[数百个站点](https://github.com/yt-dlp/yt-dlp/blob/master/supportedsites.md)。

- 下载队列重启后不丢失
- 自动读取浏览器 Cookie，年龄限制视频也能下载
- yt-dlp 自动更新

## 技术栈

- Python 3.9+
- CustomTkinter
- yt-dlp
- Pillow
- PyInstaller

## 安装

1. 从 [Releases](../../releases) 下载最新的 `.exe`
2. 直接运行。程序未签名，SmartScreen 可能提示，点"更多信息"→"仍要运行"
3. 首次启动会下载 yt-dlp 与 ffmpeg

## 从源码运行

```bash
git clone https://github.com/hejiarong31/yt-dlp-gui.git
cd yt-dlp-gui
pip install -r requirements.txt
python main.py
```

## 构建与打包

本项目使用仓库自带的 `build.py` 打包，它会自动生成 `.spec` 并调用 PyInstaller：

```bash
pip install -r requirements.txt
pip install pyinstaller
python build.py
```

产物路径：`dist\视频下载器.exe`

### 打包说明

- `build.py` 会把 `assets/`（图标）和 `src/ytdlp_gui/assets/`（主题）一起打进 exe
- 输出为**单文件免安装 exe**，双击即可运行，无需安装
- 构建产物（`dist/`、`build/`、`*.spec`、`*.exe`）已被 `.gitignore` 排除，不进仓库
- 本地运行环境说明见 [RUNNING.md](RUNNING.md)

## 使用

1. 启动后粘贴视频链接
2. 等待预览加载（标题、缩略图、画质选项）
3. 选择视频或音频、画质和保存位置，点"开始下载"
4. 在队列中查看进度

- 如果浏览器 Cookie 不生效，用 "Get cookies.txt" 扩展导出，把 `cookies.txt` 放到 exe 同目录
- 部分地区访问 YouTube 可能需要代理

## 许可

MIT License，原始版权归 `vokrob` 所有，见 [LICENSE](LICENSE)。
