# 📝 Chapter 10 Quiz — Memory Management

---

**Chapter:** 10 — Memory Management
**Total Questions:** 20
**Estimated Time:** 30–40 minutes

---

## Section 1: Multiple Choice

**1. Which function allocates memory on the heap?**

a) `alloc`
b) `malloc`
c) `create`
d) `new`

**2. What does `malloc` return if memory allocation fails?**

a) `0`
b) `-1`
c) `NULL`
d) It crashes the program

**3. Which function releases heap memory?**

a) `release`
b) `delete`
c) `free`
d) `dispose`

**4. What is a memory leak?**

a) Using too much memory at once
b) Allocated memory that is never freed
c) A pointer that points to freed memory
d) Running out of stack space

**5. What is a dangling pointer?**

a) A pointer that wasn't initialized
b) A pointer that points to freed memory
c) A pointer to a local variable
d) All of the above

**6. How does `calloc` differ from `malloc`?**

a) `calloc` is faster
b) `calloc` zero-initializes the memory
c) `calloc` doesn't require `free`
d) `calloc` allocates on the stack

**7. What does `realloc` do?**

a) Allocates memory and fills it with zeros
b) Resizes a previously allocated memory block
c) Frees memory and reallocates it
d) Allocates memory on the stack

**8. Which of the following best describes stack memory?**

a) Manual allocation, large, slow
b) Automatic allocation, fast, limited size
c) Must be freed explicitly
d) Can be resized with `realloc`

---

## Section 2: Short Answer

**9. Explain why you should set a pointer to `NULL` after calling `free`.**

*Your answer:*

**10. What happens if you forget to match every `malloc` with a `free` in a long-running program?**

*Your answer:*

**11. Why should you use `sizeof(int)` in `malloc(sizeof(int))` instead of just writing `malloc(4)`?**

*Your answer:*

---

## Section 3: Fill in the Blank

**12.** The function \_\_\_\_\_\_ allocates memory and initializes all bytes to zero.

**13.** A \_\_\_\_\_\_ pointer holds the address of memory that has already been freed.

**14.** The tool commonly used to detect memory leaks is called \_\_\_\_\_\_.

**15.** Memory allocated on the \_\_\_\_\_\_ is automatically deallocated when the function returns.

**16.** Every block allocated with `malloc` must eventually be released with \_\_\_\_\_\_.

---

## Section 4: Matching

**17. Match each function to its purpose:**

| Function | Purpose |
|----------|---------|
| 1. `malloc` | a) Resize an existing allocation |
| 2. `calloc` | b) Release allocated memory |
| 3. `realloc` | c) Allocate uninitialized memory |
| 4. `free` | d) Allocate zero-initialized memory |

**18. Match each concept to its description:**

| Concept | Description |
|---------|-------------|
| 1. Stack | a) Manual allocation, must be freed |
| 2. Heap | b) The tool that finds memory bugs |
| 3. Memory leak | c) Automatic allocation, fast, limited |
| 4. Valgrind | d) Forgetting to free allocated memory |

---

## Section 5: Practical Application

