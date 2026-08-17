# 📝 Chapter 6 Quiz — Loops & Iteration

---

**Chapter:** 06 — Loops & Iteration
**Total Questions:** 20
**Estimated Time:** 25–35 minutes

---

## Section 1: Multiple Choice (Select the best answer)

**1. How many times does this loop print "Hello"?**
```c
int i = 0;
while (i < 5) {
    printf("Hello ");
    i++;
}
```
a) 4
b) 5
c) 6
d) Infinite loop

**2. What is the output of this code?**
```c
for (int i = 0; i < 10; i += 3) {
    printf("%d ", i);
}
```
a) `0 3 6 9`
b) `0 3 6 9 12`
c) `3 6 9`
d) `0 1 2 3`

**3. Which loop guarantees at least one execution of the body?**

a) `for`
b) `while`
c) `do-while`
d) All loops guarantee this

**4. What does the `break` statement do inside a loop?**

a) Skips the rest of the current iteration and continues with the next
b) Exits the loop immediately
c) Pauses the loop and resumes later
d) Restarts the loop from the beginning

**5. How many times does the inner `printf` execute?**
```c
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 2; j++) {
        printf("*");
    }
}
```
a) 3
b) 5
c) 6
d) 8

**6. What does the `continue` statement do inside a loop?**

a) Exits the loop immediately
b) Skips the rest of the current iteration and continues with the next
c) Stops the program
d) Restarts the loop from the beginning

**7. Which of these creates an infinite loop?**

a) `for (int i = 0; i < 10; i++)`
b) `while (x < 10) { x++; }`
c) `while (1) { break; }`
d) `while (1) { }`

**8. What is the value of `i` when this loop finishes?**
```c
int i = 0;
while (i < 5) {
    i++;
}
```
a) 4
b) 5
c) 6
d) The loop never finishes

---

## Section 2: Short Answer (Explain in your own words)

**9. Explain the difference between `while` and `do-while` loops. Give an example where `do-while` is the better choice.**

*Your answer:*

**10. What is the key difference between `break` and `continue` in a loop? Give a brief example of when you'd use each.**

*Your answer:*

**11. Explain how nested loops execute. If the outer loop runs M times and the inner runs N times, how many total operations occur? Use the summit/delegate analogy.**

*Your answer:*

---

## Section 3: Fill in the Blank (Complete the sentence)

**12.** In a `for` loop header `for (init; condition; update)`, the ________ part runs only once, before the loop begins.

**13.** A `do-while` loop always executes its body at least ________.

**14.** Using `________` inside a loop skips the rest of the current iteration and jumps to the next one.

**15.** If you forget to update the loop variable in a `while` loop, you get an ________ loop.

**16.** The total number of iterations in nested loops is outer count ________ inner count.

---

## Section 4: Matching (Connect each item)

**17. Match each loop type to its best use case:**

| Loop | Use Case |
|------|----------|
| 1. `while` | a) When you must execute the body before checking the condition |
| 2. `for` | b) When the exact number of iterations is known in advance |
| 3. `do-while` | c) When the number of iterations depends on a condition that may be false initially |

**18. Match each loop control statement to its description:**

| Statement | Description |
|-----------|-------------|
| 1. `break` | a) Skips to the next iteration of the current loop |
| 2. `continue` | b) Exits the current loop immediately |
| 3. `goto` | c) Jumps to a labeled line in the code |

---

## Section 5: Practical Application

**19. The following program has multiple errors. Find and fix them:**

```c
#include <stdio.h>

int main(void)
{
    // Error 1: Intended to print 0-4
    int i = 0;
    while (i < 5);
        printf("%d ", i);
        i++;
    
    // Error 2: Intended to print 1-5
    for (int j = 0; j <= 5; j++)
        printf("%d ", j);
    
    // Error 3: Intended to print "0 1 2"
    for (int i = 0; i < 3; i++);
        printf("%d ", i);
    
    return 0;
}
```

List each error and write the corrected version:

*Your answer:*

**20. Write a complete C program that:**
- Declares an integer `n = 5`
- Uses a `for` loop to calculate the sum of numbers from 1 to n (the result should be 15)
- Uses a `while` loop that prints a countdown from n to 1, then "Done!"
- Uses a `do-while` loop to implement a simple password prompt (hardcode password as "cipher")
- Uses nested `for` loops to print an n×n grid of asterisks

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **b) 5** — The loop runs while `i < 5`, for i = 0, 1, 2, 3, 4 (5 iterations). *(Section 6.1)*
2. **a) `0 3 6 9`** — i starts at 0, increments by 3: 0, 3, 6, 9. When i=12, the condition `12 < 10` is false. *(Section 6.2)*
3. **c) `do-while`** — The condition is checked after the body, so the body always runs at least once. *(Section 6.3)*
4. **b) Exits the loop immediately** — `break` terminates the loop and execution continues after the loop. *(Section 6.4)*
5. **c) 6** — Outer loop runs 3 times, inner loop runs 2 times each. 3 × 2 = 6. *(Section 6.5)*
6. **b) Skips the rest of the current iteration and continues with the next** — `continue` jumps to the update/condition check. *(Section 6.4)*
7. **d) `while (1) { }`** — The condition `1` is always true, and there's no `break` or update. *(Section 6.1)*
8. **b) 5** — When `i` reaches 5, the condition `5 < 5` is false, and the loop exits. *(Section 6.1)*

