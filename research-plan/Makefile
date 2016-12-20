# General Makefile rules

TOPIC   = rplan
MAIN    = $(TOPIC)

BIBDIR       = refs
BIBFILES     = $(wildcard $(BIBDIR)/*.bib)
TEXFILES     = $(wildcard ./*.tex)
STYLEFILES   = $(wildcard ./*.sty)

all: research-plan

research-plan: $(MAIN).pdf

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
	rm -rf ./figs/*.pdf

# works for linux
view:
	evince $(MAIN).pdf &
