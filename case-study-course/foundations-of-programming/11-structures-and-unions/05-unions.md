# 11.5: Unions — One Memory Location, Multiple Types

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Explain what a union is and how it differs from a struct
- Declare and use union variables
- Understand that a union stores only one field at a time
- Choose between structs and unions for different scenarios

---

## 🧭 The Big Picture

> A storage box can hold either a large textbook (500 pages), a small key (a few grams), or a few sheets of paper. It can only hold ONE of these at a time. The box is the same physical size regardless of what's inside — it's designed for the largest possible item, but typically carries smaller items.
>
> A **union** is exactly this: a single memory location that can hold data of different types, but only ONE at a time. It's like a struct where all fields share the same memory — writing to one field overwrites the others.

---

## 📚 Core Content

### What Is a Union?

A union is declared with the same syntax as a struct, but all fields **share the same memory location**:

```c
union Data {
    int i;        // 4 bytes
    float f;      // 4 bytes
    char str[20]; // 20 bytes
};  // ← Semicolon required, just like struct
```

The size of a union is the size of its **largest field**. In this case, `sizeof(union Data)` is 20 bytes (the size of `str[20]`).

### Union vs. Struct: Memory Comparison

```c
#include <stdio.h>

struct StructData {
    int i;          // 4 bytes
    float f;        // 4 bytes
    char str[20];   // 20 bytes
};  // Total: ~28 bytes (may include padding)

union UnionData {
    int i;          // 4 bytes
    float f;        // 4 bytes
    char str[20];   // 20 bytes
};  // Total: 20 bytes (largest field determines size)

int main(void) {
    struct StructData s = {42, 3.14f, "Hello"};
    union UnionData u;
    
    printf("Struct size: %zu bytes\n", sizeof(s));  // 28 (with padding)
    printf("Union size:  %zu bytes\n", sizeof(u));  // 20
    
    // In a struct, each field has its own memory
    printf("Struct: i=%d, f=%f, str=%s\n", s.i, s.f, s.str);  // All valid
    
    // In a union, fields share memory — only the LAST one written is valid
    u.i = 42;
    printf("Union after writing i: %d\n", u.i);      // ✅ 42
    
    u.f = 3.14f;  // This OVERWRITES u.i!
    printf("Union after writing f: %f\n", u.f);      // ✅ 3.14
    printf("Union reading i now: %d\n", u.i);        // ❌ Garbage! i was overwritten
    
    return 0;
}
```

### When to Use a Union

Unions are useful when a variable can hold one of several types, and you know which type is currently stored:

```c
#include <stdio.h>
#include <string.h>

// A message can be one of several types
enum MessageType {
    TEXT_MESSAGE,
    CODE_MESSAGE,
    NUMERIC_DATA
};

struct AppMessage {
    enum MessageType type;  // Which kind of data is stored?
    union {
        char text[200];     // TEXT_MESSAGE
        int code;           // CODE_MESSAGE
        double value;       // NUMERIC_DATA
    } data;
};

void print_message(const struct AppMessage *msg) {
    switch (msg->type) {
        case TEXT_MESSAGE:
            printf("Text: %s\n", msg->data.text);
            break;
        case CODE_MESSAGE:
            printf("Code: %d\n", msg->data.code);
            break;
        case NUMERIC_DATA:
            printf("Value: %.2f\n", msg->data.value);
            break;
    }
}

int main(void) {
    struct AppMessage msg;
    
    // Store a text message
    msg.type = TEXT_MESSAGE;
    strcpy(msg.data.text, "Meeting confirmed for Friday.");
    print_message(&msg);
    
    // Switch to numeric data (overwrites the text)
    msg.type = NUMERIC_DATA;
    msg.data.value = 98.6;
    print_message(&msg);
    
    return 0;
}
```

### Anonymous Unions (C11)

In C11 and later, you can omit the union name when it's inside a struct:

```c
#include <stdio.h>
#include <string.h>

enum DataType { TYPE_INT, TYPE_FLOAT, TYPE_STRING };

struct FlexibleValue {
    enum DataType type;
    // Anonymous union — fields accessed directly
    union {
        int i;
        float f;
        char str[50];
    };  // No name! Access fields directly on the struct
};

int main(void) {
    struct FlexibleValue val;
    
    val.type = TYPE_STRING;
    strcpy(val.str, "Meeting Note");  // Access str directly, not val.data.str
    
    printf("Value: %s\n", val.str);
    
    return 0;
}
```

### Practical: A Command Parser Using Unions

> **Note on syntax:** The pattern below uses **anonymous structs within an anonymous union** — both the union and the inner structs have no name. This is a C11 feature that lets you access the nested fields directly (e.g., `cmd->print_cmd.text`) without naming the union. It's a powerful pattern for type-discriminated data.

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

