# 仓库审计与清理说明

## 目标

这份文档用于说明当前仓库的实际结构、哪些内容来自 `al-folio` 模板、哪些内容属于老师个人信息，以及这次在不动主站核心页面的前提下清理了哪些示例内容。

## 当前状态

- 审计时间：2026-03-21
- 当前主站入口：`/`、`/cv/`、`/publications/`、`/repositories/`、`/zh-cn/`
- 当前主页效果：头像 + 简介 + 新闻 + 精选论文
- 当前 CV 数据源：`_config.yml` 中 `jekyll_get_json` 加载的 `assets/json/resume_en-us.json` 与 `assets/json/resume_zh-cn.json`
- 当前论文数据源：`_bibliography/papers.bib`
- 当前公告数据源：`_news/en-us/*` 与 `_news/zh-cn/*`
- 当前仓库展示数据源：`_data/repositories.yml`
- 本地验证限制：当前环境缺少 Ruby，且 Docker 镜像拉取超时，因此没有完成本地 `jekyll build`；页面效果是通过线上站点 `https://www.diaoenmao.com` 和仓库静态引用关系交叉确认的。

## 仓库结构

### 一、模板骨架

这些基本都属于 `al-folio` 模板本身，负责站点框架、样式、脚本和构建，不承载老师个人内容：

- `_includes/`
- `_layouts/`
- `_sass/`
- `_plugins/`
- `assets/js/`
- `assets/css/`
- `assets/fonts/`
- `assets/webfonts/`
- `Gemfile`、`Gemfile.lock`
- `docker-compose*.yml`、`Dockerfile`
- `.github/`
- `README.md`、`INSTALL.md`、`FAQ.md`、`CUSTOMIZE.md`
  其中 `CUSTOMIZE.md` 已在本次清理中移除，因为它和当前清理后的仓库结构不再一致。

### 二、老师个人内容

这些文件里存放了老师的真实资料，后续你搭自己网站时应优先替换：

- `_config.yml`
  站点标题、姓名、邮箱、域名、学术作者名、语言与 JSON 数据入口。
- `_data/socials.yml`
  邮箱、GitHub、LinkedIn、Google Scholar。
- `_data/repositories.yml`
  展示的 GitHub 用户名和仓库列表。
- `_data/en-us/strings.yml`
  英文站点标题、联系信息文案。
- `_data/zh-cn/strings.yml`
  中文站点联系信息文案。
- `_pages/en-us/about.md`
  英文首页简介、研究方向、副标题。
- `_pages/zh-cn/about.md`
  中文首页简介、研究方向、副标题。
- `_pages/en-us/cv.md`、`_pages/zh-cn/cv.md`
  CV 页面入口。
- `_pages/en-us/publications.md`、`_pages/zh-cn/publications.md`
  论文页入口。
- `_pages/en-us/repositories.md`、`_pages/zh-cn/repositories.md`
  仓库页入口。
- `_news/en-us/*.md`、`_news/zh-cn/*.md`
  近期论文/消息公告。
- `_bibliography/papers.bib`
  论文条目、作者、摘要、代码链接、奖项。
- `assets/json/resume_en-us.json`
  英文简历数据。
- `assets/json/resume_zh-cn.json`
  中文简历数据。
- `assets/pdf/en-us/CV.pdf`、`assets/pdf/zh-cn/CV.pdf`
  中英文 PDF 简历。
- `assets/img/prof_pic.jpg`
  首页头像。
- `sitemap.xml`
  当前站点域名与页面 URL。

### 三、混合区与注意事项

- `_pages/about.md`、`_pages/cv.md`、`_pages/publications.md`、`_pages/repositories.md`
  这些根目录英文页面和 `_pages/en-us/*` 有重复。线上根路径展示内容更接近 `_pages/en-us/*`，说明当前默认语言实际走的是多语言页面，而根目录页更像旧副本。因为本地构建受限，这组重复页本次没有删除，只做记录。
- `robots.txt`
  会引用 `site.url` 生成站点地图地址，因此也属于部署相关配置，不是纯模板占位。
- `.github/`
  几乎都是模板自带的 CI、格式化、链接检查和发布工作流；它们不影响前台页面，但影响仓库自动化，因此这次不动。

## 本次清理

