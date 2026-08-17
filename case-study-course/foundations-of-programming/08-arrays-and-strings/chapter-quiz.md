# 📝 Chapter 8 Quiz — Arrays & Strings

---

**Chapter:** 08 — Arrays & Strings
**Total Questions:** 20
**Estimated Time:** 25–35 minutes

---

## Section 1: Multiple Choice

**1. What is the index of the first element in a C array?**

a) -1
b) 0
c) 1
d) Depends on the declaration

**2. `int arr[5];` — what are the valid indices?**

a) 0 through 4
b) 1 through 5
c) 0 through 5
d) 1 through 4

**3. What does `char s[] = "Hi";` create?**

a) An array of size 2: `{'H', 'i'}`
b) An array of size 3: `{'H', 'i', '\0'}`
c) An array of size 3: `{'H', 'i', ' '}`
d) A string pointer

**4. Which function copies a string safely with a size limit?**

a) `strcpy`
b) `strncpy`
c) `strcmp`
d) `strlen`

**5. How do you correctly compare two strings `a` and `b`?**

a) `if (a == b)`
b) `if (strcmp(a, b) == 0)`
c) `if (strcpy(a, b))`
d) `if (a = b)`

**6. What is `sizeof(arr) / sizeof(arr[0])` used for?**

a) Getting the total bytes of the array
b) Getting the number of elements in the array
c) Getting the size of the first element
d) Getting the memory address of the array

**7. In a 2D array `int m[3][4]`, how many elements are there?**

a) 7
b) 12
c) 3
d) 4

**8. What marks the end of a C string?**

a) A newline character `\n`
b) A null terminator `\0`
c) A period `.`
d) The end of the array

---

## Section 2: Short Answer

**9. Why are C arrays zero-indexed? Explain using pointer arithmetic.**

*Your answer:*

**10. What happens when a C string doesn't have a null terminator? Why is this dangerous?**

*Your answer:*

**11. When passing an array to a function, why must you also pass the size separately?**

*Your answer:*

---

## Section 3: Fill in the Blank

**12.** An array stores elements of the _______ type in contiguous memory.

**13.** The function that returns the number of characters in a string (excluding `\0`) is _______.

**14.** A 2D array with 3 rows and 5 columns has _______ elements total.

**15.** To safely copy a string with a size limit, use _______ instead of `strcpy`.

**16.** Using `==` to compare two strings compares their _______, not their content.

---

## Section 4: Matching

**17. Match each function to its purpose:**

| Function | Purpose |
|----------|---------|
| 1. `strlen` | a) Copy string with size limit |
| 2. `strcpy` | b) Append one string to another |
| 3. `strncpy` | c) Get string length |
| 4. `strcat` | d) Copy string (unsafe, no size check) |

**18. Match each array concept to its description:**

| Concept | Description |
|---------|-------------|
| 1. Zero-indexing | a) Elements stored row by row in memory |
| 2. Row-major order | b) The first element is at index 0 |
| 3. Bounds checking | c) C does NOT do this automatically |

---

## Section 5: Practical Application

**19. Find and fix the errors in this program:**

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    char name[5] = "Alice";
    int scores[5] = {85, 90, 78, 92, 88};
    int target[5];
    
    strcpy(target, scores);
    
    for (int i = 0; i <= 5; i++) {
        printf("%d ", scores[i]);
    }
    
    if (name == "Alice") {
        printf("Name matches!\n");
    }
    
    return 0;
}
```

**20. Write a complete C program that:**
- Declares a 2D array `int matrix[3][4]` with values of your choice
- Uses nested loops to print it as a grid
- Calculates and prints the sum of all elements
- Declares a string `char city[] = "Geneva";` and prints its length using `strlen`
- Copies it into a new array `char copy[20]` using `strncpy`

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **b) 0** — C arrays are zero-indexed. *(Section 8.1)*
2. **a) 0 through 4** — `arr[5]` has indices 0, 1, 2, 3, 4. *(Section 8.1)*
3. **b) Size 3: `{'H', 'i', '\0'}`** — String literals automatically add `\0`. *(Section 8.4)*
4. **b) `strncpy`** — Copies up to n characters. *(Section 8.5)*
5. **b) `if (strcmp(a, b) == 0)`** — `==` compares pointers, not content. *(Section 8.5)*
6. **b) Number of elements** — Total bytes / bytes per element = count. *(Section 8.2)*
7. **b) 12** — 3 × 4 = 12 elements. *(Section 8.3)*
8. **b) Null terminator `\0`** — Marks the end of the string. *(Section 8.4)*

### Section 2: Short Answer

9. **Model answer:** `arr[i]` is syntactic sugar for `*(arr + i)`. When `i = 0`, we get `*(arr + 0)` = first element. This makes pointer arithmetic natural and consistent. *(Section 8.1)*

10. **Model answer:** Without `\0`, string functions (`printf("%s")`, `strlen`, etc.) don't know where the string ends. They keep reading memory until they happen to find a zero byte. This can read sensitive data, crash (segfault), or cause security vulnerabilities. *(Section 8.4)*

11. **Model answer:** When an array is passed to a function, it decays to a pointer. `sizeof(arr)` inside the function gives the pointer size (8 bytes), not the array size. The function cannot determine how many elements the array has — you must tell it explicitly. *(Section 8.2)*

### Section 3: Fill in the Blank

12. **same** — All elements in an array are the same type. *(Section 8.1)*
13. **`strlen`** — Returns the number of characters before `\0`. *(Section 8.5)*
14. **15** — 3 × 5 = 15. *(Section 8.3)*
15. **`strncpy`** — Copies up to n characters with size check. *(Section 8.5)*
16. **addresses** (or **pointers**) — `==` compares memory addresses, not the characters. *(Section 8.5)*

### Section 4: Matching

17. **1 → c, 2 → d, 3 → a, 4 → b** *(Section 8.5)*
18. **1 → b, 2 → a, 3 → c** *(Sections 8.1–8.2)*

### Section 5: Practical Application

19. **Errors:**
    1. `char name[5] = "Alice";` — No room for null terminator. Use `[6]` or let the compiler infer size.
    2. `strcpy(target, scores);` — `strcpy` works on strings, not int arrays. Use a loop instead.
    3. `for (int i = 0; i <= 5; i++)` — Off-by-one! `<= 5` accesses index 5, which is out of bounds. Use `< 5`.
    4. `if (name == "Alice")` — Compares pointers, not strings. Use `strcmp`.

20. **Model answer:**

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    // 2D array with values
    int matrix[3][4] = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9, 10, 11, 12}
    };
    
    // Print as grid using nested loops
    int sum = 0;
    for (int r = 0; r < 3; r++) {
        for (int c = 0; c < 4; c++) {
            printf("%4d", matrix[r][c]);
            sum += matrix[r][c];
        }
        printf("\n");
    }
    printf("Sum of all elements: %d\n", sum);
    
    // String operations
    char city[] = "Geneva";
    printf("City: %s, Length: %zu\n", city, strlen(city));
    
    char copy[20];
    strncpy(copy, city, sizeof(copy) - 1);
    copy[sizeof(copy) - 1] = '\0';
    printf("Copied: %s\n", copy);
    
    return 0;
}
```

---

## 📊 Quick Self-Assessment

| Score | Assessment | Action |
|:-----:|-----------|--------|
| 18–20 | 🎉 Excellent | Ready for Chapter 9! |
| 14–17 | ✅ Good | Review 8.4–8.5 (strings) |
| 10–13 | 🔄 Fair | Re-read 8.1–8.3 |
| < 10 | 🔁 Needs Review | Re-read full chapter |
