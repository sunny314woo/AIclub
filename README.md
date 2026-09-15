# AI 趣味编程社团官网

AI 趣味编程社团是一个以兴趣为主、零基础友好、项目式驱动的学生社团。这个仓库是社团官网的纯静态版本，集中展示学生完成的电商项目视频、小游戏试玩入口、指导老师作品和社团微信群二维码。

## 在线地址

- 正式域名：<https://aiclub.wisteriasoftware.uk/>
- Cloudflare Pages 备用地址：<https://aiclub-1mb.pages.dev/>
- GitHub 仓库：<https://github.com/sunny314woo/AIclub>

## 页面内容

### 学生作品

两个学生团队完成了电商演示项目，项目周期约为 **3–7 天**，流程包括：

`注册` → `商品下单` → `支付宝沙盒支付` → `后台发货`

- `2460807 · 谢国超团队`：作品 01，视频文件为 `92123406a5749eb72c9512a9d6c52a27.mov`
- `2460804 · 廖史源团队`：作品 02，网页使用 `student-ecommerce-demo-02.mp4` 发布版

### 小游戏

主页提供两个独立 HTML 游戏的链接和二维码：

- `deepseek_html_20260909_b452cf.html`：纸飞机太空大战，使用 DeepSeek，制作耗时约半小时
- `接金币打地鼠-豆包-耗时1小时.html`：打地鼠接金币，使用豆包，制作耗时约 1 小时

两个小游戏均为静态页面，支持手机浏览器直接打开和操作。

### 指导老师作品

主页使用图片作为作品展示入口，相关链接包括：

- Baby Player：[GitHub 源码](https://github.com/sunny314woo/babyplayer)
- ChatGPT 对话目录和导出：[Chrome 应用商店](https://chromewebstore.google.com/detail/chatgpt-%E5%AF%B9%E8%AF%9D%E7%9B%AE%E5%BD%95%E5%92%8C%E5%AF%BC%E5%87%BA%EF%BC%9Ahtml%E3%80%81mark/opbngifmlnoahbhjhgmngkggedlofddj?hl=zh-CN)
- EnglishFlow：[Chrome 应用商店](https://chromewebstore.google.com/detail/englishflow/nobiefbaobhcpdbidggmfikalohfejpc?hl=zh-CN)

## 目录与素材

| 文件 | 用途 |
| --- | --- |
| `index.html` | 官网首页，包含样式、小游戏入口和动态二维码逻辑 |
| `deepseek_html_20260909_b452cf.html` | 纸飞机太空大战 |
| `接金币打地鼠-豆包-耗时1小时.html` | 打地鼠接金币 |
| `92123406a5749eb72c9512a9d6c52a27.mov` | 学生作品 01 视频 |
| `student-ecommerce-demo-02.mp4` | 学生作品 02 的 Cloudflare 发布版视频 |
| `E4392851-F426-45AC-8A2D-46E43EAC09B0.PNG` | Baby Player 作品图 |
| `IMG_2489.PNG`、`IMG_2490.PNG` | 两个浏览器插件作品截图 |
| `IMG_2497.PNG` | 社团微信群二维码截图 |

原始视频 `327bfc8f775227ba72fff11066eeb8a8.mov` 仅保留在本地，没有提交到 GitHub。原因是 Cloudflare Pages 对单个文件有 25 MiB 限制；网站发布时使用压缩后的 `student-ecommerce-demo-02.mp4`。

## 本地预览

在项目根目录运行：

```bash
python3 -m http.server 8787
```

然后打开 <http://localhost:8787/index.html>。静态网站不需要安装依赖，也不需要构建步骤。

## Cloudflare Pages 配置

Cloudflare Pages 项目名为 `aiclub`，配置如下：

- Production branch：`main`
- Framework preset：`None` 或 Static HTML
- Build command：留空
- Build output directory：`/`
- Root directory：留空

自定义域名使用 `aiclub.wisteriasoftware.uk`。Cloudflare DNS 中对应的记录为：

| 类型 | 名称 | 目标 | 代理状态 |
| --- | --- | --- | --- |
| CNAME | `aiclub` | `aiclub-1mb.pages.dev` | Proxied |

## 发布与更新

常规修改流程：

```bash
git add .
git commit -m "Update AI club website"
git push origin main
```

如果 Cloudflare Pages 已经重新连接 GitHub，推送 `main` 后会自动构建。若控制台显示 Git account disconnected，进入 Cloudflare Dashboard → Workers & Pages → `aiclub` → Settings → Build → Git repository → Manage，重新授权 GitHub Pages App。

也可以使用 Wrangler 手动发布：

```bash
npx wrangler login
npx wrangler pages deploy . --project-name aiclub --branch main
```

发布前请确认根目录包含 `index.html`、两个小游戏 HTML、视频和图片资源。不要把超过 25 MiB 的原始视频放入发布目录。

## 二维码说明

小游戏二维码由 `index.html` 中的脚本根据当前页面域名动态生成，因此部署到新域名后会自动指向新的线上地址。微信群二维码使用 `IMG_2497.PNG`，图片中的二维码有有效期，失效后替换该图片并重新发布即可。

## 项目文档

- [DEPLOYMENT.md](DEPLOYMENT.md)：完整发布记录、DNS 配置和视频大小问题说明。
