# 📝 Chapter 4 Quiz — Operators & Expressions

---

**Chapter:** 04 — Operators & Expressions
**Total Questions:** 20
**Estimated Time:** 25–35 minutes

---

## Section 1: Multiple Choice (Select the best answer)

**1. What is the result of `17 % 5`?**

a) 3
b) 2
c) 3.4
d) 12

**2. What does the following code print?**
```c
int x = 5;
int y = x++;
printf("%d %d", x, y);
```

a) `5 5`
b) `6 5`
c) `6 6`
d) `5 6`

**3. Which operator checks if two values are NOT equal?**

a) `<>`
b) `=/=`
c) `!=`
d) `!==`

**4. What is the value of `(1 && 2) || (0 && 3)` in C?**

a) 0
b) 1
c) 2
d) 3

**5. What does `12 & 10` evaluate to?**

a) 8
b) 12
c) 10
d) 22

**6. Which operator has the LOWEST precedence in C?**

a) The comma operator `,`
b) Assignment `=`
c) Logical OR `||`
d) Multiplication `*`

**7. What is the result of executing this code?**
```c
int x = 1;
x += 2;
x *= 3;
x -= 4;
printf("%d", x);
```

a) 5
b) 9
c) 1
d) 3

**8. Short-circuit evaluation means:**

a) All expressions are evaluated in parallel for speed
b) If the result of a logical expression is determined by the first operand, the second is not evaluated
c) The program stops running if a condition is false
d) Only true expressions are compiled

---

## Section 2: Short Answer (Explain in your own words)

**9. Explain the difference between bitwise `&` and logical `&&`. Give an example where they produce different results.**

*Your answer:*

**10. What is the integer division trap? How does it relate to arithmetic operators?**

*Your answer:*

**11. Why should you rarely use `==` to compare `double` values? What should you use instead?**

*Your answer:*

---

## Section 3: Fill in the Blank (Complete the sentence)

**12.** The arithmetic operator that returns the remainder of division is ________.

**13.** The relational operator for equality is written as ________ in C (two characters).

**14.** To check if a specific bit is set, you use the ________ bitwise operator.

**15.** The compound assignment operator that subtracts a value from a variable is ________.

**16.** A shift left by 2 (`x << 2`) is equivalent to multiplying by ________.

---

## Section 4: Matching (Connect each item)

**17. Match each operator to its description:**

| Operator | Description |
|----------|-------------|
| 1. `%` | a) Logical AND |
| 2. `!=` | b) Bitwise XOR |
| 3. `&&` | c) Modulo (remainder) |
| 4. `^` | d) Not equal to |

**18. Match each expression to its value (assuming `int x = 5;`):**

| Expression | Value |
|------------|-------|
| 1. `x++` | a) 6 |
| 2. `++x` | b) 4 |
| 3. `x--` | c) 5 |
| 4. `--x` | d) 5 (then x becomes 6) |

---

## Section 5: Practical Application

**19. The following program has multiple errors. Find and fix them:**

```c
#include <stdio.h>

int main(void)
{
    int a = 10;
    int b = 3;
    
    double result = a / b;
    printf("Result: %d\n", result);
    
    if (a = b) {
        printf("a equals b\n");
    }
    
    char x = "A";
    
    return 0;
}
```

List each error and write the corrected version:

*Your answer:*

**20. Write a complete C program that:**
- Declares `int count = 0;`
- Uses `++` (postfix) to increment `count` three times
- Uses compound assignment to add 10
- Uses compound assignment to multiply by 2
- Prints the final value of `count` (expected: `(0+1+1+1+10) × 2 = 26`)
- Also prints whether 26 is even or odd using `%`

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **b) 2** — 17 / 5 = 3 remainder 2. *(Section 4.1)*
2. **b) 6 5** — `x++` is postfix: y gets x's old value (5), then x becomes 6. *(Section 4.5)*
3. **c) `!=`** — Not equal. `<>` is not valid C, `=/=` is not valid, `!==` is not valid C (it's JavaScript). *(Section 4.2)*
4. **b) 1** — `1 && 2` is true (both non-zero), `0 && 3` is false (first is 0). `true || false` = true = 1. *(Section 4.3)*
5. **a) 8** — `12 = 1100`, `10 = 1010`. `1100 & 1010 = 1000 = 8`. *(Section 4.4)*
6. **a) The comma operator `,`** — The comma has the lowest precedence of all C operators. *(Section 4.5)*
7. **a) 5** — 1+2=3, 3×3=9, 9-4=5. *(Section 4.5)*
8. **b) If the result is determined by the first operand, the second is not evaluated** — Short-circuit prevents unnecessary evaluation and prevents errors like division by zero. *(Section 4.3)*

