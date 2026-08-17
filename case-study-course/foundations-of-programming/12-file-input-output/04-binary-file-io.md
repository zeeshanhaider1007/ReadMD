# 12.4: Binary File I/O — Working with Raw Data

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Distinguish between text mode and binary mode
- Write structured data to binary files using `fwrite`
- Read structured data from binary files using `fread`
- Understand when to use binary files vs. text files

---

## 🧭 The Big Picture

> A photo library stores two kinds of records: human-readable captions (text files) and the raw image data (binary files). The captions can be read by anyone. The image data is compact, machine-readable, and preserves exact pixel values without rounding or formatting.
>
> **Binary files** store data in the same format the computer uses internally. A `double` value like 3.14159 takes exactly 8 bytes in a binary file — no conversion to characters, no formatting, just the raw bytes. This makes binary files faster to read/write and more compact, but they can't be read in a text editor.

---

## 📚 Core Content

### Text vs. Binary: The Difference

**Text file** (what we've done so far):
```
The value of pi is 3.141590
```
- Human-readable
- Numbers converted to character strings (3.14159 → "3.141590" = 9 bytes)
- Different systems may format differently (decimal point, line endings)
- Larger file size for numerical data

**Binary file** (what we're learning now):
```
0x18 0x2D 0x44 0x54 0xFB 0x21 0x09 0x40
```
- Machine-readable only (raw bytes)
- Numbers stored in their native format (double = 8 bytes)
- Exact preservation of floating-point values
- Compact for numerical data
- Not portable across systems with different endianness

### Opening Binary Files

Add `"b"` to the mode string:

```c
FILE *fp_rb = fopen("data.bin", "rb");   // Read binary
FILE *fp_wb = fopen("data.bin", "wb");   // Write binary
FILE *fp_ab = fopen("data.bin", "ab");   // Append binary
```

### Writing Binary Data: `fwrite`

```c
size_t fwrite(const void *ptr, size_t size, size_t count, FILE *stream);
```

| Parameter | Description |
|-----------|-------------|
| `ptr` | Pointer to the data to write |
| `size` | Size of each element (in bytes) |
| `count` | Number of elements to write |
| `stream` | File pointer |

```c
#include <stdio.h>

int main(void) {
    // Simple data to write
    int numbers[] = {10, 20, 30, 40, 50};
    int count = 5;
    
    FILE *fp = fopen("numbers.bin", "wb");
    
    if (fp == NULL) {
        fprintf(stderr, "Error: Could not open file.\n");
        return 1;
    }
    
    // Write the entire array at once
    size_t written = fwrite(numbers, sizeof(int), count, fp);
    
    if (written != count) {
        fprintf(stderr, "Error: Only wrote %zu of %d elements.\n", written, count);
    }
    
    fclose(fp);
    printf("Wrote %d integers (%zu bytes) to numbers.bin\n", 
           count, count * sizeof(int));
    
    return 0;
}
```

### Reading Binary Data: `fread`

```c
size_t fread(void *ptr, size_t size, size_t count, FILE *stream);
```

```c
#include <stdio.h>

int main(void) {
    int numbers[5];
    
    FILE *fp = fopen("numbers.bin", "rb");
    
    if (fp == NULL) {
        fprintf(stderr, "Error: Could not open file.\n");
        return 1;
    }
    
    // Read the entire array at once
    size_t read = fread(numbers, sizeof(int), 5, fp);
    
    if (read != 5) {
        fprintf(stderr, "Error: Only read %zu elements.\n", read);
    } else {
        printf("Read %zu integers:\n", read);
        for (int i = 0; i < 5; i++) {
            printf("  numbers[%d] = %d\n", i, numbers[i]);
        }
    }
    
    fclose(fp);
    return 0;
}
```

### Writing and Reading Structs

Binary I/O excels at saving and loading structs:

```c
#include <stdio.h>
#include <string.h>

typedef struct {
    int id;
    char name[50];
    double balance;
    int is_active;
} Account;

int main(void) {
    // Create an account
    Account acc = {1001, "Maple High School", 2500000.50, 1};
    
    // Write to binary file
    FILE *fp = fopen("account.bin", "wb");
    if (fp == NULL) return 1;
    
    // Write the entire struct at once
    fwrite(&acc, sizeof(Account), 1, fp);
    fclose(fp);
    
    printf("Account written (%zu bytes).\n", sizeof(Account));
    
    // Read it back into a different variable
    Account loaded = {0};
    
    fp = fopen("account.bin", "rb");
    if (fp == NULL) return 1;
    
    fread(&loaded, sizeof(Account), 1, fp);
    fclose(fp);
    
    // Verify the data
    printf("Loaded account:\n");
    printf("  ID: %d\n", loaded.id);
    printf("  Name: %s\n", loaded.name);
    printf("  Balance: $%.2f\n", loaded.balance);
    printf("  Active: %s\n", loaded.is_active ? "Yes" : "No");
    
    return 0;
}
```

### Writing Arrays of Structs

```c
#include <stdio.h>

typedef struct {
    int id;
    char name[30];
    double salary;
} Employee;

int main(void) {
    Employee staff[3] = {
        {101, "Alice Dupont", 75000.0},
        {102, "Bob Martin", 82000.0},
        {103, "Claire Chen", 91000.0}
    };
    
    // Write all employees at once
    FILE *fp = fopen("employees.bin", "wb");
    if (fp == NULL) return 1;
    
    size_t written = fwrite(staff, sizeof(Employee), 3, fp);
    fclose(fp);
    
    printf("Wrote %zu employees (%zu bytes each)\n", 
           written, sizeof(Employee));
    
    // Read them back
    Employee loaded[3];
    
    fp = fopen("employees.bin", "rb");
    if (fp == NULL) return 1;
    
    fread(loaded, sizeof(Employee), 3, fp);
    fclose(fp);
    
    for (int i = 0; i < 3; i++) {
        printf("%d: %s — $%.0f\n", loaded[i].id, loaded[i].name, loaded[i].salary);
    }
    
    return 0;
}
```

### Binary vs. Text: When to Use Which

```c
#include <stdio.h>

typedef struct {
    int id;
    double value;
    char label[20];
} Record;

int main(void) {
    Record records[1000];
    
    // Fill with sample data
    for (int i = 0; i < 1000; i++) {
        records[i].id = i;
        records[i].value = i * 3.14;
        sprintf(records[i].label, "Item-%d", i);
    }
    
    // Binary write
    FILE *fbin = fopen("data.bin", "wb");
    fwrite(records, sizeof(Record), 1000, fbin);
    fclose(fbin);
    
    // Text write
    FILE *ftxt = fopen("data.txt", "w");
    for (int i = 0; i < 1000; i++) {
        fprintf(ftxt, "%d,%.2f,%s\n", records[i].id, records[i].value, records[i].label);
    }
    fclose(ftxt);
    
    // Compare sizes
    printf("Run this and check file sizes with ls/explorer!\n");
    
    return 0;
}
```

| Aspect | Text | Binary |
|--------|------|--------|
| Human-readable | Yes (open in any editor) | No (gibberish in text editor) |
| Size for numbers | Larger ("123456" = 6 bytes) | Compact (int = 4 bytes) |
| Precision | Limited by formatting (%.2f loses precision) | Exact (full double precision) |
| Speed | Slower (format/parse conversions) | Faster (raw byte copy) |
| Portability | Portable across systems | May have endianness issues |
| Best for | Configuration, logs, data exchange | Performance-critical data, exact numerical data, saving program state |

---

## 🧪 Try It Yourself

> **Exercise 1: Write and Read an Integer Array**
> Create an array of 10 integers. Write it to a binary file using `fwrite`. Read it back into a different array and verify the values match.

> **Exercise 2: Save and Load a Struct**
> Define a struct with at least 4 fields of different types. Create an instance, save it to a binary file, clear the struct (set all fields to 0), then load it back. Verify the data was restored.

> **Exercise 3: Size Comparison**
> Write the same data (an array of 100 doubles) to a text file and a binary file. Compare the file sizes. Which is larger? Why?

> **Exercise 4: Append to Binary**
> Write 5 integers to a binary file using `"wb"`. Then open the same file with `"ab"` and write 5 more integers. Read the file back — how many integers are there?

---

## 💡 Common Pitfalls

- ❌ **Opening binary files in text mode** — On Windows, text mode translates `\n` to `\r\n`, corrupting binary data. Always use `"wb"` and `"rb"` for binary files.

- ❌ **Assuming binary files are portable** — Different systems use different byte orders (endianness). A binary file written on x86 may not read correctly on ARM. This usually isn't an issue for personal projects but matters for data exchange.

- ❌ **Not checking `fread`/`fwrite` return values** — These functions can read/write fewer items than requested. Always check the return value.

- ❌ **Writing structs with pointers** — `fwrite` writes the pointer value, not the pointed-to data. When reading back, the pointer will be invalid. Only write structs that contain no pointers.

---

## 🔗 Connections to What You Know

> **Binary files are like a machine's native format.**
>
> Human-readable captions (text files) are useful for general use — anyone can read them. But for large or precise data, programs use their native format (binary files). The data is more compact, transfers faster, and preserves exact values. The trade-off is that you need the right decoding system to read it — just like you need the right app to open a photo file.

---

## ✅ Section Checklist

- [ ] I understand the difference between text and binary files
- [ ] I can write data to binary files using `fwrite`
- [ ] I can read data from binary files using `fread`
- [ ] I can save and load structs with binary I/O
- [ ] I know when to use binary vs. text files
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [12.5: Error Handling →](./05-error-handling.md)*
