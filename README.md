# Typst Academic Template
I created a **Typst project template** with a clear and structured design, making it easy to reuse content for academic papers, reports, or presentations.


## Design Philosophy
- **Structured Management:** Drawing from LaTeX project experiences, I organized different content types (e.g., chapters, figures, algorithms) into separate directories. This prevents a single `main.typ` file from becoming too long and unmanageable.
- **Content Reusability:** You can easily reuse existing content across different projects. For example, you can copy the entire `contents` directory to a new project or directly use pre-built figures and algorithms in a presentation.
- **Easy to Maintain:** A clear file structure makes the project simpler to maintain and update.

### Project Structure
```bash
.
├── main.typ                 # Main file, which inputs content from the contents/ directory
└── contents/
    ├── sections/            # Main paper sections (e.g., Introduction, Methods, Experiments)
    ├── references/          # Reference files (.bib)
    ├── figures/             # Figure files and their corresponding Typst code
    │   ├── original_figures/  # (Optional) For original image files (e.g., .svg, .ai, etc.)
    │   └── ...
    ├── tables/              # Table files and their corresponding Typst code
    └── algorithms/          # Pseudocode files for algorithms
```

### Usage Scenarios
1.  **Start a New Project:** Clone (`git clone`) the entire repository and start editing the files in the `contents` directory.
2.  **Switching Templates:**
    - When you need to submit to a different conference or journal, simply copy the entire `contents` directory to the new template's project.
    - In the new template's `main.typ` file, import the necessary content using commands like `#import "contents/sections/specific_section.typ"`.
3.  **Academic Presentations:**
    - When creating a presentation, you can directly reference existing files in the `figures`, `tables`, or `algorithms` directories without rewriting them.


## Additional Notes
1.  **References:** Typst natively supports various reference formats like `BibTeX` and `YAML`. You can place your `.bib` or `.yaml` files in the `contents/references` directory.
2.  **Figures:** It's recommended to create an `original_figures` subdirectory within `figures` to store the original editable files (like `.svg` or `.ai`). This makes future modifications easier. You can include both the image and its caption directly in each figure file and then `#import` it into `main.typ`.
3.  **Algorithms:** The Typst community provides various algorithm packages, such as `typst-algorithms`. You can choose and adapt them to your needs. My preference is to use LaTeX formulas for wider compatibility; you can use `mitex`, a tool that lets you write LaTeX syntax for equations within Typst files.


## Other Projects
For general use, you might consider my other project, [Latex-Academic-Template](https://github.com/yuliu625/Yu-Latex-Academic-Template). This project is based on LaTeX, which is the long-established and widely used standard for academic writing. The LaTeX community is more mature and extensive than Typst's.

**Typst** is a more modern and efficient typesetting tool, but its ecosystem is still developing. In contrast, **LaTeX**'s position in academia is still dominant, with much broader community support and adoption.

If you need compatibility between both tools, `pandoc` is a potential solution. While it doesn't currently support direct conversion, tool support in this area is expected to improve in the future. You might need to first convert a file to `html` and then to a `tex` file.

