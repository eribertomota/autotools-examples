EXTRA_DIST = $(wildcard *.el) Makefile.lisp liece.xpm liece.xbm
DISTCLEANFILES = liece-setup.el
export EMACS XEMACS PACKAGEDIR

all: elc

elc package install install-package clean:
	$(MAKE) $(AM_MAKEFLAGS) -f Makefile.lisp $@
