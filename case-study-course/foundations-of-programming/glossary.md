# 📖 Course Glossary

Every definition includes an everyday analogy to help connect the concept to what you already know.

---

## A

### Abstraction
**Hiding complex implementation details behind a simpler interface.**
*Everyday analogy:* You don't need to know how the postal sorting system works to mail a letter. You just drop it in the mailbox and say "send this." The postal system is an abstraction.
*Appears in:* Ch00

### Address (Memory Address)
**A unique identifier for a specific location in memory.**
*Everyday analogy:* Like the street address of a friend's house. You don't need to know what's inside at the address — you just need to know where it is to send something there.
*Appears in:* Ch09

### Algorithm
**A step-by-step procedure for solving a problem.**
*Everyday analogy:* Like a recipe. First, prep the ingredients. Second, combine them. Third, cook. Fourth, taste and adjust. The order matters.
*Appears in:* Ch00, Ch14

### Argument
**A value passed to a function when calling it.**
*Everyday analogy:* Like the items you hand to a cashier when checking out. The cashier (function) processes what you hand them.
*Appears in:* Ch07

### Array
**A contiguous block of memory containing elements of the same type, accessed by a numeric index.**
*IR Analogy:* Like a row of filing cabinets, each drawer labeled 0, 1, 2, 3... The cabinets are identical, next to each other, and you can jump to any drawer instantly.
*Appears in:* Ch08

### Assembly Language
**A low-level programming language that directly corresponds to machine code instructions, using mnemonics instead of binary.**
*Everyday analogy:* Like shorthand notes — more efficient than full text but requires special training to read.
*Appears in:* Ch15

---

## B

### Big-O Notation
**A mathematical notation describing the efficiency of an algorithm as input size grows.**
*Everyday analogy:* Like comparing ways to spread news. Telling each person individually O(n) — you talk to each person one by one. Posting to a group chat O(1) — you tell everyone at once. Telling team captains who tell their teams O(log n) — each captain represents many people.
*Appears in:* Ch14

### Binary
**The base-2 number system using only 0 and 1 — the fundamental language of computers.**
*IR Analogy:* Like Morse code — only dots and dashes, but they can encode any message if you know the pattern.
*Appears in:* Ch01

### Bit
**A single binary digit (0 or 1), the smallest unit of data.**
*Everyday analogy:* Like a single light switch — on or off. Not much on its own, but together with other switches it creates meaning.
*Appears in:* Ch01

### Boolean
**A data type that can only be true or false.**
*Everyday analogy:* Like a light switch — on or off. No middle ground.
*Appears in:* Ch05

### Bug
**An error in a program that causes unexpected behavior.**
*Everyday analogy:* Like a typo in a contract that changes its meaning. The contract might still be "valid syntax" but it doesn't say what you intended.
*Appears in:* Ch02

### Byte
**A group of 8 bits. The standard unit of memory.**
*Everyday analogy:* Like a phone number — 10 digits that together encode one piece of information.
*Appears in:* Ch01

---

## C

### Cache
**A small, fast memory that stores frequently accessed data.**
*Everyday analogy:* Like a desk drawer where you keep the documents you use most often, instead of walking to the filing cabinet every time.
*Appears in:* Ch01

### Call Stack
**The data structure that tracks active function calls and their local variables.**
*Everyday analogy:* Like a stack of papers on a desk. Each new task goes on top. When you finish a task, you remove it and return to whatever was underneath.
*Appears in:* Ch07

### Compiler
**A program that translates source code (human-readable C) into machine code (computer-readable instructions).**
*Everyday analogy:* Like a translator who converts a recipe from English to French. The meaning stays the same; the form changes.
*Appears in:* Ch02

### Conditional
**A statement that executes different code depending on whether a condition is true or false.**
*Everyday analogy:* "If the manager approves, then sign the order. Otherwise, return it with notes." Decision-making based on conditions.
*Appears in:* Ch05

### CPU (Central Processing Unit)
**The "brain" of the computer that fetches, decodes, and executes instructions.**
*Everyday analogy:* Like a busy reception desk — everything flows through it, and it makes moment-by-moment decisions about what to do next.
*Appears in:* Ch01

---

## D

### Dangling Pointer
**A pointer that references memory that has already been freed. Accessing it causes undefined behavior.**
*Everyday analogy:* Like having the address of a friend who has already moved away. Knocking on that door is unpredictable.
*Appears in:* Ch10

