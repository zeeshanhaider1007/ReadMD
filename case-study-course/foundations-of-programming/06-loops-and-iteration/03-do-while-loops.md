# 6.3: Do-While Loops — Execute First, Ask Later

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Write a `do-while` loop and explain when it's appropriate
- Explain why `do-while` always executes its body at least once
- Choose between `do-while` and `while` based on the problem

---

## 🧭 The Big Picture

> Imagine a store that opens its doors every morning, regardless of whether any customers show up. The opening happens first (the body of the loop). Then the store checks for customers. If there are customers, it serves them and checks again. If there are none, it closes.
>
> This is the `do-while` loop: execute the body **first**, then check the condition. If the condition is true, repeat; if false, stop.
>
> The key difference from `while` is that `do-while` guarantees **at least one execution**. A `while` loop might never run if the condition is initially false. A `do-while` always runs at least once — because the condition is checked after the body, not before.

---

## 📚 Core Content

### The `do-while` Syntax

```c
do {
    // Loop body — always executes at least once
} while (condition);  // ← Note the semicolon!
```

### Basic Example

```c
#include <stdio.h>

int main(void)
{
    int i = 0;
    
    do {
        printf("%d ", i);
        i++;
    } while (i < 5);     // ← Don't forget the semicolon!
    
    return 0;
}
```

**Output:** `0 1 2 3 4`

### The Key Difference: `while` vs. `do-while`

```c
// While: checks FIRST — might run 0 times
int x = 10;
while (x < 5) {          // Condition is false (10 < 5)
    printf("Runs? ");    // NEVER runs
    x++;
}

// Do-While: executes FIRST — always runs at least once
int y = 10;
do {
    printf("Runs? ");    // Runs ONCE
    y++;
} while (y < 5);         // Condition is false (11 < 5)
                          // But the body already executed!
```

**Output:**
```
Runs?                ← Only the do-while version printed something
```

### When to Use `do-while`

`do-while` is perfect for situations where the action must happen at least once, and the condition for repeating depends on the result of that action:

```c
// 1. Menu-driven program: show menu at least once
int choice;
do {
    printf("1. View 2. Edit 3. Exit\n");
    printf("Choice: ");
    scanf("%d", &choice);
    
    // Process choice...
} while (choice != 3);

// 2. User input validation: ask at least once
int age;
do {
    printf("Enter age (0-150): ");
    scanf("%d", &age);
} while (age < 0 || age > 150);

// 3. Game loop: play at least one round
char play_again;
do {
    play_round();
    printf("Play again? (y/n): ");
    scanf(" %c", &play_again);
} while (play_again == 'y' || play_again == 'Y');
```

### The Semicolon Trap

The `do-while` is the only loop that ends with a semicolon. Forgetting it is a common error:

```c
do {
    printf("Hello\n");
} while (0);    // ← THIS SEMICOLON IS REQUIRED!
```

Without the semicolon, the compiler will produce an error on the next line.

### Comparing All Three Loops

The diagram below shows all three loop types side by side with their syntax and usage:

![Loop Types Comparison](../assets/ch06/loop-types-comparison.svg)

```c
// Loop that runs exactly 5 times:

// 1. While (check first)
int i = 0;
while (i < 5) {
    printf("%d ", i);
    i++;
}

// 2. For (all control in one line)
for (int i = 0; i < 5; i++) {
    printf("%d ", i);
}

// 3. Do-While (run at least once)
int i = 0;
do {
    printf("%d ", i);
    i++;
} while (i < 5);
```

All three produce: `0 1 2 3 4`

### When the Condition is Initially False

```c
// While: body NEVER executes
int count = 100;
while (count < 0) {      // false
    printf("Never\n");   // skipped
}

// Do-While: body executes ONCE
int count = 100;
do {
    printf("Once\n");    // runs
} while (count < 0);     // false, but body already ran
```

### Real-World Use Case: Menu System

