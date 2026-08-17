# 📝 Chapter 11 Quiz — Structures & Unions

---

**Chapter:** 11 — Structures & Unions
**Total Questions:** 20
**Estimated Time:** 30–40 minutes

---

## Section 1: Multiple Choice

**1. What is a structure (`struct`) in C?**

a) A collection of elements of the same type accessed by index
b) A user-defined type that groups variables of different types under one name
c) A function that organizes code into reusable blocks
d) A pointer to a memory location

**2. What symbol is used to access a field of a struct variable?**

a) `->` (arrow)
b) `.` (dot)
c) `::` (scope)
d) `:` (colon)

**3. What is the size of this union?**
```c
union Data {
    int x;          // 4 bytes
    double y;       // 8 bytes
    char z[12];     // 12 bytes
};
```
a) 4 bytes
b) 8 bytes
c) 12 bytes
d) 24 bytes

**4. What operator do you use to access a struct field through a pointer?**

a) `.` (dot)
b) `->` (arrow)
c) `*` (dereference)
d) `&` (address-of)

**5. What happens when you assign one struct variable to another (e.g., `s2 = s1;`)?**

a) The pointer to `s1` is copied — both variables point to the same data
b) All fields from `s1` are copied into `s2` — they become independent
c) The program crashes because structs can't be assigned
d) Only the first field is copied

**6. In a union, what happens when you write to a different field than the one you read?**

a) The program crashes
b) All fields contain valid data simultaneously
c) The previously written field's data is overwritten — reading it gives garbage
d) The union automatically converts the data to the correct type

**7. What does `typedef` do in the context of structs?**

a) It allocates memory for a struct variable
b) It creates an alias for the struct type so you don't need to write `struct`
c) It initializes all fields to zero
d) It creates a pointer to the struct

**8. Which of the following is a valid way to initialize a nested struct?**

```c
struct Date { int day, month, year; };
struct Meeting { char agenda[50]; struct Date date; };
```
a) `struct Meeting m = {"Budget review", 15, 3, 2025};`
b) `struct Meeting m = {"Budget review", {15, 3, 2025}};`
c) `struct Meeting m = {"Budget review", 15, 3, 2025};`
d) `struct Meeting m = {agenda: "Budget review", date: {15, 3, 2025}};`

---

## Section 2: Short Answer

**9. Explain the difference between a struct and a union in terms of memory layout. When would you use each?**

*Your answer:*

**10. Why should you pass large structs to functions using pointers (`->`) instead of by value (`.`)?**

*Your answer:*

**11. What is a "self-referential struct"? Give an example and explain why you must use a pointer instead of directly including the struct type.**

*Your answer:*

---

## Section 3: Fill in the Blank

**12.** The operator used to access a struct field through a pointer is ________.

**13.** A ________ is a type that stores multiple fields that all share the same memory location.

**14.** The size of a union is determined by its ________ field.

**15.** A struct definition must end with a ________.

**16.** To prevent a function from modifying a struct passed by pointer, use the ________ qualifier.

---

## Section 4: Matching

**17. Match each concept to its description:**

| Concept | Description |
|---------|-------------|
| 1. `.` (dot) operator | a) Access a struct field through a pointer |
| 2. `->` (arrow) operator | b) Create an alias for a type |
| 3. `typedef` | c) Access a struct field directly |
| 4. Nested struct | d) A struct that contains another struct as a field |

**18. Match each memory characteristic to the correct type:**

| Characteristic | Type |
|----------------|------|
| 1. All fields have their own memory | a) Union |
| 2. Only one field can be valid at a time | b) Struct |
| 3. Size is the sum of all fields (+ padding) | c) Union |
| 4. Size is the size of the largest field | d) Struct |

---

## Section 5: Practical Application

**19. Find and fix the errors in this program:**

```c
#include <stdio.h>

struct Point {
    int x;
    int y;
}  // Missing semicolon

union Value {
    int i;
    double d;
};

int main(void) {
    struct Point p1 = {10, 20};
    struct Point *ptr = p1;  // Should be address
    
    ptr.x = 30;   // Wrong operator for pointer
    
    union Value v;
    v.i = 42;
    printf("Value: %d\n", v.i);
    
    v.d = 3.14;
    printf("Value: %d\n", v.d);  // Wrong format specifier
    
    struct Point p2;
    p2 = p1;       // Is this valid?
    
    if (p1 == p2) {  // Is this valid?
        printf("Equal\n");
    }
    
    return 0;
}
```

**20. Write a complete C program that:**

- Defines `struct Date` with fields: `int day, month, year`
- Defines `struct Event` with fields: `char name[100]`, `struct Date date`, `char location[100]`, `int attendees`
- Creates an array of 3 events (initialize with data for 2025 events)
- Writes a function `void print_event(const struct Event *e)` that prints an event in a nice format using `->`
- Writes a function `void add_attendees(struct Event *e, int count)` that increases the attendee count
- Calls the functions for each event and prints the updated data

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **b) A user-defined type that groups variables of different types under one name** — Structures group related data of potentially different types. *(Section 11.1)*
2. **b) `.` (dot)** — The dot operator accesses fields of a struct variable. *(Section 11.2)*
3. **c) 12 bytes** — The union size is determined by the largest field: `char z[12]` = 12 bytes. *(Section 11.5)*
4. **b) `->` (arrow)** — The arrow operator combines dereference and field access. *(Section 11.4)*
5. **b) All fields from `s1` are copied into `s2`** — Struct assignment performs a memberwise copy, creating independent copies. *(Section 11.2)*
6. **c) The previously written field's data is overwritten** — Union fields share memory; writing to one overwrites the others. *(Section 11.5)*
7. **b) It creates an alias for the struct type** — `typedef` lets you use `Student s1;` instead of `struct Student s1;`. *(Section 11.2)*
8. **b) `struct Meeting m = {"Budget review", {15, 3, 2025}};`** — Nested initializers use inner `{}` for nested structs. *(Section 11.3)*

