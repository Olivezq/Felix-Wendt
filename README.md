# 人和他的撒旦 · 网站部署说明

整个站点是一组静态文件（HTML + CSS + 一张图），不需要服务器、不需要数据库、不需要构建工具。

---

## 一、文件结构

```
satan-site/
├── index.html          ← 首页
├── end.html            ← 终页
├── chapters/
│   ├── ch1.html
│   ├── ch2.html
│   ├── ch3.html
│   ├── ch4.html
│   └── ch5.html
└── assets/
    ├── style.css       ← 所有样式
    └── cover.jpg       ← 你的封面图（暂未放，下面有说明）
```

---

## 二、放封面图

封面图准备好后，做两步：

1. **图片重命名成 `cover.jpg`**（或 .png，下面相应改），放进 `assets/` 文件夹。建议尺寸 800×1200 左右（2:3 长方形），文件大小压到 300KB 以内。
2. **打开 `index.html`**，找到下面这一段（在文件靠前的位置）：

```html
<div class="cover">
  <div class="cover-placeholder">
    <span class="ph-title">人和他的撒旦</span>
  </div>
  <!-- <img src="assets/cover.jpg" alt="人和他的撒旦 封面"> -->
</div>
```

把它**改成**：

```html
<div class="cover">
  <img src="assets/cover.jpg" alt="人和他的撒旦 封面">
</div>
```

（就是把上面那段占位 div 删掉，把下面那行 `<img>` 的 `<!--` 和 `-->` 注释符去掉。）

---

## 三、部署到独立网址 —— 推荐 Cloudflare Pages

这是最简单的方法，全程免费，拿到一个跟你的博客完全无关的网址。

### 步骤 1 — 把整个文件夹放到 GitHub 上

1. 去 https://github.com/new 创建一个**新仓库**，名字随便取（比如 `satan` 或 `renheta`），**不要勾**任何 README/gitignore，**不要**和你的博客仓库放一起。
2. 把整个 `satan-site` 文件夹里的内容（不包括 `satan-site` 这一层）push 上去。如果你不熟悉 git，最简单的办法是用 GitHub 网页端的 "Upload files" 直接拖文件夹上传。

### 步骤 2 — 用 Cloudflare Pages 部署

1. 注册一个 Cloudflare 账号（cloudflare.com），免费。
2. 进 Cloudflare 后台 → Workers & Pages → Create → Pages → Connect to Git。
3. 授权 GitHub，选你刚才建的那个仓库。
4. 配置：
   - **Framework preset**: None
   - **Build command**: 留空
   - **Build output directory**: `/` （根目录）
5. 点击 Save and Deploy。等大概一分钟。

完成后 Cloudflare 会给你一个网址，形如 `satan-abc.pages.dev`。这就是你的独立网站，跟 `olivezq.github.io` 没有任何关系。

### 步骤 3（可选）— 用自己的域名

如果你想要 `renheta.art`、`satan.ink` 这种自定义域名：

1. 去 Cloudflare Registrar 或 Namecheap 买一个域名（通常 30–80 人民币/年，`.art` `.ink` `.page` 这类比较有文学气息）。
2. Cloudflare Pages 项目里 → Custom domains → 添加你的域名，按指示配置 DNS。
3. 几分钟生效，整站就用新域名访问。

---

## 四、之后想改内容

所有正文在 `chapters/ch1.html` 到 `chapters/ch5.html` 里，直接打开编辑保存即可。每次 push 到 GitHub，Cloudflare Pages 会自动重新部署。

样式想调（字号、颜色、留白），改 `assets/style.css`。最上方的 `:root` 里有所有的颜色变量：

```css
--bg: #0e0d0b;           /* 背景 */
--ink: #d9d2c2;          /* 正文字色 */
--ink-soft: #a59f91;     /* 次级字色 */
--ink-faint: #5a564d;    /* 最弱字色 */
--accent: #c19a5b;       /* 强调金色（用于"終"、进度条等） */
--measure: 36rem;        /* 正文宽度 */
```

---

## 五、如果暂时不想公开

如果你只是想做完先收着，**不要把仓库设为 public**，或者**部署后不分享链接**。Cloudflare Pages 也支持密码保护（Settings → Access policies）。
