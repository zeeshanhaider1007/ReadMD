# 9.3: The Address-of Operator (`&`) — Finding Where Data Lives

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Use `&` to get the memory address of any variable
- Pass addresses to functions using `&`
- Understand that `&` cannot be used on expressions or constants

---

## 🧭 The Big Picture

> In real life, if you need to know where a friend lives, you look up their address. The `&` operator does exactly that for variables — it looks up the address and hands it to you.
>
> You've already seen `&` used with `scanf`: `scanf("%d", &age);`. Now you'll understand *why* — `scanf` needs the address of `age` so it can write the input value directly into that memory location, not into a copy.

---

## 📚 Core Content

### The `&` (Address-of) Operator

The `&` operator returns the memory address of its operand:

```c
int x = 42;
printf("%p", &x);   // Prints the address where x lives in memory
```

Think of `&` as asking: "Where do you live?" You give it a variable, and it tells you the street address.

### Rules for `&`

```c
int x = 10;
int arr[5] = {1, 2, 3, 4, 5};

// ✅ VALID: variables
&x;        // Address of x
&arr[0];   // Address of first array element
arr;       // Equivalent to &arr[0] (array name decays to pointer)

// ❌ INVALID: expressions and constants
&(x + 5);  // Cannot take address of an expression result (temporary)
&42;       // Cannot take address of a literal constant
&(x > 5);  // Cannot take address of a comparison result
```

Expressions like `x + 5` produce temporary values that don't have permanent memory locations. You can only take the address of variables (things that occupy memory).

### Why `scanf` Needs `&`

```c
#include <stdio.h>

int main(void) {
    int age;
    
    printf("Enter your age: ");
    scanf("%d", &age);   // &age passes the ADDRESS of age
    // scanf writes the input value directly into that address
    
    printf("You are %d years old.\n", age);
    return 0;
}
```

If you wrote `scanf("%d", age)` without `&`, you'd pass the *value* of `age` (which is uninitialized garbage) instead of its address. `scanf` would try to write to a random memory location — likely crashing your program.

### Exception: Arrays

Array names automatically decay to pointers — so `arr` is the same as `&arr[0]`:

```c
int arr[5] = {10, 20, 30, 40, 50};

printf("%p\n", arr);     // Address of first element
printf("%p\n", &arr[0]); // Same address
printf("%p\n", &arr);    // Same address (but different type!)
```

The first two are identical in both value AND type (`int *`). The third (`&arr`) gives the same address but with type `int (*)[5]` (pointer to an array of 5 ints) — a subtle difference you'll rarely need.

### Using `&` with Different Types

```c
int i = 5;
double d = 3.14;
char c = 'Z';
char str[] = "Hello";

int    *ip = &i;     // int *
double *dp = &d;     // double *
char   *cp = &c;     // char *
char   *sp = str;    // No & needed — str already decays to pointer
```

Each pointer type matches the variable type. You can't (safely) store a `double *` in an `int *`:

```c
int *bad = &d;   // ⚠️ Compiler warning: incompatible pointer types
```

---

## 🧪 Try It Yourself

> **Exercise 1: Address Explorer**
> Declare variables of types `int`, `double`, `char`, and an array `int arr[3]`. Print the address of each using `&`. Observe how the addresses are spaced.

> **Exercise 2: Prove `arr` == `&arr[0]`**
> Print `arr` and `&arr[0]` for an array. Are they the same? Now print `arr + 1` and `&arr[1]`. What do you notice?

> **Exercise 3: Try the Invalid**
> Intentionally try to take the address of an expression like `&(x + 5)`. What error does the compiler give?

> **Exercise 4: `scanf` Without `&`**
> Write a `scanf` call without the `&` for an integer. Compile and run it. What happens? (Be ready for a crash — this is a learning exercise!)

---

## 💡 Common Pitfalls

- ❌ **Forgetting `&` in `scanf`** — The most common beginner bug. Pass addresses, not values.
- ❌ **Taking address of wrong type** — `double *dp = &i;` (where i is int) triggers a warning. The types must match.
- ❌ **Taking address of a constant** — `&42` makes no sense. Constants live in the code, not in a variable's memory location.
- ❌ **Using `&` with string literals** — `&"Hello"` is valid in C (string literals are arrays) but confusing. Just use the string literal directly.

---

## 🔗 Connections to What You Know

> **`&` is like looking up a friend's address in your contacts.**
>
> You have the friend's name (the variable name). You check your contacts to find their address (`&variable`). Now you can send a delivery (a function) directly to that address to drop off a package or pick one up.
>
> Without `&`, you'd be shouting the message at the house from afar (pass-by-value) — they might hear it, but they can't send anything back. With `&`, you have the physical address and can have a proper exchange.

---

## ✅ Section Checklist

- [ ] I can use `&` to get the address of any variable
- [ ] I understand why `scanf` needs `&`
- [ ] I know that arrays decay to pointers automatically
- [ ] I know not to take the address of expressions or constants
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [9.4: Dereferencing Pointers (*) →](./04-dereferencing.md)*
