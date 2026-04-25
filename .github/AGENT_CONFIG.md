---
description: "Bootstrap Copilot and agent customizations: workspace instructions, file instructions for styling/design, and custom TDD agents"
---

# Workspace Agent Configuration

This document describes how the Soc Ops workspace is configured for GitHub Copilot and custom agents.

---

## 📋 What's Configured

### 1. **Workspace Instructions** (New!)
📄 [`.github/copilot-instructions.md`](.github/copilot-instructions.md)

**Purpose:** Guide all AI agents and Copilot interactions across the project

**What's Included:**
- Development checklist (build, test, code style)
- Complete project overview & architecture
- Key commands for building, running, testing
- Styling guide with CSS utility classes
- State management patterns
- Component best practices
- Testing patterns
- Troubleshooting guide

**How agents use it:**
- Automatically loaded for all chat interactions
- Ensures code suggestions follow project conventions
- Guides custom agents (TDD, UI Review, Quiz Master)
- Prevents common mistakes (inline styles, direct state mutation)

---

### 2. **File-Specific Instructions** (Already Present)
These guide Copilot when working with specific file types:

#### **CSS Utilities** 
📄 [`.github/instructions/css-utilities.instructions.md`](.github/instructions/css-utilities.instructions.md)

- Documents custom Tailwind-like utility classes
- Applied when editing `wwwroot/css/app.css`
- Helps AI suggest correct CSS class combinations

#### **Frontend Design**
📄 [`.github/instructions/frontend-design.instructions.md`](.github/instructions/frontend-design.instructions.md)

- Encourages creative, distinctive design choices
- Avoids generic AI aesthetics
- Focuses on typography, color cohesion, motion, backgrounds
- Applied when designing UI components

---

### 3. **Custom Agents** (Already Present)
Located in `.github/agents/`:

| Agent | Purpose | Use Case |
|-------|---------|----------|
| **TDD Supervisor** (`tdd.agent.md`) | Orchestrate full TDD cycle | Large features requiring structure |
| **TDD Red** (`tdd-red.agent.md`) | Write failing tests | Start feature with test-first approach |
| **TDD Green** (`tdd-green.agent.md`) | Minimal implementation | Make tests pass with minimal code |
| **TDD Refactor** (`tdd-refactor.agent.md`) | Improve code quality | Polish after green tests pass |
| **UI Review** (`ui-review.agent.md`) | Evaluate UI/UX decisions | Get feedback on design choices |
| **Quiz Master** (`quiz-master.agent.md`) | Generate quiz themes | Create custom game modes |
| **Pixel Jam** (`pixel-jam.agent.md`) | Scavenger Hunt mode | Build special game features |

---

## 🚀 How to Use

### **Option 1: Chat with Default Settings**
Simply ask questions in the chat and Copilot will follow workspace instructions:

```
In Chat:
What's the architecture of BingoGameService?
```

Copilot reads `.github/copilot-instructions.md` and responds with project context.

---

### **Option 2: Use a Custom Agent**
Invoke specific agents for guided workflows:

```
In Chat:
@agent tdd
Create a new feature that lets users filter questions by category
```

The TDD agent will:
1. Write failing tests (`tdd-red.agent.md`)
2. Implement minimal code (`tdd-green.agent.md`)
3. Refactor for quality (`tdd-refactor.agent.md`)
4. Summarize changes for review

---

### **Option 3: Background Agents (Cloud/Copilot CLI)**
Run agents in parallel without blocking:

**Copilot CLI (Local Background):**
```
Change Session Target: Copilot CLI
Add eslint rules for unused variables; run linter and fix errors
```

**Cloud Agent (Remote Background):**
```
Change Session Target: Cloud
Redesign the StartScreen component with a cyberpunk aesthetic
```

---

## 📚 Development Workflow with Agents

### **New Feature: Add Difficulty Levels**

