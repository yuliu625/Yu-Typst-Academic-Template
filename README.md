# Typst Academic Template
This is a **Typst Engineering Template** based on the "Convention over Configuration" philosophy. Its core objective is to achieve seamless migration and rapid reuse of academic assets (figures, algorithms, text) across different publication formats (Typst Conf/Thesis Styles) through **layer isolation**.


## 📂 Project Structure
This project treats paper construction as an automated pipeline, where each layer handles specific tasks to ensure total decoupling of **Content** and **Appearance**.

```bash
# 1. Raw Assets Layer
├── assets/                 # Raw experimental data (SVG, PDF, PNG, Python Plots, Excel)
│
# 2. Component Bridge Layer
├── components/             # Transition layer: Wrapping assets into Typst-callable functions/objects
│   ├── figures/            # Independent code blocks for figure(), caption, and label
│   ├── tables/             # Table logic (based on tablex or native table)
│   └── snippets/           # Wrapped pseudo-code blocks
│
# 3. Semantic Content Layer
├── contents/               # Pure text content, independent of specific layout styles
│   ├── modules/            # Main paper sections (Introduction, Method, etc.)
│   ├── appendices/         # Appendix content
│   ├── references/         # Bibliography/References database
│   └── structure.typ       # Logical organization layer; arranges modules via #include
│
# 4. Global Configs Layer
├── configs/                # Global variables, custom functions, and third-party package imports
│
# 5. Presentation Layer
├── main.typ                # Final entry point; applies publisher Show Rules (e.g., #show ethz: ..)
│
# 6. Support & Ops Layer
├── scripts/                # Automation scripts (e.g., converting data to Typst tables)
└── backups/                # Fault-tolerance: Backups of old versions for collaborators unfamiliar with Git
```


## 🌟 Core Design Philosophy
### Convention over Configuration
By using a preset folder structure, there is no need to write complex path-finding logic in `main.typ`. Simply placing content into the corresponding `modules` allows it to be invoked via standard `#include` or `#import`, significantly reducing configuration costs when migrating between different templates.

### Modular Isolation
Content in `contents/modules` is neutral:
- **Short Papers/Conferences**: Module content corresponds directly to `= Section`.
- **Long Papers/Theses**: Module content corresponds to `= Chapter`.
Typst’s automatic heading level promotion makes this transition natural and effortless.

### Bridge Layer Design
This is the essence of the template. `components` acts as the bridge between `assets` and `contents`:
- **Modification-Friendly**: If an image needs to be changed from `.pdf` to `.svg`, you only need to update the path in the `components` function without touching the core `contents`.
- **Multi-Invocation**: The same figure component can be referenced simultaneously by the paper (`main.typ`) and a presentation (`slides.typ` via Polylux).

### Collaboration Compatibility
Acknowledging that not all academic collaborators are proficient with Git, the `backups` folder provides physical storage for modified drafts or Word-exported snippets, ensuring manual fault tolerance during version rollbacks.


## 💡 Usage Guide
1.  **Prepare Assets**: Place raw experimental figures/tables into `assets/`.
2.  **Define Components**: Create Typst functions in `components/` that reference the exported files in `assets/`.
3.  **Write Content**: Complete the narrative in `contents/modules/`, calling components via labels or functions.
4.  **Inject into Container**: Assemble the entire paper in `main.typ` using `#include "contents/structure.typ"`.


## 🚀 Rapid Submission Workflow
When switching target journals (e.g., from IEEE to ACM), your workflow requires only two steps:
1.  **Replace `main.typ` Imports**: Update the `#import "@preview/..."` line to the target journal's package.
2.  **Redirect Content**: Re-mount your `structure.typ` assets under the new `show` rules.


## 🔗 Related Projects
For traditional requirements, consider my other project: [Latex-Academic-Template](https://github.com/yuliu625/Yu-Latex-Academic-Template). Built on LaTeX, it remains the long-standing and foreseeable standard for modern academic writing, offering a much larger community and broader support than Typst.

**Typst** is a more modern and efficient typesetting tool, though its ecosystem is still evolving. **LaTeX** remains unshakable in academia, with community support that far exceeds Typst.

If you need compatibility between both tools, `pandoc` is a viable option. While direct conversion isn't perfect yet, tool support is expected to improve. Currently, a common workaround involves converting to `html` first, then to `tex`.

