# 16.2: Design Document — Structuring Your Project

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Write a design document before coding
- Define all data structures needed for the project
- Plan the function interface for each component

---

## 🧭 The Big Picture

> Before a company builds a new communication system, they write a **design document**: what data will flow through the system, what components are needed, how they connect, and what each component does. The design comes before the construction.
>
> Your capstone deserves the same treatment. Before writing a single line of code, you'll define your data structures, plan your functions, and understand how everything fits together. This saves hours of debugging.

---

## 📚 Core Content

### Data Structures

Define these types:

```c
// Date structure
struct Date {
 int year;
 int month;
 int day;
};

// Priority levels
enum Priority {
 PRIORITY_LOW,
 PRIORITY_ROUTINE,
 PRIORITY_HIGH,
 PRIORITY_URGENT
};

// Message topics
enum Topic {
 TOPIC_BILLING,
 TOPIC_SUPPORT,
 TOPIC_FEATURE,
 TOPIC_ACCOUNT,
 TOPIC_SUPPORT,
 TOPIC_OTHER
};

// Main Message structure
struct Message {
 char id[20]; // e.g., "MSG-2025-001"
 char from[100]; // Sending company
 char to[100]; // Recipient
 struct Date date; // Date sent
 enum Priority priority; // Priority level
 enum Topic topic; // Message topic
 char body[2000]; // Message body text
 struct Message *next; // Linked list pointer
};
```

### Function Design

```c
// === File Operations ===
// Read all messages from a file, return linked list head
struct Message *read_messages(const char *filename);

// Append a new message to the file
int append_message(const char *filename, const struct Message *message);

// === Linked List Operations ===
// Add a message to the end of the list
struct Message *add_message(struct Message *head, const struct Message *message);

// Free the entire list
void free_messages(struct Message *head);

// Count messages in the list
int count_messages(const struct Message *head);

// === Display Functions ===
// Print a single message in formatted form
void print_message(const struct Message *message);

// Print all messages in the list
void print_all_messages(const struct Message *head);

// === Search Functions ===
// Find messages containing a keyword in body or subject
struct Message *search_by_keyword(const struct Message *head, const char *keyword);

// Find messages within a date range
struct Message *search_by_date_range(const struct Message *head, 
 struct Date start, struct Date end);

// Find messages by priority level
struct Message *search_by_priority(const struct Message *head, enum Priority p);

// Find messages by topic
struct Message *search_by_topic(const struct Message *head, enum Topic t);

// === Sorting Functions ===
// Sort messages by date (merge sort on linked list)
struct Message *sort_by_date(struct Message *head);

// Sort messages by priority (highest first)
struct Message *sort_by_priority(struct Message *head);

// === Report Functions ===
// Generate a summary report
void generate_report(const struct Message *head, const char *output_filename);

// === Parser Functions ===
// Parse a single message from file text
struct Message *parse_message(FILE *fp);

// Parse a date string "2025-03-15" into struct Date
struct Date parse_date(const char *date_str);

// Convert priority string to enum
enum Priority parse_priority(const char *str);

// Convert topic string to enum
enum Topic parse_topic(const char *str);
```

### Main Program Flow

```c
int main(int argc, char *argv[]) {
 // 1. Check command line arguments
 // 2. Open and read the message file
 // 3. Parse messages into linked list
 // 4. Display interactive menu
 // 5. Process user choices
 // 6. Clean up and exit
 return 0;
}
```

### Implementation Order

Build the project in this order. Test each step before moving on:

```
Step 1: Data structures + parse_message() — Parse ONE message from file
Step 2: read_messages() — Read ALL messages into linked list
Step 3: add_message() + free_messages() — Linked list operations
Step 4: print_message() + print_all_messages() — Display functions
Step 5: Interactive menu (print, exit)
Step 6: search_by_keyword() — Keyword search
Step 7: search_by_date_range() — Date range search
Step 8: search_by_priority() + search_by_topic() — Other searches
Step 9: sort_by_date() + sort_by_priority() — Sorting
Step 10: generate_report() — Summary report
Step 11: append_message() — Add new messages
Step 12: Error handling + polish
```

---

## 🧪 Try It Yourself

> **Exercise 1: Complete the Design**
> Write the complete function signatures for all functions listed above. Add any additional functions you think might be useful.

> **Exercise 2: Test parse_date**
> Write a small program that tests your `parse_date` function with the string "2025-03-15". Verify it returns {2025, 3, 15}.

> **Exercise 3: Plan the Menu**
> Sketch the main menu interface. What will it look like when the user runs the program? Write the menu display code.

> **Exercise 4: Edge Cases**
> What should happen if: the message file doesn't exist? A message is missing a field? The file is empty? Write pseudocode for handling each case.

---

## 💡 Common Pitfalls

- ❌ **Writing code before the design is complete** — Every hour spent designing saves 4 hours of debugging. Resist the urge to jump into coding.

- ❌ **Building everything at once** — Implement one function at a time, test it, move to the next. "Big bang" integration (writing everything then testing) is a recipe for frustration.

- ❌ **Forgetting to document your functions** — Each function should have a comment explaining what it does, its parameters, and what it returns.

---

## 🔗 Connections to What You Know

> **A design document is like a project plan.**
>
> Before an managers undertakes a major negotiation, they prepare a detailed plan: objectives, strategy, timeline, resources needed, contingency plans. They don't just "start negotiating" and figure it out as they go.
>
> Your capstone deserves the same preparation. The design document is your project plan. Follow it, and the implementation will be straightforward.

---

## ✅ Section Checklist

- [ ] I've written all struct definitions
- [ ] I've listed all function signatures
- [ ] I understand the implementation order
- [ ] I've planned the main program flow
- [ ] I wrote a **journal entry** about my design

---

*Next: [16.3: Implementation →](./03-implementation.md)*
