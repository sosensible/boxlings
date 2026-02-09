# BoxLings AI Agent Instructions

## Project Overview

BoxLings is an **interactive CLI learning tool written IN BoxLang** (dogfooding!), inspired by Rust's rustlings. It teaches BoxLang fundamentals through progressive exercises with intentional bugs that students fix. The unique approach: **tests are visible and part of learning** - students read tests first to understand requirements (TDD/BDD pedagogy).

## Architecture

### Core Components (src/)

- **BoxLings.bx** - Main CLI entry point with `main()` function convention. Routes commands (watch, run, check-all, reset, hint, list)
- **AppState.bx** - Progress tracking with JSON persistence to `.boxlings/state.json`. Manages exercise completion state
- **Exercise.bx** - Exercise model with properties: name, dir, path, test, test_path, test_mode, hint, done, skip_check_unsolved
- **InfoFile.bx** - Parses `info.json` metadata (single source of truth for all exercises)
- **Runner.bx** - Executes exercises, compiles BoxLang code, runs TestBox tests. Returns structured results (compilationSuccess, testSuccess, errors)
- **Watcher.bx** - File monitoring for watch mode (auto-rerun on save)
- **Terminal.bx** - ANSI color utilities with 256-color support, banners, gradients, status messages

### Data Flow

```
info.json → InfoFile → Exercise objects → AppState (tracks progress)
                                       ↓
                              Runner (compile/test/execute)
                                       ↓
                              Terminal (display results)
```

## BoxLang-Specific Patterns

### File Types (Critical!)
- **.bxs** - Scripts (most exercises, ~80%). Executed directly with `include` or BoxLang runtime
- **.bx** - Classes (OOP exercises, ~40%). Must have `class {}` wrapper
- **.bxm** - Templates (templating exercises, ~6%). For HTML/template syntax

### TestBox Integration
Tests extend `testbox.system.BaseSpec` with BDD syntax:
```boxlang
class extends="testbox.system.BaseSpec" {
    function run() {
        describe("Topic", () => {
            it("should do something", () => {
                include "exercise.bxs";  // Execute exercise
                expect(variables.x).toBe(10);
            });
        });
    }
}
```

### Exercise Execution Patterns
- Scripts (.bxs): Use `include` to execute in-place, variables available in `variables` scope
- Classes (.bx): Instantiate with `new`, test methods directly
- Exercises with tests: Run via `boxlang testbox run` or TestBox runner
- No tests: Direct BoxLang execution checks for compilation/runtime errors

## Key Conventions

### info.json Structure
Single source of truth. Each exercise entry:
```json
{
  "name": "variables3",
  "dir": "01_variables",
  "path": "exercises/01_variables/variables3.bxs",
  "test": true,
  "test_path": "exercises/01_variables/variables3Test.bx",
  "test_mode": "read",
  "hint": "The test expects x=10, y=20, and sum=30."
}
```

**Critical fields:**
- `test: true` - Exercise has TestBox tests (run them!)
- `test_mode: "read"/"write"` - Students read vs write tests
- `skip_check_unsolved: true` - Skip I_AM_NOT_DONE marker check (intro exercises only)

### Exercise File Pattern
All exercise files must have placeholder errors (???, missing code, wrong values). Students fix to pass tests. Common patterns:
- `var x = ???;` - Placeholder for missing value
- Missing function declarations
- Incorrect return statements
- Type mismatches

### State Management
`.boxlings/state.json` tracks:
```json
{
  "currentIndex": 3,
  "lastUpdated": "2026-02-09 12:00:00",
  "exercises": [
    {"name": "intro1", "done": true},
    {"name": "intro2", "done": true},
    {"name": "variables1", "done": false}
  ]
}
```

## Developer Workflows

### Running BoxLings
```bash
boxlang BoxLings.bx               # Watch mode (default)
boxlang BoxLings.bx run variables3    # Run specific exercise
boxlang BoxLings.bx check-all     # Test all exercises
boxlang BoxLings.bx reset variables3  # Reset exercise to original
boxlang BoxLings.bx hint variables3   # Show hint
boxlang BoxLings.bx list          # List all exercises
```

