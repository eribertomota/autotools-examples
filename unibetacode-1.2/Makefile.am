## Process this file with automake to produce Makefile.in

SUBDIRS = man src test
EXTRA_DIST = examples

#
# Add "orig" target to remove all Autotools-added files left over from
#
#      autoreconf && ./configure && make && make distclean
#
orig: distclean
	\rm -rf aclocal.m4 autom4te.cache build-aux configure *~ */*~ \
	    INSTALL Makefile.in man/Makefile.in test/Makefile.in \
	    src/Makefile.in test/Makefile.in src/config.h.in \
	    src/beta2uni.c src/uni2beta.c src/unibetaprep.c
