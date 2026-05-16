# AP Calculus BC — LaTeX Style Guide

This document defines the conventions used across all notes (`n*.tex`) and practice (`p*.tex`) files in this repository. Follow these rules precisely so every document compiles consistently and looks uniform.

---

## File Structure

### Notes files (`nX.tex`)
```latex
\documentclass[11pt]{article}
\input{../calcnotes.sty}
\fancyhead[C]{X.Y Section Title}

\begin{document}
% content
\end{document}
```

### Practice files (`pX.tex`)
```latex
\documentclass[11pt]{article}
\input{../calcpractices.sty}
\fancyhead[C]{X.Y Section Title}

\begin{document}
% content
\end{document}
```

The header center field (`\fancyhead[C]`) always matches the section number and title exactly as it appears in the textbook (e.g., `1.4 Parametric Equations`).

---

## Spacing — All Units in `ex`

**No `cm`, `pt`, `mm`, `in`, or `em` units anywhere in document body.**  
The only exceptions are:
- `\hspace{}` inside `\underline{}` (fill-in blanks) — keep `cm` to control visual blank width
- Coordinates inside `tikz`/`pgfplots` nodes — keep `cm` (tikz coordinate space)
- `\vspace{0pt}` inside `minipage[t]` — layout alignment trick, keep as-is

### Conversion Reference

| Old unit | → | `ex` equivalent |
|----------|---|----------------|
| `0.3cm`  | → | `2ex`          |
| `0.5cm`  | → | `3ex`          |
| `1cm`    | → | `7ex`          |
| `1.5cm`  | → | `10ex`         |
| `2cm`    | → | `13ex`         |
| `3cm`    | → | `20ex`         |
| `4cm`    | → | `26ex`         |
| `5cm`    | → | `33ex`         |
| `3pt`    | → | `1ex`          |
| `1em`    | → | `2ex`          |

### Standard Spacing Values

| Context | Command | Value |
|---------|---------|-------|
| After a problem statement before work space (short) | `\vspace{}` | `8ex` |
| After a problem statement before work space (medium) | `\vspace{}` | `13ex` |
| After a problem statement before work space (large) | `\vspace{}` | `20ex` |
| After a problem statement before work space (extra large) | `\vspace{}` | `26ex` |
| Between instruction text and problems | `\vspace{}` | `2ex` |
| Between multicols blocks | `\vspace{}` | `2ex` |
| After item text before graph in two-column layout | `\\[]` | `1ex` |
| After item text with no graph (short calc) | `\\[]` | `4ex` |
| After item text with no graph (medium calc) | `\\[]` | `6ex` |
| After item text with no graph (long calc) | `\\[]` | `9ex` |
| Inside `cases` environment between rows | `\\[]` | `1ex` |
| Between function label and `\smallgraph` in minipage | `\\[]` | `1ex` |

---

## Graph Commands

Two graph macros are defined in `calcpractices.sty`. Use the correct one based on context.

### `\emptygraph`
- **Size:** 8 cm × 7 cm axis area
- **Range:** x ∈ [−5, 5], y ∈ [−5, 5]
- **Use:** Full-width graphing problems — piecewise functions, trig graphs, large single items

```latex
\item Graph $f(x) = ...$

\emptygraph
```

### `\smallgraph`
- **Size:** 5 cm × 4.5 cm axis area
- **Range:** x ∈ [−5, 5], y ∈ [−5, 5] (sparse tick labels)
- **Use:** Two-column graphing problems — always placed immediately after `\\[1ex]` on the item line

```latex
\begin{multicols}{2}
    \item $\displaystyle y = x^2 - 9$\\[1ex]\smallgraph
    \item $\displaystyle y = -\sqrt{-x}$\\[1ex]\smallgraph
\end{multicols}
```

### Custom inline axes
When the default range is insufficient (trig, scatter plots, Fairbanks-style graphs), write an inline `tikzpicture`/`axis` block directly. Match the axis style of the macros: `axis lines=middle`, `grid=both`, `grid style={dashed, gray!30}`, `tick label style={font=\tiny}`.

---

## Two-Column Layouts

Use `\begin{multicols}{2}` inside `\begin{enumerate}` for side-by-side problems. Always close with `\end{multicols}`.

```latex
\begin{multicols}{2}
    \item Problem A\\[4ex]
    \item Problem B\\[4ex]
\end{multicols}
```

**Rules:**
- Instruction text goes between multicols blocks, outside any `\item`, with `\noindent`
- Use `\begin{multicols}{3}` for three short items (e.g., rewrite-with-base problems)
- Do **not** use multicols for problems that require large answer spaces or have long text — they will collide with numbering labels
- `\vspace{2ex}` between consecutive multicols blocks

---

## Side-by-Side Layouts with `minipage`

For placing a formula next to a graph (piecewise functions, tables next to plots):

