# 9.8: Function Pointers — Storing and Calling Functions Through Pointers

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Declare a pointer to a function
- Call a function through a pointer
- Pass function pointers as arguments to other functions
- Understand the callback pattern

---

## 🧭 The Big Picture

> In diplomacy, you might have a protocol that says: "When a visiting delegation arrives, perform the appropriate welcome ceremony." The welcome ceremony depends on the delegation's rank — heads of state get one ceremony, trade delegations get another, cultural exchanges get a third.
>
> A **function pointer** lets you store a reference to a function in a variable. Just as you might say "use the VIP protocol for this visit," you can say "use the `sort_ascending` function for this array."
>
> This enables the **callback** pattern: you pass a function as an argument to another function, telling it *how* to do its work.

---

## 📚 Core Content

### Declaring a Function Pointer

```c
return_type (*pointer_name)(parameter_types);
```

```c
// A pointer to a function that takes two ints and returns an int
int (*operation)(int a, int b);
```

The parentheses around `*pointer_name` are **required**. Without them, the declaration means something different:

```c
int *operation(int a, int b);  // A function that RETURNS an int pointer
int (*operation)(int a, int b);  // A POINTER to a function that returns int
```

### Assigning and Using Function Pointers

```c
#include <stdio.h>

int add(int a, int b) { return a + b; }
int subtract(int a, int b) { return a - b; }
int multiply(int a, int b) { return a * b; }

int main(void) {
    int (*op)(int, int);  // Declare function pointer
    
    op = &add;           // Point to the add function
    printf("%d\n", op(5, 3));  // 8 (call through pointer)
    
    op = &subtract;      // Re-point to subtract
    printf("%d\n", op(5, 3));  // 2
    
    op = &multiply;      // Re-point to multiply
    printf("%d\n", op(5, 3));  // 15
    
    return 0;
}
```

You can also call a function pointer without explicitly dereferencing it:

```c
op(5, 3);     // ✅ Common shorthand
(*op)(5, 3);  // ✅ Explicit dereference — same thing
```

### The Callback Pattern

The real power of function pointers is passing them as arguments to other functions:

```c
#include <stdio.h>

// A function that applies an operation to two numbers
int apply(int a, int b, int (*operation)(int, int)) {
    return operation(a, b);
}

int add(int a, int b) { return a + b; }
int multiply(int a, int b) { return a * b; }

int main(void) {
    printf("%d\n", apply(10, 5, &add));       // 15
    printf("%d\n", apply(10, 5, &multiply));  // 50
    return 0;
}
```

This is called a **callback** — the `apply` function "calls back" to the function you passed it.

### Practical Example: Sorting with Different Comparators

```c
#include <stdio.h>
#include <stdlib.h>

// Comparison functions — each tells qsort HOW to compare
int compare_ascending(const void *a, const void *b) {
    int ia = *(int *)a;
    int ib = *(int *)b;
    return ia - ib;  // Positive means a > b
}

int compare_descending(const void *a, const void *b) {
    int ia = *(int *)a;
    int ib = *(int *)b;
    return ib - ia;  // Reversed order
}

void print_array(int arr[], int size) {
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main(void) {
    int numbers[] = {42, 7, 15, 3, 28, 91, 10};
    int size = sizeof(numbers) / sizeof(numbers[0]);
    
    // Sort ascending — pass comparison function as argument
    qsort(numbers, size, sizeof(int), compare_ascending);
    print_array(numbers);  // 3 7 10 15 28 42 91
    
    // Sort descending — pass DIFFERENT comparison function
    qsort(numbers, size, sizeof(int), compare_descending);
    print_array(numbers);  // 91 42 28 15 10 7 3
    
    return 0;
}
```

Without function pointers, you'd need a separate sorting function for each comparison order. With function pointers, one `qsort` handles them all.

### Array of Function Pointers

You can have arrays of function pointers, which is useful for creating dispatch tables:

```c
#include <stdio.h>

int add(int a, int b) { return a + b; }
int subtract(int a, int b) { return a - b; }
int multiply(int a, int b) { return a * b; }
int divide(int a, int b) { return b != 0 ? a / b : 0; }

int main(void) {
    // Array of function pointers
    int (*operations[4])(int, int) = {add, subtract, multiply, divide};
    char *names[] = {"Add", "Subtract", "Multiply", "Divide"};
    
    int a = 20, b = 5;
    
    for (int i = 0; i < 4; i++) {
        printf("%s: %d\n", names[i], operations[i](a, b));
    }
    
    return 0;
}
```

### Using `typedef` for Clarity

Function pointer syntax can get messy. `typedef` helps:

```c
// Without typedef:
void sort(int *arr, int size, int (*compare)(const void *, const void *));

// With typedef — much clearer:
typedef int (*Comparator)(const void *, const void *);
void sort(int *arr, int size, Comparator compare);
```

---

## 🧪 Try It Yourself

> **Exercise 1: Simple Function Pointer**
> Write three functions: `square(int x)`, `cube(int x)`, and `double_it(int x)`. Use a function pointer to call each one with the value 5.

> **Exercise 2: Higher-Order Function**
> Write a function `void operate_on_array(int *arr, int size, int (*func)(int))` that applies `func` to every element of the array.

> **Exercise 3: Calculator with Dispatch Table**
> Create an array of 4 function pointers (add, subtract, multiply, divide) and a simple calculator that takes an operator character to select which function to call.

> **Exercise 4: `qsort` with Different Types**
> Use `qsort` to sort an array of doubles in descending order. Write the appropriate comparison function.

---

## 💡 Common Pitfalls

- ❌ **Forgetting parentheses around `(*ptr)`** — `int *func(int)` is a function returning a pointer. `int (*func)(int)` is a pointer to a function. Huge difference.
- ❌ **Wrong function signature** — The function pointer's parameter types and return type must exactly match the function you assign to it.
- ❌ **Calling without parentheses** — `op` gives the pointer value. `op()` calls the function.
- ❌ **Function pointer syntax overload** — It's complex. Use `typedef` to simplify.

---

## 🔗 Connections to What You Know

> **Function pointers are like plug-in instructions.**
>
> A restaurant has a standard process: "When an order arrives, do X." The exact behavior of X depends on the order type. You don't need different kitchen procedures — you have one procedure that accepts the specific instructions as a parameter.
>
> `qsort` is like a universal sorting procedure: "Here's the sorting algorithm, and here's HOW you compare two items." You provide the comparison function, and `qsort` handles the rest.

---

## ✅ Section Checklist

- [ ] I can declare and use function pointers
- [ ] I understand the callback pattern
- [ ] I can create arrays of function pointers
- [ ] I can use `typedef` to simplify function pointer syntax
- [ ] I wrote a **journal entry** about what I learned today

---

*→ You've completed Chapter 9! Test your knowledge with the [Chapter 9 Quiz →](./chapter-quiz.md)*
