# 📝 Chapter 12 Quiz — File Input/Output

---

**Chapter:** 12 — File Input/Output
**Total Questions:** 20
**Estimated Time:** 30–40 minutes

---

## Section 1: Multiple Choice

**1. What does `fopen("data.txt", "r")` return if the file doesn't exist?**

a) An empty `FILE *` pointer
b) `NULL`
c) `EOF`
d) It creates the file and returns a valid pointer

**2. Which function reads a single character from a file?**

a) `fgets`
b) `fscanf`
c) `fgetc`
d) `fread`

**3. What does `"w"` mode do when opening a file that already exists?**

a) Appends data to the end of the file
b) Opens the file for reading only
c) Overwrites the file completely
d) Returns an error because the file already exists

**4. Which mode should you use to add data to the end of an existing file without destroying its contents?**

a) `"r"`
b) `"w"`
c) `"a"`
d) `"r+"`

**5. What does `fgets` return when it reaches the end of a file?**

a) `EOF`
b) `0`
c) `NULL`
d) An empty string `""`

**6. Which function is best for writing formatted data (with variables) to a file?**

a) `fputs`
b) `fputc`
c) `fprintf`
d) `fwrite`

**7. What does `perror("open failed")` do?**

a) Exits the program with an error code
b) Prints "open failed: [system error message]"
c) Returns the error code as an integer
d) Clears the error flag on the file stream

**8. What is the main advantage of binary files over text files for numeric data?**

a) Binary files can be read in any text editor
b) Binary files are human-readable
c) Binary files are more compact and preserve exact values
d) Binary files don't need to be closed

---

## Section 2: Short Answer

**9. Explain the difference between `feof(fp)` and `ferror(fp)`. When should you use each?**

*Your answer:*

**10. Why must you always check if `fopen` returned `NULL` before using the returned `FILE *` pointer?**

*Your answer:*

**11. Why can't you use `fwrite` to save a struct that contains pointers (e.g., `char *name` instead of `char name[50]`)?**

*Your answer:*

---

## Section 3: Fill in the Blank

**12.** The three standard streams are `stdin`, `stdout`, and ________.

**13.** The function that writes a string to a file without formatting is ________.

**14.** Binary mode is specified by adding ________ to the mode string.

**15.** A file opened with `"w"` mode will be ________ if it already exists.

**16.** The function that prints a descriptive error message is ________.

---

## Section 4: Matching

**17. Match each file mode to its correct behavior:**

| Mode | Behavior |
|------|----------|
| 1. `"r"` | a) Opens for reading and writing (file must exist) |
| 2. `"w"` | b) Opens for appending (creates if needed) |
| 3. `"a"` | c) Opens for reading (file must exist) |
| 4. `"r+"` | d) Opens for writing (creates or overwrites) |

**18. Match each function to its purpose:**

| Function | Purpose |
|----------|---------|
| 1. `fprintf` | a) Read raw bytes from a binary file |
| 2. `fgets` | b) Write formatted output to a file |
| 3. `fread` | c) Read a line of text from a file |
| 4. `fwrite` | d) Write raw bytes to a binary file |

---

## Section 5: Practical Application

**19. Find and fix the errors in this program:**

```c
#include <stdio.h>

int main(void) {
    FILE *fp;
    
    // Error 1: Opening for reading without checking
    fp = fopen("data.txt", "r");
    fprintf(fp, "Hello, file!\n");
    
    // Error 2: Incorrect mode — overwrites instead of appends
    fp = fopen("log.txt", "w");
    fprintf(fp, "Log entry\n");
    
    // Error 3: No fclose!
    
    // Error 4: fgetc return type
    char ch;
    fp = fopen("data.txt", "r");
    while ((ch = fgetc(fp)) != EOF) {
        putchar(ch);
    }
    fclose(fp);
    
    // Error 5: fgets buffer (if file has lines longer than this)
    char small[5];
    fp = fopen("data.txt", "r");
    while (fgets(small, sizeof(small), fp) != NULL) {
        printf("%s", small);
    }
    fclose(fp);
    
    return 0;
}
```

**20. Write a complete C program that:**

- Defines a struct `struct Student` with fields: `int id, char name[50], double gpa`
- Creates an array of 3 students with sample data
- Opens a binary file `students.bin` with `"wb"` mode
- Writes the array to the file using `fwrite` (check return value!)
- Closes the file
- Opens the same file with `"rb"` mode
- Reads the data back into a different array using `fread`
- Prints the loaded data to verify it matches
- Handles all errors gracefully (file open failure, read/write failure) using `perror`

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **b) `NULL`** — `fopen` returns `NULL` on failure. *(Section 12.1)*
2. **c) `fgetc`** — Returns one character as an `int`, or `EOF` at end. *(Section 12.2)*
3. **c) Overwrites the file completely** — `"w"` destroys existing content. *(Section 12.1)*
4. **c) `"a"`** — Append mode adds data to the end without overwriting. *(Section 12.1)*
5. **c) `NULL`** — `fgets` returns `NULL` at end of file or on error. *(Section 12.2)*
6. **c) `fprintf`** — Supports format specifiers like `printf`. *(Section 12.3)*
7. **b) Prints "open failed: [system error message]"** — `perror` combines a custom message with the system's description. *(Section 12.5)*
8. **c) Binary files are more compact and preserve exact values** — No conversion to text strings. *(Section 12.4)*

### Section 2: Short Answer

