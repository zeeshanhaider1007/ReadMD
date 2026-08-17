# 7.3: Parameters and Arguments — Passing Data to Functions

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Distinguish between parameters (in the definition) and arguments (in the call)
- Explain pass-by-value and why a function can't change the caller's variable
- Write functions with correct parameter types and order

---

## 🧭 The Big Picture

> When you order food at a restaurant, you include all the necessary information: the dish, the size, the special requests. The kitchen receives this information, prepares the order, and sends back the finished dish. Crucially, the kitchen works with a **copy** of your order — they can adjust seasoning and make notes, but the original order in your hands remains unchanged.
>
> This is **pass-by-value**. When you call a function, each argument's value is **copied** into the corresponding parameter. The function works with the copy. Changes to the parameter inside the function do NOT affect the original argument in the caller.

---

## 📚 Core Content

### Parameters vs. Arguments

These terms are often used interchangeably, but there's a precise distinction:

| Term | Where It Appears | What It Is |
|------|-----------------|------------|
| **Parameter** | In the function **definition** | The variable that receives the value |
| **Argument** | In the function **call** | The actual value passed |

```c
//             vvv   vvv   ← Parameters: a and b
int add(int a, int b) {
    return a + b;
}

int main(void) {
    int result = add(5, 3);  // ^  ^  ← Arguments: 5 and 3
    return 0;
}
```

### Pass-by-Value Demonstration

C always passes arguments **by value** — a copy is made:

```c
#include <stdio.h>

void try_to_change(int x) {
    x = 100;  // Only changes the LOCAL copy x
    printf("Inside function: x = %d\n", x);
}

int main(void) {
    int original = 10;
    printf("Before call: original = %d\n", original);
    
    try_to_change(original);
    
    printf("After call: original = %d\n", original);  // Still 10!
    return 0;
}
```

**Output:**
```
Before call: original = 10
Inside function: x = 100
After call: original = 10
```

The variable `original` in `main()` is NEVER changed, because `try_to_change` receives only a copy.

### Why This Matters

```c
int x = 5;
printf("Before: %d\n", x);  // 5

// The following does NOT work — can't swap using pass-by-value!
void swap_bad(int a, int b) {
    int temp = a;
    a = b;
    b = temp;  // Only swaps the COPIES
}

swap_bad(x, 10);
printf("After: %d\n", x);  // STILL 5!
```

To actually modify a variable in the caller, you need **pointers** (Chapter 9).

### Parameter Order Matters

The order of arguments must match the order of parameters:

```c
// Definition: parameters are (name, age, salary)
void print_employee_info(const char *name, int age, double salary) {
    printf("%s, age %d, earns $%.2f\n", name, age, salary);
}

int main(void) {
    // Arguments must be in the SAME order as parameters
    print_employee_info("Alice", 30, 75000.0);  // ✅ Correct
    print_employee_info(75000.0, "Alice", 30);   // ❌ Wrong order!
    return 0;
}
```

### Default Arguments? Not in C

C does NOT support default arguments. You must provide every argument:

```c
// This is NOT valid in C:
void greet(const char *name, int repeat = 1);  // ❌ No default params in C

// You'd need two functions instead:
void greet_once(const char *name) {
    printf("Hello, %s!\n", name);
}

void greet_repeat(const char *name, int repeat) {
    for (int i = 0; i < repeat; i++) {
        printf("Hello, %s!\n", name);
    }
}
```

### Matching Parameter Types

The types of arguments should match (or be compatible with) the parameter types:

```c
double divide(int a, double b) {
    return a / b;  // a is promoted to double for the division
}

int main(void) {
    double result = divide(10, 3.0);  // int and double — OK, int promoted
    // double result = divide(10, "hello");  // ❌ Type mismatch!
    return 0;
}
```

### Practice: Well-Designed Parameters

```c
// GOOD: clear parameter names, logical order, consistent types
double calculate_tax(double income, double tax_rate, int dependents);

// GOOD: parameters describe what the function needs
void send_email(const char *recipient, const char *message);

// AVOID: too many parameters (more than 5-6)
void register_student(int id, const char *name, int year, double fee,
                      int courses, const char *status, int start_year);
// Consider using a struct (Chapter 11) for many parameters
```

---

## 🧪 Try It Yourself

> **Exercise 1: Pass-by-Value Experiment**
> Write a function `void add_ten(int x)` that adds 10 to `x` and prints the result inside the function. Call it with `int num = 5;` and print `num` after the call. What happens?

> **Exercise 2: Correct Argument Order**
> Write a function `void print_rect(char symbol, int width, int height)` that prints a rectangle. Call it correctly from `main()`.

> **Exercise 3: Wrong Order**
> Intentionally call a function with arguments in the wrong order. What does the compiler say? Does it still compile?

> **Exercise 4: Temperature Converter**
> Write a function `double to_celsius(double fahrenheit)` that converts Fahrenheit to Celsius. Call it with different values.

---

## 💡 Common Pitfalls

- ❌ **Expecting the function to modify the original variable** — Pass-by-value means the function gets a copy. Use pointers (Chapter 9) if you need to modify the original.
- ❌ **Wrong argument order** — The compiler checks types but can't read your mind. Passing arguments in the wrong order that happen to have the same type is a silent bug.
- ❌ **Too many parameters** — More than 5-6 parameters makes a function hard to use. Consider grouping related parameters into a struct.

---

## 🔗 Connections to What You Know

> **Parameters and arguments are like blanks on an order form.**
>
> When an order form specifies "Dish: ____, Size: ____" — the parameters are the blanks, and the arguments are the actual values you fill in. The instructions (function body) refer to the blanks throughout. What you put into the blanks determines what gets made.

![Functions as Restaurant Departments](../assets/ch07/functions-as-bureaucracy.svg) — each department (function) expects specific inputs (parameters) to do its work.

---

## 📖 Further Reading

- [Pass-by-Value (cppreference.com)](https://en.cppreference.com/w/c/language/operator_other) — How function calls work
- [Parameter Passing (Wikipedia)](https://en.wikipedia.org/wiki/Parameter_(computer_programming)) — Deep dive

---

## ✅ Section Checklist

- [ ] I can distinguish between parameters and arguments
- [ ] I understand pass-by-value and its implications
- [ ] I pass arguments in the correct order matching parameter types
- [ ] I know that C doesn't support default arguments
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [7.4: Return Values →](./04-return-values.md)*
