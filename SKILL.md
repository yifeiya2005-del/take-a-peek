---
name: take-a-peek
description: >-
  Enforces a strict 'Preview-First, Zero-Waste' two-stage workflow across all generative tasks:
  1) AI Image Generation: Prioritizes generating draft images without providing an API key
     (using free-ai-image-generator / Puter.js models) to protect quota-limited tools like generate_image (Imagen).
  2) Complex Tasks (CAD standard annotations, multi-page PDF compilation, large document rendering):
     Mandates producing lightweight thumbnail drafts (thumb_*.jpg) or layout wireframes first.
  STRICT RULE: Never generate production deliverables or full-resolution PNG/PDF before explicit user approval of the draft!
---

# take-a-peek: Draft-First & Quota-Protected Workflow

## 1. 核心铁律（硬性隔离）
1. **绝对审批门禁（Approval Gate）**：草图未获用户明确肯定答复（如“确认”、“满意继续”、“通过”）之前，**严禁生成任何高清成品图、正式交付物或编译最终多页文件**。
2. **两阶段严格隔离**：
   - **阶段一（草稿预览）**：仅允许且只能生成低分辨率预览草图（`thumb_*.jpg`，宽 800~1200px，体积 < 200KB）或无 API key 的免费 AI 草图。代码或脚本中绝不能同时输出成品文件。
   - **阶段二（正式出图）**：只有在用户确认满意后，才允许触发下一动作生成高清成品图或执行最终编译。
3. **额度与资源保护**：严禁在未验证构图与需求时直接消耗 Imagen 等收费/受限生图额度。

## 2. 分领域执行规范

### 领域 A：AI 图像生成
- **草稿阶段（零额度消耗）**：
  - 严禁首次请求直接调用 `generate_image` (Imagen)。
  - 优先调用 `free-ai-image-generator`（Puter.js 免 API key 模式）生成免费概念草图。
- **审批停顿点**：
  - 展示草图并暂停，询问：“这是免费草稿，构图与风格是否符合预期？”
  - 严禁在此阶段调用任何正式付费出图工具。
- **正式出图阶段**：
  - 仅在收到用户明确肯定回复后，方可调用 `generate_image` 生成最终高清图。

### 领域 B：CAD 工程图标注与多页排版
- **草稿阶段（轻量预览）**：
  - 严禁直接编译多页 PDF 或直接导出 4K/全尺寸高清 PNG。
  - 生成单张轻量缩略草图：宽度 800~1200px，`.jpg` 格式，文件名前缀必须为 `thumb_`（文件体积 < 200KB）。
  - 脚本与代码必须与成品生成隔离（例如通过 `--preview` / `--production` 区分，草稿模式下不得写入成品路径）。
- **审批停顿点**：
  - 输出轻量草图链接及核心校核指标后立即停止，等待用户审批（如“满意继续”）。
  - 未收到审批前，严禁执行成品图保存、替换或 PDF 编译。
- **正式生成阶段**：
  - 用户审批后，再执行全尺寸无损成品导出或正式文档整合。
  - 提供一键清理所有 `thumb_*` 缓存文件的选项。
