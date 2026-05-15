# AP Calc BC Notes Refactor — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Extract a shared `calcnotes.sty` preamble with 1-inch margins and fix all typos, math errors, and formatting inconsistencies across 8 lesson note files.

**Architecture:** Create `calcnotes.sty` at the project root containing all shared packages, page setup, and graph commands. Each `.tex` file replaces its full preamble with `\input{../calcnotes.sty}` and one `\fancyhead[R]{...}` line for its lesson title. All per-file typos, math errors, and inconsistencies are fixed in the same pass.

**Tech Stack:** LaTeX (pdflatex), fancyhdr, amsmath, tikz, pgfplots, geometry

---

### File Map

| Action | File | Purpose |
|--------|------|---------|
| Create | `calcnotes.sty` | Shared packages, margins, header/footer, `\emptygraph`, `\smallgraph` |
| Modify | `templates/n.tex` | Blank lesson template |
| Modify | `u1/n1.tex` | 1.1 Lines |
| Modify | `u1/n2.tex` | 1.2 Functions and Graphs |
| Modify | `u1/n3.tex` | 1.3 Exponential Functions |
| Modify | `u1/n4.tex` | 1.4 Parametric Equations |
| Modify | `u1/n5.tex` | 1.5 Functions and Logarithms |
| Modify | `u1/n6.tex` | 1.6 Trigonometric Functions |
| Modify | `u2/n1.tex` | 2.1 Rates of Change and Limits |

---

### Task 1: Create calcnotes.sty

**Files:**
- Create: `calcnotes.sty`

- [ ] **Step 1: Create `calcnotes.sty` at the project root with this exact content**

```latex
\usepackage[margin=1in]{geometry}
\usepackage{fancyhdr}
\usepackage{amsmath}
\usepackage{tikz}
\usepackage{pgfplots}
\pgfplotsset{compat=1.18}

\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{AP Calculus BC}
\fancyfoot[C]{\thepage}

\newcommand{\emptygraph}{
    \begin{center}
    \begin{tikzpicture}
        \begin{axis}[
            axis lines = middle,
            grid = both,
            width=8cm,
            height=7cm,
            xmin=-5, xmax=5,
            ymin=-5, ymax=5,
            xtick={-4,-3,...,4},
            ytick={-4,-3,...,4},
            xlabel={$x$},
            ylabel={$y$},
            tick label style={font=\tiny},
            grid style={dashed, gray!30}
        ]
        \end{axis}
    \end{tikzpicture}
    \end{center}
}

\newcommand{\smallgraph}{
    \begin{tikzpicture}
        \begin{axis}[
            axis lines = middle,
            grid = both,
            width=5cm,
            height=4.5cm,
            xmin=-5, xmax=5,
            ymin=-5, ymax=5,
            xtick={-4,-2,0,2,4},
            ytick={-4,-2,0,2,4},
            tick label style={font=\tiny},
            grid style={dashed, gray!30}
        ]
        \end{axis}
    \end{tikzpicture}
}
```

- [ ] **Step 2: Commit**

```bash
git add calcnotes.sty
git commit -m "Add shared calcnotes.sty style file"
```

---

### Task 2: Update templates/n.tex

**Files:**
- Modify: `templates/n.tex`

- [ ] **Step 1: Replace the file with this exact content**

```latex
\documentclass[11pt]{article}
\input{../calcnotes.sty}
\fancyhead[R]{X.X Lesson}

\begin{document}

\end{document}
```

- [ ] **Step 2: Compile to verify**

```
pdflatex templates/n.tex
```
Expected: `Output written on n.pdf` with no errors.

- [ ] **Step 3: Commit**

```bash
git add templates/n.tex
git commit -m "Update template to use shared calcnotes.sty"
```

---

### Task 3: Update u1/n1.tex — 1.1 Lines

**Files:**
- Modify: `u1/n1.tex`

Changes: replace preamble; fix "Caclulus" → "Calculus"; add `\noindent` to first paragraph; center first data table; fix "parallel / perpendicular" phrasing.

- [ ] **Step 1: Replace the file with this exact content**

