# 15.2: Compilers vs. Interpreters — Two Ways to Run Code

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Distinguish between compiled and interpreted languages
- Explain the advantages and disadvantages of each approach
- Understand where C fits (compiled)
- Recognize hybrid approaches (bytecode + VM)

---

## 🧭 The Big Picture

> You receive a recipe in French and need to cook from it for English-speaking friends. Two approaches:
> - **Translate the entire recipe first (compiler):** Spend time translating the whole document, then cook from the translation. Fast cooking, but you must wait for translation before you can start.
> - **Translate step by step (interpreter):** Start cooking immediately, translating each step as you go. No wait time, but slower cooking and you might hit an unfamiliar term mid-recipe.
>
> These are the two fundamental approaches to running code. A **compiler** translates the entire program before running it. An **interpreter** translates and runs line by line.

---

## 📚 Core Content

### Compilers (C, C++, Rust, Go)

A compiler translates your entire source code into machine code before execution:

```
Source Code (.c) → [PREPROCESSOR] → [COMPILER] → Assembly (.s)
    → [ASSEMBLER] → Object Code (.o) → [LINKER] → Executable (.exe)
```

You already experienced this in Chapter 2! The compilation pipeline has four stages:

```bash
# Full compilation in one command
gcc program.c -o program

# Or step by step (what's really happening)
gcc -E program.c -o program.i    # 1. Preprocess
gcc -S program.i -o program.s    # 2. Compile to assembly
gcc -c program.s -o program.o    # 3. Assemble to machine code
gcc program.o -o program          # 4. Link into executable
```

**Advantages of compilation:**
- **Fast execution** — Machine code runs directly on the CPU
- **Error detection** — Many errors caught before running
- **Optimization** — The compiler can optimize the entire program
- **Distribution** — Ship the executable (others don't need the compiler)

**Disadvantages:**
- **Slower development** — Must recompile after every change
- **Platform-specific** — Must compile separately for Windows, Mac, Linux

### Interpreters (Python, JavaScript, Ruby, PHP)

An interpreter reads and executes code line by line:

```
Source Code (.py) → [INTERPRETER] → Run
                           ↓
              (No executable file produced)
```

```python
# Python is interpreted — no compilation step
x = 10
y = 20
print(x + y)  # This line is translated and executed NOW
```

**Advantages of interpretation:**
- **Faster development** — See results immediately after editing
- **Portability** — The interpreter handles platform differences
- **Dynamic features** — Easier to generate and run code on the fly

**Disadvantages:**
- **Slower execution** — Translation happens during runtime
- **Errors at runtime** — A bug in line 100 crashes only when that line executes
- **No optimization** — Can't see the whole program to optimize it

### Compiler vs. Interpreter Visual

![Compiler vs Interpreter](../assets/ch15/compiler-vs-interpreter.svg)

### Hybrid Approaches (Java, C#)

Some languages use a **hybrid** approach: compile to an intermediate **bytecode**, then interpret or JIT-compile the bytecode:

```text
Java Source (.java) → [COMPILER] → Bytecode (.class)
                                        ↓
                              [JVM - Java Virtual Machine]
                              Interprets or JIT-compiles bytecode
```

**LLVM** is another hybrid approach: compile to an intermediate representation (IR), then compile the IR to machine code for the specific platform:

```text
C Source → [Clang (frontend)] → LLVM IR → [LLVM (backend)] → Machine Code
```

This is how Clang (a C compiler) works — and why it can support multiple languages (C, C++, Rust, Swift) with the same backend optimizer.

### Where Does C Fit?

C is a **compiled language**. When you run `gcc program.c -o program`, you're invoking a full compilation pipeline that produces a standalone executable. This is deliberate — C's philosophy is that you should see and control the entire translation process.

---

## 🧪 Try It Yourself

> **Exercise 1: Which Approach?**
> For each language, guess whether it's compiled, interpreted, or hybrid: Python, C++, Java, JavaScript, Rust, Ruby.

> **Exercise 2: Advantage Analysis**
> You're writing a program that will run on millions of devices. Would you prefer compiled or interpreted? Why? What if you're writing a small script to process data for one-time use?

> **Exercise 3: The Four Stages**
> Run the four stages of compilation on a simple C program (as shown in the code block) and examine the output at each stage.

> **Exercise 4: Error Timing**
> In a compiled language, when do you discover errors? In an interpreted language? Which is better for development?

---

## 💡 Common Pitfalls

- ❌ **Thinking interpreters don't translate** — Interpreters DO translate code to machine code. They just do it line by line during execution instead of all at once beforehand.

- ❌ **Confusing compilation with linking** — Compilation translates source to machine code. Linking combines multiple machine code files into an executable. They're separate stages.

---

## 🔗 Connections to What You Know

> **Compilation is like translating a recipe before cooking. Interpretation is like translating each step as you go.**
>
> A pre-translated recipe (compiled) can be followed instantly and checked for errors in advance. A step-by-step translation (interpreted) is more flexible — you can adapt to unexpected ingredients — but slower and mistakes can happen mid-cooking.
>
> C chooses compilation because the course philosophy is: understand the translation process, don't hide it behind a live interpreter.

---

## ✅ Section Checklist

- [ ] I understand the difference between compilation and interpretation
- [ ] I can name examples of compiled and interpreted languages
- [ ] I understand the trade-offs in speed, development time, and portability
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [15.3: Nand to Tetris Preview →](./03-nand2tetris-preview.md)*
