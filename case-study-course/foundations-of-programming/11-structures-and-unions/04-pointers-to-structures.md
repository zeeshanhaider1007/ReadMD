# 11.4: Pointers to Structures — Working with Structs Through Pointers

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Declare and use pointers to structures
- Use the arrow operator (`->`) to access struct fields through pointers
- Pass structs efficiently to functions using pointers
- Dynamically allocate structs on the heap

---

## 🧭 The Big Picture

> You don't carry an entire house with you when you visit a friend. You carry their address. When you need to visit, you follow the address. When you need to update something, you go to the address and make the change there.
>
> A **pointer to a structure** is that address. Instead of copying the entire struct every time you pass it to a function (imagine photocopying a 50-page application every time you reference it), you pass the address. The function follows the address and works with the original.

---

## 📚 Core Content

### Why Pointers to Structs?

Without pointers, passing a struct to a function copies everything:

```c
struct Student {
    int id;
    char name[100];
    int year;
    double fee;
    int is_enrolled;
    char notes[5000];  // Large array!
};

// This COPIES 5000+ bytes every time you call it
void print_student(struct Student s) {
    printf("%s (ID %d, %d)\n", s.name, s.id, s.year);
}

int main(void) {
    struct Student s1 = {1, "Maya Patel", 2025, 8000.0, 1, {0}};
    print_student(s1);  // Copies ~5KB of data — wasteful!
    return 0;
}
```

With a pointer, you pass just the address (8 bytes):

```c
// This only passes 8 bytes (the address)
void print_student(const struct Student *s) {
    printf("%s (ID %d, %d)\n", s->name, s->id, s->year);
}
```

### Declaring Pointers to Structs

```c
struct Student s1 = {1, "Maya Patel", 2025, 8000.0, 1, {0}};
struct Student *ptr;

ptr = &s1;  // ptr now holds the address of s1
```

### The Arrow Operator (`->`)

When you have a pointer to a struct, you COULD use the dereference-and-dot pattern:

```c
struct Student *ptr = &s1;

// Dereference first, then access field
(*ptr).id = 2;  // (*ptr) gets the struct, . gets the field
```

But C provides a cleaner syntax: the **arrow operator** `->`:

```c
ptr->id = 2;     // Same as (*ptr).id = 2
ptr->year = 2026;     // Same as (*ptr).year = 2026
```

The arrow operator combines dereference (`*`) and field access (`.`) into one step: `ptr->field` means "follow ptr to the struct, then get the field."

### Passing Structs to Functions (Efficiently)

```c
#include <stdio.h>
#include <string.h>

struct Student {
    int id;
    char name[100];
    int year;
    double fee;
    int is_enrolled;
};

// Read-only access — use const for safety
void print_student(const struct Student *s) {
    printf("ID %d: %s (%d)\n", 
           s->id,     // Arrow operator with const pointer
           s->name, 
           s->year);
    printf("  Fee: $%.2f\n", s->fee);
    printf("  Status: %s\n", s->is_enrolled ? "Enrolled" : "Pending");
    
    // s->is_enrolled = 1;  // ❌ Compiler error — const prevents modification
}

// Read-write access — can modify through pointer
void enroll_student(struct Student *s) {
    s->is_enrolled = 1;  // ✅ Modifies the original!
}

void add_fee(struct Student *s, double additional_fee) {
    s->fee += additional_fee;
}

int main(void) {
    struct Student s1 = {1, "Maya Patel", 2025, 5000.0, 0};
    
    print_student(&s1);      // Pass address — no copying
    
    enroll_student(&s1);     // Pass address — modifies original
    add_fee(&s1, 2000.0);  // Pass address — modifies original
    
    print_student(&s1);      // Now enrolled with updated fee
    
    return 0;
}
```

### Dynamic Allocation of Structs

Structs can be allocated on the heap using `malloc`:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Student {
    int id;
    char name[100];
    int year;
    double fee;
    int is_enrolled;
};

