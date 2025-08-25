# Typst Academic Template
我构建了一个结构清晰、内容易于复用的**Typst 项目模板**，旨在帮助你更高效地撰写学术论文、报告或进行学术演讲。

## 设计理念
- **结构化管理:** 借鉴 LaTeX 项目的经验，我将不同类型的内容(如章节、图表、算法等)分门别类地组织，避免单个 `main.typ` 文件过长而难以控制。
- **内容复用:** 你可以轻松地在不同项目间复用已有的内容。例如，将整个 `contents` 目录复制到新的项目中，或者在演示文稿中直接调用已构建的图表和算法。
- **易于维护:** 清晰的文件结构让项目更易于维护和更新。


### 项目结构
```bash
.
├── main.tex                 # 主文件，通过 input 导入 contents 中的内容
└── contents/
    ├── sections/            # 论文的主要章节内容（如引言、方法、实验等）
    ├── references/          # 参考文献文件（.bib）
    ├── figures/             # 图片文件及其对应的 Typst 代码
    │   ├── original_figures/  # （可选）存放原始图片文件（如 .svg, .ai 等）
    │   └── ...
    ├── tables/              # 表格文件及其对应的 Typst 代码
    └── algorithms/          # 算法伪代码文件
```

### 使用场景
1. **新建项目:** 将整个仓库克隆(`git clone`)到本地，然后开始编辑`contents`目录中的文件。
1. **切换模板:**
   - 当你需要提交到不同会议或期刊时，只需将整个 `contents`目录复制到新的模板项目中。
   - 在新模板的`main.typ`文件中，使用`#import "contents/sections/specific_section.typ"`等命令导入所需的内容。
1. **学术演讲:**
   - 构建演示文稿时，可以直接引用`figures`、`tables`或`algorithms`目录中已有的文件，无需重新编写。


## 更多说明
1. **参考文献:** Typst原生支持多种参考文献格式，如`BibTeX`、`YAML`等。你可以将`.bib`或`.yaml`文件放置在`contents/references`目录中。
1. **图片:** 建议在`figures`目录下创建`original_figures`子目录，用于存放图片的原始编辑文件（如`.svg`、`.ai`等），以便后续修改。你可以在每个图片文件中直接包含图片和对应的caption，然后在`main.typ`中直接`#import`导入。
1. **算法:** Typst 社区提供了丰富的算法宏包，例如 `typst-algorithms`，可以根据你的需求自由选择和调整。我的倾向是继续使用 LaTeX 的公式以保证通用性，你可以参考使用 `mitex` ，一个可以在typ文件中写LaTeX语法的公式的工具。


## 其他项目
对于常规情况，你可以考虑我的另一个项目[Latex-Academic-Template](https://github.com/yuliu625/Yu-Latex-Academic-Template)。这个项目是基于LaTeX构建的，是现代学术写作的已长久存在并且可预见依然会持续使用的标准，并且LaTeX社区的支持和广泛程度也比Typst更大。

**Typst** 是一种更现代、高效的排版工具，但目前生态仍在发展中。而 **LaTeX** 在学术界的地位依然不可动摇，社区支持和广泛程度都远超 Typst。

如果你需要兼容两种工具，`pandoc` 是一个可行的选择。虽然目前它还不支持直接转换，但未来这方面的工具支持应该会更完善。你可能需要先转换为 `html`，文件再转换为 `tex` 文件。

