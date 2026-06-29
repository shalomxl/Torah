# Torah

妥拉学习笔记，通过 GitBook 发布：<https://shalomhu.gitbook.io/torah/>

## ⚠️ 编辑约定（重要）

本仓库与 GitBook 是 **GitHub → GitBook 单向同步**，GitHub 是唯一真相源。

- ✅ **只在本仓库（本地 / GitHub）编辑内容**，编辑后 push，再到 GitBook 触发同步。
- ❌ **不要在 GitBook 网页端编辑。** GitBook 端的改动推不回 GitHub，还会触发 “Git Sync failure / 认证失败”，并可能在反向同步时重写文件名、规范化格式、丢掉 `{% file %}` 等 GitBook 专有块。

## 内容结构

- `SUMMARY.md` —— GitBook 目录（侧边栏），新增页面需在此登记。
- `tuo-la.md` —— 《妥拉是什么？》正文。
- `audio/` —— 分享音频（mp3）。
- 页面顶部音频用 GitBook 的 `{% file %}` 块嵌入，`src` 指向 GitHub raw 地址。
