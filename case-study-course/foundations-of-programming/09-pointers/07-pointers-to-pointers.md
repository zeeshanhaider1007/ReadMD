# 9.7: Pointers to Pointers — The Chain of Addresses

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Declare and use a pointer to a pointer (`int **p`)
- Understand when double indirection is needed
- Use `**` to access the value at the end of a pointer chain

---

## 🧭 The Big Picture

> In diplomacy, you might have a filing cabinet that contains a folder, which contains another folder, which contains the actual document. To reach the document, you open the cabinet, then the first folder, then the second folder.
>
> A **pointer to a pointer** is exactly this: a variable that stores the address of another pointer, which in turn stores the address of the actual data. You follow the chain twice to reach the value.

---

## 📚 Core Content

### Declaring a Pointer to a Pointer

```c
int x = 42;
int *p = &x;     // p stores the address of x
int **pp = &p;   // pp stores the address of p (which points to x)
```

Visual representation:
```
pp  →  p  →  x
(holds   (holds   (holds
 &p)      &x)      42)
```

### Following the Chain

```c
int x = 42;
int *p = &x;
int **pp = &p;

printf("%d\n", x);    // 42 — direct access
printf("%d\n", *p);   // 42 — follow p once
printf("%d\n", **pp); // 42 — follow pp, then p
```

- `pp` gives the address of `p`
- `*pp` gives the address of `x` (same as `p`)
- `**pp` gives the value of `x` (same as `*p`)

### Changing Through Double Indirection

```c
int x = 42;
int *p = &x;
int **pp = &p;

**pp = 100;  // Changes x to 100!

printf("%d\n", x);    // 100
```

### Why Double Pointers Matter

The most common use case: when a function needs to modify a pointer itself (not just the thing it points to).

Consider: you want a function that allocates memory and gives the pointer back to the caller:

```c
// ❌ WRONG: Can't modify the pointer itself
void allocate_bad(int *ptr, int size) {
    ptr = malloc(size * sizeof(int));  // Only modifies the LOCAL copy
}

// ✅ CORRECT: Use a pointer to the pointer
void allocate_good(int **ptr, int size) {
    *ptr = malloc(size * sizeof(int));  // Modifies the ORIGINAL pointer
}

int main(void) {
    int *arr = NULL;
    allocate_good(&arr, 10);  // Pass the ADDRESS of the pointer
    
    // Now arr points to allocated memory!
    arr[0] = 42;
    printf("%d\n", arr[0]);  // 42
    
    free(arr);
    return 0;
}
```

### Common Use Cases for `**`

1. **Modifying a pointer from a function** (as above)
2. **2D arrays passed to functions** — `int **matrix`
3. **Arrays of strings** — `char **argv` (command-line arguments)
4. **Linked lists** — modifying the head pointer

### Arrays of Strings (Common in C)

```c
char *countries[] = {
    "Switzerland",
    "France",
    "Germany",
    NULL  // Sentinel to mark the end
};

// countries is an array of char* pointers
// It decays to char** when passed to a function
void print_countries(char **list) {
    for (int i = 0; list[i] != NULL; i++) {
        printf("%s\n", list[i]);
    }
}

int main(void) {
    print_countries(countries);
    return 0;
}
```

### Command-Line Arguments

```c
int main(int argc, char **argv) {
    // argv is a pointer to an array of strings
    for (int i = 0; i < argc; i++) {
        printf("Argument %d: %s\n", i, argv[i]);
    }
    return 0;
}
```

`char **argv` can also be written as `char *argv[]`. They're the same thing.

---

## 🧪 Try It Yourself

> **Exercise 1: Simple Double Pointer**
> Declare `int x = 5`, `int *p = &x`, `int **pp = &p`. Print `x` using `*p` and `**pp`. Then change `x` to 10 using `**pp`.

> **Exercise 2: Modify a Pointer**
> Write a function `void make_null(int **ptr)` that sets the original pointer to `NULL`. Test it by passing `&p` and then checking if `p` is `NULL`.

> **Exercise 3: Triple Pointer (Fun)**
> Declare `int x = 7;`, then `int *p = &x;`, `int **pp = &p;`, `int ***ppp = &pp;`. Print x using `***ppp`. Understand the chain.

> **Exercise 4: Array of Strings**
> Create a `char *names[]` array with 4 names. Write a function that prints all names using `char **` as the parameter.

---

## 💡 Common Pitfalls

- ❌ **Too many levels of indirection** — Double pointers are common. Triple or quadruple pointers are rare and usually indicate a design problem.
- ❌ **Forgetting to dereference the first level** — `*ptr = malloc(...)` vs. `ptr = malloc(...)` when the parameter is `int **ptr`.
- ❌ **Confusing `*pp` with `**pp`** — One gives the intermediate pointer, the other gives the final value.

---

## 🔗 Connections to What You Know

> **Double pointers are like a filing system with two levels of lookup.**
>
> The room list (first pointer) tells you which shelf contains your documents. The shelf index (second pointer) tells you which folder has the specific paper. You go to the room, then the shelf, then read the paper.
>
> When you need to reorganize — move the paper to a different folder — you don't change the paper itself. You update the folder reference. This is what `*ptr = new_pointer` does through a double pointer: it changes the pointer, not the pointed-to data.

---

## ✅ Section Checklist

- [ ] I can declare and use pointers to pointers (`int **pp`)
- [ ] I understand when double indirection is needed
- [ ] I can modify a pointer from within a function using `**`
- [ ] I understand `char **argv` and arrays of strings
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [9.8: Function Pointers →](./08-function-pointers.md)*
