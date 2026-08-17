# 4.2: Relational Operators — Making Comparisons

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Use all six relational operators: `==`, `!=`, `<`, `>`, `<=`, `>=`
- Explain how relational expressions produce true/false (1/0) results
- Avoid the common trap of using `=` instead of `==`
- Compare variables, literals, and expressions

---

## 🧭 The Big Picture

> You constantly make comparisons:
> - "Is the assignment deadline **greater than** today's date?"
> - "Is my spending **equal to** my budget?"
> - "Is the number of items in my cart **less than** the 10-item limit?"
> - "Is my answer **not equal to** the example's?"
>
> Computers make these same comparisons constantly. Every `if` statement, every loop, every decision in a program relies on relational operators. They're the yes/no questions that your code asks the computer — and the computer always answers truthfully (with 1 for yes, 0 for no).

---

## 📚 Core Content

### The Six Relational Operators

| Operator | Meaning | Example | Reads As | English |
|----------|---------|---------|----------|---------|
| `==` | Equal to | `5 == 5` | "5 equals 5" | Is 5 equal to 5? |
| `!=` | Not equal to | `5 != 3` | "5 not equal 3" | Is 5 not equal to 3? |
| `<` | Less than | `3 < 5` | "3 less than 5" | Is 3 less than 5? |
| `>` | Greater than | `5 > 3` | "5 greater than 3" | Is 5 greater than 3? |
| `<=` | Less than or equal | `3 <= 3` | "3 less than or equal 3" | Is 3 ≤ 3? |
| `>=` | Greater than or equal | `5 >= 3` | "5 greater than or equal 3" | Is 5 ≥ 3? |

### How Comparisons Work

Every relational expression produces an **integer result**:

- **1** (true) if the comparison is correct
- **0** (false) if the comparison is incorrect

```c
#include <stdio.h>

int main(void)
{
    printf("%d\n", 5 == 5);   // 1 (true)
    printf("%d\n", 5 == 3);   // 0 (false)
    printf("%d\n", 5 != 3);   // 1 (true)
    printf("%d\n", 5 < 3);    // 0 (false)
    printf("%d\n", 5 > 3);    // 1 (true)
    printf("%d\n", 5 <= 5);   // 1 (true)
    printf("%d\n", 5 >= 3);   // 1 (true)
    
    return 0;
}
```

**This is a key insight:** In C, "true" and "false" are just integers. `1` means true, `0` means false. Any non-zero value is also considered "true" in conditions.

### Comparing Variables

You'll most often compare variables, not literals:

```c
int age = 18;
int voting_age = 18;

int can_vote = (age >= voting_age);  // can_vote = 1 (true)
int is_exactly = (age == voting_age); // is_exactly = 1 (true)
int is_different = (age != voting_age); // is_different = 0 (false)
```

And combined with arithmetic:

```c
int score = 85;
int passing = 60;
int bonus = 10;

// You can compare expressions, not just simple values
int has_passed = (score + bonus >= passing);  // 95 >= 60 → 1 (true)
```

### The Most Common Bug: `=` vs `==`

This is the single most common mistake in C programming, and even experienced developers make it:

```c
// BUG: Single = means ASSIGNMENT, not comparison!
if (x = 5)    // ❌ This ASSIGNS 5 to x, then checks if x is non-zero
              // (which it always will be, since 5 ≠ 0)

// CORRECT: Double == means COMPARISON
if (x == 5)   // ✅ This checks if x is equal to 5
```

**Why this is dangerous:** `if (x = 5)` doesn't cause a compilation error. It assigns `5` to `x`, and then checks whether `x` is non-zero (which it is). So the `if` body always executes, and you've also changed your variable's value. The bug is silent and hard to find.

**A defense mechanism:** Some programmers write the comparison in reverse order:

```c
if (5 == x)   // ✅ Still works: "is 5 equal to x?"
if (5 = x)    // ❌ Won't compile! Can't assign to a literal
```

This is called a "Yoda condition." It uses the compiler to catch the bug. If you accidentally type `=` instead of `==`, the compiler will refuse to compile `5 = x` because you can't assign a value to a literal.

### Comparing Floating-Point Numbers

Here's a tricky one: you should rarely use `==` with `float` or `double` values:

```c
double a = 0.1 + 0.2;  // You'd expect 0.3
double b = 0.3;

printf("%d\n", a == b);  // 0 (false!) — because of floating-point precision
```

Floating-point numbers have tiny rounding errors. `0.1 + 0.2` might be `0.30000000000000004`, not exactly `0.3`. Instead of `==`, check if the difference is very small:

```c
#include <math.h>   // for fabs()

double a = 0.1 + 0.2;
double b = 0.3;
double epsilon = 0.000001;

if (fabs(a - b) < epsilon) {
    printf("Approximately equal\n");  // This will run
}
```

