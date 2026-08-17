# 📝 Chapter 9 Quiz — Pointers

---

**Chapter:** 09 — Pointers
**Total Questions:** 20
**Estimated Time:** 30–40 minutes

---

## Section 1: Multiple Choice

**1. What does `int *p;` declare?**

a) An integer named p
b) A pointer to an integer named p
c) A function that returns an integer pointer
d) An array of integers

**2. What does `*p` do (when used in a statement, not a declaration)?**

a) Multiplies p by something
b) Declares p as a pointer
c) Dereferences p — follows the address to get the value
d) Takes the address of p

**3. `arr[i]` in C is equivalent to what pointer expression?**

a) `arr + i`
b) `*arr + i`
c) `*(arr + i)`
d) `&arr[i]`

**4. When you add 1 to an `int *` pointer, how many bytes does the address increase by?**

a) 1 byte
b) 4 bytes (assuming 4-byte int)
c) 8 bytes
d) Depends on the value at the address

**5. Which of the following correctly swaps two integers using pointers?**

a) `void swap(int a, int b) { int t = a; a = b; b = t; }`
b) `void swap(int *a, int *b) { int t = *a; *a = *b; *b = t; }`
c) `void swap(int *a, int *b) { int t = a; a = b; b = t; }`
d) `void swap(int a, int b) { int *t = &a; a = b; b = *t; }`

**6. What happens if you dereference a NULL pointer?**

a) Nothing — it's safe
b) The program crashes with a segmentation fault
c) It returns 0
d) The pointer automatically points to valid memory

**7. If `arr` is an `int` array, what is `sizeof(arr)` inside the function where `arr` was passed as a parameter `int arr[]`?**

a) The total array size in bytes
b) The size of a pointer (8 bytes on 64-bit)
c) The number of elements in the array
d) Compiler error

**8. What does `int **pp;` declare?**

a) A pointer to an integer
b) A pointer to a pointer to an integer
c) An array of pointers
d) A function pointer

---

## Section 2: Short Answer

**9. Explain in your own words why C uses pass-by-value for function arguments and how pointers work around this limitation.**

*Your answer:*

**10. Why must you always pass the array size separately when passing an array to a function?**

*Your answer:*

**11. What's the difference between `*p++` and `*++p` when traversing an array?**

*Your answer:*

---

## Section 3: Fill in the Blank

**12.** The operator that returns the memory address of a variable is \_\_\_\_\_\_.

**13.** A \_\_\_\_\_\_ pointer doesn't point to any valid memory and should be checked before dereferencing.

**14.** `arr + 2` is equivalent to `&arr[` \_\_\_\_\_\_ `]`.

**15.** A \_\_\_\_\_\_ is a variable that stores the address of another variable.

**16.** The expression `*p` is called \_\_\_\_\_\_ the pointer.

---

## Section 4: Matching

**17. Match each concept to its description:**

| Concept | Description |
|---------|-------------|
| 1. `&` operator | a) Follows a pointer to access the value |
| 2. `*` operator (dereference) | b) A variable holding a memory address |
| 3. Pointer | c) Returns the address of a variable |
| 4. NULL | d) Special value meaning "points to nothing" |

**18. Match each use case to the correct pointer type:**

| Use Case | Pointer Type |
|----------|-------------|
| 1. Modify a pointer from a function | a) `int *` |
| 2. Traverse an array | b) `int **` |
| 3. Store the address of a variable | c) `int (*)(int, int)` |
| 4. Call a function indirectly | d) `int *` (as array traversal) |

---

## Section 5: Practical Application

**19. Find and fix the errors in this program:**

```c
#include <stdio.h>

void add_ten(int *p) {
    p = p + 10;  // Intent: add 10 to the value pointed to by p
}

int main(void) {
    int x = 5;
    int *ptr;
    
    *ptr = &x;
    add_ten(ptr);
    printf("%d\n", ptr);
    
    return 0;
}
```

