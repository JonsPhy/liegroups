# Groups and Lie Algebras Lecture Notes

This project now follows the structure of `../mathtemplate/template`, with the existing lecture-note chapters copied into the template's `content/` directory.

## Structure

* `main.tex` - main entry point
* `.latexmkrc` - sends build artifacts to `out/`
* `metadata.tex` - project metadata and title-page content
* `style/project.sty` - packages, layout, headers, and shared defaults
* `style/commands.tex` - personal math commands and helper macros
* `style/theorems.tex` - theorem boxes and proof helpers
* `content/` - chapter files
* `ref/refs.bib` - bibliography database
* `figures/` - figures and logos

## Workflow

1. Adjust the fields in `metadata.tex` if the course details change.
2. Add new chapters in `content/`.
3. Put bibliography entries into `ref/refs.bib`.
4. Compile with `latexmk -pdf main.tex`.

## Notes

* The template uses `report` as a good middle ground for thesis-style documents and longer notes.
* The theorem boxes from the notes project are included, but regular theorem environments still work.
* `physics` is loaded because it appeared in your thesis workflow. If it ever clashes with a package in a future project, remove it centrally in `style/project.sty`.
* Generated files such as `.aux`, `.bbl`, `.log`, and the final PDF are written to `out/`.
