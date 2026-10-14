# 专业学位硕士研究生学位论文开题报告 — Makefile
# 用法：
#   make          编译生成 开题报告模板.pdf
#   make view     打开 PDF
#   make clean    清理中间文件
#   make distclean 清理所有生成文件（含 PDF）

TEX      = 开题报告模板
LATEXMK  = latexmk
LATEXOPT = -xelatex -interaction=nonstopmode -halt-on-error

.PHONY: all view clean distclean

all: $(TEX).pdf

$(TEX).pdf: $(TEX).tex
	$(LATEXMK) $(LATEXOPT) $(TEX).tex

view: $(TEX).pdf
	open $(TEX).pdf

clean:
	$(LATEXMK) -c $(TEX).tex

distclean: clean
	rm -f $(TEX).pdf
