# BoxLings - Complete Implementation Plan

## 📋 Executive Summary

**BoxLings** is an interactive CLI-based learning tool for BoxLang, inspired by rustlings. It guides students through progressive exercises covering BoxLang fundamentals to advanced concepts, with automatic compilation checking, file watching, hints, progress tracking, and **integrated TDD/BDD learning**.

**Key Innovation:** Tests are visible and part of the learning experience. Students read tests first to understand requirements, then fix code to make tests pass. Later exercises have students write their own tests!

---

## 🎯 Project Overview

### Core Architecture (Based on Rustlings)

**Rustlings Inspiration:**

- 94 exercises across 24 topic directories
- Built in Rust with CLI using Clap
- Watch mode with file change detection
- State management for tracking progress
- Embedded exercise metadata in `info.toml`
- Solutions alongside exercises

**BoxLings Implementation:**

- Written **in BoxLang itself** (dogfooding!)
- CLI app using BoxLang's native CLI capabilities
- Watch mode using BoxLang's file monitoring
- JSON-based state management
- Exercise metadata in `info.json`
- Progressive exercise structure
- **Visible tests for TDD/BDD learning**
- Three file types: `.bxs` (script), `.bx` (class), `.bxm` (template)

---

## 🏗️ Project Structure

```
boxlings/
├── BoxLings.bx              # Main CLI class with main() entry point
├── Application.bx           # Optional: for framework features
├── box.json                 # CommandBox package descriptor
├── info.json                # Exercise metadata
├── .gitignore
├── README.md
├── LICENSE
├── PLAN.md                  # This file
├── EXERCISES.md             # Complete exercise breakdown
│
├── src/                     # BoxLings source code
│   ├── AppState.bx         # Progress tracking & state management
│   ├── Exercise.bx         # Exercise model
│   ├── InfoFile.bx         # Parses info.json
│   ├── Watcher.bx          # File change detection
│   ├── Runner.bx           # Executes and checks exercises
│   ├── Terminal.bx         # Terminal UI utilities
│   └── Utils.bx            # Helper functions
│
├── exercises/               # Student exercises (with intentional errors)
│   ├── 00_intro/
│   │   ├── intro1.bxs
│   │   └── intro2.bxs
│   ├── 01_variables/
│   │   ├── variables1.bxs
│   │   ├── variables2.bxs
│   │   ├── variables3.bxs
│   │   ├── variables3Test.bx      # 👈 VISIBLE test file
│   │   └── ...
│   ├── 20_classes/
│   │   ├── classes1.bx
│   │   ├── classes1Test.bx        # 👈 VISIBLE test file
│   │   └── ...
│   ├── 23_templating/
│   │   ├── templating1.bxm        # Template files!
│   │   └── ...
│   └── ...
│
├── solutions/               # Working solutions for comparison
│   ├── 00_intro/
│   │   ├── intro1.bxs
│   │   └── intro2.bxs
│   ├── 01_variables/
│   │   └── ...
│   └── ...
│
├── tests/
│   └── specs/              # TestBox specs for BoxLings itself
│       ├── CLITest.bx
│       ├── AppStateTest.bx
│       ├── RunnerTest.bx
│       └── ...
│
├── testbox/                # Installed via box install (gitignored)
│
├── .boxlings/              # User state directory (gitignored)
│   └── state.json          # Progress tracking
│
└── .github/                # CI/CD workflows
    └── workflows/
        └── tests.yml       # Run tests on push
```

### File Naming Conventions

- **`.bxs`** - Script files (most exercises - ~80 exercises)
- **`.bx`** - Class files (OOP exercises - ~40 exercises)
- **`.bxm`** - Template files (templating exercises - ~6 exercises)
- **`*Test.bx`** - TestBox test bundles (visible to students)

---

## 📚 Exercise Topics & Breakdown

### Phase 1: MVP - Core Fundamentals (50 exercises, 10 topics)

