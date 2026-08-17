# 📝 Chapter 3 Quiz — Variables & Data Types

---

**Chapter:** 03 — Variables & Data Types
**Total Questions:** 20
**Estimated Time:** 25–35 minutes

---

## Section 1: Multiple Choice (Select the best answer)

**1. Which of the following is a valid C variable name?**

a) `1stPlace`
b) `my-var`
c) `_count`
d) `int`

**2. How many bytes does a `double` typically occupy on a modern computer?**

a) 2 bytes
b) 4 bytes
c) 6 bytes
d) 8 bytes

**3. What is the output of this code?**
```c
int x = 5;
int y = 2;
double result = x / y;
printf("%f", result);
```

a) `2.500000`
b) `2.000000`
c) `2.5`
d) `2`

**4. Which keyword makes a variable read-only after initialization?**

a) `#define`
b) `static`
c) `const`
d) `readonly`

**5. What is the ASCII value of the character `'A'`?**

a) 48
b) 65
c) 97
d) 0

**6. When does a local variable get destroyed?**

a) When the program starts
b) When the variable goes out of scope
c) When the computer runs out of memory
d) Never — it persists in memory

**7. Which of the following correctly declares an unsigned integer variable named `count` with the value 100?**

a) `unsigned int count = 100;`
b) `unsign count = 100;`
c) `unsigned integer count = 100;`
d) `int unsigned count = 100;`

**8. What happens when you declare `int x;` without initializing it, then print its value?**

a) The program crashes
b) It prints 0
c) It prints whatever random value was in that memory location
d) The compiler gives an error

---

## Section 2: Short Answer (Explain in your own words)

**9. Explain the difference between `const double PI = 3.14;` and `#define PI 3.14`. When would you use one over the other?**

*Your answer:*

**10. What is the "integer division trap"? How do you avoid it?**

*Your answer:*

**11. A `static` variable inside a function keeps its value between function calls. Explain why this is useful and give an example scenario.**

*Your answer:*

---

## Section 3: Fill in the Blank (Complete the sentence)

**12.** The format specifier for printing an `int` is ________.

**13.** A variable declared inside a function is called a ________ variable.

**14.** To convert a `double` to an `int` explicitly, you use the ________ operator.

**15.** The C keyword for declaring an integer variable is ________.

**16.** When a local variable has the same name as a global variable, the ________ variable takes precedence inside the function.

---

## Section 4: Matching (Connect each item)

**17. Match each C data type to its typical size:**

| Type | Size |
|------|------|
| 1. `char` | a) 4 bytes |
| 2. `int` | b) 8 bytes |
| 3. `float` | c) 1 byte |
| 4. `double` | d) 4 bytes |

**18. Match each variable characteristic to its definition:**

| Term | Definition |
|------|------------|
| 1. Declaration | a) Giving a variable its first value at the point of creation |
| 2. Initialization | b) Changing a variable's value after declaration |
| 3. Assignment | c) Telling the compiler a variable's name and type |
| 4. Scope | d) Where a variable can be accessed in code |

---

## Section 5: Practical Application

**19. The following program has multiple errors. Find and fix them:**

```c
#include <stdio.h>

int main(void)
{
    const int MAX = 100;
    int x = 10;
    char grade = "A";
    
    MAX = 200;
    
    double result;
    result = x / 3;
    printf("Result: %d\n", result);
    
    return 0;
}
```

List each error and write the corrected version:

*Your answer:*

**20. Write a complete C program that does the following:**
- Declares a global integer constant named `MAX_STUDENTS` with value 30 using `#define`
- In `main()`, declares `int enrolled = 22;`
- Calculates and prints the number of available seats (`MAX_STUDENTS - enrolled`)
- Then declares `double avg_grade = 85.5;` and casts it to an `int` to print the truncated average
- Uses proper format specifiers for all values

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **c) `_count`** — Must start with a letter or underscore. `1stPlace` starts with a digit, `my-var` has a hyphen, `int` is a keyword. *(Section 3.1)*
2. **d) 8 bytes** — Double is double-precision floating-point, typically 8 bytes. *(Section 3.2)*
3. **b) 2.000000** — Both `x` and `y` are `int`, so integer division happens first (5/2 = 2), then the `2` is converted to `double` for storage. *(Section 3.5)*
4. **c) `const`** — `const` makes a variable read-only. `#define` is a preprocessor directive, `static` changes lifetime/scope, `readonly` doesn't exist in C. *(Section 3.4)*
5. **b) 65** — 'A' is ASCII 65. '0' is 48, 'a' is 97. *(Section 3.2)*
6. **b) When the variable goes out of scope** — Local variables are destroyed when execution leaves the enclosing `{}` block. *(Section 3.6)*
7. **a) `unsigned int count = 100;`** — The type is `unsigned int`, the name is `count`, the value is 100. *(Section 3.2)*
8. **c) It prints whatever random value was in that memory location** — C does NOT auto-initialize local variables to 0. *(Section 3.3)*

