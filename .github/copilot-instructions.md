# Copilot Workspace Instructions

## 🚀 Development Checklist (Required Before Commit)

**Always verify:**

- [ ] `dotnet build SocOps/SocOps.csproj` passes with no errors
- [ ] `dotnet test` passes (when tests exist) 
- [ ] Linting: No unused variables, imports, or style violations
- [ ] Code follows C# conventions (PascalCase for public members)
- [ ] CSS uses utility classes from `wwwroot/css/app.css` (no inline styles)
- [ ] Components properly handle state updates

---

## 📚 Quick Overview

**Soc Ops** is a Social Bingo game built with Blazor WebAssembly (.NET 10). Players find people matching trivia questions, mark a 5×5 board, and win with 5 in a row.

**Tech:** Blazor WASM (C#) + Custom CSS Utilities + Event-Driven State Management

---

## 🏗️ Architecture

```
SocOps/
├── Components/         # Blazor components (.razor files)
│   ├── BingoBoard.razor      # Main 5x5 grid
│   ├── BingoSquare.razor     # Individual cell
│   ├── GameScreen.razor      # Active game UI
│   └── StartScreen.razor     # Welcome screen
├── Models/             # Data structures (GameState, BingoLine)
├── Services/           # Business logic
│   ├── BingoGameService.cs   # State + events
│   └── BingoLogicService.cs  # Validation
├── Data/               # Static data (Questions.cs)
├── Pages/              # Routable pages (Home.razor)
└── wwwroot/            # Static assets
    └── css/app.css     # Utility classes
```

---

## ⌨️ Key Commands

```bash
dotnet build SocOps/SocOps.csproj    # Build
dotnet run --project SocOps          # Dev server (http://localhost:5000)
dotnet watch run --project SocOps    # Watch mode with hot reload
dotnet test                           # Run tests
```

---

## 🎨 Styling

Use custom utility classes — **never inline styles**:

| Category | Examples |
|----------|----------|
| Layout | `.flex`, `.grid`, `.grid-cols-5`, `.items-center`, `.justify-center` |
| Spacing | `.p-4`, `.mb-2`, `.mx-auto`, `.gap-2` |
| Colors | `.bg-accent`, `.bg-marked`, `.text-gray-700` |
| Typography | `.text-xl`, `.font-bold`, `.text-center` |

---

## 💾 State Management

`BingoGameService` is the single source of truth:
- Stores `CurrentState` (game board, phase, selections)
- Emits `OnStateChanged` event when updated
- Components subscribe to re-render automatically
- Never mutate state directly; call service methods

---

## 🧩 Component Patterns

**Stateless (Pure Data → UI):**
```razor
[Parameter] public BingoSquareData Square { get; set; }
[Parameter] public EventCallback<int> OnClick { get; set; }
```

**State-Aware (Subscribe to Events):**
```razor
@implements IAsyncDisposable
@code {
    [Inject] public BingoGameService GameService { get; set; }
    protected override void OnInitialized() 
        => GameService.OnStateChanged += StateHasChanged;
}
```

---

## 📖 Documentation

- **Workshop:** `workshop/GUIDE.md` (structured learning)
- **Styling Guide:** `.github/instructions/css-utilities.instructions.md`
- **Design Guide:** `.github/instructions/frontend-design.instructions.md`
- **Agents:** `.github/agents/` (TDD, UI Review, Quiz Master)

---

## 🤖 Available Agents

In chat, use: `@agent [name]`

| Agent | Purpose |
|-------|---------|
| `tdd` | Full test-driven development cycle |
| `tdd-red` | Write failing tests |
| `tdd-green` | Minimal implementation |
| `tdd-refactor` | Code quality improvements |
| `ui-review` | Design & UX feedback |
| `quiz-master` | Generate quiz themes |

---

## ✨ Best Practices

- Keep components small (~50 lines max)
- Use dependency injection; never `new` services
- Store state in services, not components
- Test state transitions
- Commit frequently with clear messages
- Use events for cross-component communication

---

## 🔗 Quick Links

- [WELCOME_TOUR.md](../WELCOME_TOUR.md) — Developer onboarding
- [AGENT_QUICK_START.md](../AGENT_QUICK_START.md) — Agent reference
- [GitHub Pages Deployment](../README.md) — Deploys automatically on push

**Status:** ✅ Ready for development  
**Last Updated:** April 2026