```latex
\documentclass[11pt]{article}
\input{../calcnotes.sty}
\fancyhead[R]{1.1 Lines}

\begin{document}

\noindent Calculus is a different type of math. In most algebra classes, we talk about exact amounts, or inequalities that are exact. Calculus deals with quantities that are changing, rates of change, and increments. The increment is defined as

\[\Delta x = x_2 - x_1 \text{ and } \Delta y = y_2 - y_1\]

\noindent This looks just like the slope of a line:

\vspace{1.5cm}

\noindent Which often leads us straight to point-slope form:

\vspace{1.5cm}

\noindent Which often leads us straight to slope-intercept form:

\vspace{1.5cm}

\noindent Which sometimes leads us to the General Linear Equation:

\vspace{1.5cm}

\noindent (Did we always call it that?)

\vspace{1.5cm}

\noindent Find the slope of a line through the points $(3,-2)$ and $(4,1)$. Write the equation of a line in all three forms.

\vspace{1.5cm}

\noindent What about parallel and perpendicular lines? Write an equation for a line through the point $(-1,2)$ that is parallel and perpendicular to the line $y=3x-4$.

\newpage

\noindent What line is perpendicular to the line $x=-3$ and goes through the point $(-3,4)$?

\vspace{1.5cm}

\noindent How would we find the equation of a line given the data below (and what is the $f(x)$ notation)?

\vspace{1cm}

\begin{center}
\begin{tabular}{ |c|c| }
    \hline
    $x$ & $f(x)$ \\
    \hline
    -1 & $\frac{14}{3}$ \\
    1 & $\frac{-4}{3}$ \\
    2 & $\frac{-13}{3}$ \\
    \hline
\end{tabular}
\end{center}

\vspace{1cm}

\noindent Try it again with Fahrenheit and Celsius (what temperatures do you already know about these two scales?).

\vspace{1.5cm}

\noindent And finally, how do you model a whole set of data? By hand? By calculator? Find a linear model for the world population shown.

\vspace{1cm}

\begin{center}
    \begin{tabular}{|c|c|}
        \hline
        \multicolumn{2}{|c|}{\textbf{World Population}} \\ \hline
        \textbf{Year} & \textbf{Population (millions)} \\ \hline
        1980 & 4454 \\ \hline
        1985 & 4853 \\ \hline
        1990 & 5285 \\ \hline
        1995 & 5696 \\ \hline
        2003 & 6305 \\ \hline
        2004 & 6378 \\ \hline
        2005 & 6450 \\ \hline
    \end{tabular}
\end{center}

\end{document}
```

- [ ] **Step 2: Compile to verify**

```
pdflatex u1/n1.tex
```
Expected: `Output written on n1.pdf` with no errors.

- [ ] **Step 3: Commit**

```bash
git add u1/n1.tex
git commit -m "Refactor n1: shared preamble, fix typo, center first table"
```

---

### Task 4: Update u1/n2.tex — 1.2 Functions and Graphs

**Files:**
- Modify: `u1/n2.tex`

Changes: replace preamble; fix function definition (domain maps to range, not range to domain); fix "inverval" → "interval"; add `\noindent` to first paragraph; fix "by graphing it" → "by looking at its graph"; remove stray `c` after `\end{document}`.

- [ ] **Step 1: Replace the file with this exact content**