### 已删除的纯示例页面/集合

- `_pages/blog.md`
- `_pages/projects.md`
- `_pages/profiles.md`
- `_pages/dropdown.md`
- `_pages/teaching.md`
- `_pages/about_einstein.md`
- `_posts/` 下全部示例博文
- `_projects/` 下全部示例项目

这些页面此前虽然不在主导航里，但线上隐藏 URL 仍可访问。删除后不会影响主导航四个核心页面与首页内容，但会移除这些模板演示入口。

### 已删除的纯示例资源/旧数据

- `_data/cv.yml`
  旧的 YAML 简历数据，且含明显模板占位内容。
- `assets/json/resume.json`
  未被当前 `jekyll_get_json` 使用的旧简历副本。
- `assets/json/table_data.json`
- `assets/bibliography/2018-12-22-distill.bib`
- `assets/audio/epicaly-short-113909.mp3`
- `assets/html/relativity.html`
- `assets/img/1.jpg` 到 `assets/img/12.jpg`
- `assets/img/prof_pic_color.png`
- `assets/img/publication_preview/*`
- `assets/plotly/demo.html`
- `assets/pdf/example_pdf.pdf`
- `assets/video/pexels-engin-akyurt-6069112-960x540-30fps.mp4`
- `CUSTOMIZE.md`

这些文件仅被模板示例博文/项目页使用，和老师当前主页、论文、简历、仓库页没有数据关系。

## 你后续搭自己网站时优先要改的地方

### 第一优先级：身份与站点配置

- `_config.yml`
  替换：
  - `title`
  - `first_name`
  - `middle_name`
  - `last_name`
  - `contact_note`
  - `description`
  - `keywords`
  - `url`
  - `icon`
  - `scholar.last_name`
  - `scholar.first_name`

### 第二优先级：社交与外链

- `_data/socials.yml`
  替换：
  - `email`
  - `github_username`
  - `linkedin_username`
  - `scholar_userid`

- `_data/repositories.yml`
  替换：
  - `github_users`
  - `github_repos`

### 第三优先级：首页文案与头像

- `_pages/en-us/about.md`
  替换副标题、研究方向、英文自我介绍。
- `_pages/zh-cn/about.md`
  替换中文副标题、研究方向、中文自我介绍。
- `assets/img/prof_pic.jpg`
  换成你自己的头像。

### 第四优先级：简历与论文

- `assets/json/resume_en-us.json`
  替换英文经历、教育、语言等。
- `assets/json/resume_zh-cn.json`
  替换中文经历、教育、语言等。
- `assets/pdf/en-us/CV.pdf`
  替换英文 PDF 简历。
- `assets/pdf/zh-cn/CV.pdf`
  替换中文 PDF 简历。
- `_bibliography/papers.bib`
  替换论文条目、作者、代码仓库和奖项信息。
- `_news/en-us/*.md`、`_news/zh-cn/*.md`
  删除老师新闻，改成你自己的动态。

### 第五优先级：站点文案与部署痕迹

- `_data/en-us/strings.yml`
  至少检查 `title`、`contact_note`。
- `_data/zh-cn/strings.yml`
  至少检查 `contact_note`。
- `sitemap.xml`
  当前还是老师域名，后续改成你的域名后应同步更新或改为自动生成。

## 预览结论

线上 `https://www.diaoenmao.com` 当前可见主导航是：

- `about`
- `cv`
- `publications`
- `repositories`
- `中文`

首页主要信息块：

- 圆形头像
- “Entrepreneur and Researcher” 副标题
- 研究方向
- 邮箱 / GitHub / LinkedIn / Google Scholar 图标
- 简短教育经历介绍
- `news`
- `selected publications`

隐藏但原本仍在线的模板 URL：

- `/blog/`
- `/projects/`
- `/people/`
- `/teaching/`

本次清理后，这些模板演示 URL 将不再作为站点内容保留。

## 下一步建议

如果你下一步是把这个站改成你自己的，最省事的顺序是：

1. 先替换 `_config.yml`、`_data/socials.yml`、头像和域名。
2. 再改 `about`、`resume_*.json`、`papers.bib`、`_news/*`。
3. 最后再决定是否继续清理根目录英文重复页和 `.github/` 里的模板工作流。