```latex
\item \begin{minipage}[t]{0.38\linewidth}
\vspace{0pt}
$\displaystyle f(x) = \begin{cases} ... \end{cases}$
\end{minipage}\hfill%
\begin{minipage}[t]{0.58\linewidth}
\vspace{0pt}
\begin{tikzpicture}
\begin{axis}[axis lines=middle, grid=both, width=7.5cm, height=6.5cm,
    xmin=-5, xmax=5, ymin=-5, ymax=5,
    xtick={-4,-3,...,4}, ytick={-4,-3,...,4},
    xlabel={$x$}, ylabel={$y$},
    tick label style={font=\tiny}, grid style={dashed,gray!30}]
\end{axis}
\end{tikzpicture}
\end{minipage}
```

- Always add `\vspace{0pt}` as the first line inside `minipage[t]` to align tops correctly
- Use `\hfill%` (with `%` to suppress whitespace) between the two minipages
- Left minipage typically `0.38\linewidth`; right `0.58\linewidth`
- For table + plot side-by-side: left `0.30\linewidth`, right `0.66\linewidth`

---

## Math Formatting

- Always wrap inline math that students will read/evaluate in `$\displaystyle ...$`
- Use `\dfrac{}{}` for fractions displayed inline (not `\frac`)
- Use `\left(` / `\right)` for auto-sizing parentheses around tall expressions
- Use `\!\left(` to tighten spacing around function arguments: `f\!\left(g(x)\right)`

---

## Tables

Use `\renewcommand{\arraystretch}{1.3}` (data) or `1.2` (temperature/reference) for row padding. Always wrap the table in a group so the change is local:

```latex
{\renewcommand{\arraystretch}{1.3}
\begin{tabular}{|c|c|}
    \hline
    \textbf{Header 1} & \textbf{Header 2} \\ \hline
    data & data \\ \hline
\end{tabular}}
```

Multi-column header row:
```latex
\multicolumn{2}{|c|}{\textbf{Title}} \\ \hline
```

---

## Lettered Sub-Problems

Use the `enumerate` package (included in both style files) with `[(a)]` for multi-part items:

```latex
\item Find the following.

\begin{enumerate}[(a)]
\begin{multicols}{2}
    \item $\displaystyle f(g(x))$\\[9ex]
    \item $\displaystyle g(f(x))$\\[9ex]
\end{multicols}
\end{enumerate}
```

For non-columnar sub-parts:
```latex
\begin{enumerate}[(a)]
    \item Part one statement.\\[13ex]
    \item Part two statement.\\[13ex]
\end{enumerate}
```

---

## Matching Sections

Matching problems use horizontal rules to frame the section, answer blanks under each item, and `\fbox{}` around each graph:

```latex
\vspace{1ex}
\noindent\rule{\textwidth}{0.8pt}

\noindent\textbf{Match the function with its graph (A--E).} Write the graph letter on the blank.

\vspace{1ex}

\begin{multicols}{5}
    \item $\displaystyle y = 2^x$\\[1ex]
    Graph: \underline{\hspace{1.8cm}}
    % ... remaining items
\end{multicols}

\vspace{2ex}

\begin{center}
\setlength{\tabcolsep}{6pt}
\begin{tabular}{ccccc}
    \fbox{\begin{tikzpicture}...\end{tikzpicture}} & ... \\[1ex]
    \textbf{A} & \textbf{B} & \textbf{C} & \textbf{D} & \textbf{E}
\end{tabular}
\end{center}

\vspace{1ex}
\noindent\rule{\textwidth}{0.8pt}
\vspace{1ex}
```

Mini-graph specs for matching boxes: `width=3cm, height=2.8cm`, no tick labels, `axis lines=middle`.

---

## Page Breaks

Use `\newpage` inside `\begin{enumerate}` between major problem groups (not between individual problems). Place it after closing a multicols block or after a full-width item, before a new instruction heading.

---

## Notes vs. Practice Differences

| Feature | Notes (`calcnotes.sty`) | Practice (`calcpractices.sty`) |
|---------|------------------------|-------------------------------|
| Header right | `Notes` | `Practice` |
| Primary structure | `\noindent` paragraphs | `\begin{enumerate}` |
| Graphs | `\emptygraph` | `\emptygraph` and `\smallgraph` |
| Work space | Not applicable | `\vspace{Xex}` or `\\[Xex]` after items |
| Graph labels in minipage | `\centering label\\[1ex]\smallgraph` | Item inside multicols with `\\[1ex]\smallgraph` |

---

## Quick Reference Cheat Sheet

```
Work space sizes:
  Short answer   →  \vspace{8ex}   or  \\[8ex]
  Medium calc    →  \vspace{13ex}  or  \\[13ex]
  Long calc      →  \vspace{20ex}  or  \\[20ex]
  Full problem   →  \vspace{26ex}  or  \\[26ex]

Between groups:  \vspace{2ex}
After item/graph: \\[1ex]
In cases env:    \\[1ex]
```
