# 📝 Chapter 5 Quiz — Control Flow

---

**Chapter:** 05 — Control Flow
**Total Questions:** 20
**Estimated Time:** 25–35 minutes

---

## Section 1: Multiple Choice (Select the best answer)

**1. Which of the following values is considered FALSE in C?**

a) -1
b) 0
c) `'0'` (the character zero)
d) 100

**2. What does the following code print?**
```c
int x = 5;
if (x = 0) {
    printf("True");
} else {
    printf("False");
}
```

a) True
b) False
c) Nothing — there's a compile error
d) Neither — the program crashes

**3. How many times does the word "Hello" print?**
```c
int x = 1;
if (x > 0)     printf("Hello ");
if (x > 0)     printf("Hello ");
if (x > 0)     printf("Hello ");
```

a) 0
b) 1
c) 2
d) 3

**4. Which keyword is used to exit a `switch` case and prevent fall-through?**

a) `exit`
b) `stop`
c) `break`
d) `continue`

**5. What does the following switch statement print when `x = 2`?**
```c
switch (x) {
    case 1: printf("A ");
    case 2: printf("B ");
    case 3: printf("C "); break;
    default: printf("D ");
}
```

a) `B`
b) `B C`
c) `A B C`
d) `A B C D`

**6. What is the output of this code?**
```c
int a = 10, b = 20;
int max = (a > b) ? a : b;
printf("%d", max);
```

a) 10
b) 20
c) 0
d) Nothing — there's a syntax error

**7. Which of the following correctly checks if `x` is between 5 and 10 (inclusive)?**

a) `if (5 <= x <= 10)`
b) `if (x >= 5 && x <= 10)`
c) `if (x > 5 && x < 10)`
d) `if (x >= 5 || x <= 10)`

**8. What does short-circuit evaluation prevent in the following code?**
```c
if (ptr != NULL && *ptr == 42)
```

a) It prevents the condition from running at all
b) It prevents dereferencing a NULL pointer if `ptr` is NULL
c) It prevents the `if` statement from executing
d) It prevents `ptr` from being modified

---

## Section 2: Short Answer (Explain in your own words)

**9. Explain why `if (x = 5)` is NOT checking whether x equals 5, and what it actually does instead. How can you protect yourself from this bug?**

*Your answer:*

**10. What is "fall-through" in a `switch` statement? Give one example of when it's a bug and one example of when it's intentional.**

*Your answer:*

**11. When should you use the ternary operator (`? :`) instead of an `if-else` statement? When should you NOT use it?**

*Your answer:*

---

## Section 3: Fill in the Blank (Complete the sentence)

**12.** In C, any ________ value is considered true.

**13.** The ________ statement takes an integer expression and jumps to the matching constant case.

**14.** The ternary operator has three parts: ________, ________, and the two possible results.

**15.** To check a range in C, you must use the ________ operator to combine two comparisons.

**16.** Without a ________ statement, execution in a `switch` falls through to the next case.

---

## Section 4: Matching (Connect each item)

**17. Match each construct to its best use case:**

| Construct | Use Case |
|-----------|----------|
| 1. `if-else` | a) Choosing between two simple values in one line |
| 2. `if-else if-else` | b) Testing one value against 4+ constants |
| 3. `switch` | c) Simple binary decision with multiple statements |
| 4. Ternary `? :` | d) Multiple conditions checked in order of priority |

**18. Match each value to its truth value in C:**

| Value | Truth Value |
|-------|-------------|
| 1. 0 | a) True |
| 2. -5 | b) False |
| 3. `'A'` | c) True |
| 4. `'\0'` (null char) | d) False |

---

## Section 5: Practical Application

**19. The following program has multiple errors. Find and fix them:**

```c
#include <stdio.h>

int main(void)
{
    int score = 85;
    
    if (score >= 90);
        printf("Grade: A\n");
    else if (score >= 80);
        printf("Grade: B\n");
    else if (score >= 70);
        printf("Grade: C\n");
    
    char grade = 'B';
    switch (grade) {
        case 'A':
            printf("Excellent\n");
        case 'B':
            printf("Good\n");
        case 'C':
            printf("Average\n");
    }
    
    int x = 10;
    int message = x > 5 ? printf("Big\n") : printf("Small\n");
    
    return 0;
}
```

List each error and write the corrected version:

*Your answer:*

**20. Write a complete C program that:**
- Reads an integer from the user (use `scanf` or just assign a value)
- Uses nested `if-else` to determine whether the number is:
  - Positive AND even
  - Positive AND odd
  - Negative (any)
  - Zero
- Prints the appropriate message for each case
- Also uses the ternary operator to print "high" if the absolute value is > 50, or "low" otherwise

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **b) 0** — Only zero is false. Negative numbers, non-zero characters, and positive numbers are all true. *(Section 5.1)*
2. **b) False** — `if (x = 0)` ASSIGNS 0 to x. The result of the assignment is 0 (the value assigned), which is false. So the `else` branch runs. This is actually a rare case where the bug produces the "correct" output — but x was changed to 0! *(Section 5.1)*
3. **d) 3** — Each `if` statement is independent (not chained). All three conditions are true, so all three print. *(Section 5.2)*
4. **c) `break`** — `break` exits the current `switch` case. Without it, execution falls through to the next case. *(Section 5.3)*
5. **b) `B C`** — `case 2` matches and prints "B". Since there's no `break` after `case 2`, execution falls through to `case 3` and prints "C". The `break` after `case 3` stops the fall-through. *(Section 5.3)*
6. **b) 20** — `a > b` is false (10 > 20), so the ternary returns `b` (20). *(Section 5.4)*
7. **b) `if (x >= 5 && x <= 10)`** — Chained comparisons like `5 <= x <= 10` don't work in C. You must use `&&` between two separate comparisons. *(Section 5.1)*
8. **b) It prevents dereferencing a NULL pointer if `ptr` is NULL** — If `ptr` is NULL, `ptr != NULL` is false, so the `&&` short-circuits and `*ptr` is never evaluated. *(Section 5.1)*

