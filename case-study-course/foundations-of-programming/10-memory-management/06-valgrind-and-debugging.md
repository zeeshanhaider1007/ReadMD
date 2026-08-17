# 10.6: Valgrind and Debugging — Finding Memory Bugs

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Use Valgrind to detect memory leaks and errors
- Interpret Valgrind's output
- Use AddressSanitizer as an alternative
- Apply systematic debugging to memory issues

---

## 🧭 The Big Picture

> A well-run library has a system that tracks every book. Every loan, every return, every shelf is accounted for. When something goes wrong — a book never returned, a book shelved in the wrong place — the system can trace the issue and report it.
>
> **Valgrind** is your memory inspector. It runs your program in a controlled environment and reports every memory mistake: leaks, dangling pointer usage, invalid frees, and more.

---

## 📚 Core Content

### What is Valgrind?

Valgrind is a tool that detects memory management bugs. It runs your program in a "sandbox" and monitors every memory access.

```bash
valgrind --leak-check=full ./myprogram
```

### Detecting Memory Leaks

Consider a program with a leak:

```c
#include <stdlib.h>

int main(void) {
    int *p = malloc(100 * sizeof(int));
    p[0] = 42;
    // Forgot to free(p)!
    return 0;
}
```

Running Valgrind:
```bash
$ valgrind --leak-check=full ./leaky
==12345== HEAP SUMMARY:
==12345==     in use at exit: 400 bytes in 1 blocks
==12345==   total heap usage: 1 allocs, 0 frees
==12345== 
==12345== 400 bytes in 1 blocks are definitely lost
==12345==    at 0x4842588: malloc (vg_replace_malloc.c:393)
==12345==    by 0x10915B: main (leaky.c:4)
==12345== 
==12345== LEAK SUMMARY:
==12345==    definitely lost: 400 bytes in 1 blocks
```

### Detecting Invalid Access

```c
#include <stdlib.h>

int main(void) {
    int *p = malloc(5 * sizeof(int));
    free(p);
    p[0] = 10;  // Using freed memory!
    return 0;
}
```

```bash
==12346== Invalid write of size 4
==12346==    at 0x1091A0: main (invalid.c:6)
==12346==  Address 0x4a9c040 is 0 bytes inside a block of size 20 free'd
==12346==    at 0x48448E4: free (vg_replace_malloc.c:904)
==12346==    by 0x10919B: main (invalid.c:5)
```

### Common Valgrind Messages

| Message | What It Means |
|---------|--------------|
| `definitely lost` | Memory leak — you never freed it |
| `invalid write/read` | Using memory after `free` or out of bounds |
| `invalid free` | Calling `free` on a non-malloc'd pointer |
| `conditional jump depends on uninitialized value` | Using a variable before setting it |

### AddressSanitizer (ASan)

An alternative to Valgrind that's built into GCC and Clang:

```bash
gcc -fsanitize=address -g myprogram.c -o myprogram
./myprogram
```

ASan is faster than Valgrind and catches similar bugs. It reports:

```
==12347==ERROR: AddressSanitizer: heap-use-after-free
WRITE of size 4 at 0x60400000fff0 thread T0
    #0 0x401234 in main myprogram.c:6
```

### Systematic Memory Debugging

1. **Compile with `-g`** (debug symbols) for meaningful line numbers
2. **Run with Valgrind or ASan** to catch issues automatically
3. **Fix all warnings** — the compiler warns about potential issues
4. **Review your `malloc`/`free` pairs** — every allocation should have a matching deallocation
5. **Set pointers to `NULL` after `free`** — prevents accidental use

---

## 🧪 Try It Yourself

> **Exercise 1: Valgrind a Leaky Program**
> Write a small program with a memory leak. Run it with `valgrind --leak-check=full`. Read the output.

> **Exercise 2: Fix the Leaks**
> Fix the program from Exercise 1. Run Valgrind again. Confirm "0 bytes in 0 blocks are definitely lost."

> **Exercise 3: ASan Experiment**
> Compile a program with `-fsanitize=address` that uses memory after `free`. Run it. Compare the error message to Valgrind's.

> **Exercise 4: Debug a Given Program**
> Take a buggy program (like one of the earlier exercises) and use Valgrind to find and fix all memory issues.

---

## 💡 Common Pitfalls

- ❌ **Ignoring Valgrind output** — Every message is a real bug, even if the program "seems to work."
- ❌ **Not compiling with `-g`** — Without debug symbols, Valgrind can't show line numbers.
- ❌ **Thinking "it works" means no bugs** — Memory bugs often appear only under specific conditions.
- ❌ **Running Valgrind on optimized code** — Optimization can confuse Valgrind. Use `-O0` for debugging.

---

## 🔗 Connections to What You Know

> **Valgrind is like the UN inspection team.**
>
> They audit resource usage, track every allocation and deallocation, and report discrepancies. A clean audit means you're managing your resources responsibly. A dirty audit means you have leaks, double-frees, or dangling pointers that need fixing.

---

## ✅ Section Checklist

- [ ] I can run Valgrind to detect memory issues
- [ ] I can interpret Valgrind's output messages
- [ ] I can use AddressSanitizer as an alternative
- [ ] I follow systematic debugging for memory bugs
- [ ] I wrote a **journal entry** about what I learned today

---

*→ You've completed Chapter 10! Test your knowledge with the [Chapter 10 Quiz →](./chapter-quiz.md)*
