# 12.3: Writing Text Files — Saving Data Out

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Write text to files using `fprintf` and `fputs`
- Write characters using `fputc`
- Append data to existing files without overwriting
- Format output with proper spacing and alignment

---

## 🧭 The Big Picture

> A student drafts a journal entry, writes it on a page, and saves it in a notebook. The entry becomes a permanent record in the notebook. Later, they might add a postscript (append) or start a fresh page entirely (overwrite).
>
> Writing to a file in C follows the same pattern: you open a channel (the file), write your message, and close the channel. The tools you use — `fprintf`, `fputs`, `fputc` — are like different writing instruments: a word processor, a typewriter, and a pen.

---

## 📚 Core Content

### Writing Formatted Output: `fprintf`

`fprintf` is the file version of `printf`. It writes formatted text to a file:

```c
#include <stdio.h>

int main(void) {
    FILE *fp = fopen("notes.txt", "w");
    
    if (fp == NULL) {
        fprintf(stderr, "Error: Could not open file.\n");
        return 1;
    }
    
    // fprintf works just like printf, but takes a FILE* as first argument
    fprintf(fp, "Journal Entry\n");
    fprintf(fp, "================\n");
    fprintf(fp, "To: Study Group\n");
    fprintf(fp, "FROM: Management\n");
    fprintf(fp, "DATE: %d/%d/%d\n", 15, 3, 2025);
    fprintf(fp, "\n");
    fprintf(fp, "The visiting team will arrive on March 15.\n");
    fprintf(fp, "Total delegates: %d\n", 12);
    fprintf(fp, "Budget allocation: $%.2f million\n", 2.5);
    
    fclose(fp);
    printf("Entry written successfully.\n");
    
    return 0;
}
```

**Output file `notes.txt`:**
```
Journal Entry
================
To: Study Group
FROM: Management
DATE: 15/3/2025

The visiting team will arrive on March 15.
Total delegates: 12
Budget allocation: $2.50 million
```

### Writing Strings: `fputs`

`fputs` writes a string to a file. Unlike `fprintf`, it doesn't add formatting — it just writes the string as-is:

```c
FILE *fp = fopen("note.txt", "w");

if (fp != NULL) {
    fputs("This is a raw string.\n", fp);  // Must include \n yourself
    fputs("No formatting, no conversion.\n", fp);
    fputs("Just pure text.\n", fp);
    
    fclose(fp);
}
```

**Difference between `fprintf` and `fputs`:**
```c
fprintf(fp, "%s\n", "Hello");  // Slower — needs to parse format string
fputs("Hello\n", fp);          // Faster — just writes the string
```

For simple string output, `fputs` is faster. For anything involving variables or formatting, use `fprintf`.

### Writing Characters: `fputc`

`fputc` writes a single character to a file:

```c
FILE *fp = fopen("alphabet.txt", "w");

if (fp != NULL) {
    for (char c = 'A'; c <= 'Z'; c++) {
        fputc(c, fp);
        if (c != 'Z') {
            fputc(',', fp);  // Add comma between letters
        }
    }
    fputc('\n', fp);  // Newline at the end
    
    fclose(fp);
}
```

**Output `alphabet.txt`:**
```
A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z
```

### Writing in Append Mode (`"a"`)

Use `"a"` (append) mode to add data to the end of an existing file without overwriting:

```c
#include <stdio.h>
#include <time.h>

int main(void) {
    FILE *fp = fopen("log.txt", "a");  // Append mode!
    
    if (fp == NULL) {
        fprintf(stderr, "Error: Could not open log file.\n");
        return 1;
    }
    
    // Each run adds a new entry
    fprintf(fp, "[%d-%02d-%02d] Program executed.\n", 2025, 3, 15);
    fprintf(fp, "[%d-%02d-%02d] User logged in.\n", 2025, 3, 15);
    
    fclose(fp);
    printf("Log entry added.\n");
    
    return 0;
}
```

Each time you run this program, it adds lines to `log.txt` without removing previous entries.

### Practical: Exporting Data to CSV