### Data Type
**A classification that specifies which kind of value a variable can hold and what operations can be performed on it.**
*IR Analogy:* Like a form field — "Date of Birth" expects a date, "Country" expects text. You can't reasonably enter a date in the country field.
*Appears in:* Ch03

### Debugging
**The process of finding and fixing bugs in a program.**
*Everyday analogy:* Like investigating why a cake came out flat. You trace back through the steps, check each one, find the mistake, and correct it.
*Appears in:* Ch02

### Declaration
**A statement that introduces a variable or function to the compiler, specifying its name and type.**
*Everyday analogy:* Like reserving a parking space. Before you can park, you must tell the lot that the space exists and is yours.
*Appears in:* Ch03

### Dereference
**To access the value stored at the memory address held by a pointer.**
*Everyday analogy:* You have a friend's address (the pointer). To actually meet the friend, you go to that address and walk through the door. That's dereferencing.
*Appears in:* Ch09

### Dynamic Memory
**Memory allocated at runtime (using `malloc`), as opposed to compile-time (static/automatic).**
*Everyday analogy:* Like renting a storage locker as your belongings grow. You don't know in advance how big you'll need — you request space when you need it and return it when you're done.
*Appears in:* Ch10

---

## F

### Function
**A named block of reusable code that performs a specific task.**
*Everyday analogy:* Like a department within a restaurant. The kitchen handles cooking. You send orders there, it handles them, and returns results. You don't need to know exactly how the kitchen works internally.
*Appears in:* Ch07

---

## H

### Heap
**The region of memory used for dynamic allocation — slower, more flexible, manually managed.**
*Everyday analogy:* Like a large warehouse. You can store anything of any size, but you must explicitly take items back out when you're done with them.
*Appears in:* Ch10

---

## I

### IDE (Integrated Development Environment)
**A tool combining a text editor, compiler, debugger, and other development tools.**
*Everyday analogy:* Like a workbench with all your tools — phone, computer, filing system, reference books — in one organized workspace.
*Appears in:* Ch02

### Include / Header File
**A file (ending in .h) containing declarations that can be shared across multiple source files.**
*Everyday analogy:* Like a shared company contact list. Instead of each team maintaining its own list, there's one official directory everyone references.
*Appears in:* Ch02

### Infinite Loop
**A loop that never terminates because its condition never becomes false.**
*Everyday analogy:* A phone call that never ends because nobody hangs up. "We'll keep talking until we agree on a time" — but the time is never defined.
*Appears in:* Ch06

### Initialization
**Assigning an initial value to a variable at the time of declaration.**
*Everyday analogy:* Like filling in a form. You don't just create the blank field (declare it) — you also write a value into it (initialize it).
*Appears in:* Ch03

### Integer
**A whole number (positive, negative, or zero) with no decimal point.**
*Everyday analogy:* The number of students in a class — 25. Not 25.7. There's no such thing as half a student.
*Appears in:* Ch03

### Iteration
**One complete pass through a loop. Repeating a block of code multiple times.**
*Everyday analogy:* Like multiple rounds of a game. Round 1: Deal cards. Round 2: Play hands. Round 3: Score. Each round is an iteration.
*Appears in:* Ch06

---

## L

### Linked List
**A data structure where each element (node) contains data and a pointer to the next node.**
*Everyday analogy:* Like a train. Each car is connected to the next one. You start at the first car and follow the connections to reach the last.
*Appears in:* Ch13

### Loop
**A programming construct that repeats a block of code while a condition is true.**
*Everyday analogy:* "While the oven is on, keep checking the food." Keep doing something until a condition changes.
*Appears in:* Ch06

---

## M

### Machine Code
**The lowest-level instructions that a CPU directly executes — raw binary.**
*Everyday analogy:* Like the electrical signals in a wire. The person doesn't think in terms of signals; they think in terms of messages. The machine thinks in terms of signals.
*Appears in:* Ch02

### Memory Leak
**Memory that was allocated (with `malloc`) but never freed (`free`), gradually consuming system resources.**
*Everyday analogy:* Like borrowing library books and never returning them. The books remain checked out and unavailable, even though no one is reading them. Eventually, no books are available.
*Appears in:* Ch10

### Modular Programming
**Organizing code into separate, independent, interchangeable modules.**
*Everyday analogy:* Like departments in a company. Finance handles money, HR handles hiring, Marketing handles promotion. Each is independent but can coordinate.
*Appears in:* Ch07

---

## N

### Nested
**Placing one structure inside another of the same kind.**
*Everyday analogy:* Like a box that contains smaller boxes, and one smaller box contains even smaller boxes. Levels within levels.
*Appears in:* Ch06

