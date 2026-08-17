# 14.5: Recursion Revisited — Thinking Recursively

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Recognize recursive patterns in algorithms (divide and conquer)
- Trace recursive function calls with confidence
- Compare recursive and iterative solutions
- Identify when recursion is the natural solution

---

## 🧭 The Big Picture

> In everyday life, big problems are solved by breaking them into smaller versions of the same problem. To clean a large house, you break it into rooms. Each room is cleaned separately. Then you combine the results. If a room is still too big, you break it into sections. This is **divide and conquer** — a naturally recursive strategy.
>
> You first encountered recursion in Chapter 7. Now, with data structures and algorithms under your belt, you'll see recursion everywhere: searching, sorting, tree traversal, graph exploration. It's not just a curiosity — it's one of the most powerful patterns in computer science.

---

## 📚 Core Content

### The Recursive Pattern

Every recursive function has the same structure:

```c
return_type function(parameters) {
    // 1. BASE CASE: Simple enough to solve directly
    if (/* simplest case */) {
        return /* direct answer */;
    }
    
    // 2. RECURSIVE CASE: Break into smaller version(s) of same problem
    //    and combine the results
    return /* combine */ function(smaller_parameters);
}
```

### Recursion in Merge Sort

Merge sort is a perfect example of recursive thinking:

```c
void merge_sort(int arr[], int left, int right) {
    if (left < right) {                     // Base case: left >= right means 0 or 1 element
        int mid = left + (right - left) / 2;
        
        merge_sort(arr, left, mid);         // Sort left half
        merge_sort(arr, mid + 1, right);    // Sort right half
        
        merge(arr, left, mid, right);       // Combine the two sorted halves
    }
}
```

The recursion tree for `merge_sort([64, 34, 25, 12], 0, 3)`:

```
merge_sort(arr, 0, 3)
├── merge_sort(arr, 0, 1)
│   ├── merge_sort(arr, 0, 0) → base case (1 element)
│   └── merge_sort(arr, 1, 1) → base case (1 element)
│   └── merge(arr, 0, 0, 1) → [34, 64]
├── merge_sort(arr, 2, 3)
│   ├── merge_sort(arr, 2, 2) → base case (1 element)
│   └── merge_sort(arr, 3, 3) → base case (1 element)
│   └── merge(arr, 2, 2, 3) → [12, 25]
└── merge(arr, 0, 1, 3) → [12, 25, 34, 64]
```

### Recursion in Binary Search

```c
int binary_search_recursive(int arr[], int left, int right, int target) {
    // Base case: search space is empty
    if (left > right) {
        return -1;  // Not found
    }
    
    int mid = left + (right - left) / 2;
    
    // Base case: found it
    if (arr[mid] == target) {
        return mid;
    }
    
    // Recursive cases: search one half
    if (arr[mid] < target) {
        return binary_search_recursive(arr, mid + 1, right, target);
    } else {
        return binary_search_recursive(arr, left, mid - 1, target);
    }
}
```

Notice how the recursive version mirrors the iterative version exactly — it just uses function calls instead of a while loop.

### Recursion in Tree Traversals

Tree operations are naturally recursive because a tree is a recursive data structure (each node contains subtrees):

```c
// In-order traversal
void in_order(struct TreeNode *root) {
    if (root == NULL) return;       // Base case: empty tree
    
    in_order(root->left);           // Recursively visit left subtree
    printf("%d ", root->data);      // Visit this node
    in_order(root->right);          // Recursively visit right subtree
}

// Tree height
int tree_height(struct TreeNode *root) {
    if (root == NULL) return -1;    // Base case: empty tree
    
    int left_h = tree_height(root->left);   // Height of left subtree
    int right_h = tree_height(root->right); // Height of right subtree
    
    return (left_h > right_h ? left_h : right_h) + 1;  // Take the maximum
}

// Count nodes
int count_nodes(struct TreeNode *root) {
    if (root == NULL) return 0;     // Base case: empty tree
    
    return 1 + count_nodes(root->left) + count_nodes(root->right);
}
```

### Recursion in Graph Traversal (DFS)

Depth-First Search is naturally recursive:

```c
void dfs(struct Graph *g, int vertex, bool *visited) {
    // Base case: this vertex was already visited
    if (visited[vertex]) return;
    
    // Process this vertex
    visited[vertex] = true;
    printf("Visited: %d\n", vertex);
    
    // Recursively visit all unvisited neighbors
    struct AdjNode *neighbor = g->adj_lists[vertex];
    while (neighbor != NULL) {
        if (!visited[neighbor->vertex]) {
            dfs(g, neighbor->vertex, visited);  // Recursive call
        }
        neighbor = neighbor->next;
    }
}
```

