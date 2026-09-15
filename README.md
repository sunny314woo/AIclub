# AI 趣味编程社团官网

这是一个可直接部署到 Cloudflare Pages 的静态网站。

## 本地预览

在当前目录运行 `python3 -m http.server 8787`，然后打开 `http://localhost:8787/index.html`。两个小游戏作为独立 HTML 页面被主页链接引用，视频与作品图片也直接使用当前目录中的静态资源。

## Cloudflare Pages 部署建议

- GitHub 仓库：<https://github.com/sunny314woo/AIclub>
- Framework preset：None 或 Static HTML。
- Build command：留空。
- Output directory：`/` 或留空，按 Cloudflare Pages 页面提示选择根目录。
- 入口文件：`index.html`。

部署成功后，主页里的小游戏二维码会根据当前线上域名自动生成。
