# 📝 Chapter 14 Quiz — Algorithms & Problem Solving

---

**Chapter:** 14 — Algorithms & Problem Solving
**Total Questions:** 20
**Estimated Time:** 30–40 minutes

---

## Section 1: Multiple Choice

**1. What does Big O notation measure?**

a) The actual running time in seconds
b) The number of lines of code in an algorithm
c) How an algorithm's operations grow as input size increases
d) The amount of memory an algorithm uses

**2. What is the time complexity of binary search?**

a) O(1)
b) O(log n)
c) O(n)
d) O(n²)

**3. Which sorting algorithm has O(n log n) time complexity in all cases?**

a) Bubble sort
b) Selection sort
c) Merge sort
d) All of the above

**4. What does O(1) mean?**

a) The algorithm runs in exactly 1 second
b) The algorithm takes 1 operation regardless of input size
c) The algorithm requires 1 unit of memory
d) The algorithm only works on 1 item

**5. What requirement must data satisfy for binary search to work?**

a) The data must be small (less than 100 elements)
b) The data must be sorted
c) The data must contain only integers
d) The data must not contain duplicates

**6. Which data structure makes merge sort particularly efficient?**

a) Arrays (because of random access)
b) Hash tables (because of O(1) lookup)
c) Linked lists (because of O(1) insertions)
d) Binary trees (because of hierarchy)

**7. What does "divide and conquer" mean in algorithm design?**

a) Split the problem into smaller subproblems, solve each, combine results
b) Use multiple processors to solve a problem faster
c) Divide the data into equal parts and discard some
d) Run the algorithm multiple times and take the best result

**8. What Big O class do nested loops (each iterating n times) typically produce?**

a) O(n)
b) O(log n)
c) O(n²)
d) O(n log n)

---

## Section 2: Short Answer

**9. Explain the difference between O(n) and O(n²) in terms you would use to describe it to another person. Give a real-world analogy.**

*Your answer:*

**10. Why is bubble sort considered a poor choice for sorting large arrays, but merge sort is a good choice? Be specific about the Big O.**

*Your answer:*

**11. What is a "base case" in recursion? Why is it essential?**

*Your answer:*

---

## Section 3: Fill in the Blank

**12.** An algorithm with complexity ________ takes the same number of steps regardless of input size.

**13.** Binary search has a complexity of O(________).

**14.** Merge sort uses a ________-and-conquer strategy.

**15.** Bubble sort and selection sort both have a complexity of O(________).

**16.** In a recursive function, the condition that stops the recursion is called the ________ case.

---

## Section 4: Matching

**17. Match each algorithm to its time complexity:**

| Algorithm | Complexity |
|-----------|------------|
| 1. Linear search | a) O(n²) |
| 2. Binary search | b) O(n) |
| 3. Bubble sort | c) O(log n) |
| 4. Merge sort | d) O(n log n) |

**18. Match each algorithm characteristic to its description:**

| Characteristic | Description |
|----------------|-------------|
| 1. O(1) | a) Grows proportionally to input size |
| 2. O(log n) | b) Doubling input has no effect on steps |
| 3. O(n) | c) Doubling input multiplies steps by 4 |
| 4. O(n²) | d) Doubling input adds 1 step |

---

## Section 5: Practical Application

**19. Determine the Big O complexity of this function and explain why:**

```c
void process_array(int arr[], int size) {
    // Part A
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    // Part B
    for (int i = 0; i < size; i++) {
        for (int j = 0; j < size; j++) {
            if (arr[i] == arr[j] && i != j) {
                printf("Duplicate found: %d\n", arr[i]);
            }
        }
    }
}
```

**20. Write a complete C program that:**

- Implements a recursive function `int fibonacci(int n)` that returns the nth Fibonacci number
- Implements an iterative version `int fibonacci_iter(int n)` for comparison
- In `main()`:
  - Prints the first 15 Fibonacci numbers using the recursive function
  - Prints the first 15 Fibonacci numbers using the iterative function
  - Adds code to count how many times the recursive `fibonacci(10)` is called (use a global counter)
  - Explains why the recursive version is so much slower (refer to Big O)

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **c) How an algorithm's operations grow as input size increases** — Big O measures growth rate, not speed. *(Section 14.2)*
2. **b) O(log n)** — Binary search halves the search space each step. *(Section 14.3)*
3. **c) Merge sort** — Merge sort always performs O(n log n) operations. Bubble and selection are O(n²). *(Section 14.4)*
4. **b) The algorithm takes 1 operation regardless of input size** — Constant time, like array access. *(Section 14.2)*
5. **b) The data must be sorted** — Binary search relies on the sorted property to eliminate halves. *(Section 14.3)*
6. **c) Linked lists** — Merge sort works well on linked lists because merging doesn't require random access. *(Section 14.4)*
7. **a) Split the problem into smaller subproblems, solve each, combine results** — The essence of divide and conquer. *(Section 14.5)*
8. **c) O(n²)** — Outer loop runs n times, inner loop runs n times for each outer iteration: n × n = n². *(Section 14.2)*

