# Makefile for Dissertation

# base name of your top-level .tex file
TARGET=bare_thesis
# list of .tex files for frontmatter
FRONTMATTER= abstract.tex notations.tex
# list of .tex files for mainmatter
MAINMATTER = ch_intro.tex ch_concln.tex # ch02-yyy.tex ch03-zzz.tex
# list of .tex files for backmatter
BACKMATTER = acronyms.tex ackgt.tex pubs.tex
# list of .bbl files
BBLTARGET = $(TARGET).bbl jrnl.bbl conf.bbl
# BBLTARGET = $(basename $(MAINMATTER)).bbl jrnl.bbl conf.bbl

# alias for latex, dvips, gs, bibtex, makeindex and rm
PDFLATEX=pdflatex
BIBTEX=bibtex
MKIDX=makeindex
RM=rm -f

all: $(TARGET).pdf clean
.PHONY: all

$(TARGET).pdf: $(TARGET).tex $(TARGET).acr
	$(MAKE) $(BBLTARGET)
	$(PDFLATEX) $^
	$(PDFLATEX) $^

%.acr %.alg: %.acn
	$(MKIDX) -s $(basename $@).ist -t $(basename $@).alg -o $@ $^

%.aux %.acn %.ist %.log: %.tex
	$(PDFLATEX) $^

%.bbl: %.aux
	$(BIBTEX) $(basename $<)

# pubs.bbl: pubs.aux
#         $(BIBTEX) $(basename $<)

# $(TARGET).aux pubs.aux ch%.aux: $(TARGET).tex $(MAINMATTER)
#         $(LATEX) $(TARGET)
#         $(RM) $(TARGET).dvi
#         $(MKIDX) -s $(TARGET).ist -t $(TARGET).alg -o $(TARGET).acr $(TARGET).acn

.PHONY: clean
clean:
	$(RM) chapters/*.aux
	$(RM) *.bbl *.blg
	$(RM) *.aux *.log
	$(RM) *.acn *.glo *.ist *.acr *.alg
	$(RM) *.out *.toc *.thm
