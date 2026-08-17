# 📝 Chapter 16 Quiz — Capstone Project

---

**Chapter:** 16 — Capstone Project
**Total Questions:** 20
**Estimated Time:** 25–35 minutes

---

## Section 1: Multiple Choice

**1. What is the primary data structure used to store multiple messages in memory?**

a) Array
b) Linked list
c) Hash table
d) Binary tree

**2. What does `parse_message` return when it reaches the end of file unexpectedly?**

a) An empty message struct
b) A message with an error flag set
c) NULL
d) The last successfully parsed message

**3. Why is merge sort a good choice for sorting the message linked list?**

a) It's the simplest to implement
b) It's O(n) time complexity
c) It works efficiently on linked lists and guarantees O(n log n)
d) It doesn't require comparing elements

**4. What does `free_messages` do?**

a) Prepares messages for reuse
b) Frees all memory allocated for the linked list
c) Removes duplicate messages
d) Saves messages back to the file

**5. What is the purpose of `strstr` in the keyword search?**

a) To count occurrences of a substring
b) To find the first occurrence of a substring in a string
c) To replace a substring with another string
d) To compare two strings for equality

**6. What should you run after your program to check for memory leaks?**

a) gdb
b) valgrind
c) gcc
d) make

**7. In the message parser, what signals the end of a message?**

a) A blank line
b) The string "---END---"
c) The end of the file
d) A line starting with "MSG-"

**8. What's the first step in the implementation order?**

a) Implement sorting
b) Build the interactive menu
c) Implement parse_message (parse one message from file)
d) Generate the report

---

## Section 2: Short Answer

**9. Explain why you should build and test your capstone incrementally (one function at a time) rather than writing everything at once and then testing.**

*Your answer:*

**10. What would you check if your program crashes when you select "sort by date"? List at least 3 possible causes.**

*Your answer:*

**11. Describe the structure of your presentation: what are the 5 parts, and how long should each be?**

*Your answer:*

---

## Section 3: Fill in the Blank

**12.** The function ________ parses a single message from the file and returns a pointer to a new `Message` struct.

**13.** The string ________ signals the end of a message in the input file.

**14.** Every `malloc` must be matched with a ________ call.

**15.** To find a substring within a message's body, use the ________ function.

**16.** The capstone project stores messages in a ________ (data structure).

---

## Section 4: Matching

**17. Match each function to its purpose:**

| Function | Purpose |
|----------|---------|
| 1. `read_messages` | a) Prints a formatted summary of all messages |
| 2. `search_by_keyword` | b) Frees all allocated memory |
| 3. `generate_report` | c) Loads all messages from a file into memory |
| 4. `free_messages` | d) Finds messages containing a specific word |

**18. Match each testing scenario to what it verifies:**

| Scenario | What It Verifies |
|----------|-----------------|
| 1. Parse a single message | a) Linked list operations (add, free) |
| 2. Read multiple messages | b) File parser works correctly |
| 3. Add message to list | c) Multiple messages are loaded correctly |
| 4. Valgrind check | d) No memory leaks |

---

## Section 5: Practical Application

**19. Your program is crashing when you try to sort messages by date. The error message is "Segmentation fault." List at least 4 possible causes and explain how you would debug each.**

*Your answer:*

**20. Describe the complete process for adding a NEW feature to the capstone (for example, adding a "search by date range" feature). Include: what functions you'd add or modify, how you'd test it, and what edge cases you'd consider.**

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **b) Linked list** — The project uses a singly linked list to store messages dynamically. *(Section 16.2)*
2. **c) NULL** — `parse_message` returns NULL if it can't parse a complete message. *(Section 16.3)*
3. **c) It works efficiently on linked lists and guarantees O(n log n)** — Merge sort is ideal for linked lists because it doesn't require random access. *(Section 16.3)*
4. **b) Frees all memory allocated for the linked list** — Every `malloc` needs a matching `free`. *(Section 16.3)*
5. **b) To find the first occurrence of a substring in a string** — `strstr(haystack, needle)` returns a pointer to the first match. *(Section 16.3)*
6. **b) valgrind** — Valgrind detects memory leaks and invalid memory access. *(Section 16.4)*
7. **b) The string "---END---"** — Each message is terminated by the end marker. *(Section 16.3)*
8. **c) Implement parse_message (parse one message from file)** — Build and test one function at a time, starting with the lowest-level parser. *(Section 16.2)*

### Section 2: Short Answer

9. **Model answer:** Building incrementally lets you isolate bugs. If you write everything at once and something breaks, you don't know which part is broken. By testing each function as you write it, you know the last function you added contains any new bug. This is called "debugging at the edges" and it's the fastest way to build reliable software. *(Section 16.4)*

10. **Model answer:** (1) The linked list might have a corrupted pointer — check the `next` field after parsing. (2) The merge logic might not handle NULL properly — check edge cases. (3) The date comparison might be wrong — trace through with a small test case. (4) The `split_list` function might return the wrong midpoint — verify with 2 and 3 element lists. *(Section 16.4)*

11. **Model answer:** (1) Problem — 2 minutes, (2) Design — 3 minutes, (3) Demonstration — 5 minutes, (4) Challenges — 2 minutes, (5) Reflection — 3 minutes. Total: ~15 minutes. *(Section 16.5)*

### Section 3: Fill in the Blank

12. **`parse_message`** — Parses one message from a file. *(Section 16.3)*
13. **`---END---`** — The message end marker. *(Section 16.3)*
14. **`free`** — Every allocation needs deallocation. *(Section 16.3)*
15. **`strstr`** — Finds a substring within a larger string. *(Section 16.3)*
16. **linked list** — The primary data structure for the project. *(Section 16.2)*

### Section 4: Matching

17. **1 → c, 2 → d, 3 → a, 4 → b** *(Sections 16.2–16.3)*
18. **1 → b, 2 → c, 3 → a, 4 → d** *(Section 16.4)*

### Section 5: Practical Application

19. **Model answer:** Possible causes: (1) The linked list has been corrupted — check if `next` pointers form a valid chain. (2) A node's `next` pointer is NULL when it shouldn't be — check the `split_list` function. (3) The comparison function has undefined behavior — check date conversion. (4) Stack overflow from infinite recursion — check the recursive base case in merge sort. Debug by: adding print statements before and after each operation, testing with a small (3-element) list, and running under Valgrind to detect memory corruption. *(Section 16.4)*

20. **Model answer:** (1) Modify `find_by_keyword` as a template, creating `find_by_date_range` that takes start and end dates. (2) Add the option to the menu: case 7 for date range search. (3) Test with: messages within the range, messages before the range, messages after the range, empty range, inverted dates (start > end). (4) Test edge cases: null pointer for head, malformed dates, same-day range. (5) Run Valgrind to ensure no leaks were introduced. *(Section 16.4–16.5)*

---

## 📊 Quick Self-Assessment

| Score | Assessment | Action |
|:-----:|-----------|--------|
| 18–20 | 🎉 Excellent | Ready to build your capstone! |
| 14–17 | ✅ Good | Review sections 16.3–16.4 (implementation, testing) |
| 10–13 | 🔄 Fair | Re-read sections 16.1–16.3 (overview, design, implementation) |
| < 10 | 🔁 Needs Review | Re-read the full chapter |

---

*→ Congratulations on completing the course! Review what you've learned with the [full course cheatsheet →](../cheatsheet-c.md)*
