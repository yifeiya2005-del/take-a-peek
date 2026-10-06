# take-a-peek 👁️

> Antigravity Agent Skill: Preview-First, Zero-Waste Generative Workflow

Enforces preview gates across two generative domains to protect quotas and eliminate rework:
1. **AI Image Generation**: Generates zero-cost draft images via Puter.js models before spending quota on Imagen.
2. **Complex Layouts (CAD & Multi-page PDF)**: Produces lightweight thumbnail drafts (`thumb_*.jpg`) before compiling heavy production deliverables.

---

## 📦 Installation

### Global (All Projects)
Clone into your global Antigravity skills directory:
```bash
git clone https://github.com/<YOUR-USERNAME>/take-a-peek.git ~/.gemini/config/skills/take-a-peek
```

### Project-Specific (Single Workspace)
Place into your repository's `.agents/skills/` folder:
```bash
mkdir -p .agents/skills/take-a-peek
# Copy SKILL.md into .agents/skills/take-a-peek/
```

---

## 🚀 Usage

Trigger the skill in Antigravity chat:
- Mention `@take-a-peek`
- Run slash command `/take-a-peek`
- Or prompt: "用 take-a-peek 流程帮我生成设计草图"

---

## 📄 License

MIT License. See [LICENSE](./LICENSE) for details.
