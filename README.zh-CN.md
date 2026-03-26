# Typst Academic Template
这是一个遵循“约定优于配置”思想的 **Typst 工程化模板**。其核心目标是通过**层级隔离**，实现学术资产（图表、算法、文字）在不同出版格式（Typst Conf/Thesis Styles）间的无缝迁移与快速复用。


## 📂 项目结构
本项目将论文构建视为一条自动化流水线，每一层处理特定的任务，确保**内容 (Content)** 与 **表现形式 (Appearance)** 完全解耦。

```bash
# 1. 原始资源层 (Raw Assets)
├── assets/                 # 存放原始实验数据 (SVG, PDF, PNG, Python Plot, Excel)
│
# 2. 组件适配层 (Component Bridge)
├── components/             # 过渡层：将 Assets 包装为 Typst 可调用的函数/对象
│   ├── figures/            # 封装 figure(), caption, label 的独立代码块
│   ├── tables/             # 封装好的表格逻辑（基于 tablex 或原生 table）
│   └── algorithms/         # 封装好的伪代码块
│
# 3. 语义内容层 (Semantic Contents)
├── contents/               # 纯文字内容，不涉及具体的排版样式
│   ├── modules/            # 论文主体章节 (Introduction, Method, etc.)
│   ├── appendix/           # 附录内容
│   ├── references/         # 参考文献库
│   └── structure.typ       # 逻辑组织层，通过 #include 编排各模块
│
# 4. 环境配置层 (Global Configs)
├── configs/                # 全局变量、自定义函数、第三方包引用 (import)
│
# 5. 表现/输出层 (Presentation Layer)
├── main.typ                # 最终入口，调用出版社提供的 Show Rules (如 #show ethz: ..)
│
# 6. 辅助工具层 (Support & Ops)
├── scripts/                # 自动化处理脚本（数据转 Typst 表格等）
└── backups/                # 容错层：为不熟悉 Git 的合作者保留的旧版内容备份
```


## 🌟 核心设计哲学
### 约定优于配置
通过预设的文件夹命名结构，无需在 `main.typ` 中编写复杂的路径查找逻辑。只要将内容放入对应的 `modules`，即可通过标准的 `#include` 或 `#import` 进行调用，极大降低了在不同模板间迁移时的配置成本。

### 模块化隔离
`contents/modules` 中的内容是中性的:
- **短文/会议**: 模块内容直接对应 `= Section`。
- **长文/学位论文**: 模块内容对应 `= Chapter`。
Typst 的标题层级自动提升特性使得这种转换非常自然。

### 过渡层设计
这是本模板的精髓。`components` 作为 `assets` 与 `contents` 之间的桥梁：
- **修改友好**: 如果图片需要从 `.pdf` 换成 `.svg`，只需在 `components` 的封装函数中修改路径，无需触碰正文 `contents`。
- **多处调用**: 同一个图表组件可以同时被论文 `main.typ` 和演示文稿 `slides.typ` (Polylux) 引用。

### 协作兼容性
考虑到学术合作中并非所有成员都熟练使用 Git，`backups` 文件夹提供了一个物理存储空间，用于存放合作者修改后的旧稿或 Word 转出的草堆，确保在版本回溯时的人工容错。


## 💡 使用指南
1.  **准备素材**: 将实验原始图表放入 `assets`。
2.  **编写组件**: 在 `components/` 中定义对应的 Typst 函数，引用 `assets` 中的导出图。
3.  **撰写内容**: 在 `contents/modules/` 中完成文字叙述，并通过标签或函数调用 `components` 中的组件。
4.  **注入容器**: 在 `main.typ` 中通过 `#include "contents/structure.typ"` 完成整篇论文的组装。


## 🚀 快速切换投稿流
当需要更换投稿期刊（例如从 IEEE 换到 ACM）时，你的工作流仅需两步：
1. **替换 `main.typ` 的引用**: 修改开头 `#import "@preview/..."` 为目标期刊的包。
2. **重定向内容**: 在新的 `show` 规则下，重新挂载你的 `structure.typ` 内容资产。


## 🔗 关联项目
对于常规情况，你可以考虑我的另一个项目[Latex-Academic-Template](https://github.com/yuliu625/Yu-Latex-Academic-Template)。这个项目是基于LaTeX构建的，是现代学术写作的已长久存在并且可预见依然会持续使用的标准，并且LaTeX社区的支持和广泛程度也比Typst更大。

**Typst** 是一种更现代、高效的排版工具，但目前生态仍在发展中。而 **LaTeX** 在学术界的地位依然不可动摇，社区支持和广泛程度都远超 Typst。

如果你需要兼容两种工具，`pandoc` 是一个可行的选择。虽然目前它还不支持直接转换，但未来这方面的工具支持应该会更完善。你可能需要先转换为 `html`，文件再转换为 `tex` 文件。