**Step 1: Plan (Chat)**
```
@agent tdd
Add a difficulty selector to the StartScreen that affects question complexity.
The reducer should be: Easy (20 questions), Medium (50), Hard (50).
```

**Step 2: Review Plan**
TDD agent generates:
- Failing test cases
- Plan for implementation
- Review link for you to approve

**Step 3: Implement**
Agent runs through Red → Green → Refactor cycle, commits changes.

**Step 4: Verify**
```
Great! Now let's get UI Review feedback
@agent ui-review
Does the difficulty selector fit the visual design?
```

---

## 🎨 Design-First Development

### **Redesign Game Board with Cyberpunk Theme**

**Option A: Interactive Planning**
```
I want to redesign the bingo board with a cyberpunk aesthetic.
Use neon colors, retro fonts, and grid backgrounds.
Let's iterate on the plan first.
```

Copilot suggests:
- Color scheme (neon blue, pink, cyan)
- Typography (monospace fonts)
- Animations (glitch effects)

**Option B: Cloud Agent (Hands-Off)**
```
Change Session Target: Cloud
Redesign SocOps with cyberpunk theme: neon colors, retro fonts, scanlines.
Apply to all components and CSS.
```

Agent returns with:
- Full redesign in new branch
- Before/after preview
- Ready to merge

---

## 📂 File Organization

```
.github/
├── copilot-instructions.md         # 🆕 Workspace-wide agent guide
├── instructions/
│   ├── css-utilities.instructions.md        # CSS class patterns
│   └── frontend-design.instructions.md      # Design philosophy
├── agents/
│   ├── tdd.agent.md                # TDD Supervisor
│   ├── tdd-red.agent.md
│   ├── tdd-green.agent.md
│   ├── tdd-refactor.agent.md
│   ├── ui-review.agent.md
│   ├── quiz-master.agent.md
│   └── pixel-jam.agent.md
└── prompts/
    ├── setup.prompt.md             # Dev environment setup
    └── [other prompts...]
```

---

## ✅ Benefits for Developers

With this configuration, AI agents will:

✅ **Understand project structure** — No need to explain architecture repeatedly  
✅ **Follow code conventions** — Consistent naming, patterns, state management  
✅ **Suggest correct styling** — Use utility classes, avoid inline styles  
✅ **Automate repetitive tasks** — Run tests, linting, formatting  
✅ **Provide guided workflows** — TDD, design iteration, code review  
✅ **Generate high-quality code** — Fewer revisions needed  
✅ **Scale to team size** — Multiple agents working in parallel  

---

## 🔧 Troubleshooting Agent Discovery

If an agent/instruction isn't being used:

1. **Check file location** — Must be in `.github/agents/`, `.github/instructions/`, or `.github/prompts/`
2. **Verify frontmatter** — YAML between `---` markers with `description` field
3. **Test description** — Ask Copilot: *"Is there a TDD agent available?"*
4. **File name match** — Agent folder name should match `.agent.md` file

Example valid agent file:
```yaml
---
name: TDD Supervisor
description: "Orchestrate full TDD cycle from request to implementation"
tools: ['agent']
---
```

---

## 📖 Next Steps

1. **Review** [`.github/copilot-instructions.md`](.github/copilot-instructions.md) for full project context
2. **Read** [WELCOME_TOUR.md](WELCOME_TOUR.md) for developer onboarding
3. **Try** a custom agent in chat: `@agent tdd Create a new feature...`
4. **Explore** workshop guides in `workshop/` for structured learning

---

## 💡 Tips

- **Keep instructions concise** — Long instructions eat context tokens
- **Use applyTo patterns** — Restrict instructions to relevant files
- **Version instructions with code** — Update them when architecture changes
- **Test agent outputs** — Review AI suggestions before merging
- **Document special workflows** — Link to examples in comments

---

**Configuration Date:** April 25, 2026  
**Status:** ✅ Ready for agent-based development