### Section 2: Short Answer

9. **Model answer:** `if (x = 5)` assigns the value 5 to x, then checks whether x is non-zero (which it always is since 5 is non-zero). It does NOT compare x to 5. To protect yourself: (1) enable compiler warnings with `-Wall`, (2) use Yoda conditions like `if (5 == x)`, (3) get into the habit of typing `==` for comparison. *(Section 5.1)*

10. **Model answer:** Fall-through happens when a `case` in a `switch` doesn't end with `break`, causing execution to continue into the next case. **Bug example:** Forgetting `break` after `case 1` in a calculator program — it would run both case 1 and case 2. **Intentional example:** Stacking cases like `case 'y': case 'Y':` so both uppercase and lowercase Y trigger the same code. *(Section 5.3)*

11. **Model answer:** Use ternary when you have a simple condition that chooses between two values to assign or return — it makes the code more concise. Do NOT use ternary when: (1) each branch has multiple statements, (2) the condition or branches are complex, (3) you're choosing between actions (not values). When in doubt, use `if-else` — readability wins. *(Section 5.4)*

### Section 3: Fill in the Blank

12. **non-zero** — Zero is false, everything else is true. *(Section 5.1)*
13. **switch** — The `switch` statement provides multi-way branching based on an integer expression. *(Section 5.3)*
14. **condition**, **?**, **:** — The syntax is `condition ? value_if_true : value_if_false`. *(Section 5.4)*
15. **&&** (logical AND) — Range checking requires `x >= min && x <= max`. *(Section 5.1)*
16. **break** — `break` exits the switch block. Without it, execution falls through. *(Section 5.3)*

### Section 4: Matching

17. **1 → c, 2 → d, 3 → b, 4 → a** *(Sections 5.2–5.4)*
18. **1 → b (False), 2 → a (True), 3 → c (True), 4 → d (False)** — `0` = false. `-5` = non-zero = true. `'A'` = 65 = non-zero = true. `'\0'` = 0 = false. *(Section 5.1)*

### Section 5: Practical Application

19. **Four errors found:**

    1. **Semicolons after `if` conditions** — `if (score >= 90);` ends the if statement immediately. The `{}` block below always runs. Same for `else if (score >= 80);`. Fix: remove the semicolons.
    2. **Missing `break` in switch** — `case 'A'` and `case 'B'` have no `break`. When grade is 'B', it prints both "Good" and "Average". Fix: add `break;` after each case block.
    3. **Ternary used for actions, not values** — `int message = x > 5 ? printf("Big\n") : printf("Small\n");` uses `printf` (which has side effects) inside a ternary. The return type of `printf` is `int` (number of characters printed), so it *technically* works, but it's confusing. Fix: use `if-else` for actions.
    4. **Type mismatch** — `int message` is assigned the result of `printf()`. While this compiles (printf returns `int`), it's semantically wrong — `message` is being used for the output side effect, not the return value.

    **Corrected version:**
    ```c
    #include <stdio.h>

    int main(void)
    {
        int score = 85;
        
        if (score >= 90) {             // Fixed: removed semicolon
            printf("Grade: A\n");
        } else if (score >= 80) {       // Fixed: removed semicolon
            printf("Grade: B\n");
        } else if (score >= 70) {
            printf("Grade: C\n");
        }
        
        char grade = 'B';
        switch (grade) {
            case 'A':
                printf("Excellent\n");
                break;                  // Fixed: added break
            case 'B':
                printf("Good\n");
                break;                  // Fixed: added break
            case 'C':
                printf("Average\n");
                break;                  // Fixed: added break
        }
        
        int x = 10;
        if (x > 5) {                    // Fixed: if-else for actions
            printf("Big\n");
        } else {
            printf("Small\n");
        }
        
        return 0;
    }
    ```

20. **Model answer:**
    ```c
    #include <stdio.h>

    int main(void)
    {
        int num;
        
        printf("Enter a number: ");
        scanf("%d", &num);
        
        // Nested if-else for positive/negative/zero + even/odd
        if (num > 0) {
            if (num % 2 == 0) {
                printf("Positive and even\n");
            } else {
                printf("Positive and odd\n");
            }
        } else if (num < 0) {
            printf("Negative\n");
        } else {
            printf("Zero\n");
        }
        
        // Ternary for high/low classification
        int abs_val = (num < 0) ? -num : num;
        printf("%s\n", (abs_val > 50) ? "high" : "low");
        
        return 0;
    }
    ```

---

## 📊 Quick Self-Assessment

| Score (out of 20) | Assessment | Recommended Action |
|:-----------------:|-----------|-------------------|
| 18–20 | 🎉 Excellent | You're ready for Chapter 6! |
| 14–17 | ✅ Good | Review Sections 5.3 (switch) and 5.4 (ternary) |
| 10–13 | 🔄 Fair | Re-read Sections 5.2–5.4 and retry the hands-on exercises |
| Below 10 | 🔁 Needs Review | Re-read the full chapter and ensure you've done all the Try It Yourself exercises |

---

*→ When you're ready, continue to [Chapter 6: Loops & Iteration →](../06-loops-and-iteration/01-while-loops.md)*
