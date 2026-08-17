# 🧠 Foundations of Programming: From First Principles to Practical Mastery

### A Ground-Up Course for the Complete Beginner — Taught Through C

---

## 🎯 Who Is This Course For?

**You, if:**
- You have **never written a line of code** in your life
- Your background is in **International Relations, Humanities, Law, Social Sciences** — anything *except* Computer Science
- You've heard words like "pointer," "binary," or "compiler" and they sound like a foreign language
- You want to understand **how computers actually work**, not just how to copy-paste code from tutorials
- You're willing to be confused, frustrated, and delighted — often within the same five minutes

**This course is NOT for you if:**
- You already know how to program and just want to pick up syntax
- You're looking for a quick "learn to code in 30 days" shortcut
- You want to start with web development or mobile apps

---

## 🧭 Course Philosophy

Programming is not magic. It's not some arcane art reserved for math prodigies and genius hackers. It is **structured, logical thinking made manifest** — and you already have this skill.

Think about what you already do every day:

| What You Already Do | Programming Equivalent |
|---------------------|----------------------|
| Analyze **systems** with interconnected parts (a kitchen, a school, a city's transit network) | Design programs as systems of interacting functions and modules |
| Follow **protocols and rules** (recipes, forms, road rules) | Follow **syntax** and **APIs** — protocols for talking to computers |
| Track **state changes** (weather changing, prices rising, plans changing) | Manage **variables** and **control flow** — how data changes over time |
| Interpret **data with meaning** (receipts, schedules, grades) | Work with **data types** and **structures** — giving shape to information |
| Work within **hierarchies** (company → department → team) | Navigate **scope** and **organizational layers** in programs |
| Allocate **limited resources** (time, money, storage space) | Manage **memory** — the computer's most precious resource |

**Programming is the same skillset, applied to a different substrate.**

---

## 🏛️ Why C?

This course teaches **C** — not Python, not JavaScript, not Ruby.

> *"A language that doesn't affect the way you think about programming is not worth knowing."* — Alan Perlis

C is worth knowing because it is **transparent**. In C:
- Every variable occupies a specific amount of **memory** — you can see it, measure it
- Every **pointer** is a real memory address — not a metaphor
- Every function call creates a **stack frame** — you can trace it
- Every byte you allocate must be **freed** — or you will leak it

Python hides all of this. C reveals it.

If you learn C first:
1. You understand **what a computer actually does** — not just what a library does for you
2. Higher-level languages (Python, JavaScript, Go, Rust) will make *sense* — you'll see exactly what they're abstracting away
3. You'll never be helpless when something breaks — you can trace it down to the memory level
4. You'll write better code in *any* language because you understand the machine

---

## 📚 Course Structure

The course is divided into **5 Phases** across **17 Chapters** (plus quizzes):

```
Phase I:   Foundation (Chapters 00–02)       15–20 hours
Phase II:  The C Language (Chapters 03–12)   80–120 hours
Phase III: Data Structures & Algorithms (13–14) 30–40 hours
Phase IV:  The Big Picture (Chapter 15)      8–10 hours
Phase V:   Capstone Project (Chapter 16)     20–30 hours
                                  Total:    ~150–220 hours
```

At **10 hours per week**, this is approximately **4–5 months**.

### Chapter Map

```
┌────────────────────────────────────────────────────────────┐
│  PHASE I: FOUNDATION (No coding yet)                      │
├────────────────────────────────────────────────────────────┤
│  00  Foundations Before Code                               │
│  01  How Computers Work                                    │
│  02  Setting Up Your Tools                                 │
├────────────────────────────────────────────────────────────┤
│  PHASE II: THE C LANGUAGE                                  │
├────────────────────────────────────────────────────────────┤
│  03  Variables & Data Types                                │
│  04  Operators & Expressions                               │
│  05  Control Flow                                          │
│  06  Loops & Iteration                                     │
│  07  Functions — The Building Blocks                       │
│  08  Arrays & Strings                                      │
│  09  Pointers ← THE pivotal chapter                        │
│  10  Memory Management                                     │
│  11  Structures & Unions                                   │
│  12  File Input / Output                                   │
├────────────────────────────────────────────────────────────┤
│  PHASE III: DATA STRUCTURES & ALGORITHMS                   │
├────────────────────────────────────────────────────────────┤
│  13  Data Structures in C                                  │
│  14  Algorithms & Problem Solving                          │
├────────────────────────────────────────────────────────────┤
│  PHASE IV: THE BIG PICTURE                                 │
├────────────────────────────────────────────────────────────┤
│  15  How Programming Languages Work                        │
├────────────────────────────────────────────────────────────┤
│  PHASE V: APPLY EVERYTHING                                 │
├────────────────────────────────────────────────────────────┤
│  16  Capstone Project                                      │
└────────────────────────────────────────────────────────────┘
```

---

## 📁 How to Navigate This Course

Each chapter is a folder named `XX-chapter-name/`.

Inside each chapter folder you'll find:
- `01-section-name.md` — instructional content files
- `02-section-name.md` — more content...
- `chapter-quiz.md` — the end-of-chapter knowledge check

**Root-level files:**
- `config.json` — course metadata and settings
- `glossary.md` — lookup any term with an IR-friendly definition
- `template.md` — reference for how each section is structured
- `quiz-template.md` — reference for how each quiz is structured
- `cheatsheet-c.md` — a growing reference card for C syntax
- `learning-journal-template.md` — template for reflective journaling

**Assets** (diagrams, images, infographics) live in `assets/`:
- `assets/global/` — images used everywhere (memory model, architecture diagrams)
- `assets/chXX/` — images specific to that chapter

### Suggested Study Flow

1. **Read** the section content
2. **Type** every code example yourself (do NOT copy-paste)
3. **Complete** the "Try It Yourself" exercises
4. **Journal** for 2–3 minutes about what you learned
5. **Take** the chapter quiz (70% to pass)
6. **Ask**: "Can I explain this to someone else?"

---

## ✅ Prerequisites

- **A computer** (Windows, Mac, or Linux — any will do)
  - Minimum: 4GB RAM, 5GB free disk space
  - Recommended: 8GB RAM, 10GB free disk space
- **Basic computer literacy** (you can browse the web, save files, open applications)
- **Arithmetic** (addition, subtraction, multiplication — nothing beyond high school)
- **Curiosity and patience** — the first segfault is a rite of passage

That's it. No prior programming. No math beyond basic arithmetic. No CS degree.

---

## 🧪 How You Will Be Assessed

| Type | Purpose | Frequency |
|------|---------|-----------|
| **Section exercises** | Practice each concept immediately | Every section |
| **Chapter quizzes** | Verify understanding before moving on | End of every chapter |
| **Mini-projects** | Apply multiple concepts together | Every 2–3 chapters |
| **Capstone project** | Build something complete from scratch | Chapter 16 |
| **Learning journal** | Reflect on your progress and confusion | After every session |

---

## 📖 How to Use This Course (For Self-Study)

1. **Go chapter by chapter.** Do not skip ahead. Each chapter assumes you've mastered the previous one.
2. **Type the code.** Reading code is like reading sheet music — you're not learning to play until your fingers touch the keys.
3. **Break things.** Deliberately introduce bugs to see what happens. This is how you build an intuition for debugging.
4. **Use the glossary.** Any time a term feels fuzzy, look it up.
5. **Write in your learning journal.** After each session, write 2–3 sentences about what clicked and what didn't.
6. **Be patient with pointers.** Chapter 09 is the hardest chapter in the course. Everyone struggles here. It's normal.

---

## 🔗 References & Inspiration

This course was designed after surveying 50+ open-source programming education repositories on GitHub. Key influences include:

| Source | What We Took |
|--------|-------------|
| [Harvard CS50](https://cs50.harvard.edu/x/) | Teaching C first, the annotated code approach |
| [OSSU Computer Science](https://github.com/ossu/computer-science) | Curriculum rigor and sequencing |
| [Nand to Tetris](https://www.nand2tetris.org/) | First-principles philosophy |
| [The C Programming Language (K&R)](https://en.wikipedia.org/wiki/The_C_Programming_Language) | Precision and concision |
| [Project-Based Learning in C](https://github.com/practical-tutorials/project-based-learning) | Motivation for each concept |

---

## 📜 License

This course is licensed under **CC BY-NC-SA 4.0**.
You are free to share and adapt it for non-commercial purposes, with attribution and share-alike.

---

*Start with Chapter 00. Take a deep breath. You've got this.*
