# 📋 C Syntax Quick Reference

*Keep this open while coding. New sections are added as the course progresses.*

> **Note:** The section numbers in this cheatsheet are organized by **concept category**, not by course chapter order. Use the table of contents below to find what you need. Check the course glossary for cross-references to specific chapters.

---

## 1. Program Structure

```c
#include <stdio.h>   // Include the standard I/O library

// Function declaration (prototype) — tells the compiler "this exists"
void say_hello(void);

// The main function — every program starts here
int main(void)         // int = return type, void = no parameters
{
    say_hello();       // Call the function
    return 0;          // 0 = success (convention)
}

// Function definition — what the function actually does
void say_hello(void)
{
    printf("Hello, world!\n");
}
```

**Key Points:**
- Every C program needs a `main()` function
- `return 0;` at the end of `main()` means "program completed successfully"
- `#include` lines go at the top of your file
- Statements end with a semicolon (`;`)

---

## 2. Comments

```c
// Single-line comment — everything after // is ignored

/*
 * Multi-line comment —
 * everything between the markers is ignored
 */
```

**Use comments to explain WHY, not WHAT.** The code already shows what it does.

---

## 3. Basic Data Types

| Type | What It Stores | Size (typical) | Example |
|------|---------------|----------------|---------|
| `int` | Whole numbers | 4 bytes | `int age = 30;` |
| `float` | Decimal numbers (single precision) | 4 bytes | `float gdp = 3.14;` |
| `double` | Decimal numbers (double precision) | 8 bytes | `double pi = 3.14159265;` |
| `char` | A single character | 1 byte | `char grade = 'A';` |
| `void` | No type (used for functions) | N/A | `void log_error(void)` |
| `_Bool` | true/false (include `<stdbool.h>` for `bool`) | 1 byte | `bool is_valid = true;` |

### Type Modifiers

```c
short int s;   // Smaller integer (2 bytes typically)
long int l;    // Larger integer (8 bytes typically)
unsigned int u; // Only positive values (doubles the positive range)
```

### Sizeof Operator

```c
printf("%zu\n", sizeof(int));    // Prints: 4 (on most systems)
printf("%zu\n", sizeof(char));   // Prints: 1
```

---

## 4. Variable Declaration & Initialization

```c
// Declaration only (value is unpredictable / garbage)
int count;

// Declaration + initialization
int count = 0;

// Multiple declarations
int a = 1, b = 2, c = 3;

// Constants
const int DAYS_IN_WEEK = 7;    // Cannot be modified after declaration
#define PI 3.14159              // Preprocessor macro (text replacement)
```

---

## 5. Format Specifiers (for `printf` and `scanf`)

| Specifier | Type | Example |
|-----------|------|---------|
| `%d` | `int` (signed decimal) | `printf("%d", 42);` |
| `%f` | `float` / `double` | `printf("%.2f", 3.14);` |
| `%lf` | `double` (for `scanf`) | `scanf("%lf", &value);` |
| `%c` | `char` (single character) | `printf("%c", 'A');` |
| `%s` | String (char array) | `printf("%s", "hello");` |
| `%p` | Pointer (memory address) | `printf("%p", &x);` |
| `%zu` | `size_t` (unsigned, for sizeof) | `printf("%zu", sizeof(int));` |
| `%x` | `int` in hexadecimal | `printf("%x", 255);` // prints ff |

### Escape Sequences

```c
printf("\n");   // New line
printf("\t");   // Tab
printf("\\");   // Backslash character
printf("\"");   // Double quote character
printf("\0");   // Null character (end of string)
```

---

## 6. Operators

### Arithmetic Operators

```c
int sum   = a + b;    // Addition
int diff = a - b;     // Subtraction
int prod = a * b;     // Multiplication
int quot = a / b;     // Division (truncates for integers!)
int rem  = a % b;     // Modulo (remainder)
```

⚠️ **Integer division truncates:** `7 / 2` gives `3`, not `3.5`

### Assignment Operators

```c
x = 5;      // Assign
x += 3;     // x = x + 3
x -= 3;     // x = x - 3
x *= 3;     // x = x * 3
x /= 3;     // x = x / 3
x %= 3;     // x = x % 3
x++;        // x = x + 1  (post-increment)
++x;        // x = x + 1  (pre-increment)
x--;        // x = x - 1  (post-decrement)
--x;        // x = x - 1  (pre-decrement)
```

### Relational Operators (return 1 for true, 0 for false)

```c
a == b    // Equal to
a != b    // Not equal to
a < b     // Less than
a > b     // Greater than
a <= b    // Less than or equal to
a >= b    // Greater than or equal to
```