| Topic | Exercises | With Tests | File Types | Description |
|-------|-----------|------------|------------|-------------|
| **00_intro** | 2 | 0 | .bxs | Welcome, setup verification |
| **01_variables** | 6 | 2 | .bxs | Dynamic typing, var keyword, scopes |
| **02_functions** | 6 | 3 | .bxs | UDFs, closures, lambdas, arguments |
| **03_conditionals** | 4 | 3 | .bxs | if/else, ternary, switch |
| **04_data_types** | 8 | 5 | .bxs | string, numeric, boolean, date, arrays, structs |
| **05_arrays** | 4 | 3 | .bxs | Array operations, member functions |
| **06_scopes** | 5 | 3 | .bxs, .bx | variables, local, this, arguments, server |
| **07_structs** | 5 | 4 | .bxs | Struct literals, ordered structs, manipulation |
| **08_strings** | 6 | 4 | .bxs | String interpolation, multi-line, manipulation |
| **09_imports** | 4 | 2 | .bx | Import statements, class locators (java:, bx:) |

**Phase 1 Total:** 50 exercises, ~29 with tests (58%)

### Phase 2: Intermediate (40 exercises, 8 topics)

| Topic | Exercises | With Tests | File Types | Description |
|-------|-----------|------------|------------|-------------|
| **10_structs_advanced** | 4 | 4 | .bxs | Deep operations, merging, transformations |
| **11_null_handling** | 4 | 4 | .bxs | null, null coalescing, safe navigation |
| **12_error_handling** | 6 | 6 | .bxs | try/catch, throw, custom exceptions |
| **13_interfaces** | 4 | 3 | .bx | Implementing Java interfaces |
| **14_testing** | 5 | 5 | .bx | **Write your own tests! TDD/BDD** |
| **15_functional** | 8 | 6 | .bxs | map, filter, reduce, each, closures, lambdas |
| **16_async** | 6 | 4 | .bxs | Threads, futures, async programming |
| **17_components** | 3 | 2 | .bxs | BoxLang components (bx:http, bx:query, etc) |

**Phase 2 Total:** 40 exercises, ~34 with tests (85%)

### Phase 3: Advanced BoxLang Features (30 exercises, 6 topics)

| Topic | Exercises | With Tests | File Types | Description |
|-------|-----------|------------|------------|-------------|
| **18_casting** | 5 | 4 | .bxs, .bx | castAs operator, javaCast, type conversions |
| **19_quizzes** | 3 | 3 | .bxs, .bx | Comprehensive topic quizzes |
| **20_classes** | 8 | 6 | .bx | BoxLang classes, properties, constructors, metadata |
| **21_bifs** | 6 | 4 | .bxs | Built-in functions, member functions |
| **22_templating** | 4 | 2 | .bxm | bxm files, template syntax, output |
| **23_cli_apps** | 4 | 2 | .bx, .bxs | Building CLI apps, argument parsing |
| **24_java_interop** | 6 | 4 | .bx | Calling Java, creating objects, java: prefix |

**Phase 3 Total:** 36 exercises, ~25 with tests (69%)

### Grand Total

- **24 Topics** (removed modules for now)
- **126 Exercises**
- **~88 with Tests** (70%)
- **File Types:** ~80 .bxs, ~40 .bx, ~6 .bxm

See `EXERCISES.md` for complete exercise-by-exercise breakdown.

---

## 🎮 CLI Commands & Features

### Main Entry Point

```bash
boxlang BoxLings.bx [COMMAND] [OPTIONS]
```

### Commands

| Command | Description |
|---------|-------------|
| *(default)* | Start watch mode |
| `run [name]` | Run a specific exercise or the next pending one |
| `check-all` | Check all exercises and mark as done/pending |
| `reset <name>` | Reset an exercise to its original state |
| `hint [name]` | Show hint for an exercise |
| `show-test [name]` | Display the test file for an exercise |
| `list` | List all exercises with status |
| `--version` | Show version information |
| `--help` | Show help message |

### Watch Mode Features

- Auto-detects file changes in exercises
- Automatically reruns the current exercise
- Shows compilation errors with colors
- Shows TestBox test results (when test=true)
- Progress bar showing completion status
- File path links (clickable in modern terminals)
- Keyboard shortcuts:
  - `n` - Next exercise
  - `h` - Show hint
  - `t` - Show test file
  - `l` - List exercises
  - `r` - Manually rerun
  - `q` - Quit
  - `c` - Clear terminal

---

## 🧪 Exercise Validation System

### How Exercises Work

Each exercise is a BoxLang file with intentional errors or missing code. Students:

1. **Read the test file FIRST** (for exercises with test=true)
2. **Understand requirements** from test descriptions
3. **Fix the exercise** until it:
   - Compiles successfully (no syntax errors)
   - Runs successfully (no runtime errors)
   - Passes tests (if test=true)

