# Homepage Bio Update Plan

**Goal:** 修正个人主页与简历页中关于导师分工、研究方向和教育时间线的表述，使中文与英文版本保持一致，并避免将 `Transformer` 与“生成式建模”作为并列等价概念。

## 过程文档

**原始目标：**
- 修改主页简介与研究方向摘要。
- 修改简历页对应内容。
- 明确本科 `2021--2025`、博士 `2025--至今` 的时间线。

**当前状态：**
- 已定位主页入口：`_pages/zh-cn/about.md`、`_pages/about.md`、`_pages/en-us/about.md`。
- 已定位简历数据源：`assets/json/resume_zh-cn.json`、`assets/json/resume_en-us.json`。
- 已确认现有问题主要包括：
  - 将刁恩茂老师的指导内容错误写成“图机器学习与图基础模型”。
  - 将 `Transformer` 与“生成式建模”并列，语义层级不够准确。
  - 教育经历虽有年份字段，但主页自述未明确 `2021` 入学与 `2025` 升学时间线。
- 已完成中英文主页与中英文简历数据的首轮改写，并同步更新个人信息参考文档。
- 已完成静态校验：
  - `resume_zh-cn.json` 与 `resume_en-us.json` 均可被标准 JSON 解析器正常解析。
  - 旧的错误表述已从主页、简历源和个人信息文档中清除。
- 当前环境缺少本地 Ruby/Bundler，且容器构建受 AppArmor 环境限制，暂未完成 `jekyll build` 级别验证。

**下一步：**
- 在具备 Ruby 或可用 Docker/AppArmor 配置的环境中补跑 `jekyll build`。
- 根据你的偏好，再微调术语粒度与中英文对应方式。
