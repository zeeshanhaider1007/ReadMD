# 8.3: Multidimensional Arrays

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Declare and work with 2D and 3D arrays
- Use nested loops to traverse multidimensional arrays
- Understand that multidimensional arrays are stored in row-major order

---

## 🧭 The Big Picture

> A teacher's gradebook has rows (students) and columns (assignment scores: homework, quiz, midterm, final). This is a **2D array** — a table with rows and columns.
>
> A 3D array adds another dimension: perhaps year-by-year data for multiple regions. In C, you can have as many dimensions as needed, but 2D and 3D cover most real-world uses.

---

## 📚 Core Content

### Declaring a 2D Array

```c
type name[rows][columns];
```

```c
int matrix[3][4];  // 3 rows, 4 columns = 12 elements total
```

### Initialization

```c
// Full initialization
int grid[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};

// Flat initialization (same layout in memory)
int grid[2][3] = {1, 2, 3, 4, 5, 6};

// Partial — unspecified elements are 0
int grid[2][3] = {
    {1},
    {4, 5}
};  // { {1,0,0}, {4,5,0} }
```

### Accessing Elements

```c
grid[0][0] = 10;  // First row, first column
grid[1][2] = 99;  // Second row, third column
```

### Memory Layout (Row-Major)

C stores 2D arrays in **row-major order**: the first row is stored contiguously, then the second row, etc.

![Array Memory Layout](../assets/ch08/array-memory-layout.svg)

The same contiguous principle applies — a 2D array is just an array of arrays, all laid out linearly in memory.

```c
int arr[2][3] = {{1,2,3},{4,5,6}};

// In memory: | 1 | 2 | 3 | 4 | 5 | 6 |
// Row 0:       0   1   2
// Row 1:       3   4   5
```

### Looping Through 2D Arrays

Always use row-major order (outer = rows, inner = columns):

```c
int rows = 3, cols = 4;
int matrix[3][4] = {
    {1,  2,  3,  4},
    {5,  6,  7,  8},
    {9, 10, 11, 12}
};

for (int r = 0; r < rows; r++) {
    for (int c = 0; c < cols; c++) {
        printf("%4d", matrix[r][c]);
    }
    printf("\n");  // New line after each row
}
```

### Matrix Operations

```c
// Sum all elements
int sum = 0;
for (int r = 0; r < rows; r++)
    for (int c = 0; c < cols; c++)
        sum += matrix[r][c];

// Find max element
int max = matrix[0][0];
for (int r = 0; r < rows; r++)
    for (int c = 0; c < cols; c++)
        if (matrix[r][c] > max)
            max = matrix[r][c];
```

### 3D Arrays

```c
int cube[2][3][4];  // 2 × 3 × 4 = 24 elements

// Initialization
int cube[2][2][3] = {
    {{1,2,3}, {4,5,6}},
    {{7,8,9}, {10,11,12}}
};

// Three nested loops
for (int x = 0; x < 2; x++)
    for (int y = 0; y < 2; y++)
        for (int z = 0; z < 3; z++)
            printf("cube[%d][%d][%d] = %d\n", x, y, z, cube[x][y][z]);
```

### Practical: Trade Data Table

```c
#include <stdio.h>

int main(void) {
    // Trade data: 3 regions × 4 quarters
    double trade[3][4] = {
        {120.5, 135.2, 128.9, 142.1},  // Americas
        {98.3,  105.7, 112.4, 108.6},  // Europe
        {75.1,  82.4,  79.8,  91.2}    // Asia
    };
    
    char *regions[] = {"Americas", "Europe", "Asia"};
    
    // Print table
    printf("Region\t\tQ1\tQ2\tQ3\tQ4\n");
    printf("----------------------------------------\n");
    for (int r = 0; r < 3; r++) {
        printf("%-10s", regions[r]);
        for (int c = 0; c < 4; c++) {
            printf("\t%.1f", trade[r][c]);
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## 🧪 Try It Yourself

> **Exercise 1: Identity Matrix**
> Create a 4×4 identity matrix (1s on the diagonal, 0s elsewhere). Print it.

> **Exercise 2: Row and Column Sums**
> Given a 3×4 array, print the sum of each row and each column.

> **Exercise 3: Transpose**
> Write a program that transposes a 3×2 matrix into a 2×3 matrix.

> **Exercise 4: Grade Book**
> Create a 2D array for 5 students × 3 exam scores. Calculate and print each student's average.

---

## 💡 Common Pitfalls

- ❌ **Column-major vs. row-major** — C stores arrays row-major. Accessing in column-major order (`arr[col][row]`) causes cache misses for large arrays.
- ❌ **Wrong loop order** — Always use outer loop = rows, inner = columns for best performance.
- ❌ **Forgetting the column size when passing to functions** — For 2D arrays passed to functions, you need to specify at least the column size.

---

## 🔗 Connections to What You Know

> **A 2D array is like a seating chart.**
> Rows = tables, Columns = seats. Each cell contains the name of the guest sitting there. Operations on this chart — searching for a guest, updating a seat assignment, printing all seats — are 2D array operations.

---

## ✅ Section Checklist

- [ ] I can declare, initialize, and access 2D arrays
- [ ] I understand row-major memory layout
- [ ] I can loop through 2D arrays correctly using nested loops
- [ ] I can perform simple matrix operations
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [8.4: Strings in C →](./04-strings-in-c.md)*