### Three Testing Patterns

**Pattern A: Script Files (.bxs) with Output Testing**

```javascript
// exercises/01_variables/variables3.bxs
// Student fixes this
var x = 10;
var y = 20;
var sum = x + y;
println( "Sum: #sum#" );
```

```javascript
// exercises/01_variables/variables3Test.bx
// Student reads this FIRST
class extends="testbox.system.BaseSpec" {
    function run() {
        describe( "Variables Exercise 3", () => {
            it( "should calculate sum correctly", () => {
                savecontent variable="output" {
                    include "variables3.bxs";
                }
                expect( output ).toInclude( "Sum: 30" );
            });
        });
    }
}
```

**Pattern B: Class Files (.bx) with main()**

```javascript
// exercises/20_classes/classes1.bx
class {
    property name;
    property age;

    function init( required string name, required numeric age ) {
        variables.name = arguments.name;
        variables.age = arguments.age;
        return this;
    }

    function getInfo() {
        return "Name: #variables.name#, Age: #variables.age#";
    }

    function main( args = [] ) {
        var person = new classes1( "BoxLang", 1 );
        println( person.getInfo() );
    }
}
```

```javascript
// exercises/20_classes/classes1Test.bx
class extends="testbox.system.BaseSpec" {
    function run() {
        describe( "Classes Exercise 1", () => {
            it( "should create a person with properties", () => {
                var person = new classes1( "Luis", 40 );
                expect( person.getName() ).toBe( "Luis" );
                expect( person.getAge() ).toBe( 40 );
            });
        });
    }
}
```

**Pattern C: Template Files (.bxm)**

```xml
<!-- exercises/22_templating/templating1.bxm -->
<bx:set name="title" value="My Page">
<bx:output>
    <h1>#title#</h1>
    <p>Welcome to BoxLang!</p>
</bx:output>
```

### Exercise Metadata (info.json)

```json
{
  "format_version": 1,
  "welcome_message": "Welcome to BoxLings! We'll teach you BoxLang AND test-driven development...",
  "final_message": "Congratulations! You've mastered BoxLang fundamentals...",
  "exercises": [
    {
      "name": "intro1",
      "dir": "00_intro",
      "path": "exercises/00_intro/intro1.bxs",
      "test": false,
      "hint": "Enter 'n' to move on to the next exercise.",
      "skip_check_unsolved": true
    },
    {
      "name": "variables3",
      "dir": "01_variables",
      "path": "exercises/01_variables/variables3.bxs",
      "test": true,
      "test_path": "exercises/01_variables/variables3Test.bx",
      "hint": "Read the test file first! It shows exactly what your code should do.",
      "test_mode": "read"
    },
    {
      "name": "testing1",
      "dir": "14_testing",
      "path": "exercises/14_testing/testing1.bx",
      "test": true,
      "test_path": "exercises/14_testing/testing1Test.bx",
      "hint": "Now YOU write the tests! Follow the TestBox pattern.",
      "test_mode": "write"
    }
  ]
}
```

**New Fields:**

- `test_path` - Path to the visible test file
- `test_mode` - "read" (read tests, fix code) or "write" (write tests yourself)

---

## 🚀 Implementation Phases

### Phase 1: Core Infrastructure (Week 1-2)

- [ ] Create main `BoxLings.bx` CLI entry point
- [ ] Implement `InfoFile.bx` (parse info.json)
- [ ] Implement `Exercise.bx` model
- [ ] Implement `AppState.bx` (progress tracking with JSON)
- [ ] Implement `Runner.bx` (execute and validate exercises)
- [ ] Create basic CLI commands (run, hint, reset, show-test)
- [ ] Set up project structure
- [ ] Create box.json with TestBox devDependency

### Phase 2: Watch Mode & UI (Week 3)

- [ ] Implement `Watcher.bx` (file change detection)
- [ ] Implement `Terminal.bx` (colored output, progress bar)
- [ ] Build interactive watch mode with keyboard input
- [ ] Add terminal file links support
- [ ] Create welcome/completion screens
- [ ] Add test output formatting

### Phase 3: Exercise Creation - Basics (Week 4-5)

- [ ] **00_intro** (2 exercises)
- [ ] **01_variables** (6 exercises + 2 test files)
- [ ] **02_functions** (6 exercises + 3 test files)
- [ ] **03_conditionals** (4 exercises + 3 test files)
- [ ] **04_data_types** (8 exercises + 5 test files)
- [ ] Create corresponding solutions
- [ ] Write hints for each exercise

