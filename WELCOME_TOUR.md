🎉 **Welcome to Soc Ops!**

You're about to jump into an exciting GitHub Copilot Agent Lab. This workspace is your playground for learning advanced AI-assisted development with VS Code. Let's get you oriented!

---

## 🚀 Quick Start (2 minutes)

You're in a dev container with everything pre-configured:
- ✅ .NET 10 SDK installed and ready
- ✅ All dependencies bundled
- ✅ VS Code dev extensions loaded
- ✅ GitHub Copilot Agent Mode available

**To launch the app:**
```bash
cd SocOps
dotnet run
```
Then open **http://localhost:5000** in your browser. You'll see the Social Bingo game come to life! 🎮

---

## 🎯 What's This Project?

**Soc Ops** is a Social Bingo game — perfect for in-person mixers and team events. Players find people matching trivia questions and mark them off on their 5x5 bingo board. First to get 5 in a row wins! 

The tech stack:
- **Frontend:** Blazor WebAssembly (C#, .NET 10) - runs in your browser
- **Styling:** Custom CSS utility classes (like Tailwind, but lighter)
- **Services:** Game logic, bingo validation, and question management in C#

---

## 📁 Project Structure (Your Playground)

Here's the cool part — understanding the layout will help you navigate with Copilot:

```
SocOps/
├── Components/          ← Blazor components (.razor files)
│   ├── BingoBoard.razor        (the main 5x5 grid)
│   ├── BingoSquare.razor       (individual bingo cell)
│   ├── GameScreen.razor        (game UI)
│   └── StartScreen.razor       (welcome screen)
├── Pages/               ← Page components (routable)
│   ├── Home.razor             (landing page)
│   ├── Counter.razor          (example component)
│   └── Weather.razor          (API example)
├── Services/            ← Business logic
│   ├── BingoGameService.cs    (game state management)
│   └── BingoLogicService.cs   (bingo validation)
├── Data/                ← Static data
│   └── Questions.cs            (trivia questions)
├── Models/              ← Data structures
│   ├── GameState.cs           (game phases and data)
│   ├── BingoLine.cs           (winning lines)
│   └── BingoSquareData.cs     (square properties)
├── wwwroot/             ← Static files served to browser
│   ├── css/app.css            (styling utilities)
│   ├── index.html             (HTML entry point)
│   └── lib/                   (Bootstrap & dependencies)
└── Program.cs           ← App startup configuration
```

💡 **Pro tip:** Each `.razor` file is a component. Think of them as reusable UI building blocks. C# code in `Services/` handles the game logic.

---

## 👨‍💻 Development Workflow

Here's how you'll work with Copilot Agent Mode:

### **Step 1: Build → Run → See Live Changes**
```bash
dotnet run
# Open http://localhost:5000 in browser
# Edit a .razor file and watch it reload automatically!
```

### **Step 2: Ask Copilot to Help**
In VS Code's Chat panel, try:
- *"Explain the BingoBoard component"* — Get architectural insights
- *"Add a dark theme to the game"* — Code suggestions appear
- *"How does the winning logic work?"* — Learn the game engine

### **Step 3: Make Changes Confidently**
Copilot will suggest code. Review it → Accept → The browser reloads. Magic! ✨

---

## 🧩 Key Concepts (On Your Journey)

- **Blazor:** C# running in the browser via WebAssembly
- **Components:** Reusable `.razor` files combining HTML + C# logic
- **Services:** Encapsulated business logic (game state, validation)
- **Dependency Injection:** `Program.cs` registers services for components to use
- **CSS Utilities:** Pre-defined `.classes` for quick styling without writing CSS

---

## 🎓 Your Learning Path

### **Part 1: Setup & Context** (Done! You're here.)
- ✅ Verify environment
- ✅ Understand project structure
- ✅ Get oriented with Copilot

### **Part 2: Design-First Frontend** (`workshop/02-design.md`)
- Redesign the UI with a fresh theme
- Practice collaborative design with Copilot
- Learn CSS utilities and Blazor components

### **Part 3: Custom Quiz Master** (`workshop/03-quiz-master.md`)
- Create new question categories
- Build custom game modes
- Use agent instructions to define behavior

### **Part 4: Multi-Agent Development** (`workshop/04-multi-agent.md`)
- Build new features end-to-end
- Use agentic workflows for testing & validation
- Combine multiple AI agents for complex tasks

---

## 💬 Quick Command Reference

| What | Command |
|------|---------|
| **Run the app** | `cd SocOps && dotnet run` |
| **Build only** | `cd SocOps && dotnet build` |
| **Check .NET** | `dotnet --version` |
| **Open chat** | `Cmd+Shift+I` (Mac) or `Ctrl+Shift+I` (Windows/Linux) |
| **Agent Mode** | Type `@agent` in chat for agentic workflows |

---

## 🎮 First Thing to Try

1. **Run the app:**
   ```bash
   cd SocOps
   dotnet run
   ```

2. **Open the browser:**
   - Navigate to `http://localhost:5000`
   - Click play game
   - Try to get 5 in a row!

3. **Then explore in code:**
   - Open `SocOps/Components/GameScreen.razor`
   - Look at how components talk to services
   - Ask Copilot: *"How does the game validate a winning line?"*

---

## 🤝 You're Not Alone!

- **Workshop guide:** Check `workshop/GUIDE.md` for structured lessons
- **Copilot Agent:** Use `@agent` prefix for advanced workflows
- **Lab documentation:** Full step-by-step in `workshop/01-setup.md` through `workshop/05-complete.md`
- **GitHub Issues:** Questions? Look for existing discussions in the repo

---

## ✨ Pro Tips for Success

1. **Keep the browser open** while coding — live reload is your friend
2. **Use Copilot Chat** frequently — it knows this codebase structure
3. **Take incremental steps** — Build small features, commit often
4. **Experiment fearlessly** — This is a learning lab; breaking things is okay!
5. **Save checkpoints** — Use `Ctrl+Z` or Git to revert if needed

---

## 🎯 Ready?

You're all set! Your dev environment is configured, Copilot is ready, and the project structure makes sense. Pick your next adventure:

- 🎨 **Design enthusiast?** → Jump to `workshop/02-design.md`
- 🧠 **Logic lover?** → Explore `SocOps/Services/BingoLogicService.cs`
- 🤖 **AI curious?** → Try `@agent` in chat for automated workflows
- 📚 **Structured learner?** → Follow `workshop/GUIDE.md` start to finish

**Let's build something amazing!** 🚀

---

*Last updated: Ready for Blazor development with GitHub Copilot*
