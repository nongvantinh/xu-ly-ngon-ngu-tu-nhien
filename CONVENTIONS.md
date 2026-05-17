# Project Rules — NLP Exercises

This is a LaTeX workspace for Natural Language Processing course exercises.
Every time a new exercise arrives, follow the steps below exactly.

---

## File structure

```
exercises/
├── preamble.tex                      ← shared preamble, never modify casually
├── NN_topic_name.tex                 ← exercise sheet
├── output/                           ← gitignored, PDFs land here
└── solutions/
    ├── NN_topic_name.tex             ← English formal solution
    ├── output/                       ← gitignored
    └── vi/
        ├── NN_topic_name.tex         ← Vietnamese student version
        └── output/                   ← gitignored
```

`NN` is a two-digit zero-padded index: `01`, `02`, `03`, …

---

## Step-by-step workflow for each new exercise

### 1. Create the exercise sheet — `exercises/NN_topic_name.tex`

```latex
\documentclass[12pt,a4paper]{article}
\input{preamble}
\begin{document}
...
\end{document}
```

- Title block: course name, assignment title, duration — centered, no `\maketitle`
- Two `\noindent\rule{\linewidth}{0.6pt}` rules wrapping the Instructions block
- Sections with `\section*{}`, sub-parts with `\enumerate[label=(\alph*)]`
- Point values appear in question headers: `\textbf{Question A.} (N points)`
- Decimal separator: dot (`1.5`, `0.8176`) — English convention

### 2. Create the English formal solution — `exercises/solutions/NN_topic_name.tex`

```latex
\documentclass[12pt,a4paper]{article}
\input{../preamble}

\usepackage{mdframed}
\newmdenv[backgroundcolor=gray!12, linecolor=gray!50, linewidth=0.8pt,
          innertopmargin=6pt, innerbottommargin=6pt,
          innerleftmargin=8pt, innerrightmargin=8pt,
          skipabove=6pt, skipbelow=6pt]{answerbox}
\newcommand{\step}[1]{\medskip\noindent\textbf{\textsf{Step #1.}}\enspace}

\begin{document}
...
\end{document}
```

Rules:
- Title: `Assignment N --- SOLUTION`, total points shown
- Section headers carry point values: `\section*{Question A \hfill{\normalfont\small(N points)}}`
- Use `\step{1}`, `\step{2}`, … to label each computation step
- Wrap every final numerical result in `\begin{answerbox}...\end{answerbox}`
- Use `\boxed{}` inside math for key scalar answers
- Follow each result with a one-sentence interpretation in italics
- Decimal separator: dot — English convention

### 3. Create the Vietnamese student version — `exercises/solutions/vi/NN_topic_name.tex`

```latex
\documentclass[12pt,a4paper]{article}
\input{../../preamble}

\usepackage{polyglossia}
\setmainlanguage{vietnamese}

\fancyhead[L]{}
\fancyhead[R]{}
\fancyfoot[R]{\thepage}
\fancyfoot[C]{}
\renewcommand{\headrulewidth}{0pt}

\usepackage{mdframed}
\newmdenv[backgroundcolor=gray!10, linecolor=gray!45, linewidth=0.8pt,
          innertopmargin=6pt, innerbottommargin=6pt,
          innerleftmargin=8pt, innerrightmargin=8pt,
          skipabove=5pt, skipbelow=5pt]{ketqua}
\newcommand{\nhanxet}[1]{\smallskip\noindent\textit{\textbf{Nhận xét.}}\enspace #1\smallskip}

\begin{document}
...
\end{document}
```

Rules — strictly enforced:
- **No course name anywhere** (not in header, not in title block)
- **No point annotations** in any heading — no `(2 điểm)`, no `Tổng điểm`, nothing
- **No header rule** (`\headrulewidth{0pt}`) and both header slots empty
- **Page number**: bottom-right only, bare number — `\fancyfoot[R]{\thepage}`
- **Section labels**: `Câu A`, `Câu B`, `Câu C`; sub-parts `(a)`, `(b)`, `(c)` as `\subsection*`
- **Title block**: assignment title + "Bài Làm" label only, no total points line
- **Decimal separator**: comma `1{,}5`, `0{,}8176` — Vietnamese mathematical convention
- **Language voice**: natural Vietnamese university student — use `Ta có:`, `Vậy`, `Do đó`, `Nhận thấy`, `Áp dụng`; avoid stiff translated phrasing
- Wrap final results in `\begin{ketqua}...\end{ketqua}`
- Observations go in `\nhanxet{...}`

### 4. Compile and verify

Run from each file's directory:
```bash
latexmk -xelatex -outdir=output NN_topic_name.tex
```

A successful build produces **zero errors and zero warnings**. Fix any warning
(e.g. `\headheight too small`) before considering the task done.

---

## Shared preamble — `exercises/preamble.tex`

Contains: `fontspec` (Times New Roman), `geometry` (a4, standard margins),
`amsmath`, `amssymb`, `mathtools`, `bm`, `enumitem`, `booktabs`, `xcolor`,
`hyperref`, `fancyhdr` (headheight 14pt, left=course name, right=page N).

**Do not add** language packages (`polyglossia`) or solution-specific packages
(`mdframed`) to the shared preamble — each file type loads only what it needs.

---

## Compilation setup

- Engine: **XeLaTeX** via `latexmk -xelatex`
- Output dir: `output/` next to each `.tex` file (VS Code `outDir = %DIR%/output`)
- All `output/` directories are gitignored via the root-level `output/` pattern