9. **Model answer:** `feof(fp)` returns non-zero if the end of the file has been reached (normal condition). `ferror(fp)` returns non-zero if an actual I/O error occurred (abnormal). Use `feof` to detect normal end-of-file. Use `ferror` to detect read/write errors. After a read function returns `NULL` or fewer items than requested, check both to determine WHY. *(Section 12.5)*

10. **Model answer:** If `fopen` fails (returns `NULL`) and you try to use the pointer, your program will crash with a segmentation fault (dereferencing NULL). Always check immediately: `if (fp == NULL) { /* handle error */ }`. *(Section 12.1)*

11. **Model answer:** `fwrite` writes the raw bytes of the pointer variable (the memory address), not the data it points to. When you read the struct back, the pointer will contain a stale address that no longer points to valid memory. Only non-pointer data (fixed-size arrays, scalars, nested structs without pointers) survives binary save/load correctly. *(Section 12.4)*

### Section 3: Fill in the Blank

12. **`stderr`** — Standard error stream. *(Section 12.1)*
13. **`fputs`** — Writes a string without format conversion. *(Section 12.3)*
14. **`"b"`** — `"rb"`, `"wb"`, `"ab"` for binary access. *(Section 12.4)*
15. **overwritten** (or **destroyed**) — Existing content is lost. *(Section 12.1)*
16. **`perror`** — Combines custom message with system error description. *(Section 12.5)*

### Section 4: Matching

17. **1 → c, 2 → d, 3 → b, 4 → a** *(Section 12.1)*
18. **1 → b, 2 → c, 3 → a, 4 → d** *(Sections 12.2–12.4)*

### Section 5: Practical Application

19. **Errors:**
    1. `fprintf` to a file opened for reading (`"r"`) — Use `"w"` or `"a"` for writing
    2. `"w"` overwrites existing file — Should be `"a"` for appending
    3. No `fclose` after first two operations — Memory/resource leak
    4. `char ch` for `fgetc` — Must be `int ch` to hold `EOF` (which may be -1)
    5. Tiny buffer `char small[5]` — Lines longer than 4 characters will be split across multiple reads, which might be acceptable but is unusual

    **Corrected code:**
    ```c
    #include <stdio.h>

    int main(void) {
        FILE *fp;
        
        // Fixed: open for writing
        fp = fopen("data.txt", "w");
        if (fp != NULL) {
            fprintf(fp, "Hello, file!\n");
            fclose(fp);
        }
        
        // Fixed: append mode for log
        fp = fopen("log.txt", "a");
        if (fp != NULL) {
            fprintf(fp, "Log entry\n");
            fclose(fp);
        }
        
        // Fixed: int ch for fgetc
        fp = fopen("data.txt", "r");
        if (fp != NULL) {
            int ch;  // Must be int, not char!
            while ((ch = fgetc(fp)) != EOF) {
                putchar(ch);
            }
            fclose(fp);
        }
        
        // Buffer size is small but correct if lines are short
        char small[5];
        fp = fopen("data.txt", "r");
        if (fp != NULL) {
            while (fgets(small, sizeof(small), fp) != NULL) {
                printf("%s", small);
            }
            fclose(fp);
        }
        
        return 0;
    }
    ```

20. **Model answer:**
    ```c
    #include <stdio.h>
    #include <string.h>

    struct Student {
        int id;
        char name[50];
        double gpa;
    };

    int main(void) {
        // Create sample data
        struct Student students[3] = {
            {101, "Alice Dupont", 3.8},
            {102, "Bob Martin", 3.2},
            {103, "Claire Chen", 3.9}
        };
        struct Student loaded[3] = {{0}};
        
        // Write to binary file
        FILE *fp = fopen("students.bin", "wb");
        if (fp == NULL) {
            perror("Error opening file for writing");
            return 1;
        }
        
        size_t written = fwrite(students, sizeof(struct Student), 3, fp);
        if (written != 3) {
            fprintf(stderr, "Error: Only wrote %zu of 3 students.\n", written);
            fclose(fp);
            return 1;
        }
        
        if (fclose(fp) == EOF) {
            perror("Error closing file after write");
        }
        
        // Read from binary file
        fp = fopen("students.bin", "rb");
        if (fp == NULL) {
            perror("Error opening file for reading");
            return 1;
        }
        
        size_t read = fread(loaded, sizeof(struct Student), 3, fp);
        if (read != 3) {
            fprintf(stderr, "Error: Only read %zu of 3 students.\n", read);
            if (feof(fp)) {
                printf("(Unexpected end of file)\n");
            }
            if (ferror(fp)) {
                perror("(Read error)");
            }
            fclose(fp);
            return 1;
        }
        
        fclose(fp);
        
        // Print loaded data
        printf("Loaded %zu students:\n", read);
        for (int i = 0; i < 3; i++) {
            printf("  %d: %s — GPA: %.1f\n", 
                   loaded[i].id, loaded[i].name, loaded[i].gpa);
        }
        
        return 0;
    }
    ```

---

## 📊 Quick Self-Assessment

| Score | Assessment | Action |
|:-----:|-----------|--------|
| 18–20 | 🎉 Excellent | Ready for Chapter 13! |
| 14–17 | ✅ Good | Review sections 12.4–12.5 (binary files, error handling) |
| 10–13 | 🔄 Fair | Re-read 12.1–12.3 (streams, reading, writing) |
| < 10 | 🔁 Needs Review | Re-read full chapter |

---

*Next: [Chapter 13: Data Structures in C →](../13-data-structures-in-c/01-linked-lists.md)*
