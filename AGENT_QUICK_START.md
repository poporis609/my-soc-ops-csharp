# 🤖 Agent Quick Start Guide

Use this guide to understand what agents are available and how to use them in VS Code Chat.

---

## 🚀 30-Second Quick Start

**In VS Code Chat, type:**

```
@agent tdd
Add a settings page where users can toggle dark mode on/off
```

Copilot will:
1. Write failing tests
2. Implement the feature  
3. Pass all tests
4. Refactor for quality
5. Summarize changes

---

## 📋 Available Agents

### **🧪 TDD Agents** (Test-Driven Development)

**Full Cycle:**
```
@agent tdd
[Your feature request]
```
Orchestrates: Red → Green → Refactor → Pass

**Red (Write Tests):**
```
@agent tdd-red
Write failing unit tests for a favorite-lists feature
```

**Green (Implement):**
```
@agent tdd-green
Make all tests from the BingoLogicServiceTests pass
```

**Refactor (Polish):**
```
@agent tdd-refactor
Improve code quality in BingoGameService
```

---

### **🎨 Design Agents**

**UI Review:**
```
@agent ui-review
Does the GameScreen layout work well on mobile?
```

**Quiz Master (Create Custom Themes):**
```
@agent quiz-master
Create a "Tech Life Bingo" theme with 50 tech-industry questions
```

**Pixel Jam (Special Features):**
```
@agent pixel-jam
Add a scavenger hunt mode to the game
```

---

## 🛠️ Quick Tips

| Need | Command | Example |
|------|---------|---------|
| Tests for your idea | `@agent tdd-red` | Write tests for a timer feature |
| Fast implementation | `@agent tdd-green` | Implement what tests expect |
| Code cleanup | `@agent tdd-refactor` | Improve BingoSquare component |
| Design feedback | `@agent ui-review` | Should buttons be bigger? |
| Full feature | `@agent tdd` | Add leaderboard tracking |
| New quiz theme | `@agent quiz-master` | Create "Movie Nights" theme |

---

## 🎯 By Task

### **"I want to add a new feature"**
```
@agent tdd
[Describe your feature]
```

### **"I want to redesign the UI"**
```
First: @agent ui-review
What do you think about redesigning with dark mode?

Then: @agent tdd
Implement dark mode toggle throughout the app
```

### **"I want to fix a bug"**
```
@agent tdd
Bug: The bingo board doesn't highlight winning lines. 
Write tests first, then fix.
```

### **"I want to create content (quiz themes)"**
```
@agent quiz-master
Create a "Science & Nature" bingo theme with 50 questions
```

---

## 💬 Chat Tips

**Always provide context:**
```
❌ Bad: @agent tdd Add a timer
✅ Good: @agent tdd Add a 2-minute countdown timer to each round
```

**Be specific about requirements:**
```
❌ Bad: @agent tdd-green Make it work
✅ Good: @agent tdd-green Implement StartGame method to initialize board
```

**Review AI suggestions before merging:**
```
✅ Do: Review tests → Review implementation → Approve merge
❌ Don't: Auto-merge without checking
```

---

## 📊 Session Types

### **Local (Blocking)**
Default chat mode. Agent runs in your current context, you see output in real-time.

```
Chat → Agent → Output → You review → Approve/Reject
```

### **Copilot CLI (Background)**
Run agents without blocking (requires setup):

```
Change Session Target: Copilot CLI
[Your request]
# Returns: branch + review link
```

### **Cloud (Hands-Off)**
Run agents remotely (requires Copilot Enterprise):

```
Change Session Target: Cloud  
[Your request]
# Returns: completed branch ready to merge
```

---

## ✨ Pro Patterns

### **Design Iteration Loop**
```
1. @agent ui-review
   What if we used a retro 80s aesthetic?

2. @agent tdd
   Implement the 80s retro design

3. @agent ui-review
   Any UX improvements?

4. Merge when happy
```

### **Feature Development Pipeline**
```
1. @agent tdd-red
   Write tests for "Power-ups" feature

2. Review tests → Approve

3. @agent tdd-green
   Implement minimal code to pass tests

4. @agent tdd-refactor
   Improve code quality

5. @agent ui-review
   Does it look polished?

6. Merge to main
```

### **Batch Content Creation**
```
1. @agent quiz-master
   Create "Travel Around the World" theme

2. @agent quiz-master
   Create "Movie Marathon" theme

3. @agent quiz-master
   Create "Music Festival" theme

4. Combine all into one branch, merge
```

---

## 🐛 Troubleshooting

| Problem | Solution |
|---------|----------|
| Agent not found | Chat responds: "I don't know how to handle @agent tdd" | Check agent file exists in `.github/agents/` |
| Agent runs but ignores instructions | Agent description may not match your query | Try being more specific: *"@agent tdd Create unit tests for..."* |
| Changes didn't apply | Review the diff before approving | Always check what agent generated |
| Merge conflicts | Agent may have changed old files | Resolve conflicts manually or retry |

---

## 📚 Learn More

- **Full Workspace Instructions:** [`.github/copilot-instructions.md`](.github/copilot-instructions.md)
- **Agent Configuration:** [`.github/AGENT_CONFIG.md`](.github/AGENT_CONFIG.md)
- **Welcome Tour:** [WELCOME_TOUR.md](WELCOME_TOUR.md)
- **Workshop:** [workshop/GUIDE.md](workshop/GUIDE.md)

---

## 🎯 Your Next Step

Pick an agent and try it:

```
@agent tdd
Create an achievements/badges system for players who win streaks
```

Good luck! 🚀