int main(void) {
    // Allocate a struct on the heap
    struct Student *s = malloc(sizeof(struct Student));
    if (s == NULL) {
        fprintf(stderr, "Memory allocation failed!\n");
        return 1;
    }
    
    // Access fields through pointer (arrow operator)
    s->id = 1;
    strcpy(s->name, "Maya Patel");
    s->year = 2025;
    s->fee = 3000.0;
    s->is_enrolled = 0;
    
    printf("Created: %s (ID %d)\n", s->name, s->id);
    
    // Must free heap-allocated structs!
    free(s);
    s = NULL;
    
    return 0;
}
```

### Arrays of Struct Pointers

A common pattern is an array of pointers to structs:

```c
struct Student *students[100];  // Array of 100 pointers
                              // Each element is 8 bytes (pointer)
                              // Total: 800 bytes vs. 500KB for full structs!

// Allocate each student individually
for (int i = 0; i < 3; i++) {
    students[i] = malloc(sizeof(struct Student));
    if (students[i] != NULL) {
        students[i]->id = i + 1;
        students[i]->year = 2025;
        students[i]->is_enrolled = 0;
    }
}

// Access through the array
printf("ID %d\n", students[0]->id);

// Free each one
for (int i = 0; i < 3; i++) {
    free(students[i]);
    students[i] = NULL;
}
```

### Returning Structs from Functions

You can return a struct from a function (by value):

```c
struct Student create_student(int id, const char *name, int year) {
    struct Student s;
    s.id = id;
    strcpy(s.name, name);
    s.year = year;
    s.fee = 0.0;
    s.is_enrolled = 0;
    return s;  // Returns a COPY of the struct
}

int main(void) {
    struct Student s1 = create_student(1, "Maya Patel", 2025);
    print_student(&s1);
    return 0;
}
```

Or return a heap-allocated struct via pointer:

```c
struct Student *create_student_ptr(int id, const char *name, int year) {
    struct Student *s = malloc(sizeof(struct Student));
    if (s != NULL) {
        s->id = id;
        strcpy(s->name, name);
        s->year = year;
        s->fee = 0.0;
        s->is_enrolled = 0;
    }
    return s;  // Caller must free!
}

int main(void) {
    struct Student *s1 = create_student_ptr(1, "Maya Patel", 2025);
    if (s1 != NULL) {
        print_student(s1);
        free(s1);
        s1 = NULL;
    }
    return 0;
}
```

---

## 🧪 Try It Yourself

> **Exercise 1: Arrow Operator Basics**
> Define `struct Point { int x; int y; };`. Create a Point variable and a pointer to it. Set the coordinates through the pointer using `->`. Print using both the variable and the pointer.

> **Exercise 2: Pass by Pointer**
> Write a function `void scale_point(struct Point *p, int factor)` that multiplies both `x` and `y` by factor. Call it and verify the original changed.

> **Exercise 3: Dynamic Struct Array**
> Allocate an array of 5 `struct Student` on the heap using `malloc`. Fill them with data. Print them. Free them.

> **Exercise 4: Factory Function**
> Write a function that creates and returns a dynamically allocated struct (such as a student or employee record). Document clearly that the caller must free it.

---

## 💡 Common Pitfalls

- ❌ **Using `.` instead of `->` with a pointer** — `ptr.field` is wrong when `ptr` is a pointer. The compiler will complain. Use `ptr->field` or `(*ptr).field`.

- ❌ **Forgetting to dereference with arrow** — `ptr->field` is correct. `*ptr.field` tries to dereference the result of `ptr.field`, which won't work.

- ❌ **Not checking `malloc` return value** — Always check if `malloc` returned `NULL` before using the pointer.

- ❌ **Forgetting to `free` heap-allocated structs** — Every `malloc` needs a matching `free`. Use Valgrind to check for leaks.

- ❌ **Dangling pointer after free** — After `free(ptr);`, set `ptr = NULL;` so you don't accidentally use the freed memory.

---

## 🔗 Connections to What You Know

> **A pointer to a struct is like a document reference number in an office.**
>
> When you need to reference a file, you don't mail 50 photocopies to everyone — you send the file's reference number. Recipients look up the original in the archive. The reference number is small (like a pointer), but it gives access to the entire document.
>
> The arrow operator `->` is like saying \"open the file with this reference number and look at the field named...\" It's faster, uses less resources, and if you update the original, everyone with the reference number sees the update.

---

## ✅ Section Checklist

- [ ] I can declare pointers to structs
- [ ] I use `->` to access struct fields through pointers
- [ ] I pass structs efficiently to functions using pointers
- [ ] I can allocate and free structs on the heap
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [11.5: Unions →](./05-unions.md)*