```c
#include <stdio.h>

typedef struct {
    char country[50];
    char capital[50];
    int population;
    double area;
} Country;

int main(void) {
    Country countries[] = {
        {"Canada", "Ottawa", 38000000, 9985000.0},
        {"France", "Paris", 67000000, 551695.0},
        {"Japan", "Tokyo", 125000000, 377975.0}
    };
    int count = 3;
    
    FILE *fp = fopen("countries.csv", "w");
    
    if (fp == NULL) {
        fprintf(stderr, "Error: Could not create file.\n");
        return 1;
    }
    
    // Write header row
    fprintf(fp, "Country,Capital,Population,Area\n");
    
    // Write data rows
    for (int i = 0; i < count; i++) {
        fprintf(fp, "%s,%s,%d,%.1f\n",
                countries[i].country,
                countries[i].capital,
                countries[i].population,
                countries[i].area);
    }
    
    fclose(fp);
    printf("Exported %d countries to countries.csv\n", count);
    
    return 0;
}
```

### Writing a Formatted Report

```c
#include <stdio.h>

typedef struct {
    char country[50];
    double exports;  // in billions
    double imports;
} TradeData;

int main(void) {
    TradeData data[] = {
        {"Canada", 450.0, 420.0},
        {"France", 580.0, 620.0},
        {"Germany", 1550.0, 1320.0}
    };
    int count = 3;
    
    FILE *fp = fopen("trade_report.txt", "w");
    
    if (fp == NULL) return 1;
    
    // Write a formatted report using width specifiers for alignment
    fprintf(fp, "============================================\n");
    fprintf(fp, "  TRADE BALANCE REPORT (2024)\n");
    fprintf(fp, "============================================\n\n");
    fprintf(fp, "%-15s %12s %12s %12s\n", "Country", "Exports($B)", "Imports($B)", "Balance");
    fprintf(fp, "%-15s %12s %12s %12s\n", "-------", "-----------", "-----------", "-------");
    
    for (int i = 0; i < count; i++) {
        double balance = data[i].exports - data[i].imports;
        fprintf(fp, "%-15s %12.1f %12.1f %12.1f\n",
                data[i].country,
                data[i].exports,
                data[i].imports,
                balance);
    }
    
    fprintf(fp, "\nReport generated on 2025-03-15\n");
    
    fclose(fp);
    printf("Trade report written.\n");
    
    return 0;
}
```

---

## 🧪 Try It Yourself

> **Exercise 1: Write a Shopping List**
> Write a program that creates a file called `shopping.txt` and writes 5 items (one per line) using `fputs`. Then read it back using `fgets` to verify.

> **Exercise 2: Multiplication Table**
> Write a program that writes a 10×10 multiplication table to `multiply.txt` using `fprintf`, with proper column alignment using `%4d` width specifiers.

> **Exercise 3: Append Log**
> Write a program that opens `visits.log` in append mode and adds a line with the current date and "Visitor logged in". Run it multiple times — does the file grow?

> **Exercise 4: Data Export**
> Create an array of structs with student data (name, id, grade). Export it to a CSV file. Then read the CSV file back and verify the data matches.

---

## 💡 Common Pitfalls

- ❌ **Using `"w"` instead of `"a"`** — `"w"` overwrites the entire file. If you want to add to an existing file, use `"a"` (append).

- ❌ **Forgetting newlines** — `fputs` and `fprintf` don't add newlines automatically. Include `\n` explicitly where needed.

- ❌ **Not closing the file after writing** — Buffered data may not be written to disk until `fclose`. If your program crashes before closing, data is lost.

- ❌ **Writing to a file that can't be opened** — Always check if `fopen` returned `NULL` before trying to write.

---

## 🔗 Connections to What You Know

> **Writing to a file is like putting your thoughts on paper.**
>
> When an office issues a memo, they choose whether to: start fresh (overwrite with `"w"` — a new statement replaces the old), add a clarification (append with `"a"` — add to an existing record), or write each character deliberately (`fputc` — every word is carefully chosen). The `fprintf` function is their word processor, letting them format numbers, dates, and text into a polished document.

---

## ✅ Section Checklist

- [ ] I can write formatted output to a file using `fprintf`
- [ ] I can write strings using `fputs` and characters using `fputc`
- [ ] I understand the difference between `"w"` (overwrite) and `"a"` (append)
- [ ] I can create CSV files and formatted reports
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [12.4: Binary File I/O →](./04-binary-file-io.md)*