### Null
**A special value indicating "nothing" or "no address." In C, `NULL` is a pointer that points to nothing.**
*Everyday analogy:* Like a blank address field on a form. It means "nowhere" — if you try to go there, nothing good happens.
*Appears in:* Ch09

---

## P

### Parameter
**A variable in a function definition that receives a value when the function is called.**
*Everyday analogy:* Like a form field on an order form — "Item," "Quantity," "Delivery Address." The form defines what information is expected; the customer fills it in.
*Appears in:* Ch07

### Pointer
**A variable that stores the memory address of another variable.**
*Everyday analogy:* Like the address of a house. The address is not the house itself — it's a piece of paper that tells you where the house is. You can copy the address, share it, or follow it to the actual building.
*Appears in:* Ch09

### Pointer Arithmetic
**Performing arithmetic operations (addition, subtraction) on pointers to navigate through memory.**
*Everyday analogy:* Like knowing that if house #1 is at 100 Maple Street, house #2 is at 104, and house #3 is at 108, you can calculate where the next house is without looking it up.
*Appears in:* Ch09

---

## R

### Recursion
**When a function calls itself. A technique for solving problems by breaking them into smaller, identical subproblems.**
*Everyday analogy:* Like a dictionary definition that uses the word being defined. "Recursion: see recursion." A rule that refers to itself.
*Appears in:* Ch07

### Return Value
**The value a function sends back to the code that called it.**
*Everyday analogy:* Like a shop confirming your order — they process it and send back a decision: "Confirmed" or "Rejected." That's the return value.
*Appears in:* Ch07

---

## S

### Scope
**The region of a program where a variable can be accessed.**
*Everyday analogy:* Like the reach of a rule. A school rule applies to everyone (global scope). A classroom rule applies only within that room (local scope). You can't enforce a classroom rule in another school.
*Appears in:* Ch07

### Segmentation Fault (Segfault)
**A crash caused by accessing memory the program doesn't own or isn't allowed to access.**
*Everyday analogy:* Like trying to open a locked door without the key. The lock stops you, and your attempt fails immediately and dramatically.
*Appears in:* Ch09

### Stack
**The region of memory used for function calls and local variables. Follows Last-In-First-Out (LIFO) order.**
*Everyday analogy:* Like a stack of trays in a cafeteria. The last tray placed on top is the first one taken off. When you finish your meal, your tray is removed and the next one is revealed.
*Appears in:* Ch10

### String
**A sequence of characters (text) in C, stored as an array of `char` and terminated by a null character (`\0`).**
*Everyday analogy:* Like a text message — a sequence of characters that forms a message, with a special marker at the end indicating "message complete."
*Appears in:* Ch08

### Struct
**A user-defined type that groups related variables of different types under one name.**
*Everyday analogy:* Like a student record. A record might contain: Student ID (int), Name (string), Courses (array), Enrollment Date (string), Status (string). All related data grouped together.
*Appears in:* Ch11

### Syntax
**The rules governing the structure of valid code.**
*Everyday analogy:* Like grammar in a language. "The student read the book" is syntactically correct. "Book read student the" is not — the structure is wrong, even though the words are the same.
*Appears in:* Ch02

---

## V

### Variable
**A named storage location in memory that holds a value which can change.**
*Everyday analogy:* Like a labeled box. The label says "Monthly Expenses" — you open it, you find the current number, you can update it. The box itself is the storage; the label is the variable name.
*Appears in:* Ch03

### Virtual Machine
**A software-based emulation of a computer that executes programs as if they were running on physical hardware.**
*Everyday analogy:* Like a flight simulator used for training. It behaves like the real thing, but it's simulated — no real flights happen, no real consequences.
*Appears in:* Ch15

### Void
**A type indicating "nothing" — used for functions that don't return a value, or pointers that point to data of unknown type.**
*Everyday analogy:* Like an email that requests information but expects no direct reply — it's sent, acknowledged, and that's the end.
*Appears in:* Ch07

---

## W

### While Loop
**A loop that repeats as long as a given condition remains true.**
*Everyday analogy:* "While the queue is not empty, keep serving customers." Check the condition first; if it's true, proceed. Check again; if still true, proceed again.
*Appears in:* Ch06

---

## Z

### Zero-Indexing
**The convention (used in C) where the first element of an array is at index 0, not 1.**
*IR Analogy:* Like floor numbering in many countries — the ground floor is 0, not 1. If someone says "take the elevator to floor 3," you go to the fourth floor from ground.
*Appears in:* Ch08
