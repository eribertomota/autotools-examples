## Process this file with automake to produce Makefile.in
## $Id: Makefile.am,v 1.4 2006-08-04 20:50:19 flux Exp $

TROFF =  groff
ZOEM  =  zoem
TIDY  =  tidy

docdir = $(datadir)/doc/$(PACKAGE)
docdocdir = $(docdir)

azms =  apparix.azm

docdoc_DATA = apparix.html apparix.ps $(azms)
man_MANS    = apparix.1

EXTRA_DIST = $(azms) $(docdoc_DATA)  $(man_MANS)

SUFFIXES = .1 .7 .azm .html .ps

.azm.1:
	$(ZOEM) --allow=../src/apparix -d roff -i $< -o $@
	$(ZOEM) --allow=../src/apparix -d roff -i $< -o $@

.azm.7:
	$(ZOEM) -d roff -i $< -o $@
	$(ZOEM) -d roff -i $< -o $@

.1.ps:
	$(TROFF) -man $< > $@

.7.ps:
	$(TROFF) -man $< > $@

.azm.html:
	$(ZOEM) --allow=../src/apparix:date -d html -i $< -o $@
	$(ZOEM) --allow=../src/apparix:date -d html -i $< -o $@
	- $(TIDY) -e $@

