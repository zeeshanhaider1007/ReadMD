# 13.2: Stacks and Queues — Ordered Data Structures

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Explain the stack (LIFO) and queue (FIFO) abstractions
- Implement a stack using a linked list or array
- Implement a queue using a linked list
- Choose the right data structure for real-world problems

---

## 🧭 The Big Picture

> An office processes work in two ways. **Stacks** are like a pile of papers on a desk: the last paper placed on top is the first one you pick up (LIFO — Last In, First Out). **Queues** are like a line at the checkout counter: the first person in line is the first person served (FIFO — First In, First Out).
>
> Stacks and queues are **abstract data types** — they describe WHAT operations are possible (push, pop, enqueue, dequeue), not HOW they're implemented. You can build them using arrays or linked lists.

---

## 📚 Core Content

### The Stack (LIFO)

A stack has two main operations:
- **Push**: Add an item to the top
- **Pop**: Remove and return the item from the top

```
Push 10:  [10]                  ← top
Push 20:  [10, 20]             ← top
Push 30:  [10, 20, 30]         ← top
Pop:      [10, 20]     → returns 30
Pop:      [10]         → returns 20
```

### Stack Implementation (Linked List)

```c
#include <stdio.h>
#include <stdlib.h>

struct StackNode {
    int data;
    struct StackNode *next;
};

struct Stack {
    struct StackNode *top;  // Points to the top node
};

// Initialize an empty stack
void init_stack(struct Stack *s) {
    s->top = NULL;
}

// Push: add to the top
void push(struct Stack *s, int value) {
    struct StackNode *new_node = malloc(sizeof(struct StackNode));
    if (new_node == NULL) return;
    
    new_node->data = value;
    new_node->next = s->top;  // New node points to old top
    s->top = new_node;        // New node is now the top
}

// Pop: remove and return the top
int pop(struct Stack *s) {
    if (s->top == NULL) {
        fprintf(stderr, "Stack underflow! Can't pop from empty stack.\n");
        return -1;  // Error value
    }
    
    struct StackNode *temp = s->top;
    int value = temp->data;
    s->top = temp->next;  // Move top to next node
    free(temp);
    
    return value;
}

// Peek: look at the top without removing
int peek(const struct Stack *s) {
    if (s->top == NULL) {
        fprintf(stderr, "Stack is empty!\n");
        return -1;
    }
    return s->top->data;
}

// Check if empty
int is_empty(const struct Stack *s) {
    return s->top == NULL;
}

// Free all nodes
void free_stack(struct Stack *s) {
    while (s->top != NULL) {
        struct StackNode *temp = s->top;
        s->top = temp->next;
        free(temp);
    }
}

int main(void) {
    struct Stack s;
    init_stack(&s);
    
    push(&s, 10);
    push(&s, 20);
    push(&s, 30);
    
    printf("Top: %d\n", peek(&s));  // 30
    
    while (!is_empty(&s)) {
        printf("Popped: %d\n", pop(&s));
    }
    // Output: 30, 20, 10 (LIFO order)
    
    free_stack(&s);
    return 0;
}
```

### The Queue (FIFO)

A queue has two main operations:
- **Enqueue**: Add an item to the back
- **Dequeue**: Remove and return the item from the front

```
Enqueue 10: [10]                     ← front  ← back
Enqueue 20: [10, 20]                 ← front  ← back
Enqueue 30: [10, 20, 30]             ← front  ← back
Dequeue:    [20, 30]         → returns 10
Dequeue:    [30]             → returns 20
```

### Queue Implementation (Linked List)

