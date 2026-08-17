# 4.1: Arithmetic Operators — The Language of Calculation

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Use the five arithmetic operators: `+`, `-`, `*`, `/`, `%`
- Predict the result of integer division and understand when it truncates
- Use the modulo operator `%` to find remainders
- Combine arithmetic operators in expressions

---

## 🧭 The Big Picture

> Imagine you're organizing a community event and calculating its budget. You need to:
> - **Add** up the cost of all supplies (`+`)
> - **Subtract** the sponsor's contribution (`-`)
> - **Multiply** the daily allowance by the number of days (`*`)
> - **Divide** the total cost among participating groups (`/`)
> - Know the **remainder** when costs don't split evenly (`%`)
>
> These are the five fundamental arithmetic operations of C. You already know them from elementary school math. The only twist is that C — like any precise rulebook — has exact rules about how these operations work on different types of data.

---

## 📚 Core Content

### The Five Operators

| Operator | Name | Example | What It Does | IR Analogy |
|----------|------|---------|-------------|------------|
| `+` | Addition | `5 + 3` → `8` | Adds two values | Combining budgets |
| `-` | Subtraction | `5 - 3` → `2` | Subtracts right from left | Reducing funds |
| `*` | Multiplication | `5 * 3` → `15` | Multiplies two values | Compound calculation |
| `/` | Division | `6 / 3` → `2` | Divides left by right | Splitting costs |
| `%` | Modulo | `7 % 3` → `1` | Returns the remainder | Leftover after splitting |

### Basic Arithmetic

Arithmetic works exactly as you'd expect with integers:

```c
#include <stdio.h>

int main(void)
{
    int a = 10;
    int b = 3;
    
    printf("a + b = %d\n", a + b);  // 13
    printf("a - b = %d\n", a - b);  // 7
    printf("a * b = %d\n", a * b);  // 30
    printf("a / b = %d\n", a / b);  // 3 (NOT 3.333!)
    printf("a %% b = %d\n", a % b); // 1 (remainder of 10/3)
    
    return 0;
}
```

**Important:** When both operands of `/` are integers, C performs **integer division** — it divides and truncates (discards) any fractional part. `10 / 3` gives `3`, not `3.333`. You learned this in Chapter 3, but it bears repeating because it's one of the most common beginner mistakes.

### The Modulo Operator (`%`)

The modulo operator gives you the **remainder** after division. It's not something you use in everyday math, but it's incredibly useful in programming:

```c
int result = 17 % 5;  // 17 / 5 = 3 remainder 2
                       // result = 2
```

**How modulo works:**
```
17 % 5:
  5 goes into 17 three times (3 × 5 = 15)
  17 - 15 = 2
  Result: 2

7 % 3:
  3 goes into 7 two times (2 × 3 = 6)
  7 - 6 = 1
  Result: 1

20 % 4:
  4 goes into 20 five times (5 × 4 = 20)
  20 - 20 = 0
  Result: 0
```

**Common uses of `%`:**

```c
// Check if a number is even or odd
int num = 7;
if (num % 2 == 0) {
    printf("Even\n");
} else {
    printf("Odd\n");  // This runs (7 % 2 = 1)
}

// Extract the last digit
int year = 2026;
int last_digit = year % 10;  // 2026 % 10 = 6

// Keep a value within a range (wrapping)
int value = 27;
int wrapped = value % 12;  // 27 % 12 = 3 (like a clock)
```

### Mixed-Type Arithmetic

When you mix integers and floating-point numbers, remember the type conversion rules from Chapter 3:

```c
int x = 10;
double y = 3.0;

printf("%f\n", x + y);  // 13.000000 (int → double, result is double)
printf("%f\n", x / y);  // 3.333333 (int → double, result is double)
```

But be careful:

```c
int a = 10;
int b = 3;

// This does NOT give 3.333:
double result1 = a / b;         // 3.0 (integer division FIRST, then stored as 3.0)

// This DOES give 3.333:
double result2 = (double)a / b; // 3.333 (cast before division)
double result3 = a / 3.0;       // 3.333 (3.0 is a double literal)
```

### Combining Operators

You can combine operators in expressions, just like in math:

```c
int result = 10 + 5 * 2;      // 20 (multiplication before addition)
int total = (10 + 5) * 2;     // 30 (parentheses override)
```

**Order of operations (precedence):**
1. `()` — Parentheses first (innermost first)
2. `* / %` — Multiplication, division, modulo (left to right)
3. `+ -` — Addition and subtraction (left to right)

This is exactly the PEMDAS/BODMAS rule you learned in school. When in doubt: **add parentheses**.