We'll cover this in more detail later. For now, just remember: **don't use `==` with floating-point numbers.**

### Chaining Comparisons — A Warning

In math, you can write `0 < x < 10`. In C, this doesn't work as expected:

```c
int x = 5;

// ⚠️ This compiles but does something WRONG:
int result = (0 < x < 10);  // DON'T DO THIS!

// Here's why: C evaluates left to right:
// Step 1: (0 < x) → (0 < 5) → 1 (true)
// Step 2: (1 < 10) → 1 (true)
// So result = 1 — which happens to be correct here. But what about...

int y = 100;
int bad = (0 < y < 10);  // Step 1: (0 < 100) → 1
                           // Step 2: (1 < 10) → 1
                           // bad = 1 — WRONG! y is 100, not < 10!
```

To check if a value is between two others, use the logical AND operator (`&&`):

```c
if (x > 0 && x < 10) {    // ✅ Correct way: check both conditions
    printf("x is between 0 and 10\n");
}
```

We'll cover `&&` in the next section on logical operators.

### Relational Operators with Characters

Characters are stored as ASCII numbers, so you can compare them:

```c
char grade = 'B';

int is_a = (grade == 'A');          // 0 (false)
int passed = (grade <= 'C');        // 'B' (66) <= 'C' (67) → 1 (true)
int is_letter = (grade >= 'A' && grade <= 'Z');  // 1 (true)

// Uppercase vs. lowercase
char c = 'b';
int is_upper = (c >= 'A' && c <= 'Z');  // 0 (false, 'b' is lowercase)
```

---

## 🧪 Try It Yourself

> **Exercise 1: Basic Comparisons**
> Write a program that declares `int x = 10;` and `int y = 20;`. Print the result of all six relational operators comparing `x` and `y`. Before running, predict which will be 1 (true) and which will be 0 (false).

> **Exercise 2: Accidentally Assignment**
> Write this code and compile it:
> ```c
> int x = 5;
> if (x = 10) {
>     printf("True\n");
> }
> printf("x is now: %d\n", x);
> ```
> What prints? Why? Now fix it by changing `=` to `==`.

> **Exercise 3: Yoda Conditions**
> Rewrite `if (x == 5)` as `if (5 == x)`. Then try writing `if (5 = x)` and see what error the compiler gives. This is why Yoda conditions can protect you.

> **Exercise 4: Floating-Point Trap**
> Write a program that checks if `0.1 + 0.2 == 0.3`. Print the result. Then print the actual value of `0.1 + 0.2` with high precision (`%.20f`). What do you see?

---

## 💡 Common Pitfalls

- ❌ **`=` instead of `==`** — The most common C bug. `if (x = 5)` assigns 5 to x and always runs. Use Yoda conditions or enable compiler warnings (`-Wall`) to catch this.
- ❌ **Comparing floating-point with `==`** — Floating-point precision means `0.1 + 0.2 != 0.3`. Use a tolerance check instead.
- ❌ **Chaining comparisons like math** — `0 < x < 10` doesn't work in C. Use `x > 0 && x < 10` instead.
- ❌ **Forgetting that comparisons return integers** — `int result = (5 > 3);` gives `result = 1`, not a boolean. This is actually useful, but be aware of it.

---

## 🔗 Connections to What You Know

> **Relational operators are like the yes/no questions behind every decision.**
>
> Any process that follows rules uses standard questions to decide how to proceed:
> - "Is the number of guests **equal to** the number of seats?" (`==`)
> - "Is the remaining time **less than** the deadline?" (`<`)
> - "Is the score **greater than or equal to** the passing mark?" (`>=`)
>
> These questions have only two answers: yes or no. In C, that's 1 or 0. The computer doesn't say "maybe" or "it depends" — it gives a precise, binary answer every time.
>
> And just as you would never write "the deadline = 30 days" when you mean "the deadline == 30 days," a C programmer must never use `=` when they mean `==`. One is an order; the other is a question. Confusing them is like confusing "make it so" with "is it so?"

---

## 📖 Further Reading

- [C Relational Operators (cppreference.com)](https://en.cppreference.com/w/c/language/operator_comparison) — Official reference
- [Floating-Point Comparison](https://floating-point-gui.de/errors/comparison/) — Best practices for comparing floats
- [What Every Computer Scientist Should Know About Floating-Point](https://docs.oracle.com/cd/E19957-01/806-3568/ncg_goldberg.html) — Deep dive (advanced)

---

## ✅ Section Checklist

- [ ] I can use all six relational operators and predict their results
- [ ] I understand the difference between `=` (assignment) and `==` (comparison)
- [ ] I know why comparing floating-point with `==` is dangerous
- [ ] I know why `0 < x < 10` doesn't work and how to fix it
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [4.3: Logical Operators →](./03-logical-operators.md)*