enum CommandType {
    CMD_PRINT,
    CMD_MOVE,
    CMD_DRAW
};

struct Command {
    enum CommandType type;
    union {
        struct { char text[100]; } print_cmd;
        struct { int x; int y; } move_cmd;
        struct { char shape[20]; int size; } draw_cmd;
    };
};

void execute_command(const struct Command *cmd) {
    switch (cmd->type) {
        case CMD_PRINT:
            printf("PRINT: %s\n", cmd->print_cmd.text);
            break;
        case CMD_MOVE:
            printf("MOVE to (%d, %d)\n", cmd->move_cmd.x, cmd->move_cmd.y);
            break;
        case CMD_DRAW:
            printf("DRAW %s (size: %d)\n", cmd->draw_cmd.shape, cmd->draw_cmd.size);
            break;
    }
}

int main(void) {
    struct Command cmds[3];
    
    cmds[0].type = CMD_PRINT;
    strcpy(cmds[0].print_cmd.text, "Hello, World!");
    
    cmds[1].type = CMD_MOVE;
    cmds[1].move_cmd.x = 10;
    cmds[1].move_cmd.y = 20;
    
    cmds[2].type = CMD_DRAW;
    strcpy(cmds[2].draw_cmd.shape, "circle");
    cmds[2].draw_cmd.size = 5;
    
    for (int i = 0; i < 3; i++) {
        execute_command(&cmds[i]);
    }
    
    return 0;
}
```

### Union Size and Alignment

```c
union Example {
    char c;         // 1 byte
    int i;          // 4 bytes
    double d;       // 8 bytes (largest)
};  // Size = 8 bytes (largest field)

union Large {
    int numbers[100];   // 400 bytes
    char buffer[500];   // 500 bytes (largest)
    struct {
        char name[50];
        int id;
    } record;           // 54 bytes
};  // Size = 500 bytes (largest field)
```

### Summary: Struct vs. Union

| Feature | Struct | Union |
|---------|--------|-------|
| Memory | All fields have their own memory | All fields share the same memory |
| Size | Sum of all fields (+ padding) | Size of largest field |
| Field access | All fields are valid simultaneously | Only the last-written field is valid |
| Use case | Grouping related data of different types | Storing one of several possible types |
| Analogy | A filing cabinet with multiple drawers | A single drawer that can hold different things, one at a time |

---

## 🧪 Try It Yourself

> **Exercise 1: Union Size**
> Define a union `union Test { char c; int i; double d; };`. Print `sizeof(union Test)` and compare it to the sizes of individual fields. Which field determines the union size?

> **Exercise 2: Overwriting Fields**
> Create a union with `int` and `float` fields. Write to the `int`, print it. Then write to the `float`, print the `float` AND the `int`. What happened to the `int`?

> **Exercise 3: Type-Discriminated Union**
> Define an enum `enum Kind { INT_VAL, DOUBLE_VAL, STRING_VAL };` and a struct with the enum and an anonymous union of those three types. Write a function that prints the value based on the enum tag.

> **Exercise 4: Save Memory**
> Imagine you have 10,000 items that can each be either an `int`, a `double`, or a `char[30]`. How much memory would a struct array use? How much would a union array with a type tag use? Calculate the savings.

---

## 💡 Common Pitfalls

- ❌ **Reading the wrong union field** — If you wrote to `u.f` and then read `u.i`, you get garbage. Always track which field is currently active (use a tag/enum).

- ❌ **Assuming union clears previous values** — Unions do NOT zero out memory when you write a new field. Old bits may remain if the new field is smaller.

- ❌ **Using a union when a struct is needed** — If you need to access multiple fields simultaneously (like storing a person's name AND age), use a struct. A union only stores one at a time.

- ❌ **Forgetting the semicolon** — Like structs, union definitions must end with a semicolon.

---

## 🔗 Connections to What You Know

> **A union is like a single-compartment storage box.**
>
> The box has one compartment. You can put in a textbook (500 pages), a key (a few grams), or a few sheets of paper. But only ONE at a time. The box is designed for the largest item, and its size doesn't change based on what's inside.
>
> The tag (like an enum) is like the label on the box — it tells you what type of contents to expect. Without it, you wouldn't know whether to expect pages, grams, or sheets.

---

## ✅ Section Checklist

- [ ] I understand that union fields share memory (only one is valid at a time)
- [ ] I can declare and use union variables
- [ ] I can use a tag/enum to track which union field is active
- [ ] I know when to use a union vs. a struct
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [Chapter 11 Quiz →](./chapter-quiz.md)*
