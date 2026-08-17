# 9.2: Declaring Pointers — Syntax and Types

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Declare pointers to different data types
- Read pointer declarations correctly
- Initialize pointers at declaration time
- Understand that a pointer type determines how to interpret the data at the address

---

## 🧭 The Big Picture

> Just as an address specifies *what kind of building* you're looking for ("house", "apartment", "office"), a pointer declaration specifies *what type of data* lives at the address. An `int *` pointer says: "The address I hold points to an integer." A `char *` pointer says: "The address I hold points to a character."
>
> The pointer type matters because different data types occupy different amounts of memory. When you follow a pointer, the computer needs to know: "Should I read 1 byte (char), 4 bytes (int), or 8 bytes (double) starting from this address?"

---

## 📚 Core Content

### Pointer Declaration Syntax

```c
type *pointer_name;
```

The `*` is the key. It declares that this variable is a **pointer** to a value of `type`.

```c
int    *int_ptr;     // Pointer to an integer
char   *char_ptr;    // Pointer to a character
double *double_ptr;  // Pointer to a double
void   *void_ptr;    // Generic pointer (can point to ANY type)
```

### Reading Pointer Declarations

Read pointer declarations **from right to left**, starting at the variable name:

```c
int  *p;    // p is a pointer to int
char *q;    // q is a pointer to char
```

For more complex types:

```c
int **pp;   // pp is a pointer to (pointer to int)
int *arr[5]; // arr is an array of 5 (pointers to int)
int (*fp)(int); // fp is a pointer to (function that takes int, returns int)
```

Don't worry about the complex ones yet — you'll get there section by section.

### The Spacing Debate

All of these are valid and mean the same thing:

```c
int* p;      // Style A: "p has type int*"
int *p;      // Style B: "*p has type int" (the pointer is in the name)
int * p;     // Style C: spaces don't matter
```

**Convention in this course:** `int *p` (Style B). The logic is that when you declare multiple variables on one line, the `*` attaches to the variable, not the type:

```c
int* p, q;   // p is int*, q is int (probably not what you wanted!)
int *p, q;   // p is int*, q is int (same result, but reads more clearly)
int *p, *q;  // Both p AND q are int* (both need the *)
```

**Best practice:** Declare each pointer on its own line:

```c
int *p;
int *q;      // Clear, unambiguous
```

### Initializing Pointers

```c
int x = 42;
int *p = &x;   // p now holds the address of x

char letter = 'A';
char *cp = &letter;  // cp holds the address of letter

double pi = 3.14159;
double *dp = &pi;    // dp holds the address of pi
```

### The `NULL` Pointer

A pointer that doesn't point to anything should be set to `NULL`:

```c
int *p = NULL;  // Points to nothing (address 0)
```

`NULL` is a special value (usually address `0`) that means "this pointer doesn't point to valid memory." You should **always** check for `NULL` before using a pointer:

```c
if (p != NULL) {
    *p = 42;  // Safe: we know p points to valid memory
}
```

### Uninitialized Pointers Are Dangerous

```c
int *p;        // p contains a garbage address!
*p = 42;       // ⚠️ Writing to a random address — crash or corrupt data!
```

Always initialize pointers — either to a valid address or to `NULL`.

### Pointer Type Matters

```c
int x = 1024;    // Binary: 00000000 00000000 00000100 00000000
int *ip = &x;    // Pointer to int — reads all 4 bytes

char *cp = (char *)&x;  // Pointer to char — reads only the FIRST byte
```

When you dereference `ip`, you get the full `int` value (1024). When you dereference `cp`, you get only the first byte (which depends on your system's **endianness**). The pointer type tells the compiler how many bytes to read.

![Pointer Types Diagram](../assets/ch09/pointer-types-diagram.svg)

---

## 🧪 Try It Yourself

> **Exercise 1: Multiple Pointer Declarations**
> Declare `int a = 10;`, `int b = 20;`, and two pointers `int *pa = &a;` and `int *pb = &b;`. Print the addresses stored in each pointer.

> **Exercise 2: NULL Pointer**
> Declare `int *p = NULL;`. Try to print `*p` (dereference it). What happens? (Be prepared for a crash — this is intentional!)

> **Exercise 3: Different Types**
> Declare one variable each of `int`, `double`, and `char`. Create pointers to each. Print both the pointer values (addresses) and their sizes using `sizeof`.

> **Exercise 4: Check Before Use**
> Write a program that checks if a pointer is `NULL` before dereferencing it. If it's `NULL`, print "Pointer is null" instead of crashing.

---

## 💡 Common Pitfalls

- ❌ **Uninitialized pointer** — Contains a garbage address. Dereferencing it crashes or corrupts data. Always initialize!
- ❌ **Forgetting the `*` in declaration** — `int p;` is just a regular integer, not a pointer.
- ❌ **Confusing declaration `*` with dereference `*`** — Same symbol, different meaning. In declaration: "this is a pointer." In code: "follow this address."
- ❌ **Not checking for `NULL`** — Always check before dereferencing a pointer that might be `NULL`.

---

## 🔗 Connections to What You Know

> **Pointer types are like different types of addresses.**
>
> A house address tells you to expect a home. An office address points to a different type of building. The address format might look similar (street, number, city), but what you find when you go there differs.
>
> Similarly, `int *` and `char *` both hold addresses, but what you find when you follow them — 4 bytes of integer or 1 byte of character — is determined by the type.

---

## ✅ Section Checklist

- [ ] I can declare pointers to different data types
- [ ] I can read complex pointer declarations
- [ ] I initialize pointers to valid addresses or `NULL`
- [ ] I understand that pointer types determine how to interpret memory
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [9.3: The Address-of Operator (&) →](./03-address-of-operator.md)*
