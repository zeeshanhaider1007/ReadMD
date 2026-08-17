# 12.2: Reading Text Files — Getting Data In

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Read text from a file using `fgets`, `fscanf`, and `fgetc`
- Process a file line by line
- Detect the end of a file using `feof`
- Choose the right reading function for different scenarios

---

## 🧭 The Big Picture

> A researcher's archive contains thousands of notes. When they need to review entries from a specific period, they open the log file and read through it — one entry at a time, line by line, until they reach the end.
>
> Reading a text file in C follows the same process: open the file, read data until you reach the end, then close it. The three main tools — `fgets`, `fscanf`, and `fgetc` — are like different ways of processing a document: by lines, by formatted fields, or by individual characters.

---

## 📚 Core Content

### Reading Line by Line: `fgets`

`fgets` reads one line at a time (up to and including the newline character):

```c
#include <stdio.h>

int main(void) {
    FILE *fp = fopen("journal.txt", "r");
    
    if (fp == NULL) {
        fprintf(stderr, "Error: Could not open file.\n");
        return 1;
    }
    
    char buffer[256];
    
    // Read the file line by line
    while (fgets(buffer, sizeof(buffer), fp) != NULL) {
        // fgets returns NULL when there's nothing more to read
        printf("%s", buffer);  // Print the line (already has \n)
    }
    
    fclose(fp);
    return 0;
}
```

**How `fgets` works:**
- Reads characters into `buffer` until:
  - A newline (`\n`) is found (included in the buffer)
  - `sizeof(buffer) - 1` characters have been read
  - End-of-file is reached
- Adds a null terminator (`\0`) after the last character
- Returns `NULL` if there's no more data (end of file or error)

**Sample input file `journal.txt`:**
```
TO: Paris
FROM: Ottawa
SUBJECT: Trade Mission
The delegation of 12 officials will arrive on March 15.
Accommodation has been arranged for the visiting professor.
```

**Output:**
```
TO: Paris
FROM: Ottawa
SUBJECT: Trade Mission
The delegation of 12 officials will arrive on March 15.
Accommodation has been arranged for the visiting professor.
```

### Reading Formatted Data: `fscanf`

`fscanf` reads formatted data from a file, just like `scanf` reads from the keyboard:

```c
#include <stdio.h>

int main(void) {
    FILE *fp = fopen("countries.txt", "r");
    
    if (fp == NULL) {
        fprintf(stderr, "Error: Could not open file.\n");
        return 1;
    }
    
    char country[50];
    char capital[50];
    int population;
    
    // Read formatted data — assumes specific format in file
    while (fscanf(fp, "%s %s %d", country, capital, &population) == 3) {
        printf("%s (capital: %s, pop: %d)\n", country, capital, population);
    }
    
    fclose(fp);
    return 0;
}
```

**Sample input `countries.txt`:**
```
Canada Ottawa 38000000
France Paris 67000000
Japan Tokyo 125000000
```

**Output:**
```
Canada (capital: Ottawa, pop: 38000000)
France (capital: Paris, pop: 67000000)
Japan (capital: Tokyo, pop: 125000000)
```

**Important:** `fscanf` stops at whitespace. Use `%[^\n]` to read a whole line, or use `fgets` for lines with spaces.

### Reading Character by Character: `fgetc`

`fgetc` reads one character at a time. Returns `EOF` (end-of-file) when there's nothing more to read:

```c
#include <stdio.h>

int main(void) {
    FILE *fp = fopen("message.txt", "r");
    
    if (fp == NULL) {
        fprintf(stderr, "Error: Could not open file.\n");
        return 1;
    }
    
    int ch;  // Must be int, not char, to hold EOF
    
    // Read one character at a time
    while ((ch = fgetc(fp)) != EOF) {
        putchar(ch);  // Print the character to the screen
    }
    
    fclose(fp);
    return 0;
}
```

**When to use each reading function:**

| Function | Best For | Reads | Returns |
|----------|----------|-------|---------|
| `fgets` | Line-by-line processing | One line (including `\n`) | Pointer to buffer, or `NULL` at EOF |
| `fscanf` | Formatted/structured data | Values matching format specifiers | Number of items matched, or `EOF` |
| `fgetc` | Character-by-character processing | One character | The character as `int`, or `EOF` |

