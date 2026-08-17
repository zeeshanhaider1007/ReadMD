# 9.5: Pointers and Arrays — The Intimate Relationship

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Explain why arrays and pointers are closely related in C
- Use the array name as a pointer to the first element
- Pass arrays to functions using pointer parameters
- Distinguish between `arr` and `&arr[0]`

---

## 🧭 The Big Picture

> An office directory lists all the rooms in a building. The directory itself isn't the rooms — it's a reference that tells you where each room is located. The name of the directory ("Room List") points to the first room listed.
>
> In C, an array name works the same way. The name `arr` doesn't represent the whole array — it's a pointer to the first element, `arr[0]`. This is why you can use pointer syntax to access array elements and array syntax to access pointed-to data.

---

## 📚 Core Content

### The Array Name Is a Pointer

```c
int arr[5] = {10, 20, 30, 40, 50};

// These all print the SAME address:
printf("%p\n", arr);      // Address of first element
printf("%p\n", &arr[0]);  // Same address
printf("%p\n", &arr);     // Same address (different type, but same value)
```

The array name `arr` automatically **decays** to a pointer to its first element in most contexts.

### Array Subscript Is Pointer Arithmetic

```c
arr[i] is equivalent to *(arr + i)
```

This is the fundamental truth of C arrays. Every time you write `arr[i]`, the compiler translates it to `*(arr + i)`:

```c
int arr[5] = {10, 20, 30, 40, 50};

// These are IDENTICAL:
int a = arr[2];       // 30 — array subscript notation
int b = *(arr + 2);   // 30 — pointer arithmetic notation

// These are also IDENTICAL:
arr[0] = 99;          // Set first element
*arr = 99;            // Same thing
```

### Passing Arrays to Functions

When you pass an array to a function, you're actually passing a pointer. This is why the function can modify the original array:

```c
#include <stdio.h>

// These three function signatures are IDENTICAL:
void print_1(int arr[], int size);
void print_2(int *arr, int size);
void print_3(int arr[10], int size);  // The 10 is ignored!

// Inside the function, sizeof(arr) gives pointer size, not array size!
// This is why you MUST pass the size separately.

void double_all(int *arr, int size) {
    for (int i = 0; i < size; i++) {
        arr[i] *= 2;     // arr[i] is equivalent to *(arr + i)
    }
}

int main(void) {
    int values[] = {1, 2, 3, 4, 5};
    int count = sizeof(values) / sizeof(values[0]);
    
    double_all(values, count);  // Passes pointer to first element
    
    for (int i = 0; i < count; i++) {
        printf("%d ", values[i]);  // 2 4 6 8 10
    }
    printf("\n");
    
    return 0;
}
```

### Modifying Arrays Through Pointers

Since you're passing a pointer, the function can directly modify the original array:

```c
void set_first_to_zero(int *arr) {
    arr[0] = 0;   // Modifies the original array!
    // or equivalently:
    *arr = 0;
}

void set_all_to_zero(int *arr, int size) {
    for (int i = 0; i < size; i++) {
        *(arr + i) = 0;  // Pointer arithmetic
    }
}
```

### The Array/Pointer Equivalence

```c
int arr[5] = {10, 20, 30, 40, 50};
int *p = arr;   // p now points to the same memory as arr

// All of these are equivalent:
arr[2] = 100;
p[2] = 100;      // Pointer with array subscript — valid!
*(arr + 2) = 100;
*(p + 2) = 100;
```

### One Key Difference: `sizeof`

```c
int arr[5] = {1, 2, 3, 4, 5};
int *p = arr;

printf("%zu\n", sizeof(arr));  // 20 (5 ints × 4 bytes each)
printf("%zu\n", sizeof(p));    // 8 (size of a pointer, 64-bit)
```

`sizeof(arr)` gives the total array size because the compiler knows `arr` is an array. `sizeof(p)` gives the pointer size because `p` is just a pointer.

---

## 🧪 Try It Yourself

> **Exercise 1: Array Name as Pointer**
> Declare `int nums[5] = {10, 20, 30, 40, 50};` and print `nums`, `&nums[0]`, and `nums + 1`. What do you observe?

> **Exercise 2: Array and Pointer Equivalence**
> Declare `int data[3] = {100, 200, 300};` and `int *p = data;`. Use `p[1]` to change the second element to 999 and verify using `data[1]`.

> **Exercise 3: Function with Array Parameter**
> Write a function `int sum_array(int *arr, int size)` that returns the sum of all elements using pointer arithmetic (`*(arr + i)`). Test it.

> **Exercise 4: `sizeof` Demonstration**
> Inside `main`, declare an array and a pointer. Print `sizeof(arr)` and `sizeof(ptr)`. Then pass the array to a function and print `sizeof(arr)` inside the function. Why are they different?

---

## 💡 Common Pitfalls

- ❌ **Using `sizeof(arr)` inside a function** — Inside a function parameter, `int arr[]` decays to `int *arr`, and `sizeof` gives the pointer size (8), not the array size. Always pass the size explicitly.
- ❌ **Forgetting that `arr` decays to a pointer** — When you pass an array, you're giving the function direct access to the original data. The function can modify it.
- ❌ **Confusing `arr` and `&arr`** — Both give the same address value, but `&arr` has type `int (*)[5]` (pointer to array of 5 ints), while `arr` is `int *`. The difference rarely matters, but it exists.

---

## 🔗 Connections to What You Know

> **An array name is like the title of a file folder.**
>
> If you have a folder labeled "Receipts 2024," the title points to the first receipt in the folder. You don't say "Receipts 2024, document number 0" — you just open the folder and start with the first receipt. That's `arr[0]` — short for `*(arr + 0)`.
>
> When you lend the folder to a colleague, you hand them the folder itself. That's the pointer. They can access any receipt by counting from the first one.

---

## ✅ Section Checklist

- [ ] I understand that an array name decays to a pointer to its first element
- [ ] I know that `arr[i]` is equivalent to `*(arr + i)`
- [ ] I can pass arrays to functions and modify them through pointers
- [ ] I know why `sizeof` behaves differently for arrays vs. pointers
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [9.6: Pointer Arithmetic →](./06-pointer-arithmetic.md)*
