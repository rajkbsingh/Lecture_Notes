# Computer Science Lecture Notes (LaTeX template)

A clean, modern LaTeX template for computer-science lecture notes. It supports mathematics, code listings, algorithms, TikZ figures and plots, colored theorem boxes, exercises, a three-part footer and a faint logo at the bottom of every page. The project is split into small files, so each lecture only needs a few edits.

## Quick start

### Overleaf
1. Create a new project: **New Project → Upload Project** and select the zip (or **New Project → Templates** if published in the Gallery).
2. Make sure the main document is `main.tex` (**Menu → Main document**).
3. Compiler: **pdfLaTeX** (default). No `-shell-escape` is needed.
4. Open `settings.tex`, put in your course details, and compile.

### Local
```bash
latexmk -pdf main.tex
```
(Run twice, or use `latexmk`, so that the table of contents and the "Page x of y" footer are correct.)

## Project structure

```text
├── main.tex                 main file: loads settings, preamble, sections
├── settings.tex             course info + logo options (edit per lecture)
├── preamble/
│   ├── packages.tex         all \usepackage lines
│   ├── style.tex            colors, headings, header/footer, title block
│   ├── macros.tex           math macros, \code{}
│   ├── boxes.tex            theorem / definition / example / note boxes
│   ├── code.tex             listings and algorithm styling
│   └── watermark.tex        footer logo
├── sections/                one file per section (01_..., 02_..., ...)
├── figures/                 TikZ/pgfplots figures, images, logo
└── code/                    source files included with \lstinputlisting
```

## Customizing

### Course information and logo: `settings.tex`

```latex
\newcommand{\coursecode}{CS 2xx}
\newcommand{\coursename}{Algorithms and Data Structures}
\newcommand{\lecnumber}{1}
\newcommand{\lectitle}{Divide and Conquer}
\newcommand{\lecturer}{Prof. Jane Doe}
\newcommand{\semester}{Fall 2026}

\newif\ifshowwatermark \showwatermarktrue   % \showwatermarkfalse to hide the logo
\newcommand{\wmheight}{0.7cm}               % logo height
\newcommand{\wmopacity}{0.35}               % 0 = invisible, 1 = solid
\newcommand{\wmy}{0.95cm}                   % vertical position of the logo
```

### Colors: `preamble/style.tex`
Change `accent`, `accent2`, `accent3` (and the code colors) to re-theme the whole document.

### Logo
Upload your logo as `figures/logo.png` (or `.pdf` / `.jpg`). It is used automatically. If no logo is found, a placeholder (`figures/logo-placeholder.tex`) is shown. A PNG with a transparent background works best.

### Footer
The footer has three parts: lecturer and semester (left), the logo (center), and "Page x of y" (right). Edit the `\fancyfoot[...]` lines in `preamble/style.tex`.

### Adding a section
Create `sections/08_topic.tex` and add `\input{sections/08_topic}` to `main.tex`.

## Cheat sheet

### Numbered boxes

```latex
\begin{theorem}{Title}{label} ... \end{theorem}        % Theorem~\ref{thm:label}
\begin{lemma}{Title}{label} ... \end{lemma}            % Lemma~\ref{lem:label}
\begin{definition}{Title}{label} ... \end{definition}  % Definition~\ref{def:label}
\begin{example}{Title}{label} ... \end{example}        % Example~\ref{ex:label}
\begin{exercise}{Title}{label} ... \end{exercise}      % Exercise~\ref{exc:label}
\begin{proof} ... \end{proof}
```

Theorems, lemmas, definitions and examples share one counter, numbered within each section. Exercises are numbered separately.

### Unnumbered boxes

```latex
\begin{keyidea}[Key idea] ... \end{keyidea}
\begin{notebox}[Note] ... \end{notebox}
\begin{warnbox}[Pitfall] ... \end{warnbox}
\begin{objectives} ... \end{objectives}
```

### Math macros
`\R \N \Z \E \Pr \O` (blackboard/calligraphic sets and operators), `\norm{x}`, `\abs{x}`, `\inner{x}{y}`, `\argmin`, `\argmax`, and `\bm{x}` for bold math.

### Code

```latex
% From a file in code/ (recommended)
\lstinputlisting[language=Python, caption={Merge sort.}, label={lst:merge}]{code/merge_sort.py}

% Inline in the document
\begin{lstlisting}[language=C++, caption={...}, label={lst:x}]
int main() { return 0; }
\end{lstlisting}

% Inline snippet
\code{lo + (hi - lo) / 2}
```

### Algorithms
Uses `algorithm` + `algpseudocode`. See `sections/03_algorithms.tex` for a full example (`\Require`, `\Ensure`, `\State`, `\If`, `\While`, `\ForAll`, `\Call`, ...).

### Figures
- TikZ/pgfplots: put the code in `figures/name.tex` and include it with `\input{figures/name}` inside a `figure` environment (see `sections/05_figures.tex`).
- Images: put the file in `figures/` and use `\includegraphics[width=0.6\linewidth]{figures/name.pdf}`.

## Requirements

pdfLaTeX with a standard TeX Live or MiKTeX installation. Main packages: `tcolorbox`, `listings`, `algorithm`, `algpseudocode`, `tikz`, `pgfplots`, `eso-pic`, `fancyhdr`, `lastpage`, `titlesec`, `amsmath`, `amsthm`, `mathtools`, `bm`, `booktabs`, `caption`, `subcaption`, `hyperref`. All are included in Overleaf.

## Troubleshooting

| Problem | Fix |
|---|---|
| "Page 1 of ?" or a missing table of contents | Compile twice (Overleaf does this automatically). |
| `Theorem ??` in the text | Compile twice, and check that the reference is `thm:<label>` for the label you gave. |
| Logo not showing | Check the file name is exactly `figures/logo.png` (or `.pdf`/`.jpg`), and that `\showwatermarktrue` is set. |
| Logo overlaps the footer text | Adjust `\wmy` and `\wmheight` in `settings.tex`. |
| Logo too strong or too faint | Change `\wmopacity` in `settings.tex`. |
| Unicode symbol in a code listing fails | `listings` handles only ASCII by default. Use ASCII characters in code files. |

## Authors

Raj Kumar Baliyar Singh and Swetanjali Maharana

## License

This template is **free and open source** under the [MIT License](LICENSE). You may use, copy, modify and redistribute it, for personal, academic or commercial use, with no fee and no permission needed. The only condition is to keep the copyright and license notice in copies of the template.

Your own lecture content (text, figures, code) is yours. It is not covered by this license.
