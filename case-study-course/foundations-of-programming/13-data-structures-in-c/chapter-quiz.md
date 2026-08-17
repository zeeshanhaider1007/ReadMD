# 📝 Chapter 13 Quiz — Data Structures in C

---

**Chapter:** 13 — Data Structures in C
**Total Questions:** 20
**Estimated Time:** 35–45 minutes

---

## Section 1: Multiple Choice

**1. What makes a linked list different from an array?**

a) A linked list can only store integers
b) A linked list stores elements contiguously in memory
c) A linked list stores elements scattered in memory, linked by pointers
d) A linked list automatically sorts its elements

**2. What does LIFO stand for?**

a) Last In, First Out
b) Least In, First Out
c) Last In, Fast Out
d) Low Index, First Out

**3. In a Binary Search Tree (BST), where do values smaller than the root go?**

a) They are discarded
b) They go to the right subtree
c) They go to the left subtree
d) They replace the root

**4. What data structure provides O(1) average lookup time for key-value pairs?**

a) Linked list
b) Binary search tree
c) Hash table
d) Stack

**5. What is a collision in a hash table?**

a) Two entries with the same key
b) Two different keys that hash to the same index
c) The hash table runs out of memory
d) A key is deleted while being searched

**6. Which traversal of a BST prints values in sorted order?**

a) Pre-order
b) In-order
c) Post-order
d) Level-order

**7. In a queue, where are new elements added?**

a) The front
b) The back
c) The middle
d) A random position

**8. What is the main advantage of an adjacency list over an adjacency matrix for a sparse graph?**

a) Faster edge lookup
b) Lower memory usage
c) Easier to implement directed edges
d) Built-in weighted edges

---

## Section 2: Short Answer

**9. Explain the difference between a stack and a queue. Give a real-world example of each from diplomacy or international relations.**

*Your answer:*

**10. Why is searching in a balanced BST O(log n) while searching in a linked list is O(n)?**

*Your answer:*

**11. What happens to a hash table's performance as the load factor increases? What can you do about it?**

*Your answer:*

---

## Section 3: Fill in the Blank

**12.** In a linked list, the pointer to the first node is called the ________.

**13.** A queue follows the ________ (First In, First Out) principle.

**14.** In a BST, the ________ traversal visits the left subtree, then the root, then the right subtree.

**15.** A ________ graph has edges with no direction (mutual relationships).

**16.** A ________ in a hash table happens when two different keys produce the same index.

---

## Section 4: Matching

**17. Match each data structure to its best use case:**

| Structure | Use Case |
|-----------|----------|
| 1. Stack | a) Processing tasks in order of arrival |
| 2. Queue | b) Undo/Redo in an editor |
| 3. BST | c) Dictionary of country → capital |
| 4. Hash Table | d) Searching sorted data quickly |

**18. Match each traversal order to its description:**

| Traversal | Description |
|-----------|-------------|
| 1. Pre-order | a) Left → Root → Right |
| 2. In-order | b) Left → Right → Root |
| 3. Post-order | c) Root → Left → Right |

---

## Section 5: Practical Application

**19. Find and fix the errors in this program:**

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *next;
};

void print_list(struct Node *head) {
    struct Node *current = head;
    while (current != NULL) {
        printf("%d ", current->data);
    }
}

struct Node *insert_front(struct Node *head, int value) {
    struct Node *new = malloc(sizeof(struct Node));
    new->data = value;
    new->next = head;
    // Missing: return new
}

