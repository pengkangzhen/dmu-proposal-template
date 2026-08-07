# 大连海事大学博士学位论文开题报告 LaTeX 模板

基于《博士研究生开题、中期、预答辩、答辩相关表格（2022年版）》中的
「1博士研究生学位论文开题报告.doc」制作，使用 XeLaTeX + ctexart + biblatex 还原原 Word 模板的全部排版要素。

## 特性

- **完全还原**原 Word 模板的字体、字号、边框与表格结构
- 每节带 `1.5px solid #BFBFBF` 边框框体（`tcolorbox` 实现，可跨页）
- 封面信息表、评审小组组成表、工作计划表、评分表等全部表格模板
- 参考文献 GB/T 7714-2015 国标格式（biblatex + biber）
- macOS 系统字体（Songti SC / Heiti SC / FangSong / KaiTi）

## 环境要求

| 组件 | 版本 | 检查命令 |
|------|------|---------|
| TeX Live | 2024+ | `xelatex --version` |
| biber | 同步版本 | `biber --version` |
| biblatex-gb7714-2015 | 任意 | `kpsewhich gb7714-2015.bbx` |
| ctex | 任意 | `kpsewhich ctexart.cls` |
| macOS 系统字体 | — | Songti SC、Heiti SC 等 |

> 非 macOS 用户：将 `\documentclass` 中的 `fontset=mac` 改为 `fontset=windows` 或 `fontset=fandol`，并调整 `\setCJKfamilyfont` 中的字体名称。

## 编译

```bash
make            # 编译 → proposal.pdf
make view       # 打开 PDF
make clean      # 清理中间文件
make distclean  # 清理所有生成文件
```

或手动（不依赖 make）：

```bash
latexmk -xelatex proposal.tex
```

## 文件结构

```
├── proposal.tex       主文件（含全部 12 节 + 评分表）
├── references.bib     文献库
├── figures/           图形目录
├── Makefile           编译自动化
└── README.md          本文件
```

## 填写指南

### 1. 个人信息

在 `proposal.tex` 顶部「个人信息」区块修改（搜索 `个人信息`）：

```latex
\newcommand{\studentName}{你的姓名}
\newcommand{\studentID}{你的学号}
\newcommand{\schoolName}{学院名称}
\newcommand{\discipline}{学科专业}
\newcommand{\advisorName}{指导教师}
\newcommand{\thesisTitle}{论文题目}
\newcommand{\proposalDate}{202X年X月}
```

### 2. 正文内容

`proposal.tex` 中所有需要填写的位置均以 `% TODO` 注释标记。每个节（第 1–7 节）的结构已预置：

| 节号 | 标题 | 预置结构 |
|------|------|---------|
| 1 | 选题背景 | （1）选题科学依据 （2）研究目的与意义 |
| 2 | 文献综述 | 2.1–2.3 主题小标题 + 参考文献列表 |
| 3 | 研究内容 | （1）主要研究内容 （2）拟解决的关键问题 |
| 4 | 主要创新点 | 空白（自由发挥） |
| 5 | 研究方案 | （1）研究方法 （2）技术路线 （3）可行性 （4）难点 |
| 6 | 研究基础 | （1）工作条件 （2）经费预算表 |
| 7 | 工作计划 | 空白表格（5 行） |

第 8–12 节及评分表为行政表格，按学校流程手填或打印后手写即可。

### 3. 参考文献

**Zotero + Better BibTeX** 工作流：

1. Zotero 中新建收集夹，将文献归入其中
2. 右键收集夹 → 导出 → 格式选 **Better BibTeX** → 勾选 **Keep updated**
3. 输出路径指向 `references.bib`
4. 正文中用 `\cite{citekey}` 或 `\parencite{citekey}` 引用

引用格式自动遵循 GB/T 7714-2015 国标。

### 4. 公式

```latex
\begin{equation}
  \min \sum_{i \in I} c_i x_i + \sum_{s \in S} p_s Q_s(x, \xi_s)
  \quad \text{s.t.} \quad
  \sum_{i} x_i \le B, \quad x_i \in \{0, 1\}
\end{equation}
```

### 5. 插图

将 PDF/PNG 放入 `figures/`，在正文中引用：

```latex
\begin{figure}[H]
  \centering
  \includegraphics[width=0.85\textwidth]{figures/tech-roadmap}
  \caption{研究技术路线图}
  \label{fig:tech-roadmap}
\end{figure}
```

## 提交时转 Word（可选）

学校最终要求提交 Word 模板。内容写完后可导出再粘贴：

```bash
# 方案 A：pandoc 直接转 docx（公式转 OMML，可在 Word 编辑）
pandoc proposal.tex -o proposal_body.docx \
  --bibliography=references.bib \
  --citeproc

# 方案 B：直接提交 PDF（如学院允许）
make && open proposal.pdf
```

转出后将正文段落粘进学校官方 `.doc` 模板的对应章节，封面与签字页保留 Word 原表。

## 字体规格（参考）

| 元素 | 字体 | 字号 |
|------|------|------|
| 封面标题 | 宋体加粗 | 一号 (26pt) |
| 封面信息 | 宋体加粗 | 三号 (16pt) |
| 节标题 | 黑体 | 小四 (12pt) |
| 小节标题 | 宋体 | 小四 (12pt) |
| 正文 | 宋体 | 五号 (10.5pt) |
| 提示语 | 楷体 | 五号 (10.5pt) |
| 评分表 | 宋体 | 五号 (10.5pt) |
| 每节外框 | — | 1.5px solid #BFBFBF |

## License

MIT