```latex
\documentclass[11pt]{article}
\input{../calcnotes.sty}
\fancyhead[R]{1.2 Functions and Graphs}

\begin{document}

\noindent The values of one variable often depend on another. We call this a function. We define a function as a rule that assigns a \underline{\hspace{2cm}} element of the range ($R$) to each element in the domain ($D$). Counter-examples:

\vspace{1.5cm}

\noindent Since the purpose of mathematics is to model the world, a function is pretty important. We write a function as:

\vspace{1.5cm}

\noindent What is the function that expresses the area of a circle?

\vspace{1.5cm}

\noindent Domain is the \underline{\hspace{2cm}}. Range is the \underline{\hspace{2cm}}. What are the domain and range for the circle function?

\vspace{1.5cm}

\noindent What is interval notation? Show $-3 < x \le 6$ with interval notation (and any other way you can think of). What about for the circle above?

\noindent Identify the domain and range of the following graphs. Use interval notation.

\vspace{0.5cm}

\begin{align*}
    y=\frac{1}{x} && y=\sqrt{x}
\end{align*}

\vspace{0.5cm}

\begin{align*}
    y=\sqrt{4-x^2} && y=x^\frac{2}{3}
\end{align*}

\newpage

\noindent What is the definition of an even function? An odd function?

\vspace{1.5cm}

\noindent How do we know if a function is even or odd by looking at its graph?

\vspace{1.5cm}

\noindent Determine if the following functions are odd, even, or neither.

\begin{align*}
    f(x) = x^2 && f(x) = x^2 + 1 && f(x) = x && f(x) = x + 1
\end{align*}

\vspace{1.5cm}

\noindent How do we graph a piecewise function? Graph and find the domain and range:

\vspace{0.5cm}

\noindent
\begin{minipage}[c]{0.5\textwidth}
\[f(x) =
\begin{cases}
    -x, & x < 0 \\
    x^2, & 0 \le x \le 1 \\
    1, & x > 1
\end{cases}
\]

\vspace{1cm}
\noindent Domain: \underline{\hspace{4cm}}

\vspace{0.8cm}
\noindent Range: \underline{\hspace{4cm}}
\end{minipage}
\begin{minipage}[c]{0.5\textwidth}
\centering
\begin{tikzpicture}
    \begin{axis}[
        axis lines = middle,
        xlabel = $x$,
        ylabel = $y$,
        xmin = -3, xmax = 3,
        ymin = -1, ymax = 4,
        xtick={-2,-1,1,2},
        ytick={1,2,3},
        grid = both,
        grid style={line width=.1pt, draw=gray!10},
        major grid style={line width=.2pt,draw=gray!50},
        width=6cm,
        height=6cm,
        tick label style={font=\tiny}
    ]
    \end{axis}
\end{tikzpicture}
\end{minipage}

\newpage

\noindent Graph the following: $f(x) = |x - 2| + 3$. Then write it as a piecewise function. Also find the domain and range.

\vspace{0.5cm}

\noindent
\begin{minipage}[t]{0.5\textwidth}
    \centering
    \begin{tikzpicture}
        \begin{axis}[
            axis lines = middle,
            xlabel = $x$,
            ylabel = $y$,
            xmin = -1, xmax = 6,
            ymin = -1, ymax = 7,
            xtick={-1,0,1,2,3,4,5},
            ytick={1,2,3,4,5,6},
            grid = both,
            grid style={line width=.1pt, draw=gray!10},
            major grid style={line width=.2pt,draw=gray!50},
            width=6.5cm,
            height=6.5cm,
            tick label style={font=\tiny}
        ]
        \end{axis}
    \end{tikzpicture}
\end{minipage}

\vspace{1cm}

\noindent Finally, what is a composite function? If $f(x) = x - 7$ and $g(x) = x^2$, what is $f(g(x))$? What is $(f \circ g)(x)$? What is $g(f(2))$?

\vspace{1.5cm}

\noindent Composite functions are used a lot in Calculus.

\vspace{1.5cm}

\end{document}
```

- [ ] **Step 2: Compile to verify**

```
pdflatex u1/n2.tex
```
Expected: `Output written on n2.pdf` with no errors.

- [ ] **Step 3: Commit**

```bash
git add u1/n2.tex
git commit -m "Refactor n2: shared preamble, fix function definition, fix typos"
```

---

### Task 5: Update u1/n3.tex — 1.3 Exponential Functions

**Files:**
- Modify: `u1/n3.tex`

Changes: replace preamble; change `\begin{flushleft}` graph to `\begin{center}`; fix table formatting (split `\hline` and `\textbf{Year}` onto separate lines); wrap table in `\begin{center}`; fix "growth / decay" → "growth and decay".

- [ ] **Step 1: Replace the file with this exact content**

```latex
\documentclass[11pt]{article}
\input{../calcnotes.sty}
\fancyhead[R]{1.3 Exponential Functions}

\begin{document}

\noindent An exponential function is defined as:

\vspace{1.5cm}

\noindent What are the two types of exponential functions? What do they look like?

\vspace{1.5cm}

\noindent Graph $y=2(3^x)-4$ and state the domain and range.

\begin{center}
\begin{tikzpicture}
\begin{axis}[
    axis lines = middle,
    grid = both,
    xlabel = {$x$},
    ylabel = {$y$},
    xmin = -4, xmax = 4,
    ymin = -6, ymax = 10,
    xtick = {-4,-3,...,4},
    ytick = {-6,-4,...,10},
    width = 8cm,
    height = 8cm,
    tick label style={font=\tiny},
    minor tick num=1
]
\end{axis}
\end{tikzpicture}
\end{center}

\noindent Find the zero of $f(x)=5-2.5^x$ algebraically and graphically with a calculator.

\vspace{1.5cm}

\noindent Quick reminder of rules for exponents:

\begin{align*}
    x^5 \times x^2 = && \frac{x^5}{x^2} = && (x^5)^2 =\\
    (x^5 \times x^2)^3 = && \left(\frac{x^5}{x^2}\right)^3 = && \frac{1}{x^4} =
\end{align*}

\vspace{0.5cm}

\noindent How do we model an exponential function? Model by hand and calculator:

\vspace{0.5cm}

\begin{center}
\begin{tabular}{|c|c|}
    \hline
    \multicolumn{2}{|c|}{\textbf{U.S. Population}} \\ \hline
    \textbf{Year} & \textbf{Population (millions)} \\ \hline
    2002 & 287.9 \\ \hline
    2003 & 290.4 \\ \hline
    2004 & 293.2 \\ \hline
    2005 & 295.5 \\ \hline
\end{tabular}
\end{center}

\vspace{0.5cm}

\noindent What is the population today?

\newpage

\noindent What other ways can we model exponential growth and decay? What is a half-life?

\vspace{1.5cm}

\noindent What is the yearly percent increase in US Population?

\vspace{1.5cm}

\noindent What is that number $e$? How can we approximate it with: $f(x)=\left(1+\frac{1}{x}\right)^x$

\end{document}
```

