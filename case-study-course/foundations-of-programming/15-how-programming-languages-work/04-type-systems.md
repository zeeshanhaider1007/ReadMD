# 15.4: Type Systems — Static vs. Dynamic Typing

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Distinguish between static and dynamic type systems
- Explain the trade-offs between type safety and flexibility
- Understand where C's type system sits in the spectrum

---

## 🧭 The Big Picture

> In a library, every item has a **category**: fiction, reference, children's, or archive. The category determines where the item is stored, who can borrow it, and how it must be handled. Misplacing an item has consequences.
>
> A **type system** does the same thing for data. Every value has a **type** that determines what you can do with it, where it can be stored, and how it's interpreted. Some languages enforce types strictly (like a closed-stack library). Others are flexible (like an open library). C is strict — it checks types before your program runs.

---

## 📚 Core Content

### What Is a Type?

A **type** tells the compiler (or interpreter) three things:

1. **How much memory** the value occupies (4 bytes for int, 8 bytes for double)
2. **How to interpret the bits** (signed integer? unsigned? floating-point?)
3. **What operations are allowed** (can you multiply it? compare it? index into it?)

```c
int x = 42;       // 4 bytes, signed integer
double y = 3.14;  // 8 bytes, IEEE 754 floating-point
char z = 'A';     // 1 byte, ASCII value 65
```

### Static Typing (C, Java, C++, Rust)

**Types are checked at compile time.** Once a variable is declared with a type, it keeps that type forever.

```c
int x = 42;
x = 3.14;     // ❌ Compiler warning or error! (double → int narrowing)
x = "hello";  // ❌ Compiler error! (can't assign string to int)

// In C, you CAN do this (C trusts you):
x = (int)3.14;  // ✅ Explicit cast — you're telling the compiler you know what you're doing
```

**Advantages of static typing:**
- **Catches errors early** — Many bugs are found at compile time
- **Better performance** — The compiler knows exact sizes and can optimize
- **Self-documenting** — Types serve as documentation
- **Safer refactoring** — The type checker catches mistakes

### Dynamic Typing (Python, JavaScript, Ruby)

**Types are checked at runtime.** Variables can hold any type of value, and types can change.

```python
x = 42          # x is an integer
x = 3.14        # x is now a float — perfectly fine
x = "hello"     # x is now a string — also fine

# Error only happens at runtime:
x + 42          # ❌ Runtime error! Can't add string and int
```

**Advantages of dynamic typing:**
- **Faster to write** — No type declarations needed
- **More flexible** — Easy to handle heterogeneous data
- **Quick prototyping** — Don't need to plan types in advance

### The Type Spectrum

```text
STRICT                                          FLEXIBLE
C → Java → C++ → TypeScript → Python → JavaScript → PHP
```

C sits at the strict end. Python is flexible. JavaScript is very flexible.

### Strong vs. Weak Typing

This is a separate dimension from static/dynamic:

- **Strong typing:** Types are enforced strictly. The language doesn't automatically convert between unrelated types.
- **Weak typing:** The language may automatically convert types in unexpected ways.

```c
// C is WEAKLY typed — it does implicit conversions
int x = 3;
double y = x;       // ✅ Implicit conversion: int → double (safe)
int z = 3.14;       // ⚠️ Implicit conversion: double → int (truncates to 3!)
```

```python
# Python is STRONGLY typed — it doesn't do implicit conversions
x = 3
y = 3.14
# print(x + "hello")  # ❌ TypeError! Python won't convert int to string
print(str(x) + "hello")  # ✅ Explicit conversion
```

### Duck Typing

Some dynamically-typed languages (Python, JavaScript) use **duck typing**: "If it walks like a duck and quacks like a duck, it's a duck."

```python
def print_name(obj):
    print(obj.name)  # Works if obj HAS a 'name' attribute, regardless of type

class Person:
    name = "Alice"

class Country:
    name = "France"

print_name(Person())   # ✅ Works
print_name(Country())  # ✅ Works — same interface, different types
```

This wouldn't work in C without a common interface (struct + function pointers or union).

### C's Type System in Practice

C's type system is **static** and **weak**:

```c
// Static: types are checked at compile time
int x = 42;
// x = "hello";  // Compiler error

// Weak: implicit conversions happen
double d = 3.14;
int i = d;       // 3 — implicit truncation, no error (maybe a warning with -Wall)

// You can cast to override the type system
char c = 'A';
int *p = (int *)&c;  // ⚠️ Forces a char* to be treated as int* — dangerous!
```

---

## 🧪 Try It Yourself

> **Exercise 1: Static vs. Dynamic**
> Classify each language as statically or dynamically typed: Python, C, Java, JavaScript, Rust, Ruby.

> **Exercise 2: Implicit Conversion**
> In C, what happens when you assign a double value of 3.78 to an int variable? What if the double is 3.14e15? Run the code to see.

> **Exercise 3: Type Safety**
> Write a C program that has a type mismatch bug. Then write the equivalent in a language you know that would catch it differently.

> **Exercise 4: Duck Typing**
> Think of a scenario in diplomacy where "duck typing" applies — where what matters is behavior, not formal classification. Explain the analogy.

---

## 💡 Common Pitfalls

- ❌ **Confusing static/dynamic with strong/weak** — These are independent dimensions. C is static + weak. Python is dynamic + strong. Java is static + strong. JavaScript is dynamic + weak.

- ❌ **Thinking dynamic typing means "no types"** — Every value still has a type. The difference is WHEN the type is checked (at runtime vs. compile time).

---

## 🔗 Connections to What You Know

> **Static typing is like checking ID at the door; dynamic typing is like an open reception.**
>
> With static typing, every person entering the venue must present ID proving their age (type). You know exactly who's inside, and you can plan accordingly. But it takes time to check everyone.
>
> With dynamic typing, anyone can enter the venue (any type). You find out what they can do when they try to participate. It's faster to get started, but you might discover mid-event that someone can't do the thing you assumed.

---

## ✅ Section Checklist

- [ ] I understand the difference between static and dynamic typing
- [ ] I understand the difference between strong and weak typing
- [ ] I know where C sits on both spectrums
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [15.5: Programming Paradigms →](./05-paradigms-overview.md)*