The diagram below shows where arithmetic operators fit in the full precedence hierarchy (we'll explore the other operators in the coming sections):

![Operator Precedence](../assets/ch04/operator-precedence.svg)

For now, focus on the middle section of the diagram: `* / %` (multiplicative) above `+ -` (additive). This is the part that applies right now.

```c
// These are equivalent — but which is easier to read?
int a = 5 + 3 * 4 / 2 - 1;          // 5 + (3*4)/2 - 1 = 5 + 12/2 - 1 = 5+6-1 = 10
int b = 5 + ((3 * 4) / 2) - 1;      // Same result, much clearer
```

### Negative Numbers and Modulo

Modulo with negative numbers behaves differently in C than in some other languages:

```c
printf("%d\n",  7 %  3);   //  1
printf("%d\n", -7 %  3);   // -1  (C: result has same sign as dividend)
printf("%d\n",  7 % -3);   //  1  (C: result has same sign as dividend)
```

The rule is: `a % b` has the same sign as `a` (the dividend). This is important when dealing with negative numbers in loops and algorithms.

### Common Patterns

```c
// Parallel assignment with integers
int apples = 10;
int people = 3;
int each_gets = apples / people;  // 3 apples each
int leftover = apples % people;   // 1 apple left

// Temperature conversion (F → C)
int f = 75;
int celsius = (f - 32) * 5 / 9;   // (75-32)*5/9 = 43*5/9 = 215/9 = 23°C

// Force floating-point for precision
double precise_celsius = (f - 32) * 5.0 / 9;  // 23.888...
```

---

## 🧪 Try It Yourself

> **Exercise 1: Basic Arithmetic**
> Write a program that declares `int x = 15;` and `int y = 4;`. Print the results of `x + y`, `x - y`, `x * y`, `x / y`, and `x % y`. Before running, predict each result.

> **Exercise 2: Integer Division vs. Floating-Point**
> Write a program that computes `7 / 3` three ways:
> - Both operands as integers
> - One operand as a double literal (`7 / 3.0`)
> - Using an explicit cast `(double)7 / 3`
> Print all three and explain the differences.

> **Exercise 3: Even or Odd**
> Write a program that uses `% 2` to check whether the number 17 is even or odd. Then test with other numbers.

> **Exercise 4: Extract Digits**
> Given `int number = 4723;`, use `% 10` and `/ 10` to extract and print each digit (3, 2, 7, 4). Hint: `4723 % 10` gives 3, `4723 / 10` gives 472. Repeat!

---

## 💡 Common Pitfalls

- ❌ **Integer division when you meant floating-point** — `7 / 3` gives `2`, not `2.333`. Make at least one operand a double: `7 / 3.0` or `(double)7 / 3`.
- ❌ **Modulo with negative numbers** — `-7 % 3` gives `-1` in C, not `2`. Don't assume modulo always returns a non-negative result.
- ❌ **Division by zero** — `x / 0` crashes your program. Always check that the divisor is not zero before dividing.
- ❌ **Forgetting `%%` in printf** — To print a percent sign, use `%%`. `printf("%%");` prints `%`.
- ❌ **Misunderstanding precedence** — `5 + 3 * 2` is `11`, not `16`. Multiplication happens before addition. Use parentheses to make your intent clear.

---

## 🔗 Connections to What You Know

> **Arithmetic operators are the basic verbs of programming, just as addition and subtraction are the basic verbs of everyday life.**
>
> When someone balances a household budget, they add income, subtract expenses, multiply quantities by prices, and divide bills among roommates. These aren't just math exercises — they're the fundamental operations that turn numbers into decisions.
>
> C's arithmetic operators are exactly the same. They're not just math; they're the building blocks of every calculation your program will ever make. From counting votes to computing orbits, every numerical operation in computing decomposes into these five operators.

---

## 📖 Further Reading

- [C Arithmetic Operators (cppreference.com)](https://en.cppreference.com/w/c/language/operator_arithmetic) — Official reference
- [Modulo Operation (Wikipedia)](https://en.wikipedia.org/wiki/Modulo) — Deep dive into different languages' behavior
- [Integer Division (YouTube)](https://www.youtube.com/watch?v=mFa7WcCZxIA) — Visual explanation of truncation

---

## ✅ Section Checklist

- [ ] I can use all five arithmetic operators correctly
- [ ] I understand integer division and can predict when truncation happens
- [ ] I know how modulo works and can use it to solve real problems
- [ ] I can combine operators in expressions and predict the result
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [4.2: Relational Operators →](./02-relational-operators.md)*
