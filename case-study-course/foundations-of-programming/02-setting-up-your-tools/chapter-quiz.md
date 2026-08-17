# 📝 Chapter 2 Quiz — Setting Up Your Tools

---

**Chapter:** 02 — Setting Up Your Tools
**Total Questions:** 20
**Estimated Time:** 20–30 minutes

---

## Section 1: Multiple Choice (Select the best answer)

**1. What is the minimum RAM requirement for this course?**

a) 2 GB
b) 4 GB
c) 8 GB
d) 16 GB

**2. Which command shows your current location in the file system?**

a) `ls`
b) `cd`
c) `pwd`
d) `cat`

**3. What does the `-o` flag do in the command `gcc hello.c -o hello`?**

a) Optimize the code
b) Name the output executable "hello"
c) Open the file for editing
d) Output warnings to a file

**4. What does the `#include <stdio.h>` line do?**

a) It tells the compiler to print text to the screen
b) It inserts the contents of the standard input/output header file
c) It includes your current file in another program
d) It checks the system time

**5. What happens during the linking stage of compilation?**

a) C code is translated to assembly language
b) Assembly code is converted to machine code
c) The preprocessor inserts header file contents
d) Object files and libraries are combined into an executable

**6. Which command is used to create a new directory in the terminal?**

a) `touch`
b) `newdir`
c) `mkdir`
d) `createdir`

**7. What does `return 0;` in `main()` signify?**

a) The program has a bug
b) The program finished with an error
c) The program finished successfully
d) The program is waiting for input

**8. Which compilation flag enables all common warnings?**

a) `-Werror`
b) `-O2`
c) `-Wall`
d) `-g`

---

## Section 2: Short Answer (Explain in your own words)

**9. Why are `.o` (object) files not directly runnable?**

*Your answer:*

**10. What is the difference between `mv hello.c main.c` and `mv hello.c ../backup/`?**

*Your answer:*

**11. Why does the first compilation of "Hello, World!" produce an executable that's much larger than your 6-line source file?**

*Your answer:*

---

## Section 3: Fill in the Blank (Complete the sentence)

**12.** The ________ stage of compilation translates C code into assembly language.

**13.** The terminal command to move up one directory level is `cd _____`.

**14.** Every C statement must end with a ________.

**15.** To view the contents of a file in the terminal without opening an editor, use the ________ command.

**16.** The special character sequence `\n` in a printf string adds a ________.

---

## Section 4: Matching (Connect each item)

**17. Match each compilation stage to its output:**

| Stage | Output |
|-------|--------|
| 1. Preprocessing | a) `hello.o` (machine code object file) |
| 2. Compilation (strict) | b) `hello` (executable) |
| 3. Assembling | c) Preprocessed C code (thousands of lines) |
| 4. Linking | d) `hello.s` (assembly language code) |

**18. Match each terminal command to its description:**

| Command | Description |
|---------|-------------|
| 1. `cd` | a) List files and directories |
| 2. `ls` | b) Print working directory |
| 3. `pwd` | c) Change directory |
| 4. `rm` | d) Delete a file (permanent!) |

---

## Section 5: Practical Application

**19. You've written the following program but it won't compile. Find and fix the errors:**

```c
#include <stdio.h>

int MAIN(void)
{
    printf("Hello, World!\n")
    return 0
}
```

List the errors you found and write the corrected version:

*Your answer:*

**20. Walk through the complete process of creating, compiling, and running a new C program called `first.c` that prints "I am learning C!" Write the exact terminal commands you would use, starting from an empty terminal.**

*Your answer:*

---

## 📋 Answer Key

### Section 1: Multiple Choice

