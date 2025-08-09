# B-SAFE Methodology (LaTeX Project)

## Purpose
This repository contains LaTeX sources, figures, and supporting materials to build the B-SAFE paper (Blockchain Security Assessment Framework Enhanced with ML). It documents the structure, build instructions (latexmk + BibTeX), a unified bibliography workflow, and contribution guidelines.

## Repository layout (current)
```
B-SAFE-methodology/
├─ output/                     # Build entrypoint and artifacts
│  ├─ main.tex                 # Main LaTeX file (compile from this directory)
│  └─ main.pdf                 # Built PDF
├─ inner/                      # Section files included by main.tex
│  ├─ introduction.tex
│  ├─ literature_review.tex
│  │  ├─ 01_consensus_attacks.tex
│  │  ├─ 02_key_management_wallet_security.tex
│  │  ├─ 03_smart_contract_vulnerabilities.tex
│  │  ├─ 04_defi_protocol_risks.tex
│  │  └─ 05_exchange_infrastructure_attacks.tex
│  ├─ methodology.tex
│  │  └─ 01_business_readiness.tex
│  ├─ results_and_analysis.tex
│  ├─ discussion.tex
│  └─ future_work.tex
├─ figure/                     # Figures (optionally grouped per section)
│  ├─ fig1.png
│  └─ <section>/fig1.png
├─ template/                   # Local style helpers used by main.tex
│  ├─ cite.sty
│  └─ parskip.sty
├─ code/                       # Optional code artifacts used in the paper
├─ references.bib              # Unified bibliography for the whole team
├─ README.md                   # This file
└─ sprint_2.md                 # Planning / notes
```

## Quick start
1) Edit content in `inner/*.tex` and subfiles.
2) Add citations to `references.bib` and cite with `\cite{key}`.
3) Build from the `output/` directory:
   - macOS/Linux:
     ```bash
     cd output
     latexmk -pdf -bibtex main.tex
     ```
   - Windows (MiKTeX): open a terminal in `output/` and run the same command.
4) Open `output/main.pdf`.

## Build requirements
- A LaTeX distribution with pdflatex, BibTeX, and `latexmk`:
  - macOS: MacTeX (or BasicTeX + latexmk)
  - Linux: TeX Live
  - Windows: MiKTeX (ensure `latexmk` is installed)
- Optional editor: VS Code, TeXstudio, or your preferred LaTeX IDE.

## Bibliography (unified references.bib)
- The bibliography is externalized. `output/main.tex` uses:
  ```tex
  \bibliographystyle{ieeetr}
  \bibliography{../references}
  ```
- Add new entries to `references.bib` using standard BibTeX types (`@article`, `@inproceedings`, `@book`, `@misc`, ...).
- Cite in text with `\cite{yourKey}`.
- Keys must be unique and stable (e.g., `AuthorYearShortTitle`).
- Note: `main.tex` currently includes a temporary `\nocite{...}` list to force-display a few seed entries; remove entries from that list as they become cited in the text.

## Figures
- Place figures in `figure/` (subfolders per section are fine).
- Include with a relative path from `output/main.tex` perspective, e.g.:
  ```tex
  \includegraphics[width=0.9\linewidth]{../figure/methodology/fig1.png}
  ```
- Use labels and references:
  ```tex
  \begin{figure}[t]
    \centering
    \includegraphics[width=0.9\linewidth]{../figure/fig1.png}
    \caption{System overview}
    \label{fig:system_overview}
  \end{figure}
  As shown in Figure~\ref{fig:system_overview} ...
  ```

## Contribution guidelines
- Edit section content only in `inner/` and its subfolders.
- Do not put `thebibliography` environments inside any `.tex` file. Use `references.bib` and `\cite{...}`.
- Keep figure paths relative to `output/main.tex` (prefix with `../`).
- Keep BibTeX entries clean and complete (author, title, venue, year, doi/url when available).
- Prefer small, focused commits. If introducing new figures or code, include sources and update paths in the relevant `inner/` file.

## Troubleshooting
- Missing `../template/cite.sty` or images: run the build from the `output/` directory.
- Citations show as `?` or bibliography missing:
  - Run a clean rebuild with BibTeX:
    ```bash
    cd output
    latexmk -g -pdf -bibtex main.tex
    ```
  - Check the citation keys match those in `references.bib`.
- Stale artifacts or strange errors: clean and rebuild:
  ```bash
  cd output
  latexmk -C
  latexmk -pdf -bibtex main.tex
  ```

## Notes
- The `output/` directory is intentionally tracked to keep `main.tex` and the generated `main.pdf` under version control for collaboration.
