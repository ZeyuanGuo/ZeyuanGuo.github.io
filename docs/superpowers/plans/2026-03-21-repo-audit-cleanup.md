# Repository Audit And Cleanup Implementation Plan

> **For agentic workers:** Execute this plan using the current harness capabilities. Use checkboxes (`- [ ]`) for tracking. If subagents are explicitly requested or clearly beneficial, delegate bounded subtasks; otherwise execute directly.

**Goal:** 审计这个 GitHub Pages 仓库，区分模板自带内容与老师个人内容，完成不影响当前站点功能的最小清理，并形成后续复用模板时的替换清单。

**Architecture:** 先基于 Jekyll 配置、页面入口、数据源和资源引用建立内容映射，再用本地构建和浏览器预览确认当前站点实际启用的功能。清理只针对未出现在导航、无内容引用、且明显属于模板示例的页面、集合和静态资源；所有结论同步写入最终审计文档。

**Tech Stack:** Jekyll, al-folio, Liquid, YAML, BibTeX, GitHub Pages

---

## 过程文档

**原始目标：** 捋清仓库结构，明确模板自带内容与老师个人信息，先看预览效果，再在不影响功能的前提下清理完全多余的文件或模块，最后产出仓库现状文档与个人信息替换清单。

**当前状态：**
- 已确认仓库是基于 `al-folio` 的 Jekyll 学术主页。
- 已定位核心个人信息入口：`_config.yml`、`_data/socials.yml`、`_pages/about*.md`、`assets/json/resume*.json`、`_bibliography/papers.bib`、`_news/**`、`_data/repositories.yml`、`assets/pdf/**/CV.pdf`、`assets/img/prof_pic.jpg`。
- 已通过线上站点确认主导航只有 `about / cv / publications / repositories / 中文`，并确认 `/blog`、`/projects`、`/people`、`/teaching` 是隐藏但仍可访问的模板示例入口。
- 已删除 `_posts/`、`_projects/`、示例页面、旧版 CV 数据和仅供演示的图片/音视频/HTML/PDF 资源。
- 已形成审计文档 `docs/repo-audit.md`，记录模板内容、老师个人内容与后续替换清单。

**下一步：**
- 复核残留引用是否只存在于 README 或过程文档。
- 向用户说明当前仍保留的“可能进一步清理”的部分：根目录英文重复页、`.github/` 工作流、其余模板说明文档。

## 文件责任映射

- `/_config.yml`
  站点总配置、导航与构建开关、Jekyll 排除项。
- `/_pages/**`
  顶层页面入口，决定哪些页面对外暴露。
- `/_news/**`
  首页 about 页面里的公告源。
- `/_bibliography/papers.bib`
  论文列表与精选论文数据源。
- `/assets/json/resume*.json`
  当前 CV 页面实际使用的数据源。
- `/_data/cv.yml`
  CV 的备用数据源，当前疑似未启用。
- `/_data/socials.yml`
  社交链接和邮箱。
- `/_data/repositories.yml`
  GitHub 用户与仓库展示列表。
- `/assets/img/prof_pic.jpg`
  首页头像。
- `/assets/pdf/en-us/CV.pdf`, `/assets/pdf/zh-cn/CV.pdf`
  简历 PDF。

### Task 1: 站点结构与数据源审计

**Files:**
- Modify: `docs/superpowers/plans/2026-03-21-repo-audit-cleanup.md`
- Create: `docs/repo-audit.md`

- [ ] **Step 1: 枚举入口文件与数据源**

Run: `find . -maxdepth 2 -type d | sort`、`rg --files`
Expected: 得到页面、集合、数据和资源目录清单。

- [ ] **Step 2: 建立“模板内容/个人内容/待确认”分类**

Run: `rg -n "Enmao|Diao|diao|hotmail" _pages _data _news _projects _bibliography assets`
Expected: 找到老师个人信息落点，并将示例页单独标记。

- [ ] **Step 3: 写入审计文档初稿**

Output: 在 `docs/repo-audit.md` 记录仓库结构、启用页面、数据源和替换清单。

### Task 2: 构建与预览验证

**Files:**
- Modify: `docs/superpowers/plans/2026-03-21-repo-audit-cleanup.md`
- Modify: `docs/repo-audit.md`

- [ ] **Step 1: 本地构建站点**

Run: `bundle exec jekyll build`
Expected: 站点成功输出到 `_site/`，无阻断性错误。

- [ ] **Step 2: 启动本地预览服务**

Run: `bundle exec jekyll serve --host 127.0.0.1 --port 4000`
Expected: 浏览器可访问本地主页、论文页、项目页、CV 页。

- [ ] **Step 3: 浏览器确认当前可见页面**

Output: 记录首页、导航、论文页、简历页、仓库页的实际显示效果，以及隐藏但仍可访问的示例页。

### Task 3: 安全清理模板示例内容

**Files:**
- Modify: `_config.yml`
- Delete: `_pages/about_einstein.md`
- Delete: `_pages/blog.md`
- Delete: `_pages/dropdown.md`
- Delete: `_pages/profiles.md`
- Delete: `_pages/projects.md`
- Delete: `_pages/teaching.md`
- Delete: `_posts/*.md`
- Delete: `_projects/*.md`
- Delete: 仅被示例页使用的演示资源文件
- Modify: `docs/superpowers/plans/2026-03-21-repo-audit-cleanup.md`
- Modify: `docs/repo-audit.md`

- [ ] **Step 1: 逐项验证引用关系**

Run: `rg -n "about_einstein|/blog/|/projects/|/teaching/|/people/|1.jpg|12.jpg|example_pdf|tutorial_al_folio" .`
Expected: 示例内容仅被示例页面、模板说明文档或 README 引用。

- [ ] **Step 2: 删除未启用的模板示例页面与集合**

Method: `apply_patch`
Expected: 当前导航页和已启用功能不受影响。

- [ ] **Step 3: 删除失去引用的示例资源**

Method: `apply_patch`
Expected: 仅移除图片、音视频、HTML、PDF 等演示素材，不移除老师个人资料资源。

### Task 4: 回归验证与交付

**Files:**
- Modify: `docs/superpowers/plans/2026-03-21-repo-audit-cleanup.md`
- Modify: `docs/repo-audit.md`

- [ ] **Step 1: 重新构建**

Run: `bundle exec jekyll build`
Expected: 仍然构建成功。

- [ ] **Step 2: 重新预览关键页面**

Run: 浏览器检查 `/`, `/publications/`, `/repositories/`, `/cv/`
Expected: 关键页面正常，404 不受影响。

- [ ] **Step 3: 更新最终文档**

Output: 在 `docs/repo-audit.md` 写清：
- 仓库现状
- 模板自带内容与老师个人内容的区分
- 已清理内容
- 你后续搭建个人站点时需要优先替换的文件和字段