### Logical Operators

```c
!a          // NOT (reverses truth value)
a && b      // AND (both true → true)
a || b      // OR (at least one true → true)
```

### Bitwise Operators (operate at the bit level)

```c
a & b       // AND
a | b       // OR
a ^ b       // XOR
~a          // NOT (ones complement)
a << n      // Left shift by n bits (multiply by 2^n)
a >> n      // Right shift by n bits (divide by 2^n)
```

### Operator Precedence (highest to lowest)

1. `()` `[]` `->` `.`
2. `!` `~` `++` `--` `-` (unary) `*` (dereference) `&` (address-of)
3. `*` `/` `%`
4. `+` `-`
5. `<<` `>>`
6. `<` `<=` `>` `>=`
7. `==` `!=`
8. `&` (bitwise AND)
9. `^` (bitwise XOR)
10. `|` (bitwise OR)
11. `&&`
12. `||`
13. `=` `+=` `-=` etc.
14. `,`

**When in doubt, use parentheses!** `(a + b) * c` is clearer and safer.

---

## 7. Control Flow

### if / else if / else

```c
if (condition) {
    // runs if condition is true (non-zero)
} else if (other_condition) {
    // runs if first is false but this is true
} else {
    // runs if all conditions are false
}
```

### Ternary Operator

```c
int max = (a > b) ? a : b;   // If a > b, max = a; else max = b
```

### switch / case

```c
switch (value) {
    case 1:
        printf("One");
        break;          // Don't forget break, or execution falls through!
    case 2:
        printf("Two");
        break;
    default:
        printf("Other");
        break;
}
```

---

## 8. Loops

### while

```c
int i = 0;
while (i < 10) {
    printf("%d\n", i);
    i++;    // DON'T forget to update the counter!
}
```

### for

```c
for (int i = 0; i < 10; i++) {
    printf("%d\n", i);
}
// Structure: for (initialization; condition; update)
```

### do / while

```c
int i = 0;
do {
    printf("%d\n", i);
    i++;
} while (i < 10);
// Runs at least ONCE, then checks condition
```

### Loop Control

```c
break;       // Exit the loop immediately
continue;    // Skip to the next iteration
```

---

## 9. Functions

```c
// Function definition
return_type function_name(parameter_type parameter_name, ...)
{
    // body
    return value;  // Must match return_type (unless return_type is void)
}

// Example
int add(int a, int b)
{
    return a + b;
}

// Calling a function
int result = add(5, 3);  // result = 8
```

### Function Prototypes

```c
// Declare the function BEFORE main() so the compiler knows it exists
int multiply(int x, int y);

int main(void) {
    int product = multiply(4, 5);  // Works because prototype is above
    return 0;
}

// Define the function AFTER main()
int multiply(int x, int y) {
    return x * y;
}
```

---

## 10. Arrays

```c
// Declaration
int numbers[5];           // Array of 5 integers (uninitialized)
int scores[3] = {90, 85, 95};  // Declare + initialize

// Accessing elements
scores[0] = 92;          // Change first element
int first = scores[0];   // Read first element

// Array traversal
for (int i = 0; i < 3; i++) {
    printf("%d\n", scores[i]);
}
```

⚠️ **C arrays are zero-indexed:** `scores[0]` is the first element, `scores[2]` is the third.
⚠️ **No bounds checking:** Accessing `scores[10]` won't error at compile time but will cause undefined behavior.

### Multidimensional Arrays

```c
int matrix[3][4] = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};

// Access
matrix[1][2]  // Row 1, Column 2 → value 7
```

---

## 11. Strings (Character Arrays)

```c
// String declaration and initialization
char name[] = "Alice";          // Automatically includes \0 at end
char name[6] = "Alice";         // Must leave room for \0
char name[] = {'A', 'l', 'i', 'c', 'e', '\0'};  // Explicit

// String functions (require #include <string.h>)
#include <string.h>

strlen(str);           // Length of string (not counting \0)
strcpy(dest, src);     // Copy source string to destination
strcmp(str1, str2);    // Compare: 0 if equal, <0 if str1<str2, >0 if str1>str2
strcat(dest, src);     // Append src to end of dest
```

⚠️ **Always ensure your destination buffer is large enough!** Buffer overflows are a major source of bugs and security vulnerabilities.

---

## 12. Pointers

