# 维护说明（仅供维护者，未加入 GitBook 目录）

## 编辑约定

本仓库与 GitBook 是 **GitHub → GitBook 单向同步**，GitHub 是唯一真相源。

- ✅ 只在本仓库（本地 / GitHub）编辑内容，push 后 GitBook 自动同步。
- ❌ 不要在 GitBook 网页端编辑：改动推不回 GitHub，还可能触发同步失败，并在反向同步时重写文件名、规范化格式、丢掉内容块。

## 音频托管（Cloudflare R2）

- 音频**不进 git 仓库**（`.gitignore` 已忽略 `*.mp3` / `*.m4a`），统一放 Cloudflare R2。
- 存储桶：`torah`
- 公开访问基础 URL：`https://pub-08b87c3b3e994b51bd31c0180fa810dd.r2.dev`
- 文档中用标准 Markdown 链接引用 R2 地址（GitBook 不渲染 `<audio>`/`<iframe>`，点击链接即可在浏览器播放/下载）。

### 上传音频到 R2 的步骤

> ⚠️ 本机 nvm 的 Node **v14 排在 PATH 最前**，而 wrangler 需要 **Node v22+**。上传前必须显式切到 v22，否则报 `requires at least Node.js v22`。

```bash
# 1) 切到 Node v22
export PATH="/Users/shalomhu/.nvm/versions/node/v22.22.0/bin:$PATH"

# 2) 首次需登录（浏览器 OAuth，用最新版 wrangler 才有 R2 权限）
npx --yes wrangler@latest login

# 3) 上传（key 用纯 ASCII，避免中文/空格/& 的 URL 麻烦；设好 content-type）
npx --yes wrangler@latest r2 object put \
  "torah/moadim/three-weeks/<ascii-name>.mp3" \
  --file="<本地音频路径>" \
  --content-type="audio/mpeg" --remote
# m4a 用 --content-type="audio/mp4"

# 4) 验证公开可访问
curl -s -o /dev/null -w '%{http_code}\n' \
  "https://pub-08b87c3b3e994b51bd31c0180fa810dd.r2.dev/moadim/three-weeks/<ascii-name>.mp3"

# 5) 删除对象
npx --yes wrangler@latest r2 object delete "torah/<key>" --remote
```

### 命名规范

- key 一律小写 ASCII，用连字符：`moadim/three-weeks/20240709-tammuz-intro.mp3`
- 目录前缀对应文档分组，便于管理。
