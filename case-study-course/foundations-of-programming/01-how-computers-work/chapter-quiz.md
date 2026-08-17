# 🧪 Chapter 01 Quiz: How Computers Work

**Instructions:** Answer all questions. You must score 70% or higher to proceed to Chapter 02. Complete the quiz without referring back to the chapter content first, then check your answers.

---

## Section 1: Multiple Choice (Select the best answer)

**1.** Why do computers use binary (base-2) instead of decimal (base-10)?
   - A) Binary is easier for humans to read
   - B) Computers are built from switches that have only two states (ON/OFF)
   - C) Binary can represent more numbers than decimal
   - D) Binary was invented before decimal

**2.** How many bits are in one byte?
   - A) 2
   - B) 4
   - C) 8
   - D) 16

**3.** Which logic gate outputs 1 ONLY when both inputs are 1?
   - A) OR gate
   - B) NOT gate
   - C) AND gate
   - D) NAND gate

**4.** Why is the NAND gate called "universal"?
   - A) It's the most common gate in computers
   - B) You can build any other logic gate using only NAND gates
   - C) It's the fastest type of gate
   - D) It's the only gate that works with binary

**5.** In the fetch-decode-execute cycle, what does the Program Counter (PC) do?
   - A) It counts how many programs are running
   - B) It holds the memory address of the next instruction to execute
   - C) It counts how many cycles the CPU has completed
   - D) It stores the result of each instruction

**6.** Which of the following is the CORRECT order from fastest to slowest?
   - A) HDD → RAM → Registers → Cache
   - B) Registers → Cache → RAM → HDD
   - C) Cache → Registers → HDD → RAM
   - D) RAM → Registers → Cache → HDD

**7.** What does "volatile" mean when describing RAM?
   - A) RAM can explode if handled incorrectly
   - B) Data in RAM disappears when power is turned off
   - C) RAM is faster than other types of memory
   - D) RAM wears out after many uses

**8.** What is the Von Neumann bottleneck?
   - A) The CPU can process data faster than it can fetch data from memory
   - B) The CPU cannot perform arithmetic and logic at the same time
   - C) Memory cannot store data when the computer is running
   - D) Programs cannot be larger than the CPU cache

**9.** In the abstraction ladder, what sits directly BELOW the C language layer?
   - A) Python
   - B) Machine code / Assembly language
   - C) Operating system
   - D) The internet

**10.** What is the ASCII code for the character 'A'?
   - A) 1
   - B) 48
   - C) 65
   - D) 97

---

## Section 2: Short Answer (Explain in your own words)

**11.** Explain the fetch-decode-execute cycle as if you were describing a person processing task cards at a desk. Use the analogy of a pile of cards, a checklist, and a desk. (3-5 sentences)

**Your answer (3-5 sentences):**
_______________________________________________
_______________________________________________
_______________________________________________
_______________________________________________
_______________________________________________

**12.** Why is there a memory hierarchy in computers? Why don't we just use one type of fast memory for everything? (2-3 sentences)

**Your answer (2-3 sentences):**
_______________________________________________
_______________________________________________
_______________________________________________

**13.** Explain what abstraction means in the context of computer architecture. How does each layer "hide" the layer below it? Use the examples from Chapter 01. (3-5 sentences)

**Your answer (3-5 sentences):**
_______________________________________________
_______________________________________________
_______________________________________________
_______________________________________________
_______________________________________________

---

## Section 3: Fill in the Blank (Complete the sentence)

**14.** With N bits, you can represent __________ different values. (Write the formula)

**15.** The AND gate's output is 1 when __________.

**16.** The CPU cycle is: __________ → Decode → __________.

**17.** RAM stands for __________ Access Memory.

**18.** A kilobyte (KB) is __________ bytes.

---

## Section 4: Matching (Connect each item)

**19.** Match each memory type to its characteristic:

| Memory Type | Characteristic |
|-------------|---------------|
| 1. Register | A. Holds all running programs; ~4-64 GB |
| 2. Cache | B. Permanent storage; 500 GB+ |
| 3. RAM | C. Built into CPU; ~1 KB; fastest |
| 4. Storage (SSD/HDD) | D. Between CPU and RAM; ~1-32 MB |

**Answers:** 1-___  2-___  3-___  4-___

