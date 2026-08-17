# 10.3: `calloc` and `realloc` — Allocation Variants

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Use `calloc` to allocate zero-initialized memory
- Use `realloc` to resize an existing allocation
- Choose the right allocation function for each situation

---

## 🧭 The Big Picture

> `malloc` is like requesting a blank container — it might have old residue from the previous cargo. `calloc` is like requesting a pre-cleaned container — guaranteed spotless. `realloc` is like asking to enlarge or shrink your container after you've already started packing.

---

## 📚 Core Content

### `calloc` — Allocate and Zero-Initialize

```c
void *calloc(size_t count, size_t size);
```

`calloc` allocates memory AND sets every byte to zero:

```c
int *arr = calloc(10, sizeof(int));  // All 10 ints are initialized to 0

if (arr == NULL) {
    fprintf(stderr, "Allocation failed!\n");
    return 1;
}

// arr[0] through arr[9] are ALL 0 — no garbage values!
free(arr);
```

**`malloc` vs. `calloc`:**
| Feature | `malloc` | `calloc` |
|---------|----------|----------|
| Parameters | `(size)` — total bytes | `(count, size)` — two args |
| Initialization | Uninitialized (garbage) | Zero-initialized |
| Use case | When you'll set all values anyway | When you need clean memory |

```c
int *a = malloc(10 * sizeof(int));   // Contains garbage
int *b = calloc(10, sizeof(int));    // All zeros
```

### `realloc` — Resize an Existing Allocation

```c
void *realloc(void *ptr, size_t new_size);
```

`realloc` changes the size of a previously allocated block:

```c
int *arr = malloc(5 * sizeof(int));   // Initial: 5 elements
if (arr == NULL) return 1;

// ... fill arr[0] through arr[4] ...

// Now we need 10 elements
int *temp = realloc(arr, 10 * sizeof(int));
if (temp == NULL) {
    // realloc failed! Original block is still valid
    free(arr);
    return 1;
}
arr = temp;  // Point to the (possibly new) block

arr[5] = 50; // Now safe — space for 10 elements
// ...
free(arr);
```

### How `realloc` Works

1. If the existing block can be **expanded in place**, it does so — fast!
2. If not, it **allocates a new block**, copies the old data, and frees the old block
3. If it fails, it returns `NULL` and the **original block is still valid**

### Reallocation Strategy: Growing a Dynamic Array

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int capacity = 4;
    int *arr = malloc(capacity * sizeof(int));
    if (arr == NULL) return 1;
    
    int count = 0;  // How many elements actually used
    
    // Simulate reading unknown number of values
    int values[] = {10, 20, 30, 40, 50, 60};
    int num_values = 6;
    
    for (int i = 0; i < num_values; i++) {
        // Do we need more space?
        if (count >= capacity) {
            capacity *= 2;  // Double the capacity
            int *temp = realloc(arr, capacity * sizeof(int));
            if (temp == NULL) {
                free(arr);
                return 1;
            }
            arr = temp;
            printf("Resized to capacity %d\n", capacity);
        }
        arr[count++] = values[i];
    }
    
    for (int i = 0; i < count; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    free(arr);
    return 0;
}
```

**Output:**
```
Resized to capacity 8
10 20 30 40 50 60
```

### Choosing the Right Allocation Function

| Situation | Use |
|-----------|-----|
| Need uninitialized memory | `malloc` |
| Need zeroed memory | `calloc` |
| Need to resize existing block | `realloc` |
| Array of structs (want clean state) | `calloc` |
| Growing buffer for user input | `realloc` (doubling strategy) |

---

## 🧪 Try It Yourself

> **Exercise 1: `calloc` vs. `malloc`**
> Allocate 10 ints with `malloc`, print their values. Then allocate 10 ints with `calloc`, print their values. What's the difference?

> **Exercise 2: Growing Array**
> Start with an array of 2 `double`s using `malloc`. Use `realloc` to grow it to hold 8 values. Fill and print all values.

> **Exercise 3: Shrinking**
> Allocate 100 ints, then use `realloc` to shrink to 10 ints. (The extra 90 are lost.) Is this useful? When?

> **Exercise 4: `realloc` with `NULL`**
> What happens if you pass `NULL` to `realloc`? Try it: `realloc(NULL, 100)`. It's equivalent to which function?

---

## 💡 Common Pitfalls

- ❌ **Not using a temporary pointer with `realloc`** — If `realloc` fails, it returns `NULL` and you lose your original pointer. Always use a temp.
- ❌ **Assuming `realloc` preserves the pointer** — It might move the data to a new location. Always use the returned pointer.
- ❌ **Using `calloc` when speed matters** — Zeroing memory takes time. If you're overwriting all values anyway, use `malloc`.

---

## 🔗 Connections to What You Know

> **`realloc` is like a team that outgrows its office.**
>
> You start with a small team in a small office. As the team grows, you need a bigger office. Sometimes the office next door is available and you just knock through the wall (expand in place). Sometimes you need to move to a completely new building (new allocation, copy, free old).
>
> `calloc` is like a freshly built apartment — every room is empty and clean, ready for you to furnish.

---

## ✅ Section Checklist

- [ ] I can use `calloc` for zero-initialized allocations
- [ ] I can use `realloc` to resize allocations
- [ ] I always use a temporary pointer with `realloc`
- [ ] I know when to choose each allocation function
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [10.4: Memory Leaks →](./04-memory-leaks.md)*
