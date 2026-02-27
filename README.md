# 🔤 DFA & NFA in NLP — Spell Checker: `color` ↔ `colour`

> An interactive, browser-based demonstration of **Deterministic Finite Automata (DFA)** and **Non-Deterministic Finite Automata (NFA)** applied to a real NLP problem: recognizing American and British English spelling variants using formal automata theory.

[![GitHub](https://img.shields.io/badge/GitHub-Repository-black?style=flat-square&logo=github)](YOUR_GITHUB_LINK_HERE)
[![HTML](https://img.shields.io/badge/Built%20With-HTML%2FJS-orange?style=flat-square&logo=html5)](YOUR_GITHUB_LINK_HERE)
[![NLP](https://img.shields.io/badge/Topic-NLP%20%C3%97%20Formal%20Automata-blue?style=flat-square)]()
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)]()

---

## 📸 Preview

<!-- Replace the path below with your actual screenshot once uploaded to your repo -->
<div align="center">

| | |
|:---:|:---:|
| ![Plot 1](screenshorts/preview.png) | ![Plot 2](screenshorts/preview1.png) |

> *Live demo showing DFA and NFA state traces for the word "colour"*

---

## 📖 What Is This?

This project visually demonstrates how **Finite State Automata** — a core concept in formal language theory and NLP — power real-world spell checkers.

The example uses the word pair **"color" (American English)** and **"colour" (British English)** to show:

- How a **DFA** recognizes both spellings using two completely separate, explicit paths
- How an **NFA** shares a common stem `"col"` and then **branches non-deterministically** on the same symbol `'o'`, exploring both paths in parallel
- How **Levenshtein edit distance** extends automata to accept near-miss misspellings like `"collor"` → suggest `"color"`

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔴 **Live DFA Trace** | Step-by-step state path for exact string matching |
| 🔵 **Live NFA Trace** | Parallel active state sets shown at each character |
| 📊 **Transition Table** | Full δ/Δ table with NFA set notation highlighted |
| 📐 **Automaton Diagrams** | SVG diagrams for both DFA and NFA with labeled states |
| 📏 **Levenshtein Matrix** | Dynamic programming edit distance grid for any input |
| ⚡ **Preset Words** | One-click tests: `color`, `colour`, `collor`, `coler`, `calor` |
| 🌐 **Zero Dependencies** | Pure HTML + vanilla JS — no npm, no build step |

---

## 🚀 How to Run

### Option 1 — Just open the file (simplest)
```bash
# Clone the repo
git clone YOUR_GITHUB_LINK_HERE
cd your-repo-name

# Double-click the file OR open in browser
open spellchecker_dfa_nfa.html       # macOS
start spellchecker_dfa_nfa.html      # Windows
xdg-open spellchecker_dfa_nfa.html   # Linux
```

### Option 2 — VS Code with Live Server (recommended for editing)
1. Open the project folder in **VS Code**
2. Install the **Live Server** extension by Ritwick Dey (`Ctrl+Shift+X` → search "Live Server")
3. Right-click `spellchecker_dfa_nfa.html` → **"Open with Live Server"**
4. Browser opens at `http://127.0.0.1:5500/spellchecker_dfa_nfa.html`

> 💡 Live Server auto-refreshes on every `Ctrl+S` save — great for experimenting with the code.

### Option 3 — Any local HTTP server
```bash
# Python
python -m http.server 8080
# Then visit: http://localhost:8080/spellchecker_dfa_nfa.html
```

---

## 🧠 Theory: DFA vs NFA for Spell Checking

### The Problem
A spell checker must recognize both `"color"` and `"colour"` as correct. They share the prefix `"col"` but diverge at position 4.

### DFA Approach
```
q₀ -c→ q₁ -o→ q₂ -l→ q₃ -o→ qₐ -r→ ACCEPT  (color)
                              ↘
                               qₐ -o→ qᵤ -u→ qᵥ -r→ ACCEPT  (colour)
```
- Two **completely separate** paths after `q₃`
- Transition function: `δ(state, symbol) → one state`
- No branching, no ambiguity — but **structurally redundant**

### NFA Approach
```
q₀ -c→ q₁ -o→ q₂ -l→ q₃ -o→ { q₄ₐ, q₄ᵦ }   ← NON-DETERMINISTIC SPLIT
                                   ↓        ↓
                              q₄ₐ -r→ ACCEPT  (color)
                              q₄ᵦ -u→ q₅ᵦ -r→ ACCEPT  (colour)
```
- **Shared stem** `"col"` processed once
- Transition function: `Δ(state, symbol) → {set of states}`
- At `q₃`, reading `'o'` spawns **both paths simultaneously**
- Accepts if **any** active path reaches a final state

### Key Theorem
Both DFA and NFA recognize exactly the same class of languages (**Regular Languages**). Every NFA can be converted to an equivalent DFA via **Subset Construction**. In NLP practice:

> 🔵 **Design** with NFAs — compact, intuitive for linguistic ambiguity  
> 🔴 **Execute** with DFAs — O(n) speed, no backtracking, production-ready

---

## 📊 Transition Table Summary

| State | Symbol `o` (DFA) | Symbol `o` (NFA) | Notes |
|---|---|---|---|
| q₃ (seen: "col") | `qₐ` — single state | `{q₄ₐ, q₄ᵦ}` — **set of 2** | ★ Branch point |
| All others | Single state or ∅ | Single state or ∅ | Deterministic |

The highlighted row `q₃` is where DFA and NFA formally diverge — the NFA's transition function returning a **set** is the definition of non-determinism.

---

## 🗂️ Project Structure

```
your-repo-name/
│
├── spellchecker_dfa_nfa.html     # Main file — entire app in one HTML file
├── README.md                     # This file
└── screenshots/
    └── preview.png               # Screenshot for README (add your own)
```

---

## 📚 Concepts Covered

- **Formal Language Theory** — Regular languages, FSA, 5-tuple definition
- **DFA** — `δ: Q × Σ → Q` (deterministic transition function)
- **NFA** — `Δ: Q × (Σ ∪ {ε}) → 2^Q` (non-deterministic, returns power set)
- **ε-transitions** — Silent transitions that consume no input
- **Subset Construction** — NFA → DFA conversion algorithm
- **Levenshtein Edit Distance** — Dynamic programming for fuzzy matching
- **Morphological variation** — American vs. British English spelling

---

## 🔗 Related Projects

- [DFA & NFA Theory Reference](YOUR_GITHUB_LINK_HERE) — General automata overview with diagrams
- [Morphological Analyzer](YOUR_GITHUB_LINK_HERE) — DFA & NFA for verb inflections (run/runs/running/ran)

---

## 👤 Author

Made as part of an **NLP × Formal Automata** study series.

> 📬 Found a bug or want to extend this to more word pairs? Open an issue or pull request!

---

## 📄 License

MIT License — free to use, modify, and distribute.
