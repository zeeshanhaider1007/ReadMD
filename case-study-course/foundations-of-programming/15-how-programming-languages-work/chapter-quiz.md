# 📝 Chapter 15 Quiz — How Programming Languages Work

---

**Chapter:** 15 — How Programming Languages Work
**Total Questions:** 20
**Estimated Time:** 25–35 minutes

---

## Section 1: Multiple Choice

**1. Where does C sit on the programming language abstraction ladder?**

a) At the very top (like Python)
b) At the very bottom (machine code)
c) In the middle — high enough to be productive, low enough to be transparent
d) C is not on the abstraction ladder

**2. What is the key difference between a compiler and an interpreter?**

a) Compilers are faster; interpreters are slower
b) Compilers translate all code before execution; interpreters translate line by line
c) Compilers only work on Windows; interpreters work on any OS
d) Compilers check types; interpreters don't

**3. What is a NAND gate's output when both inputs are 1?**

a) 0
b) 1
c) It depends on the previous state
d) undefined

**4. Which of the following is true about C's type system?**

a) C is dynamically typed
b) C is statically typed and strongly typed
c) C is statically typed and weakly typed
d) C has no type system

**5. Which programming paradigm does C primarily support?**

a) Object-oriented
b) Functional
c) Imperative/Procedural
d) Logic programming

**6. What does static typing mean?**

a) Variables can only hold numbers
b) Types are checked at compile time
c) Variables cannot change their value
d) The program runs on a single thread

**7. Which language uses a hybrid approach (compiles to bytecode, runs on a VM)?**

a) C
b) Python
c) JavaScript
d) Java

**8. In Python, what happens if you try to add a string and an integer with `+`?**

a) The integer is automatically converted to a string
b) The string is automatically converted to an integer
c) A TypeError is raised at runtime
d) It works without error

---

## Section 2: Short Answer

**9. Explain the "no magic" philosophy of C. Why is this valuable for learning programming?**

*Your answer:*

**10. What is the difference between static typing and dynamic typing? Give one advantage of each.**

*Your answer:*

**11. Name and describe the four pillars of object-oriented programming.**

*Your answer:*

---

## Section 3: Fill in the Blank

**12.** The lowest level of the abstraction ladder is ________ code.

**13.** A ________ translates source code into machine code ALL AT ONCE before execution.

**14.** The ________ system determines what operations are allowed on data.

**15.** In C, you can pass a function as an argument using a ________ ________.

**16.** The Nand to Tetris course builds an entire computer system starting from a single ________ gate.

---

## Section 4: Matching

**17. Match each language to its primary execution model:**

| Language | Execution Model |
|----------|----------------|
| 1. C | a) Interpreted |
| 2. Python | b) Compiled |
| 3. Java | c) Interpreted (dynamic, duck-typed) |
| 4. JavaScript | d) Hybrid (compiled to bytecode, runs on JVM) |

**18. Match each paradigm to its key characteristic:**

| Paradigm | Characteristic |
|----------|---------------|
| 1. Imperative | a) Functions as first-class citizens |
| 2. Object-Oriented | b) Step-by-step statements changing state |
| 3. Functional | c) Bundling data and methods into objects |

---

## Section 5: Practical Application

**19. For each of these code snippets, identify the paradigm(s) used:**

a) ```c
int x = 10, y = 20;
int result = x + y;
printf("%d", result);
```

b) ```python
class Dog:
    def __init__(self, name):
        self.name = name
    def bark(self):
        return f"{self.name} says Woof!"
```

c) ```javascript
[1,2,3,4].map(n => n * n).filter(n => n > 5)
```

**20. Write a paragraph explaining why learning C first makes you a better programmer in ANY language. Include at least three specific concepts from this course that transfer to other languages.**

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **c) In the middle** — C provides abstraction while keeping the machine visible. *(Section 15.1)*
2. **b) Compilers translate all code before execution; interpreters translate line by line** — The fundamental difference in execution model. *(Section 15.2)*
3. **a) 0** — NAND(1, 1) = 0. All other combinations produce 1. *(Section 15.3)*
4. **c) C is statically typed and weakly typed** — Static (compile-time checking) + weak (implicit conversions). *(Section 15.4)*
5. **c) Imperative/Procedural** — C organizes code as sequential statements and functions. *(Section 15.5)*
6. **b) Types are checked at compile time** — The compiler verifies type correctness before running. *(Section 15.4)*
7. **d) Java** — Java compiles to bytecode which runs on the Java Virtual Machine. *(Section 15.2)*
8. **c) A TypeError is raised at runtime** — Python is strongly typed and won't do implicit string-to-int conversion. *(Section 15.4)*

### Section 2: Short Answer

9. **Model answer:** The "no magic" philosophy means C doesn't hide what the computer is doing. Memory allocation is explicit (malloc/free). Pointers are explicit. Type conversions are explicit. This is valuable because you understand what's really happening — when you later use a language that hides these details, you understand what it's hiding and can make better decisions. *(Section 15.1)*

10. **Model answer:** Static typing checks types at compile time (like C). Advantage: catches errors before running. Dynamic typing checks types at runtime (like Python). Advantage: faster to write, more flexible, no type declarations needed. *(Section 15.4)*

11. **Model answer:** (1) Encapsulation — bundling data and methods, hiding internals. (2) Inheritance — creating new classes from existing ones. (3) Polymorphism — same interface, different implementations. (4) Abstraction — hiding complexity behind simple interfaces. *(Section 15.5)*

### Section 3: Fill in the Blank

12. **machine** — Machine code (binary) is the lowest level. *(Section 15.1)*
13. **compiler** — Translates the entire program before execution. *(Section 15.2)*
14. **type** — The type system defines valid operations. *(Section 15.4)*
15. **function pointer** — C supports function pointers for callbacks. *(Section 15.5)*
16. **NAND** — The single primitive from which everything is built. *(Section 15.3)*

### Section 4: Matching

17. **1 → b, 2 → a, 3 → d, 4 → c** *(Sections 15.1–15.2)*
18. **1 → b, 2 → c, 3 → a** *(Section 15.5)*

### Section 5: Practical Application

19. **a) Imperative/Procedural** — step-by-step statements, function calls. **b) Object-Oriented** — class with data (name) and methods (bark). **c) Functional** — map and filter with anonymous functions (lambdas). *(Section 15.5)*

20. **Model answer:** Learning C first makes you a better programmer in any language because: (1) You understand **memory management** — when you use Python's lists, you know they're dynamically allocated arrays. (2) You understand **pointers** — when you use Java references, you know they're pointers under the hood. (3) You understand **the stack and heap** — you know why recursive functions can overflow and why heap allocation exists. These concepts are universal — C just makes them visible instead of hiding them. *(Whole course reflection)*

---

## 📊 Quick Self-Assessment

| Score | Assessment | Action |
|:-----:|-----------|--------|
| 18–20 | 🎉 Excellent | Ready for the Capstone! |
| 14–17 | ✅ Good | Review sections 15.3–15.5 (Nand2Tetris, types, paradigms) |
| 10–13 | 🔄 Fair | Re-read sections 15.1–15.2 (abstraction, compiler vs interpreter) |
| < 10 | 🔁 Needs Review | Re-read full chapter |

---

*Next: [Chapter 16: Capstone Project →](../16-capstone-project/01-project-overview.md)*
