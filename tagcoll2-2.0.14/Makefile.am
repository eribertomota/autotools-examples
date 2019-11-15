## Process this file with automake to produce Makefile.in

SUBDIRS = tagcoll tools bench doc .

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA=libtagcoll2.pc

man_MANS = tagcoll.1
#tagidx.1

tagcoll.1: tools/tagcoll $(srcdir)/doc/tagcoll-man-hooks
	tools/tagcoll --manpage=$(srcdir)/doc/tagcoll-man-hooks > $@ || rm $@

#tagidx.1: tools/manpage doc/tagidx-man-hooks
#	tools/manpage tagidx doc/tagidx-man-hooks > $@ || rm $@

EXTRA_DIST = autogen.sh libtagcoll2.pc.in COPYING.libtagcoll mkbench mkgraphs

CLEANFILES = tagcoll.1