### Testing BoxLings Itself
```bash
box install                       # Install TestBox
box test                          # Run BoxLings' own tests
```

### Creating New Exercises
1. Add entry to `info.json` (order matters!)
2. Create exercise file in `exercises/{dir}/{name}.bxs`
3. If has tests: Create `{name}Test.bx` with TestBox specs
4. Add solution to `solutions/{dir}/{name}.bxs`
5. Test the exercise: `boxlang BoxLings.bx run {name}`

## Critical Integration Points

### Terminal Colors
Use `Terminal.bx` methods, NOT raw ANSI codes:
- `printLine(text, color)` - 256-color support ("color81", or numeric 81)
- `printSuccess/Error/Warning/Info/Hint/Test()` - Status messages with icons
- `showBoxLangBanner()` - Gradient banner with random themes
- Always use provided utilities for consistency

### CLI Argument Parsing
BoxLang's `CLIGetArgs()` returns:
```boxlang
{
  "positionals": ["watch", "variables3"],  // Array of positional args
  "options": {"help": true, "version": false}  // Named options
}
```

### File Operations
- Use `expandPath()` for relative paths (exercise paths are workspace-relative)
- Check `fileExists()` before operations
- Use `include` for .bxs scripts (executes in current scope)
- JSON: `JSONDeserialize()` / `JSONSerialize()` (BoxLang native)

## Common Pitfalls

1. **Don't forget file types** - .bxs vs .bx have different execution models
2. **Test files must extend BaseSpec** - `class extends="testbox.system.BaseSpec"`
3. **Exercise order matters** - Controlled by `info.json` array order, not filesystem
4. **Variables scope** - In .bxs files, `var x=10` puts x in `variables` scope (testable)
5. **Path resolution** - All exercise paths in `info.json` are relative to project root
6. **State persistence** - Call `appState.save()` after marking exercises done

## BoxLang Language Notes (for AI coding)

- Dynamic typing, but `var` keyword required in function scope
- String interpolation: `"Hello #name#"` (not ${})
- Struct literals: `{key: "value"}` (loose syntax)
- Array/Struct member functions: `array.each()`, `struct.keyExists()`
- Function syntax: `function name(args) { return value; }`
- No semicolons required (but accepted)
- Case-insensitive function/variable names (convention: camelCase)
- **Async/Futures**: Use `asyncRun()`, `asyncAny()`, `asyncAll()` - NOT legacy `bx:thread`
- **File watching**: Watcher.bx uses Java's WatchService (NIO) for event-driven file monitoring (no polling!)

## Async Programming Patterns

Use BoxFutures for async operations, NOT legacy CFML threads:

```boxlang
// ✅ Modern BoxFuture approach with race condition
var watcher = new src.Watcher()
var fileFuture = asyncRun( () => watcher.watch( path, callback ) )
var inputFuture = asyncRun( () => CLIRead() )
var result = asyncAny( [ fileFuture, inputFuture ] ).get()

// ❌ Legacy thread approach (avoid)
bx:thread action="run" name="worker" { ... }
```

Key async BIFs:
- `asyncRun()` / `futureNew()` - Create CompletableFutures (preferred: asyncRun)
- `asyncAll()` - Wait for all futures to complete
- `asyncAny()` - Race futures, return first completion
- `.cancel()` - Cancel running futures
- `.get()` - Block until result available

## Quick Reference Files

- `README.md` - User-facing documentation
- `PLAN.md` - Complete implementation roadmap with exercise breakdown
- `TERMINAL_REFERENCE.md` - Color utilities guide
- `info.json` - Exercise metadata (single source of truth)
- `exercises/` - Student exercises (with bugs)
- `solutions/` - Working reference implementations
- `testbox/` - TestBox BDD framework (installed dependency)