### Section 2: Short Answer

9. **Model answer:** A struct allocates separate memory for each field — all fields can be used simultaneously. A union allocates one memory block shared by all fields — only one field is valid at a time. Use a struct when you need to group multiple related pieces of data. Use a union when a variable can hold one of several types, saving memory. *(Sections 11.1, 11.5)*

10. **Model answer:** Passing a large struct by value copies the entire struct (potentially thousands of bytes) onto the function's stack, which is slow and memory-intensive. Passing by pointer only copies the address (8 bytes on 64-bit), regardless of the struct's size. It's faster and uses less memory. *(Section 11.4)*

11. **Model answer:** A self-referential struct is a struct that contains a pointer to another instance of the same struct type, like `struct Node { int data; struct Node *next; };`. The pointer is necessary because including the struct directly would create infinite recursion (a struct containing itself of infinite size). A pointer has a fixed size (8 bytes), making it possible. *(Section 11.3)*

### Section 3: Fill in the Blank

12. **`->`** (arrow) — Accesses fields through a pointer. *(Section 11.4)*
13. **union** — Shares memory between all fields. *(Section 11.5)*
14. **largest** — The union is sized to hold its biggest member. *(Section 11.5)*
15. **semicolon** (`;`) — `struct Name { ... };` requires a semicolon after the closing brace. *(Section 11.1)*
16. **`const`** — `const struct Student *s` means the function cannot modify `s`. *(Section 11.4)*

### Section 4: Matching

17. **1 → c, 2 → a, 3 → b, 4 → d** *(Sections 11.2–11.4)*
18. **1 → d (Struct), 2 → c (Union), 3 → d (Struct), 4 → c (Union)** *(Sections 11.1, 11.5)*

### Section 5: Practical Application

19. **Errors:**
    1. Missing semicolon after `struct Point { int x; int y; }` — Add `;` after `}`
    2. `struct Point *ptr = p1;` — Should be `struct Point *ptr = &p1;` (address, not value)
    3. `ptr.x = 30;` — Should be `ptr->x = 30;` or `(*ptr).x = 30;` (arrow operator for pointers)
    4. `printf("Value: %d\n", v.d);` — `v.d` is a `double`, use `%f` not `%d`
    5. `if (p1 == p2)` — Cannot compare structs with `==`. Compare field by field.

    **Corrected code:**
    ```c
    #include <stdio.h>

    struct Point {
        int x;
        int y;
    };  // Fixed: added semicolon

    union Value {
        int i;
        double d;
    };

    int main(void) {
        struct Point p1 = {10, 20};
        struct Point *ptr = &p1;  // Fixed: address of p1
        
        ptr->x = 30;   // Fixed: arrow operator for pointer
        
        union Value v;
        v.i = 42;
        printf("Value: %d\n", v.i);
        
        v.d = 3.14;
        printf("Value: %f\n", v.d);  // Fixed: %f for double
        
        struct Point p2;
        p2 = p1;       // ✅ Valid — struct copy
        
        // Can't compare structs with ==
        if (p1.x == p2.x && p1.y == p2.y) {  // Fixed: compare field by field
            printf("Equal\n");
        }
        
        return 0;
    }
    ```

20. **Model answer:**
    ```c
    #include <stdio.h>
    #include <string.h>

    struct Date {
        int day;
        int month;
        int year;
    };

    struct Event {
        char name[100];
        struct Date date;
        char location[100];
        int attendees;
    };

    void print_event(const struct Event *e) {
        printf("=== %s ===\n", e->name);
        printf("Date: %d/%d/%d\n", e->date.day, e->date.month, e->date.year);
        printf("Location: %s\n", e->location);
        printf("Attendees: %d\n\n", e->attendees);
    }

    void add_attendees(struct Event *e, int count) {
        e->attendees += count;
    }

    int main(void) {
        struct Event events[3] = {
            {"Coding Workshop", {15, 3, 2025}, "Rome", 120},
            {"Science Fair", {22, 6, 2025}, "Paris", 500},
            {"Book Club", {10, 9, 2025}, "Oslo", 45}
        };
        
        for (int i = 0; i < 3; i++) {
            print_event(&events[i]);
        }
        
        // Add more attendees to each
        add_attendees(&events[0], 30);   // Trade Summit: 150
        add_attendees(&events[1], 100);  // Climate: 600
        add_attendees(&events[2], 15);   // Peace: 60
        
        printf("--- After adding attendees ---\n");
        for (int i = 0; i < 3; i++) {
            print_event(&events[i]);
        }
        
        return 0;
    }
    ```

---

## 📊 Quick Self-Assessment

| Score | Assessment | Action |
|:-----:|-----------|--------|
| 18–20 | 🎉 Excellent | Ready for Chapter 12! |
| 14–17 | ✅ Good | Review sections 11.4–11.5 (pointers to structs, unions) |
| 10–13 | 🔄 Fair | Re-read 11.1–11.3 (basics, declaring, nested) |
| < 10 | 🔁 Needs Review | Re-read full chapter |

---

*Next: [Chapter 12: File Input/Output →](../12-file-input-output/01-streams-in-c.md)*