**20. Write a complete C program that:**
- Declares `int values[5] = {10, 20, 30, 40, 50};`
- Declares an `int *` pointer and points it to the array
- Uses pointer arithmetic (`*(ptr + i)`) to print each element
- Writes a function `void double_values(int *arr, int size)` that doubles each element using pointers
- Calls the function and prints the doubled values

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **b) A pointer to an integer** — `int *p;` declares p as a pointer. *(Section 9.2)*
2. **c) Dereferences p — follows the address to get the value** — `*p` accesses the value at the stored address. *(Section 9.4)*
3. **c) `*(arr + i)`** — Array subscript is syntactic sugar for pointer arithmetic. *(Section 9.5)*
4. **b) 4 bytes** — `p + 1` increments by `sizeof(int)` = 4 bytes. *(Section 9.6)*
5. **b) `void swap(int *a, int *b) { int t = *a; *a = *b; *b = t; }`** — Dereferences to swap the original values. *(Section 9.4)*
6. **b) The program crashes with a segmentation fault** — Dereferencing NULL is undefined behavior. *(Section 9.2)*
7. **b) The size of a pointer (8 bytes on 64-bit)** — Array parameter decays to pointer. *(Section 9.5)*
8. **b) A pointer to a pointer to an integer** — `int **pp` requires two dereferences to reach the value. *(Section 9.7)*

### Section 2: Short Answer

9. **Model answer:** C uses pass-by-value, meaning the function receives a copy of the argument. To modify the original, we pass a pointer (the address) to the variable. The function dereferences the pointer to access and modify the original. *(Section 9.1)*

10. **Model answer:** When an array is passed to a function, it decays to a pointer. `sizeof(arr)` inside the function gives the pointer size (8 bytes), not the array size. The function can't know how many elements exist — you must pass the size separately. *(Section 9.5)*

11. **Model answer:** `*p++` dereferences the current element and then increments the pointer (post-increment). `*++p` increments the pointer first and then dereferences the new element (pre-increment). *(Section 9.6)*

### Section 3: Fill in the Blank

12. **`&`** — The address-of operator. *(Section 9.3)*
13. **NULL** — NULL pointer. *(Section 9.2)*
14. **2** — `arr + 2` = `&arr[2]`. *(Section 9.6)*
15. **pointer** — A variable that holds an address. *(Section 9.1)*
16. **dereferencing** — Following the pointer to access the value. *(Section 9.4)*

### Section 4: Matching

17. **1 → c, 2 → a, 3 → b, 4 → d** *(Sections 9.1–9.4)*
18. **1 → b, 2 → a (or d), 3 → a, 4 → c** *(Various sections)*

### Section 5: Practical Application

19. **Errors:**
    1. `int *ptr;` is uninitialized — contains garbage address. Should be `int *ptr = &x;`
    2. `*ptr = &x;` — This dereferences ptr (which is garbage!) and tries to store an address in an int. Should be `ptr = &x;`
    3. `p = p + 10;` — Adds 10 to the POINTER (address), not the value. Should be `*p += 10;`
    4. `printf("%d\n", ptr);` — Prints the address, not the value. Should be `printf("%d\n", *ptr);`
    
    **Corrected code:**
    ```c
    void add_ten(int *p) {
        *p += 10;  // Add 10 to the VALUE pointed to by p
    }
    
    int main(void) {
        int x = 5;
        int *ptr = &x;  // Initialize pointer to address of x
    
        add_ten(ptr);
        printf("%d\n", *ptr);  // Dereference to get the value
        
        return 0;
    }
    ```

20. **Model answer:**
    ```c
    #include <stdio.h>
    
    void double_values(int *arr, int size) {
        for (int i = 0; i < size; i++) {
            *(arr + i) *= 2;  // Double each element via pointer arithmetic
        }
    }
    
    int main(void) {
        int values[5] = {10, 20, 30, 40, 50};
        int *ptr = values;  // Pointer to first element
        
        // Print original using pointer arithmetic
        printf("Original: ");
        for (int i = 0; i < 5; i++) {
            printf("%d ", *(ptr + i));
        }
        printf("\n");
        
        // Double all values
        double_values(values, 5);
        
        // Print doubled values
        printf("Doubled:  ");
        for (int i = 0; i < 5; i++) {
            printf("%d ", *(ptr + i));
        }
        printf("\n");
        
        return 0;
    }
    ```

---

## 📊 Quick Self-Assessment

| Score | Assessment | Action |
|:-----:|-----------|--------|
| 18–20 | 🎉 Excellent | Ready for Chapter 10! |
| 14–17 | ✅ Good | Review sections 9.4–9.6 (dereferencing, pointers & arrays) |
| 10–13 | 🔄 Fair | Re-read sections 9.1–9.3 (pointer basics) |
| < 10 | 🔁 Needs Review | Re-read full chapter |
