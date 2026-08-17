# 2.1: Choosing a Computer — What You Really Need

---

## 🎯 Learning Objectives

By the end of this section, you will be able to:

- Determine whether your current computer is sufficient for learning C
- Identify the minimum hardware requirements for this course
- Compare Windows, macOS, and Linux for C development
- Understand that you don't need an expensive machine to start programming

---

## 🧭 The Big Picture

> Imagine you're starting a new job or moving to a new city. You need a desk, a phone, a computer, and some basic supplies. You don't need a corner office in a skyscraper — just a functional workspace.
>
> Programming is the same. You don't need a $3,000 laptop with the latest processor. You need a computer that can run a text editor and a compiler — two pieces of software that could run on a machine from 15 years ago.
>
> This is the shortest section in the course, and also one of the most important. Because if you're worried that your computer isn't good enough, that worry will distract you from learning. Let's put it to rest right now.

---

## 📚 Core Content

### The Truth: Any Computer Will Work

Here's the minimum requirement for this course:

> **A computer manufactured in the last 12 years with at least 4 GB of RAM and 5 GB of free disk space.**

That's it. If you're reading this on a computer, it almost certainly meets this requirement.

Here's why C development has such low requirements:
- C compilers are **tiny** and efficient (GCC is about 50 MB)
- C source code files are **plain text** (a full program might be 10 KB)
- The tools we use are command-line based (no heavy graphics)

| Operating System | Works for C? | Notes |
|-----------------|-------------|-------|
| Windows 10/11 | ✅ Yes | Most common; needs MinGW or WSL |
| macOS (Intel) | ✅ Yes | Xcode CLI tools include everything |
| macOS (Apple Silicon M1-M4) | ✅ Yes | Works great; Rosetta 2 or native ARM |
| Linux (Ubuntu, Fedora, etc.) | ✅ Yes | Best experience; C was born on Unix |
| ChromeOS (with Linux) | ✅ Yes | Enable Linux container |
| Old laptop (2012+) | ✅ Yes | Just needs to turn on and connect to internet |

### Does Processor Speed Matter?

No. For what you're doing in this course:
- **A 2015 laptop** will compile your code in under 1 second
- **A 2025 laptop** will compile your code in under 0.1 seconds
- You won't notice the difference either way

The heavy compilation tasks that benefit from fast processors are things like compiling the Linux kernel or a game engine. Your "Hello, World" program compiles instantly on anything.

### Does RAM Matter?

- **4 GB:** Minimum. Works fine for this course. Close other applications while coding.
- **8 GB:** Comfortable. You can have a browser, editor, and terminal open.
- **16 GB+:** Luxurious. You won't use it for C development.

C code is lightweight. Your operating system uses more RAM than your C development tools ever will.

### Does Graphics Matter?

No. C development happens in a terminal and a text editor. You could do this course on a computer without a graphics card. The most graphically demanding thing you'll do is watch a tutorial video alongside your editor.

### Does Screen Size Matter?

- **13-inch laptop:** Fine. Split the screen between editor and terminal.
- **15-inch+ laptop:** Very comfortable. More room for multiple windows.
- **External monitor:** Nice to have, not necessary.
- **Tablet with keyboard:** Unlikely to work. You need a real operating system.

### What If You Don't Have a Computer?

This is rare, but if you don't have access to a computer:

1. **Public libraries:** Most have computers you can use
2. **University labs:** If you're a student, your institution likely has computer labs
3. **Online sandboxes:** You can write and run C code in a web browser at:
   - [replit.com](https://replit.com/) — Free account, supports C
   - [onlinegdb.com](https://www.onlinegdb.com/) — Free, no account needed
   - [godbolt.org](https://godbolt.org/) — Shows the compiled assembly alongside your code

Online sandboxes aren't ideal for the full course (you'll miss out on using the terminal and compiler directly), but they're perfectly fine for getting started.

### The Bottom Line

| Your Situation | Verdict |
|---------------|---------|
| Have a laptop/desktop from the last 10 years | ✅ You're ready |
| Have a Chromebook with Linux support | ✅ You're ready |
| Have a tablet-only device | ❌ You'll need a computer |
| No computer at all | Use online sandboxes or public computers |

---

## 🧪 Try It Yourself

> **Exercise 1:** Write down your computer's specs:
> - Operating system: _________
> - RAM: _________
> - Free disk space: _________
> - Processor: _________
>
> Does it meet the minimum requirements? (If you're not sure how to check, search online for "how to check my computer specs" for your operating system.)

> **Exercise 2:** If you definitely have a computer (most likely), skip to the next section. If you're not sure, or if you need to use an online sandbox, write down which option you'll use and bookmarks the website now.

---

## 💡 Common Pitfalls

- ❌ **"I need to buy a new computer to learn programming"** — No, you don't. Your current computer is almost certainly fine. If you want to buy a new computer, buy it because you want one — not because you think you need one for this course.

- ❌ **"Macs are better for programming"** — All three major operating systems work well for C. Linux has the smoothest experience, but the differences are small. Use what you already have.

- ❌ **"I should use a cloud computer / remote server"** — Not for learning. You want your editor, terminal, and compiler running on your own machine. The instant feedback loop is essential for learning.

---

## 🔗 Connections to What You Know

> **The most effective people in any field work with what they have.** A chef doesn't wait for the perfect kitchen, a teacher doesn't wait for the perfect classroom, and a negotiator doesn't wait for the perfect briefing room. They assess their available resources and start working.
>
> The same applies here. Your current computer — whatever it is — is sufficient. The tool matters less than the mind using it.

---

## 📖 Further Reading

- [How to Check Your PC Specs (Windows)](https://support.microsoft.com/en-us/windows/see-your-pc-specs)
- [How to Check Your Mac Specs](https://support.apple.com/en-us/HT201581)
- [Online C Compiler (replit.com)](https://replit.com/) — Browser-based alternative

---

## ✅ Section Checklist

- [ ] I checked my computer's specs and confirmed they meet the minimum requirements
- [ ] I understand that I don't need an expensive or new computer for this course
- [ ] If needed, I've bookmarked an online C sandbox as a backup option
- [ ] I wrote a **journal entry** about what I learned today

---

*Next: [2.2: Installing a Compiler →](./02-installing-a-compiler.md)*