### Section 2: Short Answer

9. **Model answer:** `while` checks the condition BEFORE the body — the body may execute zero times. `do-while` checks the condition AFTER the body — the body always executes at least once. Use `do-while` for menu systems where the menu must display at least once before the user chooses to exit. *(Section 6.3)*

10. **Model answer:** `break` exits the loop entirely; `continue` skips only the current iteration. Example: Use `break` when you find the first match in a search. Use `continue` when you encounter invalid data and want to skip it without terminating the search. *(Section 6.4)*

11. **Model answer:** The outer loop runs once, then the inner loop runs completely (all N iterations). Then the outer loop runs again, and the inner loop runs completely again. Total operations = M × N. Like a summit with M countries and N delegates per country: M × N total handshakes. *(Section 6.5)*

### Section 3: Fill in the Blank

12. **initialization** — `int i = 0;` runs once at the start. *(Section 6.2)*
13. **once** — The condition is checked after the first execution. *(Section 6.3)*
14. **continue** — `continue` skips the rest of the current iteration. *(Section 6.4)*
15. **infinite** — The condition never becomes false. *(Section 6.1)*
16. **multiplied by** (or **times**) — Total = outer × inner. *(Section 6.5)*

### Section 4: Matching

17. **1 → c, 2 → b, 3 → a** *(Sections 6.1–6.3)*
18. **1 → b, 2 → a, 3 → c** *(Section 6.4)*

### Section 5: Practical Application

19. **Four errors found:**

    1. **Semicolon after `while (i < 5);`** — The semicolon terminates the `while` statement. The `printf` and `i++` are NOT part of the loop — they run once after the loop (which is infinite because i never increments). Fix: remove the semicolon and add braces.
    2. **Missing braces on the for loop** — `for (int j = 0; j <= 5; j++) printf("%d ", j);` — This is technically correct for a single statement, but without braces it's easy to add a second statement that unexpectedly runs outside the loop.
    3. **Loop prints 0-5 instead of 1-5** — `j <= 5` runs 6 times (0,1,2,3,4,5). Fix: initialize `int j = 1` or use `j < 6`.
    4. **Semicolon after `for (...)`** — `for (int i = 0; i < 3; i++);` ends the for statement immediately. The `printf("%d ", i);` runs once after the loop, but `i` is out of scope (declared inside for). Fix: remove the semicolon.

    **Corrected version:**
    ```c
    #include <stdio.h>

    int main(void)
    {
        // Fixed: prints 0-4
        int i = 0;
        while (i < 5) {             // Fixed: removed semicolon
            printf("%d ", i);
            i++;
        }
        
        // Fixed: prints 1-5
        for (int j = 1; j <= 5; j++) {  // Fixed: start at 1
            printf("%d ", j);
        }
        
        // Fixed: prints "0 1 2"
        for (int i = 0; i < 3; i++) {   // Fixed: removed semicolon
            printf("%d ", i);
        }
        
        return 0;
    }
    ```

20. **Model answer:**
    ```c
    #include <stdio.h>

    int main(void)
    {
        int n = 5;
        
        // For loop: sum 1 to n
        int sum = 0;
        for (int i = 1; i <= n; i++) {
            sum += i;
        }
        printf("Sum 1 to %d = %d\n", n, sum);  // 15
        
        // While loop: countdown
        int count = n;
        while (count > 0) {
            printf("%d ", count);
            count--;
        }
        printf("Done!\n");
        
        // Do-while: password prompt
        int guess;
        do {
            printf("Enter password: ");
            scanf("%d", &guess);
        } while (guess != 1234);    // Hardcoded password: 1234
        printf("Access granted.\n");
        
        // Nested loops: n×n grid
        for (int row = 0; row < n; row++) {
            for (int col = 0; col < n; col++) {
                printf("* ");
            }
            printf("\n");
        }
        
        return 0;
    }
    ```

---

## 📊 Quick Self-Assessment

| Score (out of 20) | Assessment | Recommended Action |
|:-----------------:|-----------|-------------------|
| 18–20 | 🎉 Excellent | You're ready for Chapter 7! |
| 14–17 | ✅ Good | Review Sections 6.4 (loop control) and 6.5 (nested loops) |
| 10–13 | 🔄 Fair | Re-read Sections 6.1–6.3 and retry the hands-on exercises |
| Below 10 | 🔁 Needs Review | Re-read the full chapter and ensure you've done all the Try It Yourself exercises |

---

*→ When you're ready, continue to [Chapter 7: Functions →](../07-functions-the-building-blocks/01-why-functions.md)*
