# 8.5: String Functions — Working with Text

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Use `strlen` to find string length
- Use `strcpy` and `strncpy` to copy strings safely
- Use `strcmp` to compare strings
- Use `strcat` to concatenate strings
- Avoid common string function pitfalls

---

## 🧭 The Big Picture

> Anyone working with text does four basic operations: measure the length of a document, make a copy, compare two versions, and combine paragraphs. These operations are so common that C provides ready-made functions for them in the `<string.h>` header.
>
> You've been using `printf` and `scanf` without knowing how they work internally. The string functions are the same — standard tools that every C programmer uses daily. Learning them saves you from writing buggy versions yourself.

---

## 📚 Core Content

### Header Required

```c
#include <string.h>   // All string functions live here
```

### `strlen` — String Length

Returns the number of characters BEFORE the null terminator. Remember that every C string is really an array of characters ending with `\0`:

![String as Char Array](../assets/ch08/string-as-char-array.svg)

```c
char word[] = "Diplomacy";
int len = strlen(word);       // 9 (not counting \0)
int size = sizeof(word);      // 10 (9 chars + \0)

printf("Length: %d, Size: %d\n", len, size);
```

```c
char word[] = "Diplomacy";
int len = strlen(word);       // 9 (not counting \0)
int size = sizeof(word);      // 10 (9 chars + \0)

printf("Length: %d, Size: %d\n", len, size);
```

### `strcpy` — String Copy

Copies a string from source to destination (including `\0`):

```c
char source[] = "Hello";
char dest[20];

strcpy(dest, source);   // Copies "Hello\0" into dest
printf("%s\n", dest);   // "Hello"
```

**⚠️ `strcpy` is dangerous** — it doesn't check that the destination is large enough:

```c
char small[5];
char large[] = "This is a very long string";
strcpy(small, large);   // ⚠️ BUFFER OVERFLOW! Writes past the end of small!
```

**Safe alternative: `strncpy`**

```c
char dest[10];
strncpy(dest, source, sizeof(dest) - 1);  // Copy at most 9 chars
dest[sizeof(dest) - 1] = '\0';            // Ensure null termination!
```

### `strcmp` — String Compare

Compares two strings character by character. Returns:
- **0** if they're equal
- **Negative** if the first differing character in s1 < s2
- **Positive** if the first differing character in s1 > s2

```c
char pass[] = "secret";

if (strcmp(user_input, pass) == 0) {
    printf("Access granted\n");
} else {
    printf("Access denied\n");
}
```

**⚠️ Don't use `==` to compare strings:** This compares pointers (memory addresses), not the actual characters:

```c
char a[] = "Hello";
char b[] = "Hello";

if (a == b) {           // ❌ WRONG! Compares ADDRESSES, not strings!
    printf("Equal\n");  // This probably won't print
}

if (strcmp(a, b) == 0) { // ✅ Correct! Compares the actual text
    printf("Equal\n");
}
```

### `strcat` — String Concatenation

Appends one string to the end of another:

```c
char greeting[50] = "Hello, ";
strcat(greeting, "Dr. ");
strcat(greeting, "Smith");
printf("%s\n", greeting);  // "Hello, Dr. Smith"
```

**⚠️ Same danger as `strcpy`** — make sure the destination has enough space.

### Putting It All Together

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    char country[50];
    char capital[50];
    char result[100];
    
    printf("Enter a country: ");
    fgets(country, sizeof(country), stdin);
    country[strcspn(country, "\n")] = '\0';  // Remove newline
    
    printf("Enter its capital: ");
    fgets(capital, sizeof(capital), stdin);
    capital[strcspn(capital, "\n")] = '\0';  // Remove newline
    
    // Build the result string
    strcpy(result, "The capital of ");
    strcat(result, country);
    strcat(result, " is ");
    strcat(result, capital);
    strcat(result, ".");
    
    printf("%s\n", result);
    printf("Length: %zu\n", strlen(result));
    
    return 0;
}
```

### Common String Functions Reference

| Function | What It Does | Watch Out For |
|----------|-------------|---------------|
| `strlen(s)` | Returns length of s | O(n) — counts characters |
| `strcpy(d, s)` | Copies s into d | Buffer overflow if d is too small |
| `strncpy(d, s, n)` | Copies at most n chars | May not null-terminate! |
| `strcmp(a, b)` | Compares a and b | Returns 0 if EQUAL |
| `strcat(d, s)` | Appends s to end of d | Buffer overflow |
| `strncat(d, s, n)` | Appends at most n chars | Safer, but check size |
| `strstr(text, key)` | Finds key in text | Returns pointer or NULL |
| `strchr(s, c)` | Finds first c in s | Returns pointer or NULL |

---

## 🧪 Try It Yourself

> **Exercise 1: Password Check**
> Write a program that reads a password and uses `strcmp` to check if it matches "opensesame".

> **Exercise 2: String Builder**
> Write a program that reads a first name and last name, then uses `strcpy` and `strcat` to build a full greeting: "Hello, [First] [Last]!"

> **Exercise 3: Compare with ==**
> Write a program where you compare two different char arrays containing "Yes" using `==` and using `strcmp`. Print the results. Why are they different?

> **Exercise 4: Buffer Overflow Experiment**
> Intentionally copy a long string into a small buffer using `strcpy`. Observe the output. Then fix it with `strncpy`.

---

## 💡 Common Pitfalls

- ❌ **Using `==` to compare strings** — This compares POINTERS, not the actual string content. Always use `strcmp`.
- ❌ **Buffer overflow with `strcpy` and `strcat`** — These functions don't check destination size. Use `strncpy` and `strncat` for safety.
- ❌ **Forgetting `strncpy` doesn't always null-terminate** — If the source is >= n chars, `strncpy` doesn't add `\0`. Always set the last byte manually.
- ❌ **Using `gets`** — Never use `gets()`. It has no bounds checking. Use `fgets` instead.

---

## 🔗 Connections to What You Know

> **String functions are like document processing tools.**
>
> `strcpy` is a photocopier — it makes an exact copy. `strcmp` is a document checker — it checks if two documents are identical. `strcat` is a document binder — it combines two documents into one. `strlen` is a word counter — it tells you how long the document is.
>
> Each tool has a specific purpose, and using the wrong one (like comparing strings with `==`) is like asking the word counter to compare two documents.

---

## ✅ Section Checklist

- [ ] I can use `strlen`, `strcpy`, `strcmp`, and `strcat` correctly
- [ ] I understand why `==` doesn't work for string comparison
- [ ] I use `strncpy` and `strncat` for safe string copying
- [ ] I always ensure destination buffers are large enough
- [ ] I wrote a **journal entry** about what I learned today

---

*→ You've completed Chapter 8! Test your knowledge with the [Chapter 8 Quiz →](./chapter-quiz.md)*
