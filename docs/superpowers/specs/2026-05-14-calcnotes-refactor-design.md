# AP Calc BC Notes Refactor — Design Spec

**Date:** 2026-05-14  
**Scope:** All `nX.tex` files across `u1/` and `u2/`, plus `templates/n.tex`  
**Goal:** Consistent formatting, clear language, shared preamble, fixed typos and math errors

---

## Context

These are student fill-in-the-blank note sheets for AP Calculus BC. Blank spaces (`\vspace`, `\underline{\hspace{...}}`) are intentional — students complete them during class. The conversational tone is intentional and should be preserved.

Files in scope:
- `templates/n.tex` — blank template
- `u1/n1.tex` — 1.1 Lines
- `u1/n2.tex` — 1.2 Functions and Graphs
- `u1/n3.tex` — 1.3 Exponential Functions
- `u1/n4.tex` — 1.4 Parametric Equations
- `u1/n5.tex` — 1.5 Functions and Logarithms
- `u1/n6.tex` — 1.6 Trigonometric Functions
- `u2/n1.tex` — 2.1 Rates of Change and Limits

---

## Architecture

### New file: `calcnotes.sty` (project root)

Contains all shared preamble content:

```latex
\usepackage[margin=1in]{geometry}
\usepackage{fancyhdr}
\usepackage{amsmath}
\usepackage{tikz}
\usepackage{pgfplots}
\pgfplotsset{compat=1.18}

\pagestyle{fancy}
\fancyhead[L]{AP Calculus BC}
\fancyfoot[C]{\thepage}

\newcommand{\emptygraph}{...}   % centered 8x7cm grid, ±5 range
\newcommand{\smallgraph}{...}   % 5x4.5cm grid, used in n6 trig panel
```

### Updated `.tex` files

Each file's preamble collapses to:

```latex
\documentclass[11pt]{article}
\input{../calcnotes.sty}
\fancyhead[R]{X.X Lesson Title}

\begin{document}
...
\end{document}
```

`templates/n.tex` uses `\fancyhead[R]{X.X Lesson}` as the placeholder.

---

## Fixes by File

### u1/n1.tex — 1.1 Lines
- Fix typo: "Caclulus" → "Calculus"
- Add `\noindent` to first paragraph after `\begin{document}`
- Center the first data table (currently flush left, second table is centered)
- Remove duplicated preamble; use `\input{../calcnotes.sty}`

### u1/n2.tex — 1.2 Functions and Graphs
- Fix typo: "inverval" → "interval"
- Remove stray `c` after `\end{document}`
- Add `\noindent` to first paragraph
- Fix function definition wording: "assigns a unique element from the domain ($D$) to each element in the range ($R$)" (original had domain and range swapped)
- Remove duplicated preamble; use `\input{../calcnotes.sty}`

### u1/n3.tex — 1.3 Exponential Functions
- Fix table formatting: `\hline` and `\textbf{Year}` were on the same line — split onto separate lines
- Center the U.S. Population table (wrap in `\begin{center}`)
- Remove duplicated preamble; use `\input{../calcnotes.sty}`

### u1/n4.tex — 1.4 Parametric Equations
- Remove local `\emptygraph` definition (now provided by `calcnotes.sty`)
- Remove duplicated preamble; use `\input{../calcnotes.sty}`

### u1/n5.tex — 1.5 Functions and Logarithms
- Fix typo: "the $x$ and $x$" → "the $x$ and $y$"
- Fix typo: "rang" → "range"
- Add missing `\noindent` to "This leads to a question: who cares?"
- Use `\cdot` instead of `\times` in log property math expressions (standard math typesetting)
- Fix missing `\` on second `log_b` in Product and Quotient rules (e.g., `log_b n` → `\log_b n`)
- Add parentheses around product argument: `\log_b m \times n` → `\log_b(mn)`
- Remove local `\emptygraph` definition; use `\input{../calcnotes.sty}`

### u1/n6.tex — 1.6 Trigonometric Functions
- Fix header typo: "Tirgnometric" → "Trigonometric"
- Fix "ona  circle" → "on a circle" (appears twice: lines 60 and 112)
- Remove local `\emptygraph` and `\smallgraph` definitions; use `\input{../calcnotes.sty}`

### u2/n1.tex — 2.1 Rates of Change and Limits
- Fix Sum Rule: remove stray `s` after `L + M`
- Fix Difference Rule: `= L + M` → `= L - M`
- Add missing space after colon in Product Rule label
- Fix Constant Multiple Rule: `\lim_{x\to0}` → `\lim_{x\to c}`
- Fix Quotient Rule: `\lim_{x\to0}` → `\lim_{x\to c}`
- Fix one-sided limit: `lim{x\to 0^+}` → `\lim_{x\to 0^+}` (missing backslash and underscore)
- Standardize `\noindent` usage for consistency with other files
- Remove duplicated preamble; use `\input{../calcnotes.sty}`

---

## What Does NOT Change

- All intentional blank spaces (`\vspace`, `\underline{\hspace{...}}`) for student fill-in
- All empty TikZ axes (students draw on these)
- Conversational/informal tone of questions
- Overall page structure and question flow within each lesson