```c
#include <stdio.h>

int main(void)
{
    int option;
    
    do {
        // Display menu
        printf("\n=== Main Menu ===\n");
        printf("1. Visa Information\n");
        printf("2. Trade Inquiry\n");
        printf("3. Emergency Contact\n");
        printf("4. Exit\n");
        printf("Select option: ");
        scanf("%d", &option);
        
        // Process option
        switch (option) {
            case 1:
                printf("Visa processing takes 5-10 business days.\n");
                break;
            case 2:
                printf("Trade inquiries are handled by the delegation.\n");
                break;
            case 3:
                printf("Emergency: Call +1-800-555-0199\n");
                break;
            case 4:
                printf("Thank you. Goodbye.\n");
                break;
            default:
                printf("Invalid option. Please try again.\n");
        }
    } while (option != 4);
    
    return 0;
}
```

This is the classic `do-while` pattern: show the menu, get input, process, then ask "should we show the menu again?" The menu always displays at least once.

---

## 🧪 Try It Yourself

> **Exercise 1: Guaranteed Execution**
> Write a program with a `do-while` loop where the condition is `while (0);`. Will the loop body execute? Run it to confirm.

> **Exercise 2: Password Prompt**
> Write a program that repeatedly asks the user to enter a password ("secret") using a `do-while` loop. Keep asking until the correct password is entered. Print "Access granted" when they succeed.

> **Exercise 3: Menu System**
> Create a simple menu with options 1-3 and an exit option (4). Use `do-while` to keep showing the menu until the user chooses to exit. Use `switch` (from Chapter 5) for option processing.

> **Exercise 4: Positive Number Only**
> Write a program that uses `do-while` to keep asking the user for a positive number until they enter one. Then print the square of that number.

> **Exercise 5: While vs Do-While**
> Write two versions of a loop that prints "Rolling dice..." and a random number (1-6). One version uses `while`, the other `do-while`. Which makes more sense for a dice-rolling simulator?

---

## 💡 Common Pitfalls

- ❌ **Forgetting the semicolon** — `do { ... } while (condition)` is a syntax error. The `;` after `while(condition)` is required and different from all other loops.
- ❌ **Using `do-while` when `while` is clearer** — If there's no reason the body must run at least once, prefer `while`. `do-while` should be reserved for cases where the first execution must happen unconditionally.
- ❌ **Infinite `do-while`** — If you forget to update the condition variable inside the loop, the loop runs forever (same as any other loop).
- ❌ **Misunderstanding "at least once"** — Some beginners think `do` makes the loop run forever. It doesn't. It just guarantees the first execution.

---

## 🔗 Connections to What You Know

> **A `do-while` loop is like the UN General Assembly's opening session.**
>
> A store opens every morning with an opening routine (the body executes). Then it decides whether to continue serving (the condition). Even if there are no customers, the opening happens — it's mandatory.
>
> A `while` loop would be like "Only open the store if there are customers waiting." It might never happen. The `do-while` says "Open the store, then decide if we need to keep serving."
>
> This pattern appears throughout everyday life: answering a phone call before knowing who's calling, making a first move in a game before seeing the opponent's response, and running a daily health check before deciding whether more checks are needed. The action always happens first — the condition for repetition comes after.

---

## 📖 Further Reading

- [do-while Loop (cppreference.com)](https://en.cppreference.com/w/c/language/do) — Official reference
- [Menu-Driven Programming Pattern](https://en.wikipedia.org/wiki/Menu-driven) — Common do-while use case
- [Loop Comparison (YouTube)](https://www.youtube.com/watch?v=4_mVRTf_cMc) — Visual explanation of all three loop types

---

## ✅ Section Checklist

- [ ] I can write a `do-while` loop with the correct syntax (including semicolon)
- [ ] I understand that `do-while` always executes at least once
- [ ] I know when to choose `do-while` over `while` (menu systems, user input)
- [ ] I can compare and contrast all three loop types
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [6.4: Loop Control — Break and Continue →](./04-loop-control.md)*
