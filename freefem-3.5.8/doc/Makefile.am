# -*- Mode: makefile  -*-
# SUMMARY:      
# USAGE:        make <make-target>
# AUTHOR:       Christophe Prud'homme
# ORG:          Christophe Prud'homme
# E-MAIL:       Christophe.Prudhomme@ann.jussieu.fr
# ORIG-DATE:     7-Aug-99 at 16:19:03
# LAST-MOD: 23-Sep-02 at 13:45:01 by Christophe Prud'homme
# DESCRIPTION:  
# DESCRIP-END.	

SUFFIXES	= .cpp .hpp .c .h .f .F .o .moc

TEX		= freefem.tex intro.tex install.tex generalities.tex examples.tex copyright.tex fdl.tex
EXTRA_DIST	= $(TEX) 

DISTCLEANFILES	= freefem.log\
freefem.idx\
freefem.aux\
freefem.out\
freefem.pdf\
copyright.aux\
freefem.toc\
intro.aux\
install.aux\
generalities.aux\
examples.aux\
fdl.aux\
freefem.ind\
freefem.ilg


all:	html pdf

html: $(TEX)

pdf: $(TEX)
	pdflatex $(srcdir)/freefem
	makeindex freefem
	pdflatex $(srcdir)/freefem
	pdflatex $(srcdir)/freefem

