# TaK4g1 Homepage 新手使用手册（从修改到 Push 全流程）

> 适用项目：`academicpages/academicpages.github.io` 模板搭建的个人主页  
> 仓库示例：`TaK4g1/TaK4g1.github.io`

---

## 1. 你现在拥有什么

你的网站本质上是一个 GitHub 仓库。  
你每次修改文件并 `push` 到 GitHub，GitHub Pages 会自动重新部署网站。

你的网站地址通常是：

```text
https://<你的GitHub用户名>.github.io
```

例如你的是：

```text
https://tak4g1.github.io
```

---

## 2. 必备概念（小白版）

- **仓库（Repository）**：放网站文件的“网盘+版本管理”。
- **本地（Local）**：你电脑里的项目目录。
- **远程（Remote）**：GitHub 上的仓库。
- **commit**：一次“存档”。
- **push**：把本地存档上传到 GitHub。
- **GitHub Pages**：自动把仓库变成网站的服务。

---

## 3. 项目目录是做什么的

以下是你最常改的目录/文件：

- `_config.yml`：全站配置（站点名、邮箱、侧边栏信息、社交链接等）
- `_data/navigation.yml`：顶部导航栏菜单
- `_pages/`：独立页面（About、CV、Publications、Talks、Teaching、Blog入口页等）
- `_publications/`：每篇论文一个 Markdown 文件
- `_talks/`：每次报告/演讲一个 Markdown 文件
- `_teaching/`：每门课程一个 Markdown 文件
- `_posts/`：博客文章（按日期命名）
- `images/`：图片（头像通常放这里）
- `files/`：PDF、附件等可下载文件
- `.github/workflows/`：GitHub Actions 工作流（自动任务）

---

## 4. 最常见修改：改个人信息

打开 `_config.yml`，重点改这些：

- `title`：网站标题
- `name`：你的名字
- `description`：网站描述
- `url`：你的站点地址（如 `https://tak4g1.github.io`）
- `repository`：仓库名（如 `TaK4g1/TaK4g1.github.io`）
- `author.name`：侧边栏名字
- `author.bio`：一句简介
- `author.email`：邮箱
- `author.github / linkedin / googlescholar / orcid`：社交链接

改完保存即可。

---

## 5. 改首页 About 内容

文件：`_pages/about.md`

你可以直接写 Markdown 文本，例如：

```markdown
Welcome to my homepage.

I am TaK4g1. My research interests include ...
```

---

## 6. 改顶部导航栏

文件：`_data/navigation.yml`

你可以增删菜单项，例如：

```yml
main:
  - title: "About"
    url: /
  - title: "Publications"
    url: /publications/
  - title: "Talks"
    url: /talks/
```

---

## 7. 换头像（最简单）

1. 准备头像图片（建议正方形）
2. 放到 `images/`，命名为 `profile.png`（或你自定义文件名）
3. 如果不是 `profile.png`，改 `_config.yml`：

```yml
author:
  avatar: "你的文件名.jpg"
```

---

## 8. 添加论文 / 演讲 / 教学 / 博客

### 8.1 添加论文（Publications）

在 `_publications/` 新建一个 `.md` 文件（文件名建议 `YYYY-MM-DD-xxx.md`）：

```markdown
---
title: "Paper Title"
collection: publications
permalink: /publication/2026-paper-title
date: 2026-02-27
venue: "Conference/Journal Name"
---

Paper summary here.
```

### 8.2 添加演讲（Talks）

在 `_talks/` 新建 `.md` 文件，格式类似：

```markdown
---
title: "Talk Title"
collection: talks
type: "Talk"
permalink: /talks/2026-talk-title
venue: "University/Conference"
date: 2026-02-27
location: "City, Country"
---

Talk abstract here.
```

### 8.3 添加教学（Teaching）

在 `_teaching/` 新建 `.md` 文件：

```markdown
---
title: "Course Name"
collection: teaching
type: "Undergraduate course"
permalink: /teaching/2026-course-name
venue: "Your University"
date: 2026-02-27
---

Course description here.
```

### 8.4 添加博客（Blog）

在 `_posts/` 新建文件，命名必须是：

```text
YYYY-MM-DD-your-post-title.md
```

内容示例：

```markdown
---
title: "My First Post"
date: 2026-02-27
---

Hello world!
```

---

## 9. 从“修改”到“上线”的完整命令流程

每次改完都按这个顺序走：

```bash
cd /Users/liujiecheng/codesample/codex/TaK4g1.github.io
git status
git add .
git commit -m "Describe what you changed"
git push
```

如果是第一次推分支，用：

```bash
git push -u origin main
```

---

## 10. GitHub 认证（Mac，HTTPS + PAT）

如果 `git push` 提示认证失败，请这样做：

1. GitHub 创建 PAT（Personal Access Token）
   - `Settings -> Developer settings -> Personal access tokens`
   - 推荐 classic token 勾选：`repo`、`workflow`
2. 清空旧凭证：

```bash
printf "protocol=https\nhost=github.com\n" | git credential-osxkeychain erase
```

3. 再次 push，输入：
   - Username：你的 GitHub 用户名
   - Password：粘贴 PAT（不是 GitHub 登录密码）

---

## 11. 部署设置（只需检查一次）

仓库网页中：

1. 进入 `Settings -> Pages`
2. `Build and deployment` 选择 `Deploy from a branch`
3. Branch 选 `main`，Folder 选 `/(root)`
4. 保存后等待 1-3 分钟

访问站点：

```text
https://tak4g1.github.io
```

---

## 12. 常见报错与解决

### 报错：`fatal: not a git repository`
你不在项目目录。先执行：

```bash
cd /Users/liujiecheng/codesample/codex/TaK4g1.github.io
```

### 报错：`invalid credentials`
你用的是账号密码，不是 PAT，或 PAT 权限不够。重新生成 PAT。

### 报错：`refusing to allow a Personal Access Token to create or update workflow ...`
PAT 缺少 `workflow` 权限。  
classic token 需要勾选 `workflow`；fine-grained token 需要给 Workflows 写权限。

### 报错：`main -> main (fetch first)`
远程比本地新，先同步再推：

```bash
git pull --rebase origin main
git push
```

---

## 13. 推荐操作习惯（防翻车）

- 每次改动前先 `git pull --rebase origin main`
- 每次 commit 信息写清楚（方便回滚）
- 改配置文件后仔细检查缩进（YAML 对缩进敏感）
- 不要直接删 `.github/workflows/`，除非你确定不用自动流程
- 大改前先复制一份文件备份

---

## 14. 一次完整示例（可照抄）

假设你做了三件事：改邮箱、换头像、改 About 文案。

```bash
cd /Users/liujiecheng/codesample/codex/TaK4g1.github.io
git pull --rebase origin main
git add _config.yml _pages/about.md images/profile.png
git commit -m "Update email, avatar, and about page"
git push
```

完成后等 Pages 自动部署，刷新网站即可看到变化。

---

如果你愿意，我下一步可以再给你做一份“只用 10 条命令就能维护网站”的极简速查版。