- [ ] **Step 2: Compile to verify**

```
pdflatex u1/n3.tex
```
Expected: `Output written on n3.pdf` with no errors.

- [ ] **Step 3: Commit**

```bash
git add u1/n3.tex
git commit -m "Refactor n3: shared preamble, fix table formatting, center graph"
```

---

### Task 6: Update u1/n4.tex — 1.4 Parametric Equations

**Files:**
- Modify: `u1/n4.tex`

Changes: replace preamble (removes local `\emptygraph` definition, now provided by `calcnotes.sty`); add `\ ` spacing in math for readability; consistent `\quad` separators in displayed equations.

- [ ] **Step 1: Replace the file with this exact content**

```latex
\documentclass[11pt]{article}
\input{../calcnotes.sty}
\fancyhead[R]{1.4 Parametric Equations}

\begin{document}

\noindent And now for something completely different: parametric equations. Why? The best way to understand is to look at something in motion:

\vspace{1cm}

\noindent We can describe motion in a coordinate plane, but we cannot also show the time of motion. To do that, we introduce a third variable, $t$, called a parameter. Bad news: this is challenging. Good news: we can use our calculator.

\vspace{1cm}

\noindent Describe the graph of the relation determined by $x = \sqrt{t},\ y = t,\ t \ge 0$. Indicate the direction in which the curve is traced and find the Cartesian equation.

\emptygraph

\noindent Notice how important domain is\dots we call the domain $I$ the parameter interval.

\vspace{0.5cm}

\noindent \textbf{Definition:} If $x$ and $y$ are given as functions $x = f(t),\ y = g(t)$ over an interval of $t$-values, then the set of points $(x,y) = (f(t), g(t))$ defined by these equations is a \textbf{parametric curve}. The equations are \textbf{parametric equations} for the curve.

\newpage

\noindent Also notice that direction matters\dots the parameter $t$ determines where the curve starts and ends. Describe the graph of the relation determined by the following. Determine initial and terminal points and find the Cartesian equation.

\[x = 2\cos t,\quad y = 2\sin t,\quad 0 \le t \le 2\pi\]

\emptygraph

\noindent Graph the parametric curve: $x = 3\cos t,\quad y = 4\sin t,\quad 0 \le t \le 2\pi$

\emptygraph

\newpage

\noindent At this point, you might think that parametric equations are used primarily for graphs of conics. However, we can also graph a line segment. Draw and identify the graph of the parametric curve: $x = 3t,\ y=2-2t,\ 0 \le t \le 1$

\emptygraph

\noindent Find a parameterization for the line segment with endpoints $(-2,1)$ and $(3,5)$.

\vspace{4cm}

\end{document}
```

- [ ] **Step 2: Compile to verify**

```
pdflatex u1/n4.tex
```
Expected: `Output written on n4.pdf` with no errors.

- [ ] **Step 3: Commit**

```bash
git add u1/n4.tex
git commit -m "Refactor n4: shared preamble, remove local emptygraph definition"
```

---

### Task 7: Update u1/n5.tex — 1.5 Functions and Logarithms

**Files:**
- Modify: `u1/n5.tex`

