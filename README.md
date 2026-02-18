# 🥊 BoxLings

> Small exercises to get you used to reading and writing **BoxLang** code while learning **Test-Driven Development (TDD)**!

Inspired by [rustlings](https://github.com/rust-lang/rustlings), BoxLings is an interactive CLI tool that guides you through learning BoxLang fundamentals through hands-on exercises with intentional errors. You fix the code, run tests, and progress through topics at your own pace.

**What makes BoxLings special?** We teach you **TDD/BDD** alongside BoxLang! Tests are visible and part of the learning experience. Read tests first to understand requirements, then fix code to make them pass.

---

## ✨ Features

- 🎯 **126 Progressive Exercises** across 24 topics
- 🧪 **TDD/BDD Learning** - Read and write TestBox tests
- 👀 **Watch Mode** - Auto-rerun on file changes
- 💡 **Hints System** - Get help when stuck
- 📊 **Progress Tracking** - Resume where you left off
- 🎨 **Beautiful CLI** - Colored output, progress bars
- 📝 **Three File Types** - Scripts (.bxs), Classes (.bx), Templates (.bxm)
- ✅ **Solutions Included** - Compare your code
- 🚀 **Built in BoxLang** - Dogfooding at its finest!

---

## 📋 Prerequisites

- **BoxLang 1.0+** installed ([Installation Guide](https://boxlang.ortusbooks.com/getting-started/installation))
- **CommandBox** (optional, for development) ([Install CommandBox](https://commandbox.ortusbooks.com/setup/installation))

---

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/ortus-boxlang/boxlings.git
cd boxlings
```

### 2. Start Learning

```bash
boxlang BoxLings.bx
```

That's it! BoxLings will:

- Show you a welcome message
- Start **watch mode**
- Display the first exercise
- Auto-rerun when you save changes

---

## 🎮 How to Use

### Watch Mode (Default)

```bash
boxlang BoxLings.bx
```

Watch mode automatically:

- Shows current exercise
- Watches for file changes
- Reruns exercise on save
- Shows test results (if exercise has tests)

**Keyboard Shortcuts:**

- `n` - Next exercise (after completing current)
- `h` - Show hint
- `t` - Show test file
- `l` - List all exercises
- `r` - Manually rerun current exercise
- `c` - Clear terminal
- `q` - Quit

### Run Specific Exercise

```bash
boxlang BoxLings.bx run variables3
```

### Check All Exercises

```bash
boxlang BoxLings.bx check-all
```

### Reset an Exercise

```bash
boxlang BoxLings.bx reset variables3
```

### Show Hint

```bash
boxlang BoxLings.bx hint variables3
```

### Show Test File

```bash
boxlang BoxLings.bx show-test variables3
```

### List All Exercises

```bash
boxlang BoxLings.bx list
```

---

## 📚 Learning Path

### Phase 1: Core Fundamentals (50 exercises)

Perfect for beginners and those new to BoxLang:

1. **Introduction** (2) - Get started
2. **Variables** (6) - Dynamic typing, var keyword
3. **Functions** (6) - UDFs, closures, lambdas
4. **Conditionals** (4) - if/else, ternary, switch
5. **Data Types** (8) - Strings, numbers, booleans, arrays, structs
6. **Arrays** (4) - Array operations and member functions
7. **Scopes** (5) - variables, local, this, arguments
8. **Structs** (5) - Struct manipulation
9. **Strings** (6) - Interpolation, multi-line, operations
10. **Imports** (4) - Import classes, java: prefix

### Phase 2: Intermediate (40 exercises)

Dive deeper into BoxLang:

11. **Structs Advanced** (4) - Deep operations, merging
12. **Null Handling** (4) - Elvis operator, safe navigation
13. **Error Handling** (6) - try/catch, throw, exceptions
14. **Interfaces** (4) - Implementing Java interfaces
15. **Testing** (5) - **Write your own tests!**
16. **Functional** (8) - map, filter, reduce, lambdas
17. **Async** (6) - Threads, futures, async programming
18. **Components** (3) - bx:http, bx:query, etc.

### Phase 3: Advanced (36 exercises)

Master BoxLang-specific features:

19. **Casting** (5) - castAs, javaCast, conversions
20. **Quizzes** (3) - Comprehensive reviews
21. **Classes** (8) - OOP, properties, metadata
22. **BIFs** (6) - Built-in functions, member functions
23. **Templating** (4) - .bxm files, template syntax
24. **CLI Apps** (4) - Building CLI tools
25. **Java Interop** (6) - Calling Java, java: prefix

---

## 🧪 TDD/BDD Learning Journey

BoxLings teaches you test-driven development alongside BoxLang:

### Step 1: Reading Tests (Topics 1-10)

**You learn to:**

- Read TestBox specs
- Understand `describe()` and `it()` blocks
- Interpret expectations: `expect().toBe()`, `expect().toInclude()`
- Use tests as documentation

**Example:**

```javascript
// Read this test FIRST
class extends="testbox.system.BaseSpec" {
    function run() {
        describe( "Variables Exercise 3", () => {
            it( "should calculate sum correctly", () => {
                // Your code should set x=10, y=20, sum=30
                expect( sum ).toBe( 30 );
            });
        });
    }
}
```

### Step 2: Understanding Patterns (Topics 11-14)

**You see:**

- Multiple assertions
- Setup/teardown (`beforeEach`, `afterEach`)
- Edge cases and error handling
- Complex test scenarios

### Step 3: Writing Tests (Topic 14: Testing)

**Now YOU write tests!**

- Practice `describe` / `it` / `expect` syntax
- Learn to think tests-first
- Write your own TestBox specs

### Step 4: TDD Practice (Topics 15-25)

**Apply full TDD cycle:**

- Write test (RED)
- Write code to pass (GREEN)
- Refactor (REFACTOR)

---

## 📂 Project Structure

```
boxlings/
├── BoxLings.bx              # Main CLI entry point
├── box.json                 # Package descriptor
├── info.json                # Exercise metadata
├── exercises/               # Your workspace - fix these!
│   ├── 00_intro/
│   │   ├── intro1.bxs      # Exercise files
│   │   └── intro2.bxs
│   ├── 01_variables/
│   │   ├── variables3.bxs
│   │   └── variables3Test.bx   # Test files (visible!)
│   └── ...
├── solutions/               # Working solutions
└── .boxlings/              # Your progress (auto-created)
    └── state.json          # Progress tracking
```

---

## 🎓 Exercise Format

### Exercises WITHOUT Tests

Simple syntax fixes - compilation is the check:

```javascript
// exercises/01_variables/variables1.bxs
// TODO: Add the missing keyword
function main() {
    x = 5;  // <-- Fix this!
    println( "x = #x#" );
}
```

### Exercises WITH Tests

**Read the test FIRST:**

```javascript
// exercises/01_variables/variables3Test.bx
class extends="testbox.system.BaseSpec" {
    function run() {
        describe( "Variables Exercise 3", () => {
            it( "should initialize x with value 10", () => {
                include "variables3.bxs";
                expect( variables.x ).toBe( 10 );
            });
        });
    }
}
```

**Then fix the exercise:**

```javascript
// exercises/01_variables/variables3.bxs
// TODO: Read variables3Test.bx first!
// TODO: Initialize x with the value 10

// Fix this
x = ???

println( "x = #x#" );
```

---

## 🛠️ Development

### Install TestBox (for developing BoxLings itself)

```bash
box install
```

### Run BoxLings Tests

```bash
box run-script test
```

### Add New Exercise

1. Create exercise file in `exercises/{topic}/`
2. Optionally create test file: `exercises/{topic}/{name}Test.bx`
3. Add entry to `info.json`
4. Create solution in `solutions/{topic}/`
5. Test it!

---

## 🤝 Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Add your exercises or improvements
4. Write tests for new features
5. Submit a pull request

See `CONTRIBUTING.md` for detailed guidelines.

---

## 📖 Resources

- **BoxLang Documentation**: https://boxlang.ortusbooks.com/
- **TestBox Documentation**: https://testbox.ortusbooks.com/
- **BoxLang CLI Guide**: https://boxlang.ortusbooks.com/getting-started/running-boxlang/cli-scripting
- **BoxLang GitHub**: https://github.com/ortus-boxlang/boxlang
- **Rustlings** (inspiration): https://github.com/rust-lang/rustlings

---

## 📝 License

MIT License - see [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **Rustlings** - The original inspiration for this project
- **Ortus Solutions** - For creating BoxLang
- **BoxLang Community** - For feedback and contributions

---

## 💬 Community & Support

- **Community Forum**: https://community.ortussolutions.com/c/boxlang/42
- **Slack**: https://boxteam.ortussolutions.com/
- **Issues**: https://github.com/ortus-boxlang/boxlings/issues

---

## 🎯 Goals

BoxLings aims to:

- ✅ Make learning BoxLang fun and interactive
- ✅ Teach TDD/BDD as a core skill
- ✅ Provide immediate feedback and guidance
- ✅ Build confidence through progressive difficulty
- ✅ Create a community of BoxLang learners

---

**Happy Learning! 🚀**

Start your BoxLang journey:

```bash
boxlang BoxLings.bx
```
