# 9.4: Dereferencing Pointers (`*`) — Following the Address

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Use `*` to dereference a pointer and access the value at the address
- Distinguish between declaration `*`, dereference `*`, and multiplication `*`
- Modify the original variable through a pointer
- Understand pass-by-reference semantics using pointers

---

## 🧭 The Big Picture

> You're holding an address card: "45 Maple Street." What do you do? You **follow** the address — you walk to 45 Maple Street and enter the house. Now you're inside, and you can do things there: meet the residents, pick up mail, rearrange the furniture.
>
> Dereferencing a pointer (`*p`) is exactly that: you follow the stored address to reach the actual variable. Once you're there, you can read the value, modify it, or use it in calculations.

---

## 📚 Core Content

### The Dereference Operator `*`

The `*` operator (in a statement, not a declaration) **follows** a pointer to access the value at the stored address:

```c
int x = 42;
int *p = &x;   // p holds the address of x

printf("%d\n", *p);  // Follow p to x, get the value → 42
```

`*p` says: "Go to the address stored in `p` and get the value you find there."

### The Three Meanings of `*`

```c
// 1. DECLARATION: Indicates a pointer type
int *p;   // "p is a pointer"

// 2. DEREFERENCE: Follows the pointer to access the value
*p = 10;  // "go to the address in p and set the value to 10"

// 3. MULTIPLICATION: Arithmetic operator
int product = a * b;  // "multiply a and b"
```

Context tells you which is which. In a declaration, `*` means "pointer." In a statement, `*` before a pointer means "dereference." Between two values, it's multiplication.

### Reading and Writing Through Pointers

```c
#include <stdio.h>

int main(void) {
    int x = 42;
    int *p = &x;
    
    // READ through pointer
    printf("Value of x: %d\n", *p);  // 42
    
    // WRITE through pointer
    *p = 100;  // Changes x to 100!
    
    printf("New value of x: %d\n", x);  // 100
    
    return 0;
}
```

When you write `*p = 100;`, you're saying: "Go to the address stored in `p` and put 100 there." Since `p` holds `&x`, this changes `x` itself.

### Pass-by-Reference Using Pointers

This is the killer feature of pointers — they let functions modify the caller's variables:

```c
#include <stdio.h>

void swap(int *a, int *b) {
    int temp = *a;   // Read value at address a
    *a = *b;         // Write value from address b into address a
    *b = temp;       // Write temp into address b
}

int main(void) {
    int x = 10, y = 20;
    
    printf("Before: x = %d, y = %d\n", x, y);
    
    swap(&x, &y);   // Pass addresses, not values
    
    printf("After: x = %d, y = %d\n", x, y);  // x=20, y=10!
    
    return 0;
}
```

Without pointers, `swap` would only swap copies. With pointers, it swaps the originals.

### Dereferencing a `NULL` Pointer Crashes

```c
int *p = NULL;
printf("%d\n", *p);  // ⚠️ CRASH! Dereferencing NULL causes a segfault
```

This is why you *always* check:

```c
if (p != NULL) {
    printf("%d\n", *p);
} else {
    printf("Pointer is NULL — cannot dereference\n");
}
```

### Chain of Access with Pointers

```c
int x = 42;
int *p = &x;     // p points to x
int **pp = &p;   // pp points to p (which points to x)

// All of these access x:
printf("%d\n", x);    // Direct access — 42
printf("%d\n", *p);   // Follow p once — 42
printf("%d\n", **pp); // Follow pp, then p — 42
```

This is like having an address card that points to another address card that points to the house. You follow the chain until you reach the building.

### Dereferencing with Different Types

![Pointer as Direct Address](../assets/ch09/pointer-as-direct-address.svg)

---

## 🧪 Try It Yourself

> **Exercise 1: Read and Write**
> Declare `int value = 50;` and `int *ptr = &value;`. Print `*ptr`. Then set `*ptr = 99;` and print `value`. What changed?

> **Exercise 2: Swap Function**
> Write the `swap` function shown above and test it with two integers. Verify the originals are swapped.

> **Exercise 3: Reset to Zero**
> Write a function `void set_zero(int *p)` that sets the pointed-to value to 0. Call it on a variable and verify.

> **Exercise 4: Triple Pointer (Challenge)**
> Declare `int x = 7;`, then `int *p1 = &x;`, `int **p2 = &p1;`, `int ***p3 = &p2;`. Print `x` by dereferencing each pointer level. (This is just for understanding — you'll rarely need triple pointers in practice.)

---

## 💡 Common Pitfalls

- ❌ **Dereferencing an uninitialized pointer** — The address is garbage. You'll write to a random memory location.
- ❌ **Dereferencing `NULL`** — Immediate crash. Always check for `NULL`.
- ❌ **Forgetting `*` in assignment** — `p = 100;` changes the POINTER (the address it holds), not the pointed-to value. You want `*p = 100;`.
- ❌ **Using undeclared pointer** — `*p = 10;` without declaring `int *p = something;` first. The compiler will reject this.

---

## 🔗 Connections to What You Know

> **Dereferencing is like following an address to its destination.**
>
> You have an address card (`p`). The action of walking to that address and entering the building is **dereferencing** (`*p`). Once inside, you can:
> - Read the mail on the table — `printf("%d", *p);`
> - Leave new mail behind — `*p = new_value;`
> - Take something with you — `int y = *p;`
>
> Without dereferencing, the address card is useless — it's just a piece of paper with writing. The power comes from *going to the address and interacting with what's there.*

---

## ✅ Section Checklist

- [ ] I can dereference a pointer using `*` to access the pointed-to value
- [ ] I can distinguish declaration `*`, dereference `*`, and multiplication `*`
- [ ] I can modify a variable through a pointer
- [ ] I always check for `NULL` before dereferencing
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [9.5: Pointers and Arrays →](./05-pointers-and-arrays.md)*
