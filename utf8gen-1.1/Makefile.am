## Process this file with automake to produce Makefile.in

SUBDIRS = doc man src test

#
# Add "orig" target to remove all Autotools-added files left over from
#
#      autoreconf && ./configure && make && make distclean
#
orig: distclean
	\rm -rf aclocal.m4 autom4te.cache build-aux configure *~ */*~ \
	    INSTALL Makefile.in doc/Makefile.in man/Makefile.in \
	    src/Makefile.in test/Makefile.in src/config.h.in doc/utf8gen.info
