# 7.2: Function Syntax — How to Write a Function

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Write a function with the correct syntax: return type, name, parameters, body
- Distinguish between function declaration (prototype) and definition
- Call a function and use its return value
- Understand the flow of control when a function is called

---

## 🧭 The Big Picture

> Writing a function is like creating a new recipe. You need to specify:
> - What kind of **dish** will be produced (return type)
> - What the recipe is **called** (function name)
> - What **ingredients** are needed to make it (parameters)
> - What **steps** to follow (function body)
>
> Just as a cook follows a recipe when asked, a program calls a function when needed. The function executes its steps and returns a result — like a recipe producing a finished dish.

![Functions as Restaurant Departments](../assets/ch07/functions-as-bureaucracy.svg)

---

## 📚 Core Content

### The Function Blueprint

```c
return_type function_name(parameter_list) {
    // Function body — statements that execute
    return value;  // Must match the return_type
}
```

```c
int add(int a, int b) {    // return_type: int, name: add, params: a, b
    int sum = a + b;        // Function body
    return sum;             // Return the result
}
```

### Anatomy of a Function

| Part | Example | Description |
|------|---------|-------------|
| **Return type** | `int` | What kind of value the function sends back |
| **Function name** | `add` | How you call the function (verb_noun convention) |
| **Parameters** | `(int a, int b)` | Inputs the function receives (each with type and name) |
| **Function body** | `{ int sum = a + b; return sum; }` | The code that runs when the function is called |
| **Return statement** | `return sum;` | Sends a value back to the caller and exits |

### Declaration vs. Definition

A **function declaration** (also called a **prototype**) tells the compiler: "A function with this signature exists, but the full definition is elsewhere."

A **function definition** provides the actual body of the function.

```c
// DECLARATION (prototype) — tells the compiler this function exists
int add(int a, int b);

int main(void) {
    int result = add(5, 3);  // OK: compiler knows add() exists
    printf("%d\n", result);
    return 0;
}

// DEFINITION — provides the actual code
int add(int a, int b) {
    return a + b;
}
```

If you define the function BEFORE it's called, you don't need a separate declaration:

```c
// DEFINITION comes BEFORE main — no declaration needed
int add(int a, int b) {
    return a + b;
}

int main(void) {
    int result = add(5, 3);  // OK: compiler already knows add()
    return 0;
}
```

**Convention:** For short programs, define functions before `main`. For larger programs, use declarations (often in header files) and put definitions in separate files.

### Calling a Function

When you call a function, execution **jumps** to the function, runs its body, and **returns** to where it was called:

```c
#include <stdio.h>

void print_greeting(void) {
    printf("Welcome to the cafe!\n");
}

int main(void) {
    printf("Before call...\n");
    print_greeting();           // Jump to print_greeting
    printf("After call!\n");    // Return here after function finishes
    return 0;
}
```

**Output:**
```
Before call...
Welcome to the cafe!
After call!
```

### The `void` Keyword

`void` has two uses in functions:

```c
// void return type: function returns NOTHING
void print_message(void) {
    printf("Hello!\n");
    // No return statement needed
}

// void parameter: function takes NO arguments
int get_number(void) {
    return 42;
}
```

### Function Naming Conventions

Good function names are **verbs** or **verb_noun** combos:

```c
// GOOD: describes what the function does
int calculate_average(int a, int b);
void print_report(void);
bool is_valid_email(const char *email);
double convert_currency(double amount, double rate);

// BAD: vague or misleading
int stuff(int x);
void do_it(void);
int data(int a, int b);
```

### Multiple Parameters

Functions can take any number of parameters (including zero):

```c
void print_summary(const char *title, int year, double budget) {
    printf("=== %s (%d) ===\n", title, year);
    printf("Budget: $%.2f million\n", budget);
}

int main(void) {
    print_summary("Trade Agreement", 2026, 450.50);
    return 0;
}
```

### Example: A Complete Program with Functions

```c
#include <stdio.h>

// Function declarations
double calculate_gdp_growth(double current, double previous);
void print_report(double growth);

int main(void) {
    double gdp_2025 = 25000.0;  // billions
    double gdp_2026 = 26250.0;
    
    double growth = calculate_gdp_growth(gdp_2026, gdp_2025);
    print_report(growth);
    
    return 0;
}

// Function definitions
double calculate_gdp_growth(double current, double previous) {
    return ((current - previous) / previous) * 100.0;
}

void print_report(double growth) {
    if (growth > 0) {
        printf("GDP grew by %.2f%%\n", growth);
    } else {
        printf("GDP declined by %.2f%%\n", -growth);
    }
}
```

---

## 🧪 Try It Yourself

> **Exercise 1: Write a Simple Function**
> Write a function `int square(int x)` that returns `x * x`. Call it from `main()` with a few values and print the results.

> **Exercise 2: Void Function**
> Write a `void` function `print_line(char symbol, int count)` that prints a line of `count` symbols. Call it to print a line of 10 asterisks.

> **Exercise 3: Declaration vs. Definition**
> Write a program where you declare a function prototype, define the function AFTER `main()`, and call it FROM `main()`. Verify it compiles.

> **Exercise 4: Multiple Parameters**
> Write a function `double average(double a, double b, double c)` that returns the average of three numbers. Test it.

---

## 💡 Common Pitfalls

- ❌ **Missing function declaration** — If you call a function before defining it and don't provide a prototype, the compiler gives a warning or error.
- ❌ **Return type mismatch** — If the function says it returns `int`, you must `return` an `int`. Returning a `double` from an `int` function truncates the value.
- ❌ **Forgetting to return a value** — A non-void function MUST return a value. If you forget, the function returns a garbage value.
- ❌ **Semicolon after function definition** — Don't put a semicolon after the closing brace of a definition: `int add(int a, int b) { return a + b; };` ← wrong!

---

## 🔗 Connections to What You Know

> **Function syntax is like the structure of a well-designed form.**
>
> A form has a clear title (function name), states its purpose (return type), lists the fields to fill in (parameters), specifies the actions to be taken (function body), and declares the outcome (return value). Every part has a precise meaning and a required position — just like a function declaration.

---

## 📖 Further Reading

- [Function Declarations (cppreference.com)](https://en.cppreference.com/w/c/language/function_declaration) — Official reference
- [Function Definitions (cppreference.com)](https://en.cppreference.com/w/c/language/function_definition) — Official reference

---

## ✅ Section Checklist

- [ ] I can write a function with correct syntax
- [ ] I understand the difference between declaration and definition
- [ ] I can call a function and understand the flow of control
- [ ] I know how to use `void` for no return or no parameters
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [7.3: Parameters and Arguments →](./03-parameters-and-arguments.md)*
