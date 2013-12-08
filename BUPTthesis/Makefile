# Makefile for Dissertation

# base name of your top-level .tex file
TARGET=bare_thesis
# list of .tex files for frontmatter
FRONTMATTER= abstract.tex notations.tex
# list of .tex files for mainmatter
MAINMATTER = chapters/ch01_intro.tex		\
             chapters/ch02_env.tex		\
             chapters/ch03_twostep.tex		\
             chapters/ch04_threestep.tex	\
             chapters/ch05_qd.tex		\
             chapters/ch06_concln.tex

# list of .tex files for backmatter
BACKMATTER = acronyms.tex ackgt.tex pubs.tex
# list of .bbl files
#BBLTARGET = $(TARGET).bbl jrnl.bbl conf.bbl
BBLTARGET = jrnl.bbl conf.bbl			\
            chapters/ch01_intro.bbl 		\
            chapters/ch02_env.bbl		\
            chapters/ch03_twostep.bbl		\
            chapters/ch04_threestep.bbl		\
            chapters/ch05_qd.bbl		\
            chapters/ch06_concln.bbl

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

chapters/%.bbl: %.aux
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
	$(RM) *.bbl *.blg chapters/*.bbl chapters/*.blg
	$(RM) *.aux *.log
	$(RM) *.acn *.glo *.ist *.acr *.alg
	$(RM) *.out *.toc *.thm
