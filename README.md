# Natural Language Processing — Exercises & Assignments

LaTeX workspace for NLP course exercises and tests. Each exercise lives in its own `.tex` file and compiles to an independent PDF.

## Requirements

- **TeX Live** with XeLaTeX (`xelatex`, `latexmk`)
- **LaTeX Workshop** (VS Code extension) — recommended

## Structure

```
exercises/
├── preamble.tex                         # shared packages & page style
├── 01_mlp_binary_classification.tex    # Assignment 1
└── output/                             # compiled PDFs (gitignored)
```

Add new exercises as `exercises/NN_topic_name.tex`, each starting with `\input{preamble}`.

## Compiling

**VS Code (recommended):** Open any `.tex` file inside `exercises/` and press the compile button (or `Ctrl+Alt+B`). The PDF lands in `exercises/output/`.

**Command line:**
```bash
cd exercises
latexmk -xelatex -outdir=output 01_mlp_binary_classification.tex
```

To clean build artifacts:
```bash
latexmk -C -outdir=output 01_mlp_binary_classification.tex
```
