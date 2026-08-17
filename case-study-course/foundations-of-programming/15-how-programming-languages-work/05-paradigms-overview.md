# 15.5: Programming Paradigms — Different Ways of Thinking

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Distinguish between imperative, functional, and object-oriented paradigms
- Recognize that C is primarily imperative/procedural
- Understand that most modern languages support multiple paradigms
- Appreciate why learning C first gives you a foundation for any paradigm

---

## 🧭 The Big Picture

> Chefs have different cooking styles. Some follow a strict recipe step by step (procedural). Some build a kitchen around reusable stations and tools (object-oriented). Some focus on combining simple operations into larger transformations (functional).
>
> Programming **paradigms** are different styles of thinking about how to structure code. They're not better or worse — they're different tools for different problems. C is primarily **imperative/procedural**. But understanding C gives you a foundation for learning any paradigm.

---

## 📚 Core Content

### The Three Major Paradigms

### 1. Imperative/Procedural (C, Pascal, Fortran)

This is what we've been doing throughout this course. **Imperative** programming describes computation as a sequence of statements that change state. **Procedural** programming organizes code into functions (procedures).

```c
// Imperative/Procedural style
// Step by step: tell the computer exactly WHAT to do and WHEN
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int main(void) {
    int x = 10;
    int y = 20;
    int result = add(x, y);   // Call a procedure
    printf("%d\n", result);    // Output the result
    return 0;
}
```

**Key idea:** Computation = statements + functions that modify state.

### 2. Object-Oriented (C++, Java, Python, C#)

**Object-oriented programming (OOP)** bundles data and the functions that operate on that data into **objects**. Instead of passing data to functions, you ask objects to perform operations on themselves.

```cpp
// C++ — Object-Oriented style
// Objects contain BOTH data AND methods
class Calculator {
private:
    int total;
public:
    Calculator() { total = 0; }
    int add(int a, int b) { return a + b; }
    void add_to_total(int value) { total += value; }
};

int main() {
    Calculator calc;
    int result = calc.add(10, 20);  // Ask the object to do work
    calc.add_to_total(result);       // Tell the object to update itself
    return 0;
}
```

**Four pillars of OOP:**
1. **Encapsulation** — Bundle data and methods together; hide internal details
2. **Inheritance** — Create new classes based on existing ones
3. **Polymorphism** — Same interface, different implementations
4. **Abstraction** — Hide complex implementation behind simple interfaces

### 3. Functional (Haskell, Lisp, Clojure, F#)

**Functional programming** treats computation as the evaluation of mathematical functions. It avoids changing state and mutable data. Functions are first-class citizens — they can be passed as arguments and returned from other functions.

```haskell
-- Haskell — Functional style
-- No loops! No variables! Pure functions only!
add :: Int -> Int -> Int
add a b = a + b

-- Map applies a function to every element in a list
double_all :: [Int] -> [Int]
double_all list = map (\x -> x * 2) list

-- Usage: double_all [1,2,3,4] → [2,4,6,8]
```

**Key ideas:**
- **Pure functions** — Same input always produces same output, no side effects
- **Immutability** — Data never changes; you create new data instead
- **First-class functions** — Functions can be passed like any other value
- **No side effects** — Functions don't modify external state

### C and Function Pointers (A Functional Flavor)

Even C has some functional capability through **function pointers** (Chapter 9):

```c
#include <stdio.h>

int add(int a, int b) { return a + b; }
int multiply(int a, int b) { return a * b; }

// Function that takes another function as an argument (higher-order function)
int apply(int a, int b, int (*operation)(int, int)) {
    return operation(a, b);
}

int main(void) {
    printf("%d\n", apply(10, 20, add));       // 30
    printf("%d\n", apply(10, 20, multiply));  // 200
    return 0;
}
```

This is a taste of functional programming — passing functions as arguments — even in C.

### Paradigms in Practice

Most modern languages are **multi-paradigm**:

| Language | Imperative | OOP | Functional |
|----------|-----------|-----|------------|
| C | ✅ Primary | ❌ | ⚠️ Limited (function pointers) |
| Python | ✅ | ✅ | ✅ (some features) |
| JavaScript | ✅ | ✅ | ✅ (first-class functions) |
| Java | ✅ | ✅ Primary | ⚠️ Limited (lambdas in Java 8+) |
| C++ | ✅ | ✅ Primary | ⚠️ Limited (lambdas in C++11) |
| Rust | ✅ | ⚠️ (trait-based) | ✅ (functional features) |

### Why C First?

Learning C first gives you an advantage because:

1. **Imperative is the foundation** — Every paradigm ultimately runs on imperative machine code
2. **You see what's happening** — No hidden objects, no invisible garbage collection
3. **Transferable concepts** — Pointers, memory, and scope are the same in every language
4. **You appreciate abstractions** — When you see Python's `list`, you understand it's built on pointers and arrays — just like the linked list you implemented in C

---

## 🧪 Try It Yourself

> **Exercise 1: Identify the Paradigm**
> Look at the following code snippets and identify which paradigm(s) they represent:
> ```python
> class Dog:
>     def bark(self):
>         print("Woof!")
> ```

> ```c
> int numbers[] = {1, 2, 3, 4, 5};
> for (int i = 0; i < 5; i++) {
>     printf("%d\n", numbers[i]);
> }
> ```

> ```javascript
> [1,2,3,4].map(x => x * 2).filter(x => x > 4)
> ```

> **Exercise 2: Function Pointer as Callback**
> Write a function `void process_array(int arr[], int size, int (*transform)(int))` that applies a transformation function to every element of an array. Test it with `double_it` and `square` functions.

> **Exercise 3: OOP Analogy**
> Think of an everyday analogy for each of the four OOP pillars (encapsulation, inheritance, polymorphism, abstraction). Write a sentence for each.

> **Exercise 4: Why C First?**
> Write a paragraph explaining to a friend why learning C first will make them a better programmer in any language.

---

## 💡 Common Pitfalls

- ❌ **Thinking one paradigm is "best"** — Each paradigm has strengths. OOP excels at modeling real-world entities. Functional excels at data transformation. Imperative gives you the most control.

- ❌ **Confusing language with paradigm** — C is not "procedural" in the sense that it CAN'T do other paradigms — it's that it doesn't BUILT-IN support for them. You CAN implement OOP in C (structs + function pointers), it's just not as convenient.

---

## 🔗 Connections to What You Know

> **Paradigms are like schools of thought in any field.**
>
> Realism (imperative) focuses on practical power relations — step by step, state by state, what you see is what you get.
> Liberalism (OOP) focuses on institutions and relationships — structures that persist and interact over time.
> Constructivism (functional) focuses on ideas and identities — how the relationships between concepts shape outcomes.
>
> No single school explains everything. The best practitioners understand all three. The same is true for programming paradigms.

---

## ✅ Section Checklist

- [ ] I can explain the three major programming paradigms
- [ ] I understand that C is primarily imperative/procedural
- [ ] I know what function pointers enable (a taste of functional programming)
- [ ] I understand why learning C first is valuable for any paradigm
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [Chapter 15 Quiz →](./chapter-quiz.md)*