---

## Section 5: Practical Application

**20.** You're explaining to a friend how a computer works. They ask: "So when I press a key on my keyboard, how does that become a letter on the screen?" Based on everything in Chapter 01, write a 3-5 sentence explanation that traces the path from keyboard to screen.

**Your answer (3-5 sentences):**
_______________________________________________
_______________________________________________
_______________________________________________
_______________________________________________
_______________________________________________

---

## 📊 Answer Key

*(Check your answers here after completing the quiz.)*

| Question | Answer | Explanation |
|----------|--------|-------------|
| 1 | B | Computers are built from switches (transistors) with two states: ON (1) and OFF (0). Binary matches this hardware reality. |
| 2 | C | 1 byte = 8 bits. A byte can represent 2⁸ = 256 different values. |
| 3 | C | AND gate: output is 1 only when BOTH inputs are 1. All other combinations produce 0. |
| 4 | B | NAND is universal because you can construct AND, OR, NOT, XOR — any gate — using only NAND gates. |
| 5 | B | The Program Counter holds the address of the next instruction. It's automatically incremented after each fetch. |
| 6 | B | Fastest to slowest: Registers → Cache → RAM → HDD. Each level is ~10-100x slower than the one above. |
| 7 | B | Volatile memory loses its data when power is removed. This is why you need storage (non-volatile) for permanent data. |
| 8 | A | The CPU can process data faster than it can fetch it from memory. Cache helps hide this bottleneck. |
| 9 | B | Machine code / Assembly language sits directly below C. The compiler translates C into assembly, then assembler into machine code. |
| 10 | C | 'A' = 65. (Lowercase 'a' = 97 — they differ by 32, just one bit.) |
| 11 | (Model) | The person has a pile of task cards (instructions). They look at their checklist (Program Counter) to know which card is next. They pick up that card (fetch), read it (decode), and do what it says (execute). Then they check the next item on the list and repeat. |
| 12 | (Model) | Fast memory is physically different and much more expensive than slow memory. Registers and cache are built directly on the CPU chip, which has limited space. A balance of size, speed, and cost creates the hierarchy. |
| 13 | (Model) | Abstraction means each layer provides a simpler interface while hiding complexity. Transistors hide behind gates. Gates hide behind machine code. Machine code hides behind assembly. Assembly hides behind C. Each layer makes the next one possible. |
| 14 | 2^N | N bits → 2^N different values. 1 bit → 2 values. 8 bits → 256 values. |
| 15 | both inputs are 1 | AND gate: 1 AND 1 = 1. All other combinations = 0. |
| 16 | Fetch / Execute | The full cycle is: Fetch → Decode → Execute → (repeat). |
| 17 | Random | RAM = Random Access Memory. "Random" means any address can be accessed in the same time. |
| 18 | 1024 | 1 KB = 1024 bytes (2^10). (Hard drive manufacturers sometimes use 1000, but in programming, it's 1024.) |
| 19 | 1-C, 2-D, 3-A, 4-B | Register (1-C), Cache (2-D), RAM (3-A), Storage (4-B). |
| 20 | (Model) | Pressing a key sends an electrical signal to the keyboard controller, which converts it to a scan code. The CPU reads this code via an interrupt. The operating system translates the scan code to an ASCII value (e.g., 'A' = 65). This value is stored in RAM as a binary number, then the graphics system reads it and renders the letter on your screen by lighting specific pixels. |

---

## 📝 Reflection Prompt

After completing this quiz, write 2-3 sentences in your learning journal about:

- **What felt easy** — which concepts from Chapter 01 are solidifying?
- **What felt difficult** — which ideas need more review?
- **How would I explain today's topics to someone else?**
- **What's your favorite new mental model from this chapter?**

---

## 📊 Quiz Scoring Guide

| Score | Interpretation |
|-------|---------------|
| **90-100%** | Strong foundation. Move to Chapter 02. |
| **70-89%** | Good understanding. Review missed concepts briefly, then proceed. |
| **50-69%** | Surface understanding. Review the chapter again, especially the sections you missed. |
| **< 50%** | Concepts haven't clicked yet. Re-read the chapter, redraw the diagrams from memory, retake the quiz. |

*Target score: 70% or higher to proceed. You've built a foundation that will serve you through the entire course.*