Changes: replace preamble; fix "the $x$ and $x$" → "the $x$ and $y$"; fix missing `x` in function `-2 + 4` → `-2x + 4`; fix "rang" → "range"; add `\noindent` to "This leads to a question"; fix log properties (missing `\` on second `\log_b`, parentheses around product argument, `\cdot` instead of `\times`); fix "Sarah invest" → "Sarah invests"; use `\cdot` for multiplication.

- [ ] **Step 1: Replace the file with this exact content**

```latex
\documentclass[11pt]{article}
\input{../calcnotes.sty}
\fancyhead[R]{1.5 Functions and Logarithms}

\begin{document}

\noindent What is a function?

\vspace{1.5cm}

\noindent What is a one-to-one function?

\noindent Definition: a function $f(x)$ is one-to-one on domain $D$ if $f(a) \neq f(b)$ whenever $a \neq b$ (note that we can make a function one-to-one by \underline{\hspace{2cm}}).

\noindent This leads to a question: who cares?

\vspace{1.5cm}

\noindent An inverse means that we took the $x$ and $y$ (or $f(x)$) and flipped them. Find the inverse of $y = f(x) = -2x + 4$.

\vspace{1.5cm}

\noindent Graph the function and its inverse. What is $(f \circ g)(x)$?

\emptygraph

\noindent Do all of that again for $f(x) = x^2,\ x > 0$. This time do it parametrically.

\emptygraph

\noindent What is the inverse of $y=a^x\ (a > 0,\ a \neq 1)$? (Why the limitations?)

\vspace{1.5cm}

\noindent What is the domain and range of \underline{\hspace{3cm}}? Graph:

\emptygraph

\noindent Quick refresher: write the inverse of $y = \log_2 x$ and $y = 3^x$.

\vspace{1.5cm}

\noindent What do we call $y = \ln x$? What is the base? What about $y = \log x$?

\vspace{1.5cm}

\noindent Refresh on log properties.

\noindent Solve for $x$:

\begin{align*}
    \ln x = 3t + 5 && e^{2x} = 10
\end{align*}

\noindent Properties of logarithms:

\begin{itemize}
    \item Product: $\log_b(mn) = \log_b m + \log_b n$
    \item Quotient: $\log_b \frac{m}{n} = \log_b m - \log_b n$
    \item Power: $\log_b m^p = p \cdot \log_b m$
\end{itemize}

\noindent How about the change of base formula? Use it to graph $f(x) = \log_2 x$.

\emptygraph

\noindent Application: Sarah invests \$1000 in an account that earns 5.25\% interest compounded annually. How long will it take the account to reach \$2500?

\end{document}
```

- [ ] **Step 2: Compile to verify**

```
pdflatex u1/n5.tex
```
Expected: `Output written on n5.pdf` with no errors.

- [ ] **Step 3: Commit**

```bash
git add u1/n5.tex
git commit -m "Refactor n5: shared preamble, fix typos, fix log property math"
```

---

### Task 8: Update u1/n6.tex — 1.6 Trigonometric Functions

**Files:**
- Modify: `u1/n6.tex`

Changes: replace preamble (removes local `\emptygraph` and `\smallgraph` definitions); fix header "Tirgnometric" → "Trigonometric"; fix "ona  circle" → "on a circle" (two occurrences); fix "Why? Why not?" → "Why or why not?".

- [ ] **Step 1: Replace the file with this exact content**

```latex
\documentclass[11pt]{article}
\input{../calcnotes.sty}
\fancyhead[R]{1.6 Trigonometric Functions}

\begin{document}

\noindent What's a radian? Why do we use it?

\vspace{1.5cm}

\noindent Find the length of an arc subtended on a circle of radius $3$ by a central angle of measure $\frac{2\pi}{3}$.

\vspace{1.5cm}

\noindent Remember this? I hope so\dots

\vspace{0.5cm}

\begin{center}
\begin{tikzpicture}[scale=3.0]
    \draw[thick, green!70!black] (0,0) circle(1);
    \draw[->, blue!80!black, thick] (-1.45,0) -- (1.45,0);
    \draw[->, blue!80!black, thick] (0,-1.45) -- (0,1.45);

    \foreach \a in {30,45,60,120,135,150,210,225,240,300,315,330} {
        \draw[blue!80!black, thin] (0,0) -- (\a:1);
        \fill[blue!80!black] (\a:1) circle(0.5pt);
        \pgfmathtruncatemacro{\opp}{mod(\a+180,360)}
        \node[anchor=\opp, font=\tiny] at (\a:1.35)
            {$\bigl(\underline{\hspace{0.45cm}},\underline{\hspace{0.45cm}}\bigr)$};
    }

    \draw[blue!80!black, thin] (0,0) -- (1,0);
    \fill[blue!80!black] (1,0) circle(0.5pt);
    \node[anchor=west, font=\tiny, fill=white, inner sep=1pt] at (1.35, 0)
        {$\bigl(\underline{\hspace{0.45cm}},\underline{\hspace{0.45cm}}\bigr)$};

    \draw[blue!80!black, thin] (0,0) -- (0,1);
    \fill[blue!80!black] (0,1) circle(0.5pt);
    \node[anchor=south, font=\tiny, fill=white, inner sep=1pt] at (0, 1.35)
        {$\bigl(\underline{\hspace{0.45cm}},\underline{\hspace{0.45cm}}\bigr)$};

    \draw[blue!80!black, thin] (0,0) -- (-1,0);
    \fill[blue!80!black] (-1,0) circle(0.5pt);
    \node[anchor=east, font=\tiny, fill=white, inner sep=1pt] at (-1.35, 0)
        {$\bigl(\underline{\hspace{0.45cm}},\underline{\hspace{0.45cm}}\bigr)$};

    \draw[blue!80!black, thin] (0,0) -- (0,-1);
    \fill[blue!80!black] (0,-1) circle(0.5pt);
    \node[anchor=north, font=\tiny, fill=white, inner sep=1pt] at (0, -1.35)
        {$\bigl(\underline{\hspace{0.45cm}},\underline{\hspace{0.45cm}}\bigr)$};

    \node[font=\tiny] at ( 1.52,  1.52) {$\underline{\hspace{1.1cm}}$};
    \node[font=\tiny] at (-1.52,  1.52) {$\underline{\hspace{1.1cm}}$};
    \node[font=\tiny] at (-1.52, -1.52) {$\underline{\hspace{1.1cm}}$};
    \node[font=\tiny] at ( 1.52, -1.52) {$\underline{\hspace{1.1cm}}$};
\end{tikzpicture}

\vspace{0.4cm}
$\cos \longrightarrow \underline{\hspace{1.5cm}}$ \hspace{4cm} $\sin \longrightarrow \underline{\hspace{1.5cm}}$
\end{center}

\noindent Write an angle $\theta$ in standard position on a circle of radius $r$ and find the six basic trig functions at that point.

\newpage

\noindent Graph all six basic trig functions below. Which are even? Odd? Neither?

\begin{center}
    \begin{minipage}{0.32\textwidth}
        \centering $y = \sin x$\\[3pt]
        \smallgraph
    \end{minipage}
    \begin{minipage}{0.32\textwidth}
        \centering $y = \cos x$\\[3pt]
        \smallgraph
    \end{minipage}
    \begin{minipage}{0.32\textwidth}
        \centering $y = \tan x$\\[3pt]
        \smallgraph
    \end{minipage}

    \vspace{1cm}

    \begin{minipage}{0.32\textwidth}
        \centering $y = \csc x$\\[3pt]
        \smallgraph
    \end{minipage}
    \begin{minipage}{0.32\textwidth}
        \centering $y = \sec x$\\[3pt]
        \smallgraph
    \end{minipage}
    \begin{minipage}{0.32\textwidth}
        \centering $y = \cot x$\\[3pt]
        \smallgraph
    \end{minipage}
\end{center}

\vspace{1cm}

\noindent What is the period for the six basic trig functions? How do we define period?

\vspace{1.5cm}

\noindent Here are some problems to try:

\begin{enumerate}
    \item Find all of the trig values of $\theta$ if $\sin \theta = \frac{-3}{5}$ and $\tan \theta < 0$.

    \newpage

    \item Graph $y = 3\cos\!\left(2\left(x-\frac{\pi}{2}\right)\right) + 1$. Label the period, amplitude, domain, range, and shifts.

    \emptygraph
\end{enumerate}

\noindent And now the hard stuff (ha!). What does $\cos^{-1}(-0.5)$ mean?

\vspace{1.5cm}

\noindent Can we use any spot on the unit circle? Why or why not? Is there a difference between that question and solving $\cos(x) = -0.5$?

\vspace{1.5cm}

\noindent What are the domain and range for the inverse trig functions?

\vspace{1.5cm}

\noindent Can you graph them?

\begin{center}
    \begin{minipage}{0.32\textwidth}
        \centering $y = \sin^{-1} x$\\[3pt]
        \smallgraph
    \end{minipage}
    \begin{minipage}{0.32\textwidth}
        \centering $y = \cos^{-1} x$\\[3pt]
        \smallgraph
    \end{minipage}
    \begin{minipage}{0.32\textwidth}
        \centering $y = \tan^{-1} x$\\[3pt]
        \smallgraph
    \end{minipage}
\end{center}

\end{document}
```

- [ ] **Step 2: Compile to verify**

```
pdflatex u1/n6.tex
```
Expected: `Output written on n6.pdf` with no errors.

- [ ] **Step 3: Commit**

```bash
git add u1/n6.tex
git commit -m "Refactor n6: shared preamble, fix Trigonometric spelling, fix typos"
```

---

### Task 9: Update u2/n1.tex — 2.1 Rates of Change and Limits

**Files:**
- Modify: `u2/n1.tex`

Changes: replace preamble; fix "wit" → "with"; fix Sum Rule stray `s`; fix Difference Rule `L + M` → `L - M`; add space after colon in Product Rule; use `\cdot` for multiplication in all rules; fix `\lim_{x\to0}` → `\lim_{x\to c}` in Constant Multiple and Quotient Rules; fix `lim{x\to 0^+}` → `\lim_{x\to 0^+}`; standardize `\noindent`; use proper LaTeX quotes `''..''`; capitalize "Sandwich Theorem".

- [ ] **Step 1: Replace the file with this exact content**

```latex
\documentclass[11pt]{article}
\input{../calcnotes.sty}
\fancyhead[R]{2.1 Rates of Change and Limits}

\begin{document}

Today, we start working on Calculus-like things. The first of which is a limit. Limits will come up repeatedly all year! They are difficult to understand (sometimes), but not difficult to work with.

\vspace{1.5cm}

\noindent To illustrate, how do we calculate average velocity? Start by saying $y = f(t)$ and $y$ is a position or distance function. Average velocity is\dots

\vspace{1.5cm}

\noindent If the displacement function of a falling object is $y=16t^2$, find the average speed over the first $2$ seconds.

\vspace{1.5cm}

\noindent Now for the Calculus part, how do we find the \emph{instantaneous speed}---that is, the speed at any \emph{instant}? Look at the average speed formula:

\vspace{1.5cm}

\noindent We want to calculate this as $h$ gets closer and closer to zero (we can't divide by zero, can we?).

\vspace{1.5cm}

\noindent Use the example above to find the instantaneous velocity at $t = 2$ seconds.

\vspace{1.5cm}

\noindent Ok, that works well in this case. Let's write and solve a more difficult one\dots

\[\lim_{x\to0} \frac{\sin x}{x} =\]

\newpage

We need a definition (Calculus likes these; it is very theory-based).\\
Assume $f$ is defined in a neighborhood of $c$ and let $c$ and $L$ be real numbers. The function $f$ has the limit $L$ as $x$ approaches $c$ if, given any positive number $\varepsilon$, there is a positive number $\delta$ such that for all $x$:

\vspace{0.5cm}

$0 < |x - c| < \delta \Rightarrow |f(x) - L| < \varepsilon$, we write $\lim_{x\to c} f(x) = L$

\vspace{0.5cm}

\noindent Examples help here\dots\\
Graph $f(x) = \frac{x^2 - 1}{x - 1}$,
$g(x) = \begin{cases}
    \frac{x^2 - 1}{x - 1}, & x \neq 1 \\[1ex]
    1, & x = 1
\end{cases}$, $h(x) = x + 1$

\vspace{0.5cm}

% This graph is AI generated
\begin{center}
\begin{minipage}{0.32\textwidth}
\centering
\textbf{Graph of $f(x)$}\\[0.2cm]
\begin{tikzpicture}
\begin{axis}[
    axis lines = center,
    xmin=-3.5, xmax=3.5,
    ymin=-1.5, ymax=4.5,
    xtick={-3,-2,-1,1,2,3},
    ytick={-1,1,2,3,4},
    grid = both,
    grid style={line width=.1pt, draw=gray!30},
    width=5.2cm, height=5.2cm,
    tick label style={font=\tiny}
]
\end{axis}
\end{tikzpicture}
\end{minipage}
\hfill
\begin{minipage}{0.32\textwidth}
\centering
\textbf{Graph of $g(x)$}\\[0.2cm]
\begin{tikzpicture}
\begin{axis}[
    axis lines = center,
    xmin=-3.5, xmax=3.5,
    ymin=-1.5, ymax=4.5,
    xtick={-3,-2,-1,1,2,3},
    ytick={-1,1,2,3,4},
    grid = both,
    grid style={line width=.1pt, draw=gray!30},
    width=5.2cm, height=5.2cm,
    tick label style={font=\tiny}
]
\end{axis}
\end{tikzpicture}
\end{minipage}
\hfill
\begin{minipage}{0.32\textwidth}
\centering
\textbf{Graph of $h(x)$}\\[0.2cm]
\begin{tikzpicture}
\begin{axis}[
    axis lines = center,
    xmin=-3.5, xmax=3.5,
    ymin=-1.5, ymax=4.5,
    xtick={-3,-2,-1,1,2,3},
    ytick={-1,1,2,3,4},
    grid = both,
    grid style={line width=.1pt, draw=gray!30},
    width=5.2cm, height=5.2cm,
    tick label style={font=\tiny}
]
\end{axis}
\end{tikzpicture}
\end{minipage}
\end{center}

\noindent Find the limit for each function as $x$ approaches 1.

\vspace{1.5cm}

We define some properties of limits with $L$, $M$, $c$, and $k$ as real numbers and $\lim_{x\to c} f(x) = L$ and $\lim_{x\to c} g(x) = M$:
\begin{itemize}
    \item Sum Rule: $\lim_{x\to c}(f(x) + g(x)) = L + M$
    \item Difference Rule: $\lim_{x\to c}(f(x) - g(x)) = L - M$
    \item Product Rule: $\lim_{x\to c}(f(x) \cdot g(x)) = L \cdot M$
    \item Constant Multiple Rule: $\lim_{x\to c}(k \cdot f(x)) = k \cdot L$
    \item Quotient Rule: $\lim_{x\to c}\frac{f(x)}{g(x)} = \frac{L}{M},\ M \neq 0$
\end{itemize}

\newpage

\noindent Most of these are common sense, but they pop up often. Find the limits:

\begin{align*}
    \lim_{x\to3}[x^2(2-x)] && \lim_{x\to0}\frac{\tan x}{x} && \lim_{x\to1}\frac{x^2 - 3x + 2}{x^2 - 1}
\end{align*}

\vspace{1.5cm}

\noindent It is important to remember that you can only find a limit if it approaches the same thing from \emph{both} sides. See if you can find: $\lim_{x\to2}\frac{x^3 - 1}{x - 2}$

\vspace{1.5cm}

\noindent This bugs some people, so we say, ``Fine, we can also find it from just one side:''

\begin{align*}
    \lim_{x\to 0^-} = && \lim_{x\to 0^+} =\\
    &\lim_{x\to 0} =
\end{align*}

\noindent To illustrate, look at this diagram:

\noindent
\begin{minipage}{0.45\textwidth}
    \begin{align*}
        \lim_{x\to 1^-} f(x) &= \underline{\hspace{1cm}} & \lim_{x\to 1^+} f(x) &= \underline{\hspace{1cm}} \\[1ex]
        \lim_{x\to 2^-} f(x) &= \underline{\hspace{1cm}} & \lim_{x\to 2^+} f(x) &= \underline{\hspace{1cm}}
    \end{align*}
\end{minipage}
\hfill
\begin{minipage}{0.5\textwidth}
    \centering
    \begin{tikzpicture}[scale=0.8]
    \begin{axis}[
        axis lines = center,
        xmin=-0.5, xmax=4.5,
        ymin=-0.5, ymax=3.5,
        xtick={1,2,3,4},
        ytick={1,2,3},
        grid = both,
        grid style={line width=.1pt, draw=gray!20},
        width=7cm, height=6cm,
        clip=false
    ]
        \addplot[domain=0:1, samples=2, thick, blue] {-x + 1};
        \fill[blue] (axis cs:0,1) circle (2pt);
        \draw[blue, fill=white] (axis cs:1,0) circle (2pt);

        \addplot[domain=1:2, samples=2, thick, blue] {1};
        \fill[blue] (axis cs:1,1) circle (2pt);
        \draw[blue, fill=white] (axis cs:2,1) circle (2pt);

        \fill[blue] (axis cs:2,2) circle (2pt);

        \addplot[domain=2:3, samples=2, thick, blue] {x - 1};
        \draw[blue, fill=white] (axis cs:2,1) circle (2pt);
        \fill[blue] (axis cs:3,2) circle (2pt);

        \addplot[domain=3:4, samples=2, thick, blue] {-x + 5};
        \draw[blue, fill=white] (axis cs:3,2) circle (2pt);
        \draw[blue, fill=white] (axis cs:4,1) circle (2pt);
    \end{axis}
    \end{tikzpicture}
\end{minipage}

\vspace{0.5cm}

\noindent Finally, something called the (seriously) Sandwich Theorem. Don't worry too much about this one (there will be more later).\\
Show that $\lim_{x\to0}\left[x^2\sin\!\left(\frac{1}{x}\right)\right]=0$.

\end{document}
```

- [ ] **Step 2: Compile to verify**

```
pdflatex u2/n1.tex
```
Expected: `Output written on n1.pdf` with no errors.

- [ ] **Step 3: Commit**

```bash
git add u2/n1.tex
git commit -m "Refactor u2/n1: shared preamble, fix limit property errors"
```