int main(void) {
    struct Node *head = NULL;
    head = insert_front(head, 10);
    head = insert_front(head, 20);
    head = insert_front(head, 30);
    
    print_list(head);  // Should print: 30 20 10
    
    // Missing: free_list(head)
    
    return 0;
}
```

**20. Write a complete C program that:**

- Defines a `struct TreeNode` for a binary search tree (int data, left, right pointers)
- Implements `insert` to add values to the BST
- Implements `in_order` to print the tree in sorted order
- Implements `search` that returns 1 if found, 0 otherwise
- In `main()`:
  - Inserts: 55, 30, 70, 20, 40, 60, 80
  - Prints in-order traversal
  - Searches for 40 and 100, printing whether each was found
  - Frees all memory

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **c) A linked list stores elements scattered in memory, linked by pointers** — Each node contains a pointer to the next node. *(Section 13.1)*
2. **a) Last In, First Out** — The last item pushed is the first item popped. *(Section 13.2)*
3. **c) They go to the left subtree** — BST property: left < root < right. *(Section 13.3)*
4. **c) Hash table** — Hash tables provide O(1) average lookup with a good hash function. *(Section 13.4)*
5. **b) Two different keys that hash to the same index** — Collisions are resolved with chaining or open addressing. *(Section 13.4)*
6. **b) In-order** — In-order traversal: Left → Root → Right gives sorted order. *(Section 13.3)*
7. **b) The back** — Enqueue adds to the back; dequeue removes from the front. *(Section 13.2)*
8. **b) Lower memory usage** — Adjacency lists use O(V+E) memory; matrices use O(V²). *(Section 13.5)*

### Section 2: Short Answer

9. **Model answer:** A stack is LIFO — the last item added is the first removed. Example: a pile of papers on a desk where the newest is read first. A queue is FIFO — the first item added is the first removed. Example: a checkout line where customers are served in order of arrival. *(Section 13.2)*

10. **Model answer:** In a balanced BST, each comparison eliminates half the remaining nodes, so the search space halves each step — O(log n). In a linked list, each comparison eliminates only one node, so you may need to traverse all n nodes — O(n). *(Section 13.3)*

11. **Model answer:** As the load factor increases, chains get longer, and search time increases (more collisions). When the load factor exceeds a threshold (typically 0.75), you should resize the table (create a larger array and rehash all entries). *(Section 13.4)*

### Section 3: Fill in the Blank

12. **head** — The entry point to the linked list. *(Section 13.1)*
13. **FIFO** — First In, First Out. *(Section 13.2)*
14. **in-order** — Left, Root, Right. *(Section 13.3)*
15. **undirected** — Mutual relationships with no direction. *(Section 13.5)*
16. **collision** — Two keys mapping to the same bucket. *(Section 13.4)*

### Section 4: Matching

17. **1 → b, 2 → a, 3 → d, 4 → c** *(Various sections)*
18. **1 → c, 2 → a, 3 → b** *(Section 13.3)*

### Section 5: Practical Application

19. **Errors:**
    1. `print_list` infinite loop — Missing `current = current->next;` inside the while loop
    2. `insert_front` has no return statement — `return new;` is missing
    3. No `free_list` function — Memory is never freed

    **Corrected code:**
    ```c
    #include <stdio.h>
    #include <stdlib.h>

    struct Node {
        int data;
        struct Node *next;
    };

    void print_list(struct Node *head) {
        struct Node *current = head;
        while (current != NULL) {
            printf("%d ", current->data);
            current = current->next;  // Fixed: advance pointer
        }
        printf("\n");
    }

    struct Node *insert_front(struct Node *head, int value) {
        struct Node *new = malloc(sizeof(struct Node));
        new->data = value;
        new->next = head;
        return new;  // Fixed: return the new head
    }

    void free_list(struct Node *head) {
        struct Node *current = head;
        while (current != NULL) {
            struct Node *temp = current;
            current = current->next;
            free(temp);
        }
    }

    int main(void) {
        struct Node *head = NULL;
        head = insert_front(head, 10);
        head = insert_front(head, 20);
        head = insert_front(head, 30);
        
        print_list(head);  // 30 20 10
        
        free_list(head);   // Fixed: free memory
        
        return 0;
    }
    ```

20. **Model answer:**
    ```c
    #include <stdio.h>
    #include <stdlib.h>

    struct TreeNode {
        int data;
        struct TreeNode *left;
        struct TreeNode *right;
    };

    struct TreeNode *create_node(int value) {
        struct TreeNode *node = malloc(sizeof(struct TreeNode));
        if (node) {
            node->data = value;
            node->left = NULL;
            node->right = NULL;
        }
        return node;
    }

    struct TreeNode *insert(struct TreeNode *root, int value) {
        if (root == NULL) return create_node(value);
        if (value < root->data)
            root->left = insert(root->left, value);
        else if (value > root->data)
            root->right = insert(root->right, value);
        return root;
    }

    void in_order(struct TreeNode *root) {
        if (root == NULL) return;
        in_order(root->left);
        printf("%d ", root->data);
        in_order(root->right);
    }

    int search(struct TreeNode *root, int target) {
        if (root == NULL) return 0;
        if (target == root->data) return 1;
        if (target < root->data)
            return search(root->left, target);
        else
            return search(root->right, target);
    }

    void free_tree(struct TreeNode *root) {
        if (root == NULL) return;
        free_tree(root->left);
        free_tree(root->right);
        free(root);
    }

    int main(void) {
        struct TreeNode *root = NULL;
        
        root = insert(root, 55);
        root = insert(root, 30);
        root = insert(root, 70);
        root = insert(root, 20);
        root = insert(root, 40);
        root = insert(root, 60);
        root = insert(root, 80);
        
        printf("In-order: ");
        in_order(root);
        printf("\n");
        
        printf("Search for 40: %s\n", search(root, 40) ? "Found" : "Not found");
        printf("Search for 100: %s\n", search(root, 100) ? "Found" : "Not found");
        
        free_tree(root);
        return 0;
    }
    ```

---

## 📊 Quick Self-Assessment

| Score | Assessment | Action |
|:-----:|-----------|--------|
| 18–20 | 🎉 Excellent | Ready for Chapter 14! |
| 14–17 | ✅ Good | Review sections 13.3–13.5 (trees, hash tables, graphs) |
| 10–13 | 🔄 Fair | Re-read sections 13.1–13.2 (linked lists, stacks, queues) |
| < 10 | 🔁 Needs Review | Re-read full chapter |

---

*Next: [Chapter 14: Algorithms & Problem Solving →](../14-algorithms-and-problem-solving/01-what-is-an-algorithm.md)*
