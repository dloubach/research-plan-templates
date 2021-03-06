# General Makefile rules

TOPIC   = presentation
MAIN    = $(TOPIC)

BIBDIR       = refs
BIBFILES     = $(wildcard $(BIBDIR)/*.bib)
TEXFILES     = $(wildcard ./*.tex)
STYLEFILES   = $(wildcard ./*.sty)

all: $(MAIN).pdf

# main rule
$(MAIN).pdf: $(MAIN).tex $(TEXFILES)  Makefile $(STYLEFILES) $(BIBFILES)
   # Create PDF-files
	pdflatex $(subst .pdf,.tex,$@)
	pdflatex $(subst .pdf,.tex,$@)
	bibtex $(subst .pdf,,$@)
	pdflatex $(subst .pdf,.tex,$@)	
	@while ( grep "Rerun to get cross-references" 	\
	$(subst .pdf,.log,$@) > /dev/null ); do		\
	        echo '** Re-running LaTeX **';		\
	        pdflatex $(subst .pdf,.tex,$@);         \
	done

# clean rule
clean:
	rm -f ./*.aux
	rm -f ./*.tex~
	rm -f ./*.log
	rm -f ./*.ps
	rm -f ./*.dvi
	rm -f ./*.blg
	rm -f ./*.bbl
	rm -f ./*.tmp
	rm -f ./*.bib~
	rm -f ./*.thm
	rm -f ./*.toc
	rm -f ./*.lo*
	rm -f ./comment.cut
	rm -f ./*.nav
	rm -f ./*.out
	rm -f ./*.snm
	rm -f ./*~
	rm -f ./*.pdf
	rm -f ./*.gl*
	rm -f ./*.ist
	rm -f ./*.rel
	rm -f ./\#*
	rm -f ./*.tdo
	rm -f ./*.gz
	rm -f ./*.fdb_latexmk
	rm -f ./*.fls
	rm -rf ./figs/*.pdf
	rm -rf ./*-blx.bib
	rm -rf ./*.run.xml


# works for linux and mac
# decide which PDF viewer based on the operating system
LINUX_PDF_VIEWER = evince
MAC_PDF_VIEWER = open
PDF_VIEWER =
UNAME_S := $(shell uname -s)
ifeq ($(UNAME_S),Linux)
	PDF_VIEWER = $(LINUX_PDF_VIEWER)
else
	PDF_VIEWER = $(MAC_PDF_VIEWER)
endif

view: $(MAIN).pdf
	@echo Currently using $(UNAME_S) 
	$(PDF_VIEWER) $(MAIN).pdf &


# continuous latex compilation
continous:
	make all
	latexmk -pvc -bibtex -pdf -view=none $(MAIN).tex
