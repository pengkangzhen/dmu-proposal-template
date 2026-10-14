# 大连海事大学研究生开题报告 LaTeX 模板集

| 目录 | 模板 | 编译 |
|------|------|------|
| [`专业学位硕士研究生-开题报告LaTeX模板/`](专业学位硕士研究生-开题报告LaTeX模板/) | 专业学位硕士研究生-开题报告LaTeX模板（2019年1月版 .doc 逐元素复刻，A4 空表单） | `make` 或 `xelatex 开题报告模板.tex` ×2 |
| [`博士研究生-开题报告LaTeX模板/`](博士研究生-开题报告LaTeX模板/) | 博士研究生-开题报告LaTeX模板（2022年版表格，ctexart + biblatex，12 节 + 评分表） | `make`（latexmk -xelatex + biber） |
| [`beamer-dmu/`](beamer-dmu/) | 开题/组会汇报 Beamer 模板（16:9，校徽横幅视觉） | `latexmk -xelatex example.tex` |

均为 XeLaTeX 中文模板，填写方法与字体规格见各自目录内 README。

## 环境要求

- TeX Live 2024+（xelatex / latexmk）
- 博士模板另需 biber + biblatex-gb7714-2015
- 硕士模板字体：优先 Word for Mac 自带中文字体（自动回退 macOS 系统字体）

## License

MIT
