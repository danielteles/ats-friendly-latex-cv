# ATS-Friendly LaTeX Resume Template

This template creates a clean, single-column resume in LaTeX. Applicant Tracking Systems (ATS) can read the PDF text in the correct order, because the layout uses no tables or columns. The template targets software engineers and other technical professionals who apply for roles in the US, in Europe, and at remote-first companies.

The repository includes a fictional example, filled in with placeholder data, in two languages: English and Brazilian Portuguese. Use one as your starting point.

---

## Repository Structure

```
en/         English template (main.tex, compiled main.pdf)
pt-br/      Brazilian Portuguese template (main.tex, compiled main.pdf)
README.md
LICENSE
```

Each language folder is self-contained: its `main.tex` compiles on its own, with no shared includes across folders. To add another language, copy a folder, translate the content inside `main.tex`, and keep the macros (`\cventry`, `\keytech`, `\skillrow`, `\cvsection`) and packages untouched.

---

## Why This Template Exists

Many LaTeX resume templates use multi-column layouts, tables, or icon fonts. These layouts often break ATS software, such as Workday, Greenhouse, and Lever. When an ATS reads a table out of order, a bullet point can end up next to the wrong date or the wrong company. This template avoids that risk. It uses a single column of plain text, so the PDF keeps a predictable reading order.

The template gives you:

- A single-column layout, with no tables or multi-column blocks
- Correct Unicode text extraction, through the `cmap` package and a `glyphtounicode` mapping
- A Key Technologies line under each role, for keyword matching
- Visible link text, for example `linkedin.com/in/username` instead of a plain label such as LinkedIn
- PDF metadata (title, author, language), set from one place in the file
- No photo, age, marital status, or full home address, in line with US, EU, and international conventions
- A small set of standard, well-maintained LaTeX packages: `geometry`, `titlesec`, `enumitem`, `xcolor`, `hyperref`, and `cmap`.

---

## How to Build the PDF

### Option 1: Local build, with VS Code

1. Install a LaTeX distribution. Use MacTeX or BasicTeX on macOS, or MiKTeX on Windows.
2. Install the LaTeX Workshop extension in VS Code.
3. Open `en/main.tex` (or `pt-br/main.tex`) in VS Code.
4. Edit your details in the file.
5. Save the file. VS Code compiles the PDF on save.

### Option 2: Cloud build, with Overleaf

1. Create a new project in [Overleaf](https://www.overleaf.com/).
2. Upload the contents of the language folder you want (`en/main.tex` or `pt-br/main.tex`).
3. Click Recompile.

### Option 3: Command line, with latexmk

```
cd en      # or: cd pt-br
latexmk -pdf main.tex
```

---

## Customize the Template

The settings that you change most often sit in one place, near the top of the file, in the `USER CONFIGURATION` section:

- Your name, in the `\candidatename` command
- The accent color, in the `\definecolor{accent}{...}` line
- The space between entries, in the `\cventrysep` and `\cvblocksep` lengths.

The file uses four macros to keep formatting consistent:

- `\cventry{Role}{Company}{Location}{Dates}`, for each job or degree entry
- `\keytech{...}`, for a line of key technologies under a role
- `\skillrow{Category}{Items}`, for one line in the Skills section
- `\cvsection{Title}`, for each section heading.

To add a job or degree, copy an existing `\cventry` block, with its bullet list. To remove a section, delete its `\cvsection` command and the content under it. To reorder sections, move a whole section block, from one `\cvsection` command to the next.

---

## Validate ATS Compatibility

### Manual text-extraction check

1. Open the compiled PDF.
2. Select all text, with Cmd+A on macOS or Ctrl+A on Windows.
3. Copy the text.
4. Paste the text into a plain text editor, such as TextEdit or Notepad.

Read the pasted text. The order must match the resume, and no characters can be missing or garbled. If both are true, the PDF is ready for ATS submission.

### Local text-extraction checks

Run with Poppler's `pdftotext`, `pdffonts`, and `pdfinfo` (`brew install poppler` on macOS):

```
pdftotext -layout main.pdf -   # reading order
pdffonts main.pdf              # font embedding, should show emb:yes and uni:yes for every font
pdfinfo main.pdf               # document metadata: no JavaScript, no form fields, not encrypted
```

### Structural parser checkers

Tools such as [wolfresume.com's parser-test](https://wolfresume.com/parser-test) simulate how an ATS parses the PDF into sections, dates, and job/company pairs — useful for catching layout issues before you submit.

`en/main.pdf` was run through wolfresume's parser-test; the full report is in [`en/wolfresume-parser-report.txt`](en/wolfresume-parser-report.txt) (Overall status: PASS, 0 critical/warn/info findings, 5/5 recruiter-scan signals visible). Re-run this check after you edit the content, since the result reflects the template as populated at the time of the test, not a guarantee for every edit.

### Third-party ATS/keyword checkers

Structural parsing is only part of ATS compatibility — tools like [Jobscan](https://www.jobscan.co/), [Resume Worded](https://resumeworded.com/), and [Enhancv's resume checker](https://enhancv.com/) score keyword match against a specific job description, which is a different signal than parser-test tools.

---

## Contributing

To contribute, open an issue or submit a pull request. Focus areas include layout, package choices, and documentation.

## License

This project uses the MIT License. See the `LICENSE` file for details.
