# DMU Beamer 主题（beamerthemeDMU）

由大连海事大学 2026-09 版汇报 PPT 复刻的 LaTeX Beamer 模板，用于开题答辩与组会演示（配套根目录的论文版开题报告模板使用）。

## 文件

| 文件 | 说明 |
|------|------|
| `beamerthemeDMU.sty` | 主题文件（颜色/横幅/标题/进度条/目录/分节页/封面） |
| `dmu-emblem.png` | 圆形校徽（源：PPTX 渲染图裁剪，透明底） |
| `example.tex` | 示例文稿（封面、目录、分节页、列表、分栏、色块、表格） |
| `example.pdf` | 示例编译产物，可直接预览 |

> 横幅上的校名、学院名（含中英文）为**文字排版**，字体取自 PPTX slide2 的原始规格：中文华文行楷（Xingkai SC Bold，PPT 源写行楷-繁，同套字形）+ 英文 Zapfino 花体，两个文本框字号规格一致——校名与院名的中英文同字体同字号。竖线位置由 tikz calc 锚定字标实际宽度，改文案无需重算坐标。

## 用法

把 `beamerthemeDMU.sty` 与 `dmu-emblem.png` 放在文稿同目录，然后：

```latex
\documentclass[aspectratio=169]{beamer}
\usetheme{DMU}

% 底部进度条条目名（英文逗号分隔，与 \section 顺序一致；
% 当前节深蓝高亮、其余灰色；不配置则底部只显示页码）
\dmusetprogress{选题科学依据,已有研究不足,主要研究内容与创新点,所研究问题的难点}

% 转场页副述（英文逗号分隔，与 \section 顺序一致；不配置则转场页无副述行）
\dmusetsectiondesc{第一节一句话副述,第二节,第三节,第四节}

\title{论文题目}
\subtitle{硕士学位论文开题报告}   % 封面顶部小字
\author{报告人：××× \and 导师：××× 教授}
\institute{大连海事大学 · 交通运输工程学院}
\date{2026 年 9 月}

\AtBeginSection[]{\frame{\sectionpage}}   % 每节自动插入过渡页（可选）

\begin{document}
\begin{coverframe}          % 封面：保留横幅，隐藏进度条与页码
  \titlepage
\end{coverframe}
\begin{frame}{目录}
  \begin{dmuoutline}        % 目录条目：编号自动；副述为一句话说明
    \dmuoutlineitem{选题科学依据}{一句话副述。}
    \dmuoutlineitem{已有研究不足}{一句话副述。}
    \dmuoutlineitem{主要研究内容与创新点}{一句话副述。}
    \dmuoutlineitem{所研究问题的难点}{一句话副述。}
  \end{dmuoutline}
\end{frame}
...
```

编译必须用 **xelatex**（字体经 fontspec/xeCJK 加载）：`latexmk -xelatex example.tex`。

> 目录页样式复刻 IMHFC 2026 会议模板（desktop-wsl `~/projects/research/imhfc-ecr-mcnf/presentation/presentation_beamer.tex` 121–133 行）：每节一条浅色圆角块 = accent 大编号 + 深蓝标题 + 灰色一句话副述，编号自动。转场页（sectionpage）复刻同文件 74–96 行 `\divider` 样式：页面居中 accent 大编号 + 短横线 + 深蓝标题 + 灰色斜体副述。

## 视觉规格（与 PPTX 的对应关系）

| 元素 | 取值 | 来源 |
|------|------|------|
| 顶部横幅 | `#292F89`，高 8.3mm | 幻灯片实测主色；35mm/381mm × 90mm |
| 目录/章节编号与标题字色 | `#27308E` | PPT 目录页表格字色 |
| 强调色（分节页大数字/二级符号） | `#00A2FF` | theme1.xml accent1 |
| 警告色（alertblock） | `#FF644E` | theme1.xml accent5 |
| 底部进度条 | 与页码同一行：条目色块统一横幅蓝紫 `#292F89`，当前节白字高亮、其余灰字；页码在右端 | 汇报目录导航（第 2 页起显示，封面除外） |

可调宏：`\dmuuniv{...}`/`\dmuuniven{...}`（横幅校名中/英文）、`\dmucollege{...}`/`\dmucollegeen{...}`（横幅学院名中/英文）、`\dmubannerheight`（横幅高度长度）。

## 字体替换表

主题默认按 macOS 设置（正文西文 PT Sans + 中文 HarmonyOS Sans SC，两款字体需先安装到 `~/Library/Fonts`）：

| 平台 | 正文西文 | 正文中文 | 横幅字标中文 | 横幅字标英文 |
|------|------|------|------|------|
| macOS（默认） | PT Sans | HarmonyOS Sans SC | Xingkai SC Bold（系统自带行楷） | Zapfino（系统自带） |
| Windows | Arial 或 Segoe UI | Microsoft YaHei | 华文行楷 STXingkai（Office 附带） | Zapfino 需另装，可用 Palace Script 等手写体替代 |
| Overleaf | TeX Gyre Heros | FandolHei / Noto Sans CJK SC | 系统无行楷，需上传字体文件或回退图片方案 | 同左 |

更换平台时改 `beamerthemeDMU.sty` 中「字体」一节的对应行：正文改 `\setsansfont` 与 `\setCJKsansfont`；横幅字标改 `\newCJKfontfamily\dmu@wmcn` 与 `\newfontfamily\dmu@wmen` 两行。
