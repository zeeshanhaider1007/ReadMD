# 7.4: Return Values — Sending Results Back

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Use `return` to send a value back to the caller
- Understand that `return` also exits the function immediately
- Write functions with `void` return type (no return value)
- Handle functions that return error codes or status indicators

---

## 🧭 The Big Picture

> When you submit a loan application to a bank, you expect a response: approved or denied. The bank processes the application and sends back a decision. Without that response, you don't know what to do next.
>
> In C, the `return` statement is that response. It sends a value back from the function to the caller. The caller can then use that value — store it, print it, or make decisions based on it.

---

## 📚 Core Content

### The `return` Statement

```c
return value;   // Send 'value' back to the caller
```

The `return` statement does two things:
1. **Exits** the function immediately (nothing after `return` executes)
2. **Sends** a value back to the caller

```c
#include <stdio.h>

int get_answer(void) {
    return 42;           // Function ends here
    printf("This never prints!\n");  // DEAD CODE
}

int main(void) {
    int result = get_answer();
    printf("The answer is %d\n", result);  // 42
    return 0;
}
```

### Using Return Values

The caller can use the return value in several ways:

```c
// 1. Store in a variable
double rate = get_exchange_rate("USD", "EUR");

// 2. Use directly in an expression
double total = price * get_discount_rate(is_vip);

// 3. Use in a condition
if (is_valid_passport("AB123456")) {
    printf("Valid passport\n");
}

// 4. Pass to another function
printf("Sum: %d\n", add(5, 3));

// 5. Ignore it (only if you don't need the result)
printf("Enter your age: ");   // We ignore printf's return value
```

### Early Returns

A function can have multiple `return` statements. The first one reached ends the function:

```c
const char *classify_temperature(int temp) {
    if (temp > 40) {
        return "Extreme heat";
    }
    if (temp > 30) {
        return "Hot";
    }
    if (temp > 20) {
        return "Warm";
    }
    if (temp > 10) {
        return "Cool";
    }
    return "Cold";  // Default / fallback
}
```

**The guard clause pattern** — check invalid conditions first and return early:

```c
double calculate_discount(double price, int quantity) {
    if (price <= 0) return 0.0;           // Invalid price
    if (quantity <= 0) return 0.0;        // Invalid quantity
    if (quantity >= 100) return price * 0.2;  // Bulk discount
    if (quantity >= 50)  return price * 0.1;  // Medium discount
    return 0.0;                                 // No discount
}
```

### `void` Functions — No Return Value

Some functions perform an action but don't need to return a value:

```c
void print_header(void) {
    printf("===============\n");
    printf("  DAILY LOG  \n");
    printf("===============\n");
    // No return statement needed
}

void greet(const char *name) {
    printf("Welcome, %s!\n", name);
    // return;  // Optional: can use 'return;' with no value to exit early
}
```

You can use `return;` (with no value) in a `void` function to exit early:

```c
void process_order(int quantity) {
    if (quantity <= 0) {
        printf("Invalid order.\n");
        return;  // Exit early, nothing more to do
    }
    printf("Processing %d items...\n", quantity);
    // No return needed at the end
}
```

### Returning Multiple Values

C functions can only return ONE value. To return multiple values, you need pointers or structs (later chapters):

```c
// Can only return one value
int get_stats(int a, int b) {
    return a + b;  // What if we also want a - b, a * b?
}

// Workaround: use pointers as parameters (Chapter 9)
void get_stats(int a, int b, int *sum, int *diff, int *prod) {
    *sum = a + b;
    *diff = a - b;
    *prod = a * b;
}
```

### Return Type vs. What You Actually Return

```c
int get_pi(void) {
    return 3.14159;   // ⚠️ 3.14159 is truncated to 3!
}

int main(void) {
    printf("%d\n", get_pi());  // Prints 3, not 3.14159!
    return 0;
}
```

The return type tells the caller what to expect. If the return type doesn't match what you return, C converts it (possibly losing data).

### Return Values as Status Indicators

Many C library functions return values to indicate success or failure:

```c
// scanf returns the number of items successfully read
int items_read = scanf("%d", &value);
if (items_read != 1) {
    printf("Failed to read input.\n");
    return 1;  // Return non-zero to indicate error
}
```

By convention, `main()` returns `0` for success and non-zero for errors. This allows other programs (or the operating system) to check if your program succeeded.

---

## 🧪 Try It Yourself

> **Exercise 1: Temperature Classifier**
> Write a function `const char *classify(int temp)` that returns "Cold", "Warm", or "Hot" based on temperature ranges you define. Call it with several values.

> **Exercise 2: Early Return Guard**
> Write a function `double divide(int a, int b)` that returns `a / b` but checks if `b` is 0 first. If `b` is 0, print an error and return 0.0 (the guard clause pattern).

> **Exercise 3: Void with Early Exit**
> Write a `void` function `print_positive(int x)` that only prints the number if it's positive. If `x <= 0`, return early without printing.

> **Exercise 4: Status Return**
> Write a function `int read_age(void)` that asks the user for their age. If they enter a valid age (1-120), return it. If invalid, return -1 to indicate an error.

---

## 💡 Common Pitfalls

- ❌ **Returning the wrong type** — `return 3.14;` from an `int` function truncates to `3`. Use the correct return type.
- ❌ **Code after `return`** — Any code after a `return` statement never executes (dead code). The compiler may warn you.
- ❌ **Forgetting to return in a non-void function** — This is undefined behavior. The function returns a garbage value. Always ensure every path returns a value.
- ❌ **Trying to return multiple values** — Use pointers, structs, or pass-by-reference patterns (later chapters).

---

## 🔗 Connections to What You Know

> **Return values are like the responses you get from services.**
>
> Every request you make receives a response: approved, rejected, or more information needed. The response determines what happens next. Without a clear response, the process stalls.
>
> In C, `return` is that response. It tells the caller: "Here's the result of my work. Use it as you see fit." A `void` function is like an action that doesn't require a formal response — like nodding to acknowledge that you received something.

![Functions as Restaurant Departments](../assets/ch07/functions-as-bureaucracy.svg) — each department sends back a response (return value) after processing a request.

---

## ✅ Section Checklist

- [ ] I can use `return` to send a value back to the caller
- [ ] I understand that `return` exits the function immediately
- [ ] I can write `void` functions that perform actions without returning values
- [ ] I use guard clauses to handle invalid inputs early
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [7.5: Scope and Lifetime Revisited →](./05-scope-and-lifetime.md)*
