# B-SAFE METHODOLOGY

## Purpose
This  repository contains LaTeX sources, figures and supporting materials to write and build a research paper about the "B-SAFE" methodology (a security framework for blockchain). This README explains repository layout, LaTeX build instructions, bibliography handling, recommend tooling, and quick examples so you can produce a final PDF reliably.

## Repository layout (recommend)
```
B-SAFE-methodology/
├─ template/                 # main LaTeX files and class/style files
│  ├─ main.tex               # main LaTeX entry
│  ├─ references.bib         # bibliography file
│  └─ Makefile               # optional build helper
├─ inner/                    # small .tex files for sections/chapters (easier to maintain)
│  ├─ 0-title.tex
│  ├─ 1-intro.tex
│  ├─ 2-related-work.tex
│  ├─ 3-method.tex
│  ├─ 4-experiments.tex
│  └─ 5-conclusion.tex
├─ figure/                   # figures, diagrams (PNG, PDF, EPS, SVG)
├─ code/                     # experiment scripts, notebooks, reproducible artifacts
├─ output/                   # build artifacts (PDFs), logs
├─ README.md or READ_ME.md   # this file
└─ b-safe-research-outline.md # the research outline / notes
```

Storing each logical section in `inner/` and using `\input{}` from `template/main.tex` helps parallel editing and version control.

## Required software
- VSCode, MiKTeX and strawberryperl.
- You can watch this following youtube video to set up: https://www.youtube.com/watch?v=4lyHIQl4VM8&t=337s&ab_channel=FedericoTartarini

## Example `main.tex` skeleton
Put a small wrapper in `template/main.tex` that inputs section files:
```tex
\documentclass[a4paper]{article}
\usepackage{...}
...
% bibliography: choose natbib or biblatex
\begin{document}
...
\input{../inner/introduction.tex}
\input{../inner/literature_review.tex}
\input{../inner/methodology.tex}
\input{../inner/results_and_analysis.tex}
\input{../inner/discussion.tex}
\input{../inner/future_work.tex}
\section{Conclusion}...
\section{Acknowledgement}...
\begin{thebibliography}{(#number of references)}
\bibitem{1} ...
\bibitem{2} ...
...
\end{thebibbliopgraphy}

\end{document}
```

## Working with figures
- Put figures (pictures or graphs) in `figures/`. Use relative paths in LaTeX so includes work:
  ```tex
  \includegraphics[<custom figure>]{../figure/architecture.pdf}
  ```
- Use `\ref{fig:<fig_name>}` to reference the figure:
  ```tex
  The following figure \ref{fig:gen_1_diagram} and figure  \ref{fig:gen_2_diagram} show theese two main aproaches:
  
  \begin{figure}[H]
  \centering
  \includegraphics[scale=0.50]{gen_1_diagram.jpg}
  \caption{\label{fig:gen_1_diagram}GA to increase code coverage}
  \end{figure}

  \begin{figure}[H]
  \centering
  \includegraphics[scale=0.50]{gen_2_diagram.jpg}
  \caption{\label{fig:gen_2_diagram}GA to get minimal functional test suite}
  \end{figure}
  ```
  
## Working with codes
- Pakage:
  ```tex
  \usepackage{listings}
  \usepackage{xcolor}
  \lstset{
    basicstyle=\ttfamily\small,
    breaklines=true,
    numbers=none,
    frame=single,
    captionpos=b
  }
  \usepackage{fancyvrb}
  ```
- Input code:
  ```
  % Code with bounding box:
  \section{Comparison of print statements}

  \subsection*{Python}          % this one just for highlight the language in document, you can skip it if you want.
  \lstinputlisting[language=Python, caption={Python: hello.py}, label={lst:py}]{code/hello.py}

  \subsection*{C++}
  \lstinputlisting[language=C++, caption={C++: hello.cpp}, label={lst:cpp}]{code/hello.cpp}

  \lstinputlisting[caption={Pseudocode example},label={lst:ps1}]{code/hello.txt}

  % Code without bounding box:
  \VerbatimInput[fontsize=\small]{code/hello.txt}
  ```

## Troubleshooting
- **Images and code not shown: confirm file paths and formats (pdf/png for pdflatex).