### Section 2: Short Answer

9. **Model answer:** O(n) is like a teacher taking attendance: if there are 10 students, 10 checks; if 100 students, 100 checks. O(n²) is like every student shaking hands with every other student: 10 students = 45 handshakes, 100 students = 4,950 handshakes. The growth is much faster for O(n²). *(Section 14.2)*

10. **Model answer:** Bubble sort is O(n²) — for 1 million elements, that's 10¹² operations, which is impractical (hours or days). Merge sort is O(n log n) — for 1 million elements, that's about 20 million operations, which takes under a second. The algorithm choice doesn't just make it a little faster — it makes the impossible possible. *(Section 14.4)*

11. **Model answer:** A base case is the simplest version of the problem that can be solved directly without recursion. It's essential because without it, the recursive function would call itself forever, leading to a stack overflow. Every recursive function must reach its base case eventually. *(Section 14.5)*

### Section 3: Fill in the Blank

12. **O(1)** — Constant time. *(Section 14.2)*
13. **log n** — Logarithmic time. *(Section 14.3)*
14. **divide** — Divide and conquer. *(Section 14.4)*
15. **n²** — Quadratic time. *(Section 14.4)*
16. **base** — The base case stops recursion. *(Section 14.5)*

### Section 4: Matching

17. **1 → b, 2 → c, 3 → a, 4 → d** *(Sections 14.2–14.4)*
18. **1 → b, 2 → d, 3 → a, 4 → c** *(Section 14.2)*

### Section 5: Practical Application

19. **Part A** is a single loop iterating n times → **O(n)**. **Part B** is a nested loop (n × n iterations) → **O(n²)**. The overall complexity is O(n + n²), but since n² dominates for large n, the total is **O(n²)**. *(Section 14.2)*

20. **Model answer:**
    ```c
    #include <stdio.h>

    int fib_calls = 0;  // Global counter

    int fibonacci(int n) {
        fib_calls++;
        if (n <= 1) return n;           // Base cases
        return fibonacci(n - 1) + fibonacci(n - 2);  // Recursive case (O(2ⁿ)!)
    }

    int fibonacci_iter(int n) {
        if (n <= 1) return n;
        int a = 0, b = 1, c;
        for (int i = 2; i <= n; i++) {
            c = a + b;
            a = b;
            b = c;
        }
        return b;
    }

    int main(void) {
        printf("First 15 Fibonacci numbers:\n");
        printf("n:  Recursive  Iterative\n");
        printf("--  ---------  ---------\n");
        
        for (int i = 0; i < 15; i++) {
            printf("%2d: %5d     %5d\n", i, fibonacci(i), fibonacci_iter(i));
        }
        
        // Count calls for fibonacci(10)
        fib_calls = 0;
        int result = fibonacci(10);
        printf("\nfibonacci(10) = %d\n", result);
        printf("Recursive calls made: %d\n", fib_calls);
        // This demonstrates why O(2ⁿ) is terrible:
        // fibonacci(10) makes over 100 calls!
        // fibonacci(30) would make over 2 million calls!
        // fibonacci(50) would take years to compute!
        // The iterative version makes exactly n iterations.
        
        return 0;
    }
    ```

---

## 📊 Quick Self-Assessment

| Score | Assessment | Action |
|:-----:|-----------|--------|
| 18–20 | 🎉 Excellent | Ready for Chapter 15! |
| 14–17 | ✅ Good | Review sections 14.2–14.4 (Big O, searching, sorting) |
| 10–13 | 🔄 Fair | Re-read sections 14.1–14.3 (algorithms, Big O, searching) |
| < 10 | 🔁 Needs Review | Re-read full chapter |

---

*Next: [Chapter 15: How Programming Languages Work →](../15-how-programming-languages-work/01-the-abstraction-ladder.md)*
