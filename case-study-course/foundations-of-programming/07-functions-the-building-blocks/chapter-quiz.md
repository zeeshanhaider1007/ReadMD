# 📝 Chapter 7 Quiz — Functions

---

**Chapter:** 07 — Functions
**Total Questions:** 20
**Estimated Time:** 25–35 minutes

---

## Section 1: Multiple Choice (Select the best answer)

**1. What is the term for a variable that receives a value inside a function definition?**

a) Argument
b) Parameter
c) Return value
d) Global variable

**2. What does the following code print?**
```c
void change(int x) { x = 100; }
int main(void) {
    int a = 5;
    change(a);
    printf("%d", a);
    return 0;
}
```
a) 5
b) 100
c) Nothing — compile error
d) 0

**3. Which of the following is a valid function prototype?**

a) `int add(int a, b);`
b) `int add(int a, int b)`
c) `int add(int, int);`
d) `add(int a, int b);`

**4. What does `return;` do inside a `void` function?**

a) Returns the value 0
b) Exits the function immediately
c) Returns a garbage value
d) Causes a compile error

**5. How many times does `factorial(3)` call itself (not counting the initial call)?**

```c
int factorial(int n) {
    if (n == 0) return 1;
    return n * factorial(n - 1);
}
```
a) 2
b) 3
c) 4
d) 0

**6. What is a stack overflow?**

a) When the stack grows too large and crashes the program
b) When a function returns too many values
c) When a variable overflows its data type
d) When you use too many global variables

**7. Which keyword makes a local variable persist between function calls?**

a) `global`
b) `persist`
c) `static`
d) `extern`

**8. A recursive function must have:**

a) At least one parameter
b) A base case and a recursive case
c) A return value
d) A loop inside it

---

## Section 2: Short Answer (Explain in your own words)

**9. Explain pass-by-value. If a function modifies its parameter, why doesn't the original variable in the caller change?**

*Your answer:*

**10. What are the three benefits of using functions? Give a brief example of each.**

*Your answer:*

**11. Explain the difference between a function declaration (prototype) and a function definition. When would you use each?**

*Your answer:*

---

## Section 3: Fill in the Blank (Complete the sentence)

**12.** The _______ statement sends a value back to the caller and exits the function.

**13.** A function that takes no parameters and returns nothing would have the signature `_______ (void)`.

**14.** The _______ is a region of memory that grows and shrinks as functions are called and return.

**15.** Without a _______ case, a recursive function will call itself forever.

**16.** A variable declared inside a function is called a _______ variable.

---

## Section 4: Matching (Connect each item)

**17. Match each term to its description:**

| Term | Description |
|------|-------------|
| 1. Parameter | a) The value sent back to the caller |
| 2. Argument | b) The variable in the function that receives a value |
| 3. Return value | c) The value passed in a function call |
| 4. Prototype | d) The declaration of a function before it's defined |

**18. Match each variable type to its lifetime:**

| Type | Lifetime |
|------|----------|
| 1. Local | a) Entire program execution |
| 2. Global | b) The function call that created it |
| 3. Static local | c) Entire program execution (but limited scope) |

---

## Section 5: Practical Application

**19. The following program has multiple errors. Find and fix them:**

```c
#include <stdio.h>

// Error 1: Fix this function
double calculate(double a, b)
    return a + b;
}

int main(void)
{
    int result = calculate(5, 3);
    print("Result: %d\n", result);
    
    // Error 2: Why doesn't this work?
    void reset(int x) {
        x = 0;
    }
    int value = 10;
    reset(10);
    printf("%d", value);
    
    return 0;
}
```

