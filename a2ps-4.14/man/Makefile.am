## Process this file with automake to produce Makefile.in -*-Makefile-*-
man_MANS = a2ps.1 card.1 fixps.1 pdiff.1 psmandup.1 psset.1 texi2dvi4a2ps.1
man_aux = $(man_MANS:.1=.x)

irregular_men = a2ps.1 texi2dvi4a2ps.1
a2ps.1 : $(top_srcdir)/src/main.c
texi2dvi4a2ps.1: $(top_srcdir)/contrib/texi2dvi4a2ps

EXTRA_DIST = $(man_MANS) $(HELP2MAN) $(man_aux) \
  Makefile.maint GNUmakefile common.x
PERL = @PERL@
HELP2MAN = help2man
MAINTAINERCLEANFILES = $(man_MANS)

# For additional rules usually of interest only to the maintainer,
# see GNUmakefile and Makefile.maint.
