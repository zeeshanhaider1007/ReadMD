# 12.5: Error Handling — Robust File Operations

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Check for errors in all file operations
- Use `ferror` to detect read/write errors
- Use `perror` to print descriptive error messages
- Handle file errors gracefully without crashing

---

## 🧭 The Big Picture

> In real life, not every message arrives intact. Some are blocked, some are corrupted in transmission, some never arrive at all. A well-run service has protocols for every scenario: verify delivery, request resending, log the failure, and escalate if necessary.
>
> File operations in C fail for many reasons: the file doesn't exist, the disk is full, permissions are denied, the file is corrupted, or the hardware fails. Your program needs to handle these failures gracefully — just as a delivery service handles lost packages without collapsing.

---

## 📚 Core Content

### The Golden Rule of File I/O

**Every file operation can fail. Always check the return value.**

### Error 1: `fopen` Returns NULL

This is the most common file error. Always check immediately:

```c
#include <stdio.h>

int main(void) {
    FILE *fp = fopen("nonexistent.txt", "r");
    
    if (fp == NULL) {
        printf("Error: Could not open file.\n");
        return 1;  // Exit with error code
    }
    
    // Safe to use fp here
    fclose(fp);
    return 0;
}
```

### Error 2: `fclose` Can Fail

Even closing a file can fail (e.g., disk full during buffer flush):

```c
if (fclose(fp) == EOF) {
    printf("Error: Problem closing file (data may not have been saved!)\n");
} else {
    fp = NULL;
}
```

### Error 3: Read/Write Operations Can Be Partial

`fread` and `fwrite` may read/write fewer items than requested:

```c
int buffer[100];
size_t items_read = fread(buffer, sizeof(int), 100, fp);

if (items_read == 0) {
    if (feof(fp)) {
        printf("End of file reached.\n");
    } else if (ferror(fp)) {
        printf("Error reading file.\n");
    }
} else if (items_read < 100) {
    printf("Warning: Only read %zu of 100 items.\n", items_read);
    if (ferror(fp)) {
        printf("A read error occurred.\n");
    }
}
```

### Using `ferror` to Check for Errors

`ferror` returns non-zero if an error occurred during the last file operation:

```c
#include <stdio.h>

int main(void) {
    FILE *fp = fopen("data.txt", "r");
    if (fp == NULL) {
        perror("Error opening file");
        return 1;
    }
    
    char buffer[100];
    while (fgets(buffer, sizeof(buffer), fp) != NULL) {
        printf("%s", buffer);
    }
    
    // After the loop, check WHY it stopped
    if (feof(fp)) {
        printf("(Reached end of file)\n");
    } else if (ferror(fp)) {
        printf("(An error occurred while reading)\n");
    }
    
    fclose(fp);
    return 0;
}
```

### Using `perror` for Descriptive Error Messages

`perror` prints a human-readable error message based on the global `errno` variable:

```c
#include <stdio.h>
#include <errno.h>

int main(void) {
    FILE *fp = fopen("missing.txt", "r");
    
    if (fp == NULL) {
        perror("fopen failed");
        // Prints something like: "fopen failed: No such file or directory"
        return 1;
    }
    
    fclose(fp);
    return 0;
}
```

The message includes both your custom prefix AND the system's description of what went wrong.

### A Complete Robust File Reader

```c
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>

int main(int argc, char *argv[]) {
    // Check command line arguments
    if (argc != 2) {
        fprintf(stderr, "Usage: %s <filename>\n", argv[0]);
        return 1;
    }
    
    // Open file with user-specified name
    FILE *fp = fopen(argv[1], "r");
    
    if (fp == NULL) {
        fprintf(stderr, "Error: Could not open '%s'.\n", argv[1]);
        perror("Reason");
        return 1;
    }
    
    // Read and process file
    char line[256];
    int line_num = 0;
    int error_occurred = 0;
    
    while (fgets(line, sizeof(line), fp) != NULL) {
        line_num++;
        
        // Remove trailing newline
        size_t len = strlen(line);
        if (len > 0 && line[len - 1] == '\n') {
            line[len - 1] = '\0';
        }
        
        printf("%4d: %s\n", line_num, line);
    }
    
    // Check why the loop ended
    if (ferror(fp)) {
        fprintf(stderr, "Error reading '%s' at line %d.\n", argv[1], line_num);
        perror("Reason");
        error_occurred = 1;
    } else if (feof(fp)) {
        printf("\n(End of file — %d lines read)\n", line_num);
    }
    
    // Close and check if successful
    if (fclose(fp) == EOF) {
        fprintf(stderr, "Error closing '%s'.\n", argv[1]);
        perror("Reason");
        error_occurred = 1;
    }
    
    return error_occurred ? 1 : 0;
}
```

