## Python Workflow

```
    [ START ]
        │
  1.  PLANNING      (Requirements & Design)
        │
  2.  SETUP         (Virtual Env & Packages)
        │
  ┌─────┴────────┐
  │ 3. CODE      │ <───┐
  │      │       │     │
  │    RUN       │   DEBUG
  │      │       │     │
  │    TESTS ────┼─────┘
  └─────┬────────┘
        │ (Pass)
        ▼
  4.  REFACTOR      (Clean up code)
        │
  5.  RELEASE       (Docs & Deployment)
        │
     [ END ]
```

### 1. Planning (The Strategy) 📋
This is where you define what you are building and how it will work. You decide on the features and the "logic" before touching the keyboard to avoid getting lost later.

### 2. Setup (The Foundation) 🛠️
You prepare your workspace. In Python, this usually means creating a Virtual Environment so your project’s tools don't interfere with other apps on your computer.

Key tools: venv, pip, conda.

### 3. Code Loop (The Engine) 🔄
This is the heart of the project. It’s a repeating cycle:

Code: You write the instructions.

Run: You execute the program to see it in action.

Tests/Debug: You check if the results are correct. If there is a "bug" (an error), you fix it and loop back to the start.

### 4. Refactor (The Polish) ✨
Once the code works, it might be messy or slow. Refactoring is the process of cleaning it up—making it faster and easier for other humans to read—without changing what it actually does.

Key tools: Ruff, Black, MyPy.

### 5. Release (The Launch) 🚀
The final step! You package your code so others can use it. This includes writing a manual (Documentation) and putting it on a server or a site like GitHub or PyPI.