### Recursion vs. Iteration

| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| Readability | Natural for recursive structures (trees, graphs) | Natural for linear sequences (arrays) |
| Memory | O(depth) — uses call stack | O(1) — single frame |
| Performance | Function call overhead | No overhead |
| Risk | Stack overflow for deep recursion | No stack overflow |
| Debugging | Harder to trace (many frames) | Easier to trace (single loop) |

### When Recursion Wins

**Recursion is the better choice when:**
- The problem is naturally recursive (trees, graphs, divide-and-conquer)
- The recursive version is significantly simpler and clearer
- The recursion depth is limited (under ~1000)

```c
// Natural recursion: Tower of Hanoi
void tower_of_hanoi(int n, char from, char to, char aux) {
    if (n == 1) {
        printf("Move disk 1 from %c to %c\n", from, to);
        return;
    }
    tower_of_hanoi(n - 1, from, aux, to);
    printf("Move disk %d from %c to %c\n", n, from, to);
    tower_of_hanoi(n - 1, aux, to, from);
}

// Natural recursion: Generate all subsets
void generate_subsets(int arr[], int n, int index, int subset[], int subset_size) {
    if (index == n) {
        printf("{ ");
        for (int i = 0; i < subset_size; i++) printf("%d ", subset[i]);
        printf("}\n");
        return;
    }
    
    // Exclude current element
    generate_subsets(arr, n, index + 1, subset, subset_size);
    
    // Include current element
    subset[subset_size] = arr[index];
    generate_subsets(arr, n, index + 1, subset, subset_size + 1);
}
```

### Tail Recursion (Optimization)

A recursive function is **tail-recursive** if the recursive call is the LAST operation performed (no computation after the call):

```c
// NOT tail recursive: multiplication happens AFTER the recursive call
int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);  // n * ... happens AFTER recursive call
}

// Tail recursive: the recursive call IS the last operation
int factorial_tail(int n, int accumulator) {
    if (n <= 1) return accumulator;
    return factorial_tail(n - 1, n * accumulator);  // Nothing after the call
}

// Usage:
// factorial(5) = 5 * factorial(4) = 5 * 24 = 120
// factorial_tail(5, 1) = factorial_tail(4, 5) = factorial_tail(3, 20)
//                    = factorial_tail(2, 60) = factorial_tail(1, 120) = 120
```

Some compilers can optimize tail-recursive functions into iterative loops (eliminating stack overhead).

---

## 🧪 Try It Yourself

> **Exercise 1: Recursive Sum**
> Write a recursive function `int sum_to_n(int n)` that returns the sum of numbers from 1 to n. Identify the base case and recursive case.

> **Exercise 2: Palindrome Checker**
> Write a recursive function `int is_palindrome(const char *s, int start, int end)` that checks if a string is a palindrome (reads the same forward and backward).

> **Exercise 3: Count Occurrences**
> Write a recursive function that counts how many times a target value appears in an array.

> **Exercise 4: Recursive Binary Search**
> Implement the recursive binary search function shown above. Test it with a sorted array of 10 integers. Trace the recursive calls for searching for a value at each end and the middle.

---

## 💡 Common Pitfalls

- ❌ **Missing base case** — Without a base case, recursion never ends and causes stack overflow.

- ❌ **Base case never reached** — If the recursive step doesn't move toward the base case, you get infinite recursion.

- ❌ **Too deep** — Recursion depth beyond ~10,000 causes stack overflow regardless. Use iteration for deep problems.

- ❌ **Doing redundant work** — The naive recursive Fibonacci function recomputes the same values exponentially. Use memoization or iteration instead.

---

## 🔗 Connections to What You Know

> **Recursion is like solving puzzles that contain smaller versions of themselves.**
>
> To fold a large blanket, you fold it in half. To fold the half, you fold it in half again — a smaller version of the same task. Eventually, you reach a piece too small to fold (the base case).
>
> Understanding that smallest piece allows you to understand each larger piece that built on it, and so on up to the original blanket. The solution to today's problem is built from solutions to smaller versions of the same problem — exactly like recursion.

---

## ✅ Section Checklist

- [ ] I can identify the base case and recursive case in any recursive function
- [ ] I can trace recursive function calls
- [ ] I understand when recursion is better than iteration
- [ ] I can write recursive versions of common algorithms
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [Chapter 14 Quiz →](./chapter-quiz.md)*
