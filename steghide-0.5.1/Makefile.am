AUTOMAKE_OPTIONS = dist-bzip2 dist-zip foreign
SUBDIRS = m4 intl po doc src tests
docdir = $(prefix)/share/doc/$(PACKAGE)
EXTRA_DIST = config.rpath ABOUT-NLS BUGS CREDITS HISTORY LEAME depcomp
doc_DATA = ABOUT-NLS BUGS COPYING CREDITS HISTORY INSTALL LEAME README TODO
MAINTAINERCLEANFILES = Makefile.in aclocal.m4 config.guess config.h.in \
config.sub configure depcomp install-sh missing steghide.doxygen steghide.spec

ACLOCAL_AMFLAGS = -I m4

uninstall-local:
	rmdir $(docdir)