### Phase 4: Exercise Creation - Core (Week 6-7)

- [ ] **05_arrays** (4 exercises + 3 test files)
- [ ] **06_scopes** (5 exercises + 3 test files)
- [ ] **07_structs** (5 exercises + 4 test files)
- [ ] **08_strings** (6 exercises + 4 test files)
- [ ] **09_imports** (4 exercises + 2 test files)
- [ ] Create solutions and hints

### Phase 5: Testing & Polish (Week 8)

- [ ] Write comprehensive tests for BoxLings CLI
- [ ] Test all exercises on multiple platforms
- [ ] Create installation scripts
- [ ] Write comprehensive README
- [ ] Create .gitignore
- [ ] Add LICENSE

### Phase 6: Documentation & Launch (Week 9)

- [ ] Create GitHub repository
- [ ] Set up CI/CD for testing
- [ ] Create documentation
- [ ] Create tutorial/walkthrough
- [ ] Announce to BoxLang community

### Phase 7: Intermediate Topics (Week 10-12)

- [ ] Topics 10-17 (40 exercises)
- [ ] Focus on TDD/BDD learning in Topic 14
- [ ] Create solutions and tests

### Phase 8: Advanced Topics (Week 13-15)

- [ ] Topics 18-24 (36 exercises)
- [ ] Include template exercises (.bxm)
- [ ] Java interop exercises
- [ ] CLI app building exercises

---

## 📦 Technology Stack

- **Language**: BoxLang (dogfooding!)
- **Package Manager**: CommandBox (box.json)
- **Testing**: TestBox 6.0+ with BoxLang CLI runner
- **CLI Framework**: Native BoxLang CLI capabilities
- **File Watching**: BoxLang's built-in file monitoring or Java's WatchService
- **Terminal UI**: ANSI escape codes via BoxLang
- **State Management**: JSON files
- **JSON Parsing**: Native BoxLang JSON functions

---

## 🎓 Educational Philosophy

### Core Principles

1. **Learning by Fixing**: Exercises have intentional errors (rustlings approach)
2. **Progressive Difficulty**: Concepts build on each other
3. **Immediate Feedback**: Watch mode gives instant results
4. **Tests as Documentation**: Read tests to understand requirements
5. **TDD/BDD Integration**: Learn testing alongside language features
6. **Real-World Patterns**: Teach practical BoxLang idioms
7. **Compiler as Teacher**: Let BoxLang's error messages guide learning

### TDD/BDD Learning Progression

**Phase 1: Reading Tests (Topics 00-09)**

- Students read TestBox specs
- Understand test structure (describe, it, expect)
- Use tests as documentation
- Fix code to make tests pass

**Phase 2: Understanding Patterns (Topics 10-13)**

- See more complex test patterns
- Multiple assertions
- Setup/teardown (beforeEach, afterEach)
- Edge cases and error handling

**Phase 3: Writing Tests (Topic 14)**

- Students write their own TestBox specs
- Practice describe/it/expect syntax
- Learn to think in tests-first

**Phase 4: TDD Practice (Topics 15-24)**

- Apply TDD to all exercises
- Write test, watch it fail (RED)
- Write code to pass (GREEN)
- Refactor (REFACTOR)

---

## 🌟 Unique BoxLang Features to Highlight

### Language Features

- Dynamic typing with type inference
- Case-insensitive by default
- Multiple file types (.bx, .bxs, .bxm)
- Expression interpolation with `#`
- Multi-line strings (single quote!)
- Null coalescing `?:` and safe navigation `?.`
- Closure `=>` vs Lambda `->` distinction
- High-precision mathematics

### Runtime Features

- Built-in functions (BIFs) and member functions
- Component system (bx:http, bx:query, etc)
- Java interoperability (java: prefix)
- Async programming (bx:thread, runAsync)
- Multiple scopes (variables, local, this, arguments, server, etc)
- Class system with properties and metadata
- main() convention for CLI apps

---

## 📊 Success Metrics

- Number of exercises completed by students
- Time to complete each topic
- Community contributions (new exercises)
- GitHub stars/forks
- Adoption in BoxLang courses/workshops
- Student feedback on TDD/BDD learning

---

## 🔧 Technical Implementation Details

### Runner.bx - Core Validation Logic

