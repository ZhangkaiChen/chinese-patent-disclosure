# 中文专利交底书.skill

![中文专利交底书 Skill](assets/icon.svg)

面向论文、代码、模型结构、实验材料和现有专利模板的中文发明专利交底书撰写 Skill。它用于把科研或工程材料整理为可交给代理人继续处理的专利交底书，重点强调项目扫描、专利点提炼、查新、公式自检、关键点/保护点归纳和迭代修订。

## 能做什么

- 从论文、代码、技术方案或 DOCX/PPTX 草稿中提炼可保护创新点。
- 判断候选专利点是否具备与现有技术的区分度，避免把常规做法或论文已有公开内容直接包装成创新。
- 按你的交底书风格撰写背景技术、现有技术缺点、技术方案、关键点、欲保护点、替代方案和技术优点。
- 在提供现有专利或交底书模板时，严格按模板章节、标题层级和行文习惯改写。
- 支持国知局公布公告优先查新，失败或无结果时降级到 WebSearch、Google Scholar 或 Google Patents。
- 检查公式变量、参数范围、逻辑闭环、前后文一致性和明显 AI 味表述。
- 指导小改高亮/修订、大版本另存新文件的迭代方式。

## 适用场景

- “给你一篇论文和代码，帮我总结可写专利的创新点。”
- “参考这份已有交底书模板，重写我的新专利。”
- “检查这份专利公式、变量解释和关键点/保护点是否一致。”
- “补充现有技术和与最接近现有技术相比的技术优点。”
- “绘制黑白专利流程图或网络结构图。”

## 安装

### 方式一：复制到本地 Codex skills 目录

```powershell
git clone https://github.com/ZhangkaiChen/chinese-patent-disclosure.git
Copy-Item -Recurse -Force .\chinese-patent-disclosure "$env:USERPROFILE\.codex\skills\chinese-patent-disclosure"
```

重启 Codex 后即可使用。

### 方式二：用 Skill Installer 从 GitHub 安装

在 Codex 中请求：

```text
使用 skill-installer，从 https://github.com/ZhangkaiChen/chinese-patent-disclosure.git 安装这个 skill。
```

安装后重启 Codex。

## 使用方式

安装后可以直接调用：

```text
使用 $chinese-patent-disclosure，阅读论文和代码，先给出项目扫描摘要和候选专利点，再等我确认后撰写交底书。
```

```text
使用 $chinese-patent-disclosure，按我提供的现有专利模板格式，重写这份专利交底书，并检查公式变量是否完整。
```

```text
使用 $chinese-patent-disclosure，只做审查，不修改文件：检查全文逻辑、现有技术区分度、公式参数和关键点/保护点对应关系。
```

## 工作流程

1. 项目扫描：优先读取 README、论文、技术说明、已有草稿和核心代码；DOCX/PPTX 先抽取文本或转 Markdown 后扫描。
2. 专利点融合：列出候选点，合并重复点，剔除常规做法，保留具备技术区分度的点。
3. 查新定位：正式成稿或写现有技术时，优先国知局公布公告，必要时降级 WebSearch / Google Scholar / Google Patents。
4. 交底书成稿：按中文发明专利交底书风格撰写，公式满足 Word 公式或 MathType 可转换要求。
5. 自检修订：检查逻辑闭环、公式与参数一致、术语范围一致、关键点/保护点对应关系。
6. 迭代修改：小改在 Word 中高亮或修订，大版本修改或方向纠正另存新文件。

## 目录结构

```text
chinese-patent-disclosure/
├── SKILL.md
├── agents/openai.yaml
├── references/
│   ├── project_scan.md
│   ├── patent_point_fusion.md
│   ├── prior_art_search.md
│   ├── writing-style.md
│   ├── prior-art-and-innovation.md
│   ├── disclosure_self_check.md
│   ├── audit-checklist.md
│   ├── iteration_policy.md
│   └── figure-guidelines.md
├── scripts/
│   ├── cnipa_epub_search.py
│   ├── cnipa_epub_parse.py
│   ├── cnipa_epub_crawler.py
│   └── requirements-cnipa.txt
├── assets/icon.svg
└── examples/usage.md
```

## 依赖

基础撰写和审查不需要额外依赖。

国知局公布公告查新脚本需要：

```bash
pip install -r scripts/requirements-cnipa.txt
python -m playwright install chromium
```

脚本来源于 `handsomestWei/patent-disclosure-skill` 的 CNIPA 检索工具组，并随附原 MIT 许可文本：`scripts/LICENSE.patent-disclosure-skill`。

## 示例效果

### 候选专利点输出

```text
1. 缺模态感知的掩码交叉注意力融合机制
本申请针对普通交叉注意力默认所有 Token 均有效、缺失占位值可能污染注意力归一化的问题，设计 Softmax 前掩码屏蔽机制，使无效连接不参与注意力归一化。

2. 质量驱动的缺模态鲁棒训练与视图一致性约束
本申请根据模态质量和有效覆盖比例构造缺失视图，并以完整视图作为教师信号，约束缺失视图输出保持一致。
```

### 审查输出

```text
主要问题：式（7）中的质量阈值未在正文解释，且后文推理阶段使用了不同符号。
修改建议：统一使用 θ_m 表示模态质量阈值，并在式（17）后补充其取值范围和业务含义。
```

## 注意事项

- 现有专利不是必需输入；只给论文或代码也可以提炼专利点并撰写。
- 如果提供现有专利模板，应严格按模板格式写，不机械保留模板旧技术内容。
- 查新结果不得虚构公开号、链接或摘要内容。
- 自检清单只作为修订依据，不写入交底书正文。
- 本 Skill 生成的是技术交底书草稿，不替代专利代理人的法律判断。

## 许可

本仓库采用 MIT License。CNIPA 检索脚本保留其原始 MIT 许可说明，见 `scripts/LICENSE.patent-disclosure-skill`。