### Error Handling Strategy Summary

| Situation | Check | Action |
|-----------|-------|--------|
| `fopen` fails | `fp == NULL` | Print error, return/exit |
| Read fails mid-file | `fgets == NULL` or `fread < count` | Check `feof` and `ferror` |
| Write fails | `fprintf < 0` or `fwrite < count` | Check `ferror`, possibly abort |
| `fclose` fails | Return value `== EOF` | Data may not have been saved |
| Any I/O error | `ferror(fp) != 0` | Report and recover if possible |

### Common Error Scenarios and Messages

```c
#include <stdio.h>
#include <errno.h>
#include <string.h>  // for strerror()

int main(void) {
    // Try various error scenarios
    FILE *fp;
    
    // Scenario 1: File doesn't exist
    fp = fopen("does_not_exist.txt", "r");
    if (fp == NULL) {
        printf("Error value: %d — %s\n", errno, strerror(errno));
        // Output: Error value: 2 — No such file or directory
    }
    
    // Scenario 2: Permission denied (try opening a system file)
    fp = fopen("/etc/shadow", "r");  // On Linux — may get permission error
    if (fp == NULL) {
        printf("Error value: %d — %s\n", errno, strerror(errno));
        // May output: Error value: 13 — Permission denied
    }
    
    return 0;
}
```

---

## 🧪 Try It Yourself

> **Exercise 1: Graceful File Open**
> Write a program that asks the user for a filename, tries to open it, and prints "File opened successfully!" if it works, or "Could not open file: [reason]" using `perror` if it fails.

> **Exercise 2: Error Detection in Reading**
> Write a program that reads a file character by character until EOF or error. After the loop, use `feof` and `ferror` to report which condition ended the loop.

> **Exercise 3: Robust Command-Line Tool**
> Write a program that takes a filename as a command-line argument, reads it line by line with full error checking (reporting which line failed if an error occurs), and exits with code 0 on success or 1 on failure.

> **Exercise 4: Write with Verification**
> Write a program that writes 100 integers to a file, then immediately reads them back to verify. If the verification fails, print "FILE CORRUPTION DETECTED!" and delete the file using `remove("filename.bin")`.

---

## 💡 Common Pitfalls

- ❌ **Not checking `fopen` return value** — The most common file I/O bug. Always check `fp != NULL` before using the pointer.

- ❌ **Confusing `feof` and `ferror`** — `feof` means end of file (normal). `ferror` means something went wrong (abnormal). They are different conditions.

- ❌ **Assuming `fclose` always succeeds** — Buffered data may fail to write during close. Check the return value.

- ❌ **Not using `perror` or `strerror`** — Raw error codes are meaningless. `perror("context")` gives a clear message like "fopen failed: Permission denied".

---

## 🔗 Connections to What You Know

> **Error handling in file I/O is like protocol for delivery failures.**
>
> When a package goes missing, the service doesn't panic. They follow protocol: verify the package wasn't delivered (check error), identify the failure point (`feof` vs `ferror`), log the incident (`perror`), and take corrective action (retry, report, or abort). The system is designed to handle failure gracefully because in delivery — and in programming — things WILL go wrong.

---

## ✅ Section Checklist

- [ ] I always check if `fopen` returned `NULL`
- [ ] I can use `feof` and `ferror` to diagnose read failures
- [ ] I use `perror` for descriptive error messages
- [ ] I check the return value of `fclose`
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [Chapter 12 Quiz →](./chapter-quiz.md)*