**19. Find and fix the errors in this program:**

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int *p = malloc(sizeof(int));
    int *q = malloc(sizeof(int));
    
    *p = 10;
    *q = 20;
    
    p = q;  // Intent: p and q both point to the same value
    
    free(p);
    free(q);
    
    printf("%d\n", *p);  // Print the value
    
    return 0;
}
```

**20. Write a complete C program that:**
- Allocates an array of 10 integers using `malloc`
- Fills it with values from 0 to 9
- Uses `realloc` to expand it to 15 integers
- Fills the new elements with values 10 to 14
- Prints all elements
- Frees the array
- Sets the pointer to `NULL` after freeing

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **b) `malloc`** — Allocates memory on the heap. *(Section 10.2)*
2. **c) `NULL`** — Always check the return value! *(Section 10.2)*
3. **c) `free`** — Returns memory to the heap. *(Section 10.2)*
4. **b) Allocated memory that is never freed** — Gradual memory consumption. *(Section 10.4)*
5. **d) All of the above** — Any pointer to invalid memory is dangerous. *(Section 10.5)*
6. **b) `calloc` zero-initializes the memory** — Sets every byte to 0. *(Section 10.3)*
7. **b) Resizes a previously allocated memory block** — May copy data to a new location. *(Section 10.3)*
8. **b) Automatic allocation, fast, limited size** — Stack is the backpack: fast, automatic, but small. *(Section 10.1)*

### Section 2: Short Answer

9. **Model answer:** After `free`, the pointer still holds the address of freed memory. If you accidentally use it, you access invalid memory (undefined behavior). Setting it to `NULL` ensures that any accidental dereference is caught by a `NULL` check. *(Section 10.5)*

10. **Model answer:** The program gradually consumes more and more memory. For a short program, this might not matter (OS reclaims on exit). For a long-running program (server, editor), it will eventually crash when memory is exhausted. *(Section 10.4)*

11. **Model answer:** `sizeof(int)` is portable — it works correctly on any system regardless of `int`'s size. Hardcoding `4` assumes a specific system and will break on systems where `int` has a different size. *(Section 10.2)*

### Section 3: Fill in the Blank

12. **`calloc`** — Allocates and zero-initializes. *(Section 10.3)*
13. **dangling** — Points to freed memory. *(Section 10.5)*
14. **Valgrind** (or **AddressSanitizer/ASan**) — Memory debugging tool. *(Section 10.6)*
15. **stack** — Stack memory is automatically managed. *(Section 10.1)*
16. **`free`** — Every allocation needs a matching free. *(Section 10.2)*

### Section 4: Matching

17. **1 → c, 2 → d, 3 → a, 4 → b** *(Sections 10.2–10.3)*
18. **1 → c, 2 → a, 3 → d, 4 → b** *(Sections 10.1, 10.4, 10.6)*

### Section 5: Practical Application

19. **Errors:**
    1. `p = q;` — This makes `p` point to the same memory as `q`, losing the original `p` allocation (memory leak)
    2. `free(p); free(q);` — Since `p` and `q` now point to the same block, this is a DOUBLE FREE!
    3. `printf("%d\n", *p);` — Using `p` after freeing (dangling pointer)
    
    **Corrected code:**
    ```c
    int main(void) {
        int *p = malloc(sizeof(int));
        int *q = malloc(sizeof(int));
        
        *p = 10;
        *q = 20;
        
        // If p and q should have the same VALUE:
        *p = *q;    // Copy value, not pointer
        
        // Or if both should point to same allocation:
        // free(q);
        // p = q;    // Make p point to q's allocation
        
        printf("%d %d\n", *p, *q);
        
        free(p);
        free(q);
        p = NULL;
        q = NULL;
        
        return 0;
    }
    ```

20. **Model answer:**
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void) {
        // Allocate initial array
        int *arr = malloc(10 * sizeof(int));
        if (arr == NULL) return 1;
        
        // Fill first 10 elements
        for (int i = 0; i < 10; i++) {
            arr[i] = i;
        }
        
        // Expand to 15 elements
        int *temp = realloc(arr, 15 * sizeof(int));
        if (temp == NULL) {
            free(arr);
            return 1;
        }
        arr = temp;
        
        // Fill new elements
        for (int i = 10; i < 15; i++) {
            arr[i] = i;
        }
        
        // Print all
        for (int i = 0; i < 15; i++) {
            printf("%d ", arr[i]);
        }
        printf("\n");
        
        // Clean up
        free(arr);
        arr = NULL;
        
        return 0;
    }
    ```

---

## 📊 Quick Self-Assessment

| Score | Assessment | Action |
|:-----:|-----------|--------|
| 18–20 | 🎉 Excellent | Ready for Chapter 11! |
| 14–17 | ✅ Good | Review sections 10.2–10.4 (malloc/free/leaks) |
| 10–13 | 🔄 Fair | Re-read sections 10.1–10.3 (stack vs heap) |
| < 10 | 🔁 Needs Review | Re-read full chapter |