### Section 2: Short Answer

9. **Model answer:** `&` operates on individual bits (bitwise AND), while `&&` operates on truth values (logical AND). Example: `2 & 1` = `10 & 01` = `00` = 0. `2 && 1` = `true && true` = 1. They produce completely different results. *(Section 4.4)*

10. **Model answer:** The integer division trap happens when both operands of `/` are integers, causing C to truncate the fractional part. For example, `10 / 3` gives `3`, not `3.333`. To avoid it, make at least one operand a floating-point type: `10 / 3.0` or `(double)10 / 3`. *(Section 4.1)*

11. **Model answer:** Floating-point numbers have tiny precision errors due to binary representation. `0.1 + 0.2` might not equal exactly `0.3`. Instead of `==`, check if the absolute difference is very small: `fabs(a - b) < epsilon`. *(Section 4.2)*

### Section 3: Fill in the Blank

12. **`%`** (modulo) — Returns the remainder of integer division. *(Section 4.1)*
13. **`==`** — Two equals signs. One equals sign (`=`) is assignment. *(Section 4.2)*
14. **`&`** (bitwise AND) — Used with a mask to check if specific bits are set. *(Section 4.4)*
15. **`-=`** — `x -= 5` is equivalent to `x = x - 5`. *(Section 4.5)*
16. **4** (2²) — Left shift by N multiplies by 2^N. *(Section 4.4)*

### Section 4: Matching

17. **1 → c, 2 → d, 3 → a, 4 → b** *(Sections 4.1–4.4)*
18. **1 → d, 2 → a, 3 → c, 4 → b** — Postfix `x++` yields the old value (5) then increments to 6. Prefix `++x` increments first then yields the new value (6). Postfix `x--` yields old value (5) then decrements to 4. Prefix `--x` decrements first then yields 4. *(Section 4.5)*

### Section 5: Practical Application

19. **Three errors found:**
    1. `double result = a / b;` — Integer division! `10/3 = 3`, then stored as `3.0`. Fix: `(double)a / b`
    2. `printf("Result: %d\n", result);` — `result` is a `double` but `%d` is for integers. Fix: use `%lf`
    3. `if (a = b)` — Single `=` is assignment, not comparison. This assigns `b` (3) to `a`, then the condition is always true (3 is non-zero). Fix: `if (a == b)`
    4. `char x = "A";` — `char` stores a single character (single quotes). `"A"` is a string literal. Fix: `char x = 'A';`

    **Corrected version:**
    ```c
    #include <stdio.h>

    int main(void)
    {
        int a = 10;
        int b = 3;
        
        double result = (double)a / b;     // Fixed: cast to avoid integer division
        printf("Result: %lf\n", result);    // Fixed: %lf for double
        
        if (a == b) {                       // Fixed: == for comparison
            printf("a equals b\n");
        }
        
        char x = 'A';                       // Fixed: single quotes for char
        
        return 0;
    }
    ```

20. **Model answer:**
    ```c
    #include <stdio.h>

    int main(void)
    {
        int count = 0;
        
        count++;   // count = 1
        count++;   // count = 2
        count++;   // count = 3
        
        count += 10;  // count = 13
        count *= 2;   // count = 26
        
        printf("Final count: %d\n", count);  // 26
        
        if (count % 2 == 0) {
            printf("%d is even\n", count);
        } else {
            printf("%d is odd\n", count);
        }
        
        return 0;
    }
    ```

---

## 📊 Quick Self-Assessment

| Score (out of 20) | Assessment | Recommended Action |
|:-----------------:|-----------|-------------------|
| 18–20 | 🎉 Excellent | You're ready for Chapter 5! |
| 14–17 | ✅ Good | Review Sections 4.4 (bitwise) and 4.5 (increment/assignment) |
| 10–13 | 🔄 Fair | Re-read Sections 4.1–4.3 and retry the hands-on exercises |
| Below 10 | 🔁 Needs Review | Re-read the full chapter and ensure you've done all the Try It Yourself exercises |

---

*→ When you're ready, continue to [Chapter 5: Control Flow →](../05-control-flow/01-boolean-expressions.md)*