```javascript
class {

    function checkExercise( required exercise ) {
        var result = {
            success: false,
            output: "",
            errors: []
        };

        try {
            // 1. Compile check
            var compiled = compileBoxLangFile( exercise.path );

            // 2. If has tests, show test location and run
            if ( exercise.test ) {
                println( "📝 Read the test first: #exercise.test_path#" );
                println( "" );
                println( "Running tests..." );

                var testResult = runTestBoxTests( exercise );
                result.output = testResult.output;
                result.success = testResult.success;

                if ( !testResult.success ) {
                    println( "" );
                    println( "💡 The test output shows what's expected vs actual." );
                }

                return result;
            }

            // 3. For non-test exercises, execute and check output
            var output = executeBoxLangFile( exercise.path );
            result.output = output;
            result.success = true;

        } catch( any e ) {
            result.errors.append( e.message );
        }

        return result;
    }

    private function runTestBoxTests( required exercise ) {
        var testPath = exercise.test_path;
        var result = { output: "", exitCode: 0 };

        // Run TestBox via CLI - it prints results to console
        bx:execute
            name="boxlang"
            arguments="testbox run --bundles=#testPath#"
            variable="result.output"
            errorVariable="result.errorOutput"
            returnVariable="result.exitCode"
            timeout="30" {
        }

        return {
            success: result.exitCode == 0,
            output: result.output ?: result.errorOutput,
            exitCode: result.exitCode
        };
    }
}
```

### AppState.bx - Progress Tracking

```javascript
class {
    property name="exercises" type="array";
    property name="currentIndex" type="numeric" default="0";
    property name="statePath" type="string" default=".boxlings/state.json";

    function init() {
        loadState();
        return this;
    }

    function loadState() {
        if ( fileExists( variables.statePath ) ) {
            var stateData = deserializeJSON( fileRead( variables.statePath ) );
            variables.currentIndex = stateData.currentIndex ?: 0;
            // Load done/pending status for each exercise
        }
    }

    function saveState() {
        var stateData = {
            currentIndex: variables.currentIndex,
            exercises: variables.exercises.map( e => {
                return { name: e.name, done: e.done };
            })
        };

        directoryCreate( getDirectoryFromPath( variables.statePath ), true, true );
        fileWrite( variables.statePath, serializeJSON( stateData ) );
    }

    function markCurrentDone() {
        variables.exercises[ variables.currentIndex ].done = true;
        saveState();
    }

    function moveToNext() {
        variables.currentIndex++;
        saveState();
    }
}
```

---

## 🤝 Next Steps

### Immediate (Weeks 1-2)

1. ✅ Create project structure
2. ✅ Write planning documents
3. ⏳ Implement core CLI (BoxLings.bx)
4. ⏳ Implement Runner.bx, AppState.bx
5. ⏳ Create box.json with TestBox

### Short-term (Weeks 3-5)

1. Build watch mode
2. Create first 20 exercises (00-02)
3. Test on real users
4. Iterate based on feedback

### Medium-term (Weeks 6-9)

1. Complete Phase 1 MVP (50 exercises)
2. Polish UI and error messages
3. Create comprehensive README
4. Launch to BoxLang community

### Long-term (Weeks 10-15)

1. Build Phase 2 (intermediate topics)
2. Build Phase 3 (advanced topics)
3. Gather community contributions
4. Consider advanced topics (modules, etc)

---

## 📝 Open Questions

1. **TestBox Reporter**: Currently using default console output - is this sufficient?
2. **Exercise Reset**: Should reset pull from git or embedded originals?
3. **Solutions Access**: When should students be able to see solutions?
4. **Hints System**: Progressive hints (hint 1, hint 2, etc) or single hint?
5. **Community Exercises**: Allow community to contribute via PRs?

---

## 📚 Resources

- **Rustlings**: https://github.com/rust-lang/rustlings
- **BoxLang Docs**: https://boxlang.ortusbooks.com/
- **TestBox Docs**: https://testbox.ortusbooks.com/
- **BoxLang CLI**: https://boxlang.ortusbooks.com/getting-started/running-boxlang/cli-scripting
- **TestBox CLI Runner**: https://testbox.ortusbooks.com/getting-started/running-tests/boxlang-cli-runner

---

**Version:** 1.0.0
**Last Updated:** February 7, 2026
**Status:** Planning Complete - Ready for Implementation