```c
#include <stdio.h>
#include <stdlib.h>

struct QueueNode {
    int data;
    struct QueueNode *next;
};

struct Queue {
    struct QueueNode *front;  // Remove from front
    struct QueueNode *back;   // Add to back
};

void init_queue(struct Queue *q) {
    q->front = NULL;
    q->back = NULL;
}

// Enqueue: add to the back
void enqueue(struct Queue *q, int value) {
    struct QueueNode *new_node = malloc(sizeof(struct QueueNode));
    if (new_node == NULL) return;
    
    new_node->data = value;
    new_node->next = NULL;
    
    if (q->back == NULL) {
        // Queue was empty
        q->front = new_node;
        q->back = new_node;
    } else {
        q->back->next = new_node;
        q->back = new_node;
    }
}

// Dequeue: remove from the front
int dequeue(struct Queue *q) {
    if (q->front == NULL) {
        fprintf(stderr, "Queue underflow! Can't dequeue from empty queue.\n");
        return -1;
    }
    
    struct QueueNode *temp = q->front;
    int value = temp->data;
    q->front = temp->next;
    
    if (q->front == NULL) {
        q->back = NULL;  // Queue is now empty
    }
    
    free(temp);
    return value;
}

int queue_is_empty(const struct Queue *q) {
    return q->front == NULL;
}

void free_queue(struct Queue *q) {
    while (q->front != NULL) {
        struct QueueNode *temp = q->front;
        q->front = temp->next;
        free(temp);
    }
    q->back = NULL;
}

int main(void) {
    struct Queue q;
    init_queue(&q);
    
    enqueue(&q, 10);
    enqueue(&q, 20);
    enqueue(&q, 30);
    
    while (!queue_is_empty(&q)) {
        printf("Dequeued: %d\n", dequeue(&q));
    }
    // Output: 10, 20, 30 (FIFO order)
    
    free_queue(&q);
    return 0;
}
```

### Real-World Applications

| Structure | Use Case | Analogy |
|-----------|----------|---------|
| **Stack** | Function call stack (Chapter 7) | Pile of documents on a desk |
| **Stack** | Undo/Redo in editors | Browser back button |
| **Stack** | Expression evaluation | Matching parentheses `({[]})` |
| **Queue** | Printer spooling | Line at a checkout counter |
| **Queue** | Keyboard buffer | Processing keystrokes in order |
| **Queue** | Breadth-first search | Processing help-desk tickets by submission time |

### Stack Application: Undo System

```c
#define MAX_UNDO 100

struct UndoStack {
    char actions[MAX_UNDO][50];
    int top;  // -1 means empty
};

void push_action(struct UndoStack *us, const char *action) {
    if (us->top < MAX_UNDO - 1) {
        us->top++;
        strcpy(us->actions[us->top], action);
    }
}

void undo(struct UndoStack *us) {
    if (us->top >= 0) {
        printf("Undoing: %s\n", us->actions[us->top]);
        us->top--;
    }
}
```

### Queue Application: Request Processing

```c
struct Request {
    int id;
    char description[100];
};

struct RequestQueue {
    struct Request requests[100];
    int front;
    int back;
    int count;
};

void add_request(struct RequestQueue *q, int id, const char *desc) {
    if (q->count < 100) {
        q->requests[q->back].id = id;
        strcpy(q->requests[q->back].description, desc);
        q->back = (q->back + 1) % 100;  // Circular buffer
        q->count++;
    }
}
```

---

## 🧪 Try It Yourself

> **Exercise 1: Stack Reversal**
> Use a stack to reverse a string. Push each character of "DIPLOMACY" onto a stack, then pop them. Print the result.

> **Exercise 2: Queue Simulation**
> Simulate a visa counter: enqueue 5 people, dequeue 3, then enqueue 2 more. Print the queue state at each step.

> **Exercise 3: Bracket Matching**
> Write a function that uses a stack to check if parentheses in a string are balanced: `"({[]})"` is valid, `"({[})"` is not.

> **Exercise 4: Queue using Two Stacks**
> Implement a queue using TWO stacks internally. Enqueue pushes to stack 1. Dequeue pops from stack 2 (refilling from stack 1 when empty).

---

## 💡 Common Pitfalls

- ❌ **Stack underflow** — Popping from an empty stack is a bug. Always check if the stack is empty before popping.

- ❌ **Queue underflow** — Dequeuing from an empty queue is also a bug. Always check first.

- ❌ **Forgetting to update both front AND back in a queue** — When a queue becomes empty after a dequeue, BOTH pointers must be set to NULL.

- ❌ **Confusing stack and queue** — Stack = LIFO (last in, first out). Queue = FIFO (first in, first out). Remember: stack is a pile of papers; queue is a line of people.

---

## 🔗 Connections to What You Know

> **Stacks and queues model how everyday places process work.**
>
> A busy desk is a stack: new papers go on top, and the most recent is handled first. The checkout line is a queue: customers are served in order of arrival, regardless of how many are waiting.
>
> Both are simple, universal patterns. Once you recognize the pattern — LIFO or FIFO — you can apply the right data structure instantly.

---

## ✅ Section Checklist

- [ ] I can explain the difference between LIFO and FIFO
- [ ] I can implement a stack with push, pop, and peek
- [ ] I can implement a queue with enqueue and dequeue
- [ ] I can identify real-world scenarios for stacks and queues
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [13.3: Binary Trees →](./03-binary-trees.md)*