```c
int x = 42;
int *p;       // Declare a pointer to an integer
p = &x;       // p now holds the memory address of x

// & is the "address-of" operator
// * is the "dereference" operator

printf("%d\n", *p);   // Dereference: prints 42 (the value at the address)
printf("%p\n", p);    // Prints the address itself (e.g., 0x7ffd1234)
printf("%p\n", &x);   // Same address

*p = 100;             // Change x through the pointer
printf("%d\n", x);    // Now prints 100
```

### Pointer to Pointer

```c
int x = 42;
int *p = &x;     // p holds address of x
int **pp = &p;   // pp holds address of p

printf("%d\n", **pp);  // 42 — dereference twice
```

### NULL Pointers

```c
int *p = NULL;   // Points to nothing (safety: always check before dereferencing)
if (p != NULL) {
    *p = 42;     // Safe to dereference
}
```

### Function Pointers

```c
// Declare a pointer to a function that takes two ints and returns an int
int (*operation)(int, int);

operation = add;       // Point to the 'add' function
int result = operation(5, 3);  // Call through the pointer → 8
```

---

## 13. Dynamic Memory Allocation

```c
#include <stdlib.h>   // Required for malloc, free, etc.

// Allocate memory for 5 integers (20 bytes on most systems)
int *arr = (int *)malloc(5 * sizeof(int));

if (arr == NULL) {
    // Handle allocation failure
    fprintf(stderr, "Memory allocation failed!\n");
    return 1;
}

// Use the memory
arr[0] = 10;
arr[1] = 20;

// MUST free when done
free(arr);
arr = NULL;   // Good practice: set to NULL after freeing
```

### Other Allocation Functions

```c
calloc(n, size);   // Allocate + zero-initialize n elements of size bytes
realloc(ptr, new_size);  // Resize previously allocated memory
```

---

## 14. Structures

```c
// Define a struct
struct Student {
    int id;
    char name[100];
    int year;
};

// Declare and use
struct Student s1;
s1.id = 1;
s1.year = 2025;
strcpy(s1.name, "Maya Patel");

// Typedef — avoids typing 'struct' everywhere
typedef struct {
    int id;
    char name[100];
    int year;
} Student;

Student s2;
s2.id = 2;

// Pointer to struct — use -> operator
Student *p = &s2;
p->id = 3;   // Equivalent to (*p).id = 3
```

---

## 15. File I/O

```c
#include <stdio.h>

// Opening files
FILE *fp = fopen("data.txt", "r");   // Read mode
FILE *fp = fopen("data.txt", "w");   // Write mode (overwrites!)
FILE *fp = fopen("data.txt", "a");   // Append mode
FILE *fp = fopen("data.txt", "r+");  // Read + write

// Always check if fopen succeeded!
if (fp == NULL) {
    printf("Failed to open file\n");
    return 1;
}

// Reading
char buffer[100];
fgets(buffer, sizeof(buffer), fp);  // Read one line
fscanf(fp, "%d %s", &num, str);     // Formatted read

// Writing
fprintf(fp, "Hello, file!\n");      // Formatted write
fputs("Some text\n", fp);           // Write string

// Closing
fclose(fp);

// Standard streams (automatically available)
stdin   // Standard input (keyboard by default)
stdout  // Standard output (screen by default)
stderr  // Standard error (screen by default)
```

---

## 16. Common Compiler Commands

```bash
# Compile a single file
gcc -std=c99 -Wall -Wextra -Wpedantic -Werror -g -O0 program.c -o program

# Compile with warnings only (don't treat as errors)
gcc -std=c99 -Wall -Wextra -Wpedantic -g -O0 program.c -o program

# Run the compiled program
./program

# Compile multiple files
gcc -std=c99 -Wall -Wextra -g -O0 main.c helper.c -o program

# Check for memory leaks (Linux/Mac)
valgrind ./program
```

---

## 17. Common `printf` / `scanf` Patterns

```c
// printf — printing to the screen
printf("Simple text\n");
printf("Value: %d\n", x);
printf("Name: %s, Age: %d\n", name, age);
printf("Pi to 3 decimals: %.3f\n", 3.14159);

// scanf — reading input from the user
int age;
scanf("%d", &age);          // Note the &

char name[50];
scanf("%s", name);          // No & needed for arrays (they're already pointers)

// Safer alternative: fgets for strings
fgets(name, sizeof(name), stdin);
```

---

## 🔄 Before/After Each Chapter

| ⚡ Before starting a chapter | ✅ After finishing a chapter |
|----------------------------|----------------------------|
| Read the learning objectives | Review all objectives — can you do each one? |
| Skim the section headers | Retake any quiz questions you got wrong |
| Check the glossary for new terms | Add 2–3 things to your learning journal |

---

*This cheatsheet grows with you. Each new chapter adds a section.*
