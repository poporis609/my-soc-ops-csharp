# Copilot Workspace Instructions

This file guides GitHub Copilot and AI agents when working on the Soc Ops project. It documents project conventions, architecture, and workflows that should be followed for all development.

---

## 🚀 Development Checklist

**Before committing any changes, verify:**

- [ ] `dotnet build SocOps/SocOps.csproj` passes with no errors
- [ ] All Razor components compile without warnings
- [ ] Code follows C# naming conventions (PascalCase for public members, camelCase for locals)
- [ ] No unused variables, imports, or breaking changes to component APIs
- [ ] CSS uses utility classes from `wwwroot/css/app.css` (avoid inline styles)
- [ ] Components properly handle state updates and re-renders

---

## 📚 Project Overview

**Soc Ops** is an interactive Social Bingo game for in-person events and team mixers. Players find people matching trivia questions, mark squares on a 5×5 board, and compete to get 5 in a row horizontally, vertically, or diagonally.

**Tech Stack:**
- **Frontend:** Blazor WebAssembly (C#, .NET 10)
- **UI Framework:** Custom CSS utilities (Tailwind-like patterns)
- **Runtime:** Runs entirely in the browser via WASM
- **State Management:** Event-driven services with localStorage persistence
- **Deployment:** GitHub Pages (auto-deploys on push to `main`)

---

## 🏗️ Architecture

### Directory Structure

```
SocOps/
├── Components/              # Reusable Blazor components
│   ├── BingoBoard.razor          # Main 5x5 grid display
│   ├── BingoSquare.razor         # Individual cell component
│   ├── BingoModal.razor          # Popup/dialog component
│   ├── GameScreen.razor          # Active game UI
│   └── StartScreen.razor         # Welcome & setup screen
├── Models/                  # Data structures
│   ├── GameState.cs              # Game phases, state, properties
│   ├── BingoSquareData.cs        # Single square properties
│   └── BingoLine.cs              # Winning line detection
├── Services/                # Business logic & state management
│   ├── BingoGameService.cs       # Game state, event subscriptions
│   └── BingoLogicService.cs      # Validation, scoring, win detection
├── Data/                    # Static data
│   └── Questions.cs              # Question bank & categories
├── Pages/                   # Routable pages
│   ├── Home.razor                # Landing page
│   ├── Counter.razor             # Example template
│   ├── Weather.razor             # API example
│   └── NotFound.razor            # 404 handler
├── Layout/                  # Layout & navigation
│   ├── MainLayout.razor
│   ├── MainLayout.razor.css
│   ├── NavMenu.razor
│   └── NavMenu.razor.css
├── wwwroot/                 # Static assets served to browser
│   ├── index.html                # HTML entry point
│   ├── css/
│   │   └── app.css              # 🎨 CSS utility classes (critical!)
│   ├── lib/                      # Bootstrap & dependencies
│   └── sample-data/
├── Program.cs               # App startup & DI registration
├── App.razor                # Root component
├── _Imports.razor           # Global using statements
└── SocOps.csproj            # Project file (.NET 10)
```

### Key Design Patterns

**Event-Driven State:**
- `BingoGameService` emits `OnStateChanged` event
- Components subscribe to state updates
- Automatic re-render when state changes

**Component Composability:**
- `BingoBoard` → loops over `BingoSquare` components
- `GameScreen` → orchestrates `BingoBoard` + `BingoModal`
- Stateless UI components receive data via @parameters

**Service Locator Pattern:**
- Services registered in `Program.cs`
- Components inject via `@inject BingoGameService GameService`
- Scoped lifetime ensures one instance per circuit

---

## ⌨️ Key Commands

```bash
# Build the project
dotnet build SocOps/SocOps.csproj

# Run development server (with hot reload)
dotnet run --project SocOps
# Open: http://localhost:5000 (port 5166 on some configs)

# Watch for changes & rebuild
dotnet watch run --project SocOps

# Production build
dotnet publish -c Release

# Clean build artifacts
dotnet clean SocOps/SocOps.csproj
```

---

## 🎨 Styling & CSS

**Custom Utility System** — Located in `wwwroot/css/app.css`

This project uses Tailwind-like utility classes. **Never write inline styles**; always use utilities:

### Common Classes

| Category | Examples |
|----------|----------|
| **Layout** | `.flex`, `.flex-col`, `.grid`, `.grid-cols-5`, `.items-center`, `.justify-center`, `.justify-between` |
| **Spacing** | `.p-4`, `.px-2`, `.py-3`, `.mb-4`, `.mx-auto`, `.gap-2`, `.space-y-3` |
| **Sizing** | `.h-full`, `.w-full`, `.min-h-full`, `.max-w-md`, `.aspect-square` |
| **Colors** | `.bg-white`, `.bg-accent` (primary blue), `.bg-marked` (green), `.text-gray-700`, `.text-green-600` |
| **Typography** | `.text-sm`, `.text-2xl`, `.font-bold`, `.font-semibold`, `.text-center`, `.leading-tight` |
| **States** | `.opacity-50`, `.hover:opacity-75`, `.cursor-pointer`, `.disabled:opacity-50` |

**Example Components:**
```razor
<div class="flex items-center justify-center min-h-full bg-gray-50">
  <div class="grid grid-cols-5 gap-2 p-4 bg-white rounded">
    @* BingoSquare components here *@
  </div>
</div>
```

---

## 💾 State Management

**BingoGameService** is the single source of truth:

```csharp
public class BingoGameService
{
    public GameState CurrentState { get; private set; }
    public event Action? OnStateChanged;
    
    // Methods that trigger state updates:
    public void StartGame();
    public void MarkSquare(int index);
    public BingoLine? CheckForWin();
    public void ResetGame();
}
```

**State Flow:**
1. Component calls `GameService.MarkSquare(index)`
2. Service validates & updates `CurrentState`
3. Service raises `OnStateChanged` event
4. Subscribed components re-render automatically
5. State persists to localStorage (if implemented)

**⚠️ Important Rules:**
- Never mutate state directly; always call service methods
- Components should be stateless (derived from state, not internal state)
- Use `@key` directive for list rendering if items have unique IDs

---

## 🎯 Component Guidelines

### Stateless UI Components
```razor
@* ✅ GOOD: Pure data → UI *@
@code {
    [Parameter] public BingoSquareData Square { get; set; }
    [Parameter] public EventCallback<int> OnClick { get; set; }
}
```

### State-Aware Components
```razor
@* ✅ GOOD: Subscribe to service *@
@implements IAsyncDisposable
@code {
    [Inject] public BingoGameService GameService { get; set; }
    
    protected override void OnInitialized()
    {
        GameService.OnStateChanged += StateHasChanged;
    }
    
    async ValueTask IAsyncDisposable.DisposeAsync()
    {
        GameService.OnStateChanged -= StateHasChanged;
    }
}
```

### Avoid
- ❌ Creating services in components (use DI)
- ❌ Storing game state in component fields (use `BingoGameService`)
- ❌ Direct DOM manipulation (let Blazor handle it)
- ❌ Inline styles (use `.css` utilities)

---

## 🧪 Testing Patterns

When writing tests (if TDD agents are used):

```csharp
[TestClass]
public class BingoLogicServiceTests
{
    [TestMethod]
    public void MarkSquare_WithValidIndex_UpdatesSquareState()
    {
        // Arrange
        var service = new BingoLogicService();
        var squareIndex = 12;
        
        // Act
        service.MarkSquare(squareIndex);
        
        // Assert
        Assert.IsTrue(service.Board[squareIndex].IsMarked);
    }
}
```

---

## 📋 Workflow: Adding a Feature

1. **Plan** — Write feature description in a comment or chat
2. **Create Tests** (optional) — Use TDD agents if available
3. **Implement** — Update components/services following patterns above
4. **Build & Test** — `dotnet build` must pass
5. **Review** — Check styling uses utilities, state flows properly
6. **Commit** — Write clear message, include testing notes

---

## 🚀 Deployment

**GitHub Pages:**
- Automatic deploy on every push to `main`
- Site: `https://{username}.github.io/{repo-name}`
- Built via GitHub Actions workflow

**Manual Build:**
```bash
dotnet publish -c Release
# Check: SocOps/bin/Release/net10.0/publish/wwwroot
```

---

## 📖 Documentation & Resources

- **Workshop Guide:** `workshop/GUIDE.md` — Structured learning path
- **Lab Parts:**
  - `workshop/01-setup.md` — Environment setup
  - `workshop/02-design.md` — UI redesign
  - `workshop/03-quiz-master.md` — Custom agents
  - `workshop/04-multi-agent.md` — TDD workflows
- **Styling:** `.github/instructions/css-utilities.instructions.md`
- **Design:** `.github/instructions/frontend-design.instructions.md`
- **Custom Agents:** `.github/agents/` (TDD, UI Review, Quiz Master)

---

## 🤖 Using Custom Agents

Available agents in `.github/agents/`:

| Agent | Purpose |
|-------|---------|
| `tdd.agent.md` | Orchestrate full TDD cycle |
| `tdd-red.agent.md` | Write failing tests |
| `tdd-green.agent.md` | Minimal implementation |
| `tdd-refactor.agent.md` | Improve code quality |
| `ui-review.agent.md` | Review UI/UX decisions |
| `quiz-master.agent.md` | Create custom quiz themes |
| `pixel-jam.agent.md` | Scavenger hunt mode |

**Usage in Chat:**
```
@agent tdd
Create a new feature: users can filter questions by category
```

---

## 💡 Best Practices

1. **Keep components small** — Single responsibility, ~50 lines max
2. **Use dependency injection** — Never `new` up services
3. **Test state transitions** — Services should be testable
4. **CSS utility classes first** — Only create new classes when truly needed
5. **Document breaking changes** — Especially in component APIs
6. **Commit frequently** — Small commits are easier to review and revert
7. **Use events for cross-component communication** — Avoid tight coupling

---

## ❓ Troubleshooting

| Issue | Solution |
|-------|----------|
| Port 5000 already in use | `dotnet run --project SocOps -- --urls "http://localhost:5001"` |
| Component not re-rendering | Check if service raises `OnStateChanged` event |
| CSS not applying | Verify class name in `app.css`, check for typos |
| Build errors after pull | `dotnet clean && dotnet build` |
| Hot reload not working | Restart dev server: `Ctrl+C` then `dotnet run` |

---

## 🎯 Quick Start

For new developers:

1. Read [WELCOME_TOUR.md](WELCOME_TOUR.md)
2. Run `cd SocOps && dotnet run`
3. Open http://localhost:5000
4. Read `Components/GameScreen.razor` to understand flow
5. Ask Copilot: *"Explain the BingoSquare component"*

---

**Last Updated:** April 2026  
**For Issues:** Check workshop/ folder or README.md references