### Section 2: Short Answer

9. **Model answer:** `const double PI = 3.14;` is a compile-time constant with a type, memory address, and scope. You can use `&` to get its address and the debugger can see it. `#define PI 3.14` is a preprocessor directive that does text substitution before compilation — it has no type, no address, and no scope. Use `const` for almost everything because it's type-safe. Use `#define` for header guards, conditional compilation, or truly universal constants. *(Section 3.4)*

10. **Model answer:** The integer division trap happens when both operands of `/` are integers, causing C to do integer division (truncating the decimal). For example, `7 / 3` gives `2`, not `2.333`. To avoid it, make at least one operand a floating-point type: use `7.0 / 3`, `(double)7 / 3`, or `7 / 3.0`. *(Section 3.5)*

11. **Model answer:** A `static` local variable is useful when a function needs to remember something between calls without using a global variable. For example, a function that generates unique IDs: each call increments a `static int next_id;` and returns the new value. The counter persists across calls but is only accessible from within the function. *(Section 3.6)*

### Section 3: Fill in the Blank

12. **`%d`** — The format specifier for `int` in `printf()`. *(Section 3.2)*
13. **local** (or **automatic**) — Declared inside a function, it's local to that function. *(Section 3.6)*
14. **cast** — The cast operator `(type)` explicitly converts one type to another. *(Section 3.5)*
15. **`int`** — Short for "integer." *(Section 3.2)*
16. **local** — The local variable shadows (hides) the global one inside the function. *(Section 3.6)*

### Section 4: Matching

17. **1 → c (char = 1 byte), 2 → a (int = 4 bytes), 3 → d (float = 4 bytes), 4 → b (double = 8 bytes)** *(Section 3.2)*
18. **1 → c, 2 → a, 3 → b, 4 → d** *(Section 3.3)*

### Section 5: Practical Application

19. **Four errors found:**

    1. `char grade = "A";` — A `char` stores a single character (single quotes). `"A"` is a string literal. Fix: `char grade = 'A';`
    2. `MAX = 200;` — `MAX` is declared `const`. A `const` variable cannot be modified after initialization. Fix: remove this line or don't use `const`.
    3. `result = x / 3;` — Integer division! `x` is 10 and `3` is an integer literal, so `10/3 = 3`, then stored as `3.0`. Fix: `result = x / 3.0;` or `result = (double)x / 3;`
    4. `printf("Result: %d\n", result);` — `result` is a `double` but `%d` is for integers. Fix: use `%lf` instead of `%d`.

    **Corrected version:**
    ```c
    #include <stdio.h>

    int main(void)
    {
        const int MAX = 100;
        int x = 10;
        char grade = 'A';             // Fixed: single quotes for char
        
        // MAX = 200;                  // Removed: can't modify const
        
        double result;
        result = (double)x / 3;       // Fixed: cast to avoid integer division
        printf("Result: %lf\n", result);  // Fixed: %lf for double
        
        return 0;
    }
    ```

20. **Model answer:**
    ```c
    #include <stdio.h>

    #define MAX_STUDENTS 30          // Global constant

    int main(void)
    {
        int enrolled = 22;
        int available = MAX_STUDENTS - enrolled;  // Integer subtraction
        
        double avg_grade = 85.5;
        int truncated_avg = (int)avg_grade;       // Explicit cast truncates .5
        
        printf("Maximum students: %d\n", MAX_STUDENTS);
        printf("Enrolled: %d\n", enrolled);
        printf("Available seats: %d\n", available);
        printf("Average grade: %lf\n", avg_grade);
        printf("Truncated average: %d\n", truncated_avg);
        
        return 0;
    }
    ```

---

## 📊 Quick Self-Assessment

| Score (out of 20) | Assessment | Recommended Action |
|:-----------------:|-----------|-------------------|
| 18–20 | 🎉 Excellent | You're ready for Chapter 4! |
| 14–17 | ✅ Good | Review Sections 3.5 (type conversion) and 3.6 (scope) |
| 10–13 | 🔄 Fair | Re-read Sections 3.3–3.5 and retry the hands-on exercises |
| Below 10 | 🔁 Needs Review | Re-read the full chapter and ensure you've done all the Try It Yourself exercises |

---

*→ When you're ready, continue to [Chapter 4: Operators & Expressions →](../04-operators-and-expressions/01-arithmetic-operators.md)*
