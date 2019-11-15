## Process this file with automake to produce Makefile.in

noinst_DATA = html/index.html libtagcoll.doxytags

PAPER=tagbk-draft

if DO_DOCS
libtagcoll.doxytags: libtagcoll.dox ../tagcoll/libtagcoll2.la
	doxygen $<

html/index.html: libtagcoll.dox ../tagcoll/libtagcoll2.la
	doxygen $<

$(PAPER).pdf: $(PAPER).aux
	pdflatex $(PAPER).tex

$(PAPER).ps: $(PAPER).dvi
	dvips $(PAPER) -o

$(PAPER).dvi: $(PAPER).bbl
	latex $(PAPER).tex
	latex $(PAPER).tex

$(PAPER).aux: $(PAPER).tex
	latex $<

$(PAPER).bbl: $(PAPER).aux
	bibtex $(PAPER)

else
libtagcoll.doxytags: libtagcoll.dox ../tagcoll/libtagcoll2.la
	touch $@

html/index.html: libtagcoll.dox ../tagcoll/libtagcoll2.la
	mkdir html || true
	touch $@
endif

EXTRA_DIST = libtagcoll.dox tagbk-draft.tex local.bib tagcoll-man-hooks taggrep-man-hooks tagidx-man-hooks

CLEANFILES = libtagcoll.doxytags $(PAPER).aux $(PAPER).bbl $(PAPER).blg $(PAPER).ps $(PAPER).pdf $(PAPER).dvi $(PAPER).idx $(PAPER).log 

clean-local:
	rm -rf html
