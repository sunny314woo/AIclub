# AI 趣味编程社团发布记录

最后发布：2026-09-15

## 已发布地址

- 正式域名：<https://aiclub.wisteriasoftware.uk/>
- Cloudflare Pages：<https://aiclub-1mb.pages.dev/>
- GitHub 仓库：<https://github.com/sunny314woo/AIclub>
- Cloudflare Pages 项目：`aiclub`

截至记录时，正式域名和 Pages 地址均可正常访问并返回 HTTP 200。

## GitHub

生产代码位于 `main` 分支。

- 首次提交：`a624812`，Publish AI club static website
- 发布修复：`dd05432`，Fix Pages video asset size

本地仓库已经初始化，并将远程地址设置为 SSH：

```text
git@github.com:sunny314woo/AIclub.git
```

## Cloudflare Pages 配置

- 项目名：`aiclub`
- 生产分支：`main`
- Framework preset：None / 静态 HTML
- Build command：留空
- Build output directory：`/`
- Root directory：留空

首次通过 Git 集成构建时，第二个原始视频超过了 Cloudflare Pages 单文件 25 MiB 限制。已生成网页发布版 `student-ecommerce-demo-02.mp4`，网页引用该压缩版；原始文件 `327bfc8f775227ba72fff11066eeb8a8.mov` 仍保留在本地，但已通过 `.gitignore` 排除在 GitHub 和 Pages 发布目录之外。

本次最终生产部署使用 Wrangler 直接上传到同一个 Pages 项目，来自提交 `dd05432`。

## 自定义域名 DNS

Cloudflare 已在 `wisteriasoftware.uk` 区域自动添加以下记录：

| 类型 | 名称 | 目标 | 代理 |
| --- | --- | --- | --- |
| CNAME | `aiclub` | `aiclub-1mb.pages.dev` | Proxied |

对应访问地址为 `https://aiclub.wisteriasoftware.uk/`。如果以后重新添加域名，位置是 Cloudflare Dashboard → Workers & Pages → `aiclub` → Custom domains。

## 后续更新

修改网站后：

```bash
git add .
git commit -m "Update AI club website"
git push origin main
```

当前 Cloudflare 控制台对该项目显示 Git account disconnected 警告。如果 GitHub 推送没有自动触发构建，可先在 Pages → Settings → Build → Git repository → Manage 中重新授权 Cloudflare Pages GitHub App；也可以使用已经授权的 Wrangler 直接发布：

```bash
npx wrangler pages deploy <发布目录> --project-name aiclub --branch main
```

本项目是纯静态网站，发布目录需要包含 `index.html`、两个小游戏 HTML、视频、图片等静态资源。

## 二维码说明

小游戏二维码由首页脚本根据当前线上域名动态生成，部署到正式域名后会自动指向：

- `deepseek_html_20260909_b452cf.html`
- `接金币打地鼠-豆包-耗时1小时.html`

微信群二维码使用 `IMG_2497.PNG`。原图提示二维码有有效期，失效后需要替换该图片并重新提交部署。
