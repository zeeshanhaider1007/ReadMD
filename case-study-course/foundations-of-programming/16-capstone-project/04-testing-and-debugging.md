# 16.4: Testing and Debugging — Making It Work

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Test each component of your capstone systematically
- Use debugging techniques to find and fix bugs
- Use Valgrind to detect memory leaks
- Handle edge cases gracefully

---

## 🧭 The Big Picture

> An analyst's first independent report is always reviewed by a senior colleague. They check: is the format correct? Are all required fields present? Is the categorization appropriate? Is the message clear?
>
> Testing is the same process. You check each component: does it parse correctly? Does it handle edge cases? Does it leak memory? Is the output correct?

---

## 📚 Core Content

### Testing Strategy

Test in order. Don't move to the next test until the current one passes.

```text
1. parse_message() → Test with ONE message
2. read_messages() → Test with MULTIPLE messages
3. print_message() → Verify output format
4. add_message() → Verify list operations
5. search functions → Test with known data
6. sort functions → Verify sorted order
7. generate_report() → Compare output to expected
8. Memory leak check → Run Valgrind
9. Edge cases → Empty file, missing fields
```

### Test 1: Parse a Single Message

Create a test file `test_message.txt`:

```
MSG-2025-TEST
FROM: Test Department
TO: Test Office
DATE: 2025-06-01
PRIORITY: HIGH
TOPIC: TRADE
BODY:
This is a test message body.
It has multiple lines.
---END---
```

Write a small test program:

```c
#include <stdio.h>

int main(void) {
 FILE *fp = fopen("test_message.txt", "r");
 if (fp == NULL) {
 printf("FAIL: Could not open test file.\n");
 return 1;
 }
 
 struct Message *c = parse_message(fp);
 fclose(fp);
 
 if (c == NULL) {
 printf("FAIL: parse_message returned NULL.\n");
 return 1;
 }
 
 // Verify fields
 int passed = 0;
 int total = 6;
 
 if (strcmp(c->id, "MSG-2025-TEST") == 0) passed++; else printf("FAIL: id\n");
 if (strcmp(c->from, "Test Department") == 0) passed++; else printf("FAIL: from\n");
 if (strcmp(c->to, "Test Office") == 0) passed++; else printf("FAIL: to\n");
 if (c->date.year == 2025 && c->date.month == 6 && c->date.day == 1) passed++; else printf("FAIL: date\n");
 if (c->priority == PRIORITY_HIGH) passed++; else printf("FAIL: priority\n");
 if (c->topic == TOPIC_BILLING) passed++; else printf("FAIL: topic\n");
 
 printf("Passed %d/%d tests.\n", passed, total);
 
 free(c);
 return 0;
}
```

### Test 2: Read Multiple Messages

```c
int main(void) {
 struct Message *head = read_messages("test_messages.txt");
 
 if (head == NULL) {
 printf("FAIL: read_messages returned NULL.\n");
 return 1;
 }
 
 int count = 0;
 struct Message *current = head;
 while (current != NULL) {
 count++;
 printf("Message %d: %s (%s → %s)\n", count, current->id, current->from, current->to);
 current = current->next;
 }
 
 printf("Total messages: %d\n", count);
 
 // Verify expected count
 if (count == 3) {
 printf("PASS: Expected 3 messages.\n");
 } else {
 printf("FAIL: Expected 3 messages, got %d.\n", count);
 }
 
 free_messages(head);
 return 0;
}
```

### Common Bugs and Fixes

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| First message parses, rest don't | File position not advancing | Check that `parse_message` reads until `---END---` |
| Memory leak | Nodes not freed | Call `free_messages()` before exit |
| Crash when searching | Head pointer was lost | Always return new head from sort functions |
| Wrong sort order | Date comparison logic | Convert YYYY-MM-DD to integer for comparison |
| `fgets` reads partial line | Buffer too small | Increase buffer size or use dynamic allocation |
| Infinite loop in menu | `scanf` leaves newline | Add `getchar()` after `scanf` |

### Memory Leak Testing

```bash
# Compile with debug symbols
gcc -g feedback_analyzer.c -o feedback_analyzer

# Run with Valgrind
valgrind --leak-check=full ./feedback_analyzer messages.txt

# Expected output:
# HEAP SUMMARY:
# in use at exit: 0 bytes in 0 blocks
# All heap blocks were freed -- no leaks are possible
```

### Edge Case Testing

Test these scenarios:

1. **Empty file** — `read_messages` should return NULL gracefully
2. **Missing field** — What if a message has no TOPIC line?
3. **Very long body** — Does your 2000-byte buffer handle it?
4. **No messages matching search** — Should print "0 messages found"
5. **Duplicate IDs** — Program should handle gracefully
6. **Binary characters in file** — Should be handled safely

---

## 🧪 Try It Yourself

> **Exercise 1: Test parse_message**
> Write the test program shown above and run it with your test message. Fix any failures.

> **Exercise 2: Test Multiple Messages**
> Create a file with 3 messages. Run read_messages and verify all 3 are loaded correctly.

> **Exercise 3: Search Testing**
> Test your keyword search with: a keyword that exists, one that doesn't, and an empty string.

> **Exercise 4: Valgrind Check**
> Run your full program with Valgrind. Fix any memory leaks until the output shows "0 bytes in 0 blocks."

---

## 💡 Common Pitfalls

- ❌ **Only testing the "happy path"** — Test empty files, missing fields, very long inputs. Those are where bugs hide.

- ❌ **Ignoring compiler warnings** — Compile with `-Wall -Wextra -Wpedantic -Werror` and fix ALL warnings.

- ❌ **Fixing symptoms instead of causes** — If the sort is wrong, trace through the merge logic rather than patching the output.

---

## 🔗 Connections to What You Know

> **Testing is like quality assurance.**
>
> Before a report is published, it's reviewed by editors, subject matter experts, and proofreaders. Each reviewer checks a different aspect. They don't assume it's correct because the first draft was well-written — they verify.
>
> Your capstone deserves the same rigorous review. Test every function. Check edge cases. Run Valgrind. Don't assume it works — verify.

---

## ✅ Section Checklist

- [ ] I've tested parse_message with a known message
- [ ] I've tested read_messages with multiple messages
- [ ] I've tested search, sort, and report functions
- [ ] I've run Valgrind and fixed all memory leaks
- [ ] I've tested edge cases (empty file, missing fields)
- [ ] I wrote a **journal entry** about what I tested

---

*Next: [16.5: Presentation →](./05-presentation.md)*