### Detecting End of File

There are two ways to detect EOF:

**1. Check the return value of the read function:**
```c
while (fgets(buffer, sizeof(buffer), fp) != NULL) { ... }
while (fscanf(fp, "%d", &num) == 1) { ... }
while ((ch = fgetc(fp)) != EOF) { ... }
```

**2. Use `feof` to check after a read fails:**
```c
char buffer[256];
fgets(buffer, sizeof(buffer), fp);

if (feof(fp)) {
    printf("Reached end of file.\n");
} else if (ferror(fp)) {
    printf("Error reading file.\n");
}
```

> **Best practice:** Always check the return value of the read function. Don't use `feof` before reading — it only becomes true AFTER a read attempt hits the end.

### A Complete Example: Reading a Configuration File

```c
#include <stdio.h>
#include <string.h>

#define MAX_LINE 200

int main(void) {
    FILE *fp = fopen("config.txt", "r");
    
    if (fp == NULL) {
        fprintf(stderr, "Error: Could not open config.txt\n");
        return 1;
    }
    
    char line[MAX_LINE];
    int line_num = 0;
    
    printf("=== Configuration ===\n");
    
    while (fgets(line, sizeof(line), fp) != NULL) {
        line_num++;
        
        // Remove trailing newline (fgets includes it)
        size_t len = strlen(line);
        if (len > 0 && line[len - 1] == '\n') {
            line[len - 1] = '\0';
        }
        
        // Skip empty lines and comments
        if (line[0] == '#' || line[0] == '\0') {
            continue;
        }
        
        printf("  %s\n", line);
    }
    
    fclose(fp);
    printf("(%d lines processed)\n", line_num);
    
    return 0;
}
```

**Sample `config.txt`:**
```
# Server Configuration
server_name = Library Mail System
port = 8080
max_connections = 100
# Logging
log_level = INFO
```

---

## 🧪 Try It Yourself

> **Exercise 1: Read and Print a File**
> Create a text file called `poem.txt` with a short poem (4 lines). Write a program that opens and reads it using `fgets`, printing each line with its line number.

> **Exercise 2: Character Counter**
> Write a program that reads a file character by character using `fgetc` and counts the total number of characters (including spaces and newlines). Print the count.

> **Exercise 3: Formatted Data Reader**
> Create a file `grades.txt` with lines like: `Alice 85 92 78`. Write a program that reads each student's name and three grades, calculates the average, and prints it.

> **Exercise 4: CSV Parser**
> Create a file `cities.csv` with: `City,Country,Population`. Write a program that reads the CSV using `fgets` and `sscanf`, printing each city's data in a formatted table.

---

## 💡 Common Pitfalls

- ❌ **Using `feof` before a read attempt** — `feof` only becomes true AFTER a read hits the end. Don't use it to predict the end. Always check the read function's return value.

- ❌ **Not removing the trailing newline from `fgets`** — `fgets` includes the newline in the buffer. If you need to process the line without it, remove it with `buffer[strcspn(buffer, "\n")] = '\0';`.

- ❌ **Using `fscanf` when lines contain spaces** — `%s` stops at whitespace. For lines with spaces, use `fgets` instead.

- ❌ **Declaring the `fgetc` result as `char` instead of `int`** — `EOF` is typically -1, which doesn't fit in a `char`. Always use `int ch;` for `fgetc`.

---

## 🔗 Connections to What You Know

> **Reading a file is like reviewing your journal.**
>
> You have three ways to review entries: read the whole notebook in order (`fgets` — line by line), search for entries matching specific criteria (`fscanf` — formatted extraction), or inspect each character for hidden details (`fgetc` — character by character). Each method has its place.
>
> The end-of-file marker is like the last page in the notebook — when you've read it, you know there's nothing more to review. You don't ask "is there more?" before each read; you find out when the read returns nothing.

---

## ✅ Section Checklist

- [ ] I can read a text file line by line using `fgets`
- [ ] I can read formatted data using `fscanf`
- [ ] I can read character by character using `fgetc`
- [ ] I can detect end of file correctly
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [12.3: Writing Text Files →](./03-writing-text-files.md)*