1. **b)** 4 GB — This is the minimum. 8 GB is comfortable, but 4 GB works fine. *(Section 2.1)*
2. **c)** `pwd` — Print Working Directory. `ls` lists files, `cd` changes directory, `cat` views file contents. *(Section 2.3)*
3. **b)** Name the output executable "hello" — Without `-o`, the default output is `a.out`. *(Section 2.4)*
4. **b)** It inserts the contents of `stdio.h` — The preprocessor finds and includes the header file. *(Section 2.4)*
5. **d)** Object files and libraries are combined into an executable — The linker resolves external function calls like `printf`. *(Section 2.5)*
6. **c)** `mkdir` — Make Directory. `touch` creates files, `newdir` is not a command. *(Section 2.3)*
7. **c)** The program finished successfully — `0` means success. Non-zero values indicate errors. *(Section 2.4)*
8. **c)** `-Wall` — "All Warnings." `-Werror` treats warnings as errors, `-O2` optimizes, `-g` adds debug info. *(Section 2.5)*

### Section 2: Short Answer

9. **Model answer:** Object files contain machine code but have unresolved references to external functions (like `printf`). They need the linker to combine them with library code before they can run. An object file is like a chapter of a book — it needs the rest of the book and the binding to be complete.

10. **Model answer:** `mv hello.c main.c` renames the file within the same directory. `mv hello.c ../backup/` moves the file into a different directory (`../backup/`) without renaming it. Both use the same `mv` command, but the destination determines whether it's a rename or a move.

11. **Model answer:** The executable includes not just your code, but also the linked library code for `printf`, startup code that runs before `main()`, operating-system-specific executable headers, and other overhead. The `#include` directive also inserted hundreds of lines from `stdio.h` during preprocessing.

### Section 3: Fill in the Blank

12. **compilation** (or **compiling**) — The second stage (strict sense) translates C to assembly.
13. **..** — Two dots represent the parent directory.
14. **semicolon** (`;`) — Every statement in C ends with a semicolon.
15. **cat** — Short for "concatenate," displays file contents to the terminal.
16. **newline** — It moves the cursor to the next line.

### Section 4: Matching

17. **1 → c, 2 → d, 3 → a, 4 → b**
    - Preprocessing → Preprocessed C code (thousands of lines)
    - Compilation (strict) → Assembly code (`hello.s`)
    - Assembling → Object file (`hello.o`)
    - Linking → Executable (`hello`)

18. **1 → c, 2 → a, 3 → b, 4 → d**
    - `cd` → Change directory
    - `ls` → List files
    - `pwd` → Print working directory
    - `rm` → Delete a file (permanent)

### Section 5: Practical Application

19. **Three errors found:**
    1. `int MAIN(void)` should be `int main(void)` — C is case-sensitive; `main` must be lowercase
    2. Missing semicolon after `printf("Hello, World!\n")` — Every statement ends with `;`
    3. Missing semicolon after `return 0` — Same as above

    **Corrected version:**
    ```c
    #include <stdio.h>

    int main(void)
    {
        printf("Hello, World!\n");
        return 0;
    }
    ```

20. **Model answer:**
    ```bash
    # 1. Create the C source file (using touch, then editing with VS Code)
    touch first.c

    # 2. Edit first.c to contain:
    #    #include <stdio.h>
    #    int main(void)
    #    {
    #        printf("I am learning C!\n");
    #        return 0;
    #    }

    # 3. Compile the program
    gcc -Wall -Wextra first.c -o first

    # 4. Run the program
    ./first
    # (or: first.exe on Windows Command Prompt)
    ```

---

## 📊 Quick Self-Assessment

| Score (out of 20) | Assessment | Recommended Action |
|:-----------------:|-----------|-------------------|
| 18–20 | 🎉 Excellent | You're ready for Chapter 3! |
| 14–17 | ✅ Good | Review Sections 2.3 and 2.5 (terminal and compilation) |
| 10–13 | 🔄 Fair | Re-read Sections 2.2–2.5 and retry the hands-on exercises |
| Below 10 | 🔁 Needs Review | Re-read the full chapter and ensure you've done all the Try It Yourself exercises |

---

*→ When you're ready, continue to [Chapter 3: Variables and Data Types →](../03-variables-data-types/01-what-is-a-variable.md)*