**20. Write a complete C program that:**
- Declares a function `int max_of_three(int a, int b, int c)` that returns the largest of three integers
- Declares a `void` function `print_line(int length)` that prints a line of `length` dashes
- In `main()`, calls both functions to find the maximum of 17, 42, and 8
- Uses a recursive function `int sum_to(int n)` to calculate the sum from 1 to n (test with n=10)
- Prints all results

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **b) Parameter** — Parameters are in the function definition; arguments are in the call. *(Section 7.2)*
2. **a) 5** — Pass-by-value: `change` gets a copy of `a`. The original `a` in `main` is unchanged. *(Section 7.3)*
3. **c) `int add(int, int);`** — A prototype needs return type, name, and parameter types. Parameter names are optional in declarations. *(Section 7.2)*
4. **b) Exits the function immediately** — `return;` in a `void` function exits without returning a value. *(Section 7.4)*
5. **b) 3** — factorial(3) calls factorial(2), which calls factorial(1), which calls factorial(0) (base case). That's 3 recursive calls. *(Section 7.6)*
6. **a) When the stack grows too large and crashes the program** — Usually caused by infinite recursion or deep recursion. *(Section 7.6)*
7. **c) `static`** — `static int x;` inside a function persists across calls. *(Section 7.5)*
8. **b) A base case and a recursive case** — The base case stops recursion; the recursive case calls itself with a smaller problem. *(Section 7.6)*

### Section 2: Short Answer

9. **Model answer:** Pass-by-value means a COPY of the argument's value is passed to the function parameter. The function works with the copy. When the function returns, the copy is destroyed. The original variable in the caller remains unchanged. This protects the caller's data from unintended modification.

10. **Model answer:** (1) **Reuse** — write the logic once, call it many times (like a `max` function). (2) **Abstraction** — hide complex logic behind a simple interface (like `printf`). (3) **Modularity** — change one function without affecting others.

11. **Model answer:** A declaration (prototype) tells the compiler "this function exists" with its signature but no body. A definition provides the actual code. Declarations go in header files for multi-file programs. Definitions go in source files.

### Section 3: Fill in the Blank

12. **`return`** — Returns a value and exits the function. *(Section 7.4)*
13. **`void`** — `void function_name(void)` takes nothing and returns nothing. *(Section 7.2)*
14. **call stack** (or **stack**) — Manages function call frames. *(Section 7.5)*
15. **base** — The base case stops the recursion. *(Section 7.6)*
16. **local** (or **automatic**) — Declared inside a function. *(Section 7.5)*

### Section 4: Matching

17. **1 → b, 2 → c, 3 → a, 4 → d** *(Sections 7.2–7.3)*
18. **1 → b, 2 → a, 3 → c** *(Section 7.5)*

### Section 5: Practical Application

19. **Three errors found:**
    1. Missing parameter type for `b`: `double calculate(double a, b)` should be `double calculate(double a, double b)`
    2. Missing opening brace: `double calculate(double a, double b) return a + b; }` should have `{` after the parameters
    3. Cannot define a function inside another function: `void reset(int x)` is inside `main()`. Move it outside.
    4. `print` should be `printf`
    5. `reset(10)` passes the literal 10, not the variable `value`. Should be `reset(value)`

    **Corrected version:**
    ```c
    #include <stdio.h>

    double calculate(double a, double b) {
        return a + b;
    }

    void reset(int x) {
        x = 0;
    }

    int main(void) {
        double result = calculate(5, 3);
        printf("Result: %f\n", result);
        
        int value = 10;
        reset(value);
        printf("%d\n", value);  // Still 10 (pass-by-value)
        
        return 0;
    }
    ```

20. **Model answer:**
    ```c
    #include <stdio.h>

    int max_of_three(int a, int b, int c) {
        int max = (a > b) ? a : b;
        return (max > c) ? max : c;
    }

    void print_line(int length) {
        for (int i = 0; i < length; i++) {
            printf("-");
        }
        printf("\n");
    }

    int sum_to(int n) {
        if (n <= 0) return 0;
        return n + sum_to(n - 1);
    }

    int main(void) {
        int max = max_of_three(17, 42, 8);
        printf("Max of 17, 42, 8: %d\n", max);
        
        print_line(20);
        
        int sum = sum_to(10);
        printf("Sum 1 to 10: %d\n", sum);
        
        return 0;
    }
    ```

---

## 📊 Quick Self-Assessment

| Score (out of 20) | Assessment | Recommended Action |
|:-----------------:|-----------|-------------------|
| 18–20 | 🎉 Excellent | You're ready for Chapter 8! |
| 14–17 | ✅ Good | Review Sections 7.3 (parameters) and 7.6 (recursion) |
| 10–13 | 🔄 Fair | Re-read Sections 7.2–7.4 and retry the hands-on exercises |
| Below 10 | 🔁 Needs Review | Re-read the full chapter and ensure you've done all the exercises |
