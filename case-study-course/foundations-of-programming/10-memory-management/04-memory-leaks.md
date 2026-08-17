# 10.4: Memory Leaks — When Memory Disappears Forever

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Identify memory leaks in your programs
- Understand how memory leaks degrade system performance
- Use tools and patterns to prevent memory leaks

---

## 🧭 The Big Picture

> Someone borrows a book from the library, reads part of it, and then... simply walks away. The book sits unreturned forever, unavailable for anyone else. If enough readers do this, eventually there are no books left.
>
> A **memory leak** is exactly this: memory that was allocated with `malloc` but never released with `free`. The memory is still "in use" from the operating system's perspective, but your program has lost the pointer to it. It can never be freed. It sits there forever, gradually consuming all available memory.

---

## 📚 Core Content

### What Is a Memory Leak?

A memory leak occurs when you allocate memory and lose all references to it before calling `free`:

```c
void leak(void) {
    int *p = malloc(1000);  // Allocate
    p = NULL;               // Lost the pointer — can never free this!
}                           // 1000 bytes leaked
```

### How Leaks Happen

**1. Overwriting a pointer without freeing first:**
```c
int *data = malloc(100 * sizeof(int));
// ... use data ...
data = malloc(200 * sizeof(int));  // ❌ First allocation is now unreachable!
free(data);                         // Only frees the second allocation
```

**2. Returning without freeing:**
```c
int *process_data(void) {
    int *temp = malloc(5000);
    if (something_wrong) {
        return NULL;  // ❌ Forgot to free(temp) before returning!
    }
    return temp;  // Caller must free this
}
```

**3. Losing the pointer in a loop:**
```c
for (int i = 0; i < 1000; i++) {
    int *p = malloc(1000);  // Allocate 1000 bytes
    // ... use p ...
    // ❌ Forgot to free(p)!
}  // 1000 bytes leaked per iteration = 1 MB total!
```

### The Cost of Memory Leaks

| Duration | Impact |
|----------|--------|
| Short program (runs for seconds) | Minor — OS reclaims all memory when program exits |
| Long-running program (server, editor) | Critical — gradually consumes all RAM, eventually crashes |
| Embedded system | Immediate disaster — limited memory means early crash |

### Detecting Memory Leaks

**Visual inspection:** Look for `malloc`/`calloc`/`realloc` calls without matching `free`.

**Valgrind (Linux):** The gold standard for memory analysis:
```bash
valgrind --leak-check=full ./myprogram
```

**AddressSanitizer (GCC/Clang):** Compile with:
```bash
gcc -fsanitize=address -g myprogram.c -o myprogram
```

### Patterns to Prevent Leaks

**Pattern 1: Clear ownership**
```c
// Document who is responsible for freeing
// Returns: allocated array — CALLER must free
int *create_array(int size) {
    int *arr = malloc(size * sizeof(int));
    return arr;
}
```

**Pattern 2: Free before reassigning**
```c
int *data = malloc(1000);
// ... use ...
free(data);       // Free OLD allocation
data = malloc(2000);  // Then allocate new
```

**Pattern 3: Use a cleanup label**
```c
int *process(void) {
    int *data = malloc(10000);
    if (error_condition) {
        free(data);
        return NULL;
    }
    // More processing...
    return data;
}
```

---

## 🧪 Try It Yourself

> **Exercise 1: Create a Leak**
> Write a program that allocates 1000 bytes in a loop 100 times without freeing. Run it and observe system memory usage.

> **Exercise 2: Leak-Free Loop**
> Rewrite the above to free inside the loop. Verify no leak.

> **Exercise 3: Documentation**
> Write a function that returns a `malloc`'d buffer. Document clearly that the caller must free it.

---

## 💡 Common Pitfalls

- ❌ **"The OS will clean it up"** — True for short programs. False for servers, games, or any long-running process.
- ❌ **Losing the only pointer** — If you overwrite the pointer variable, the memory is leaked forever.
- ❌ **Thinking `free` is optional** — It's not. Every `malloc` needs a matching `free`.

---

## 🔗 Connections to What You Know

> **Memory leaks are like unreturned library books.**
>
> Every book not returned reduces the collection. Over time, the library stops serving readers. Responsible readers always return what they borrow. Responsible C programmers always free what they allocate.

---

## ✅ Section Checklist

- [ ] I understand what causes memory leaks
- [ ] I know how to prevent leaks with proper `free`
- [ ] I can identify potential leaks in code
- [ ] I document ownership of allocated memory
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [10.5: Dangling Pointers →](./05-dangling-pointers.md)*
