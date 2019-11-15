## Process this file with automake to produce Makefile.in

## ------------------------------------------------------------------------
## Makefile.am (toplevel)
## autotools build system for libfixbuf
## ------------------------------------------------------------------------
## @OPENSOURCE_LICENSE_START@
## libfixbuf 2.0
##
## Copyright 2018-2019 Carnegie Mellon University. All Rights Reserved.
##
## NO WARRANTY. THIS CARNEGIE MELLON UNIVERSITY AND SOFTWARE
## ENGINEERING INSTITUTE MATERIAL IS FURNISHED ON AN "AS-IS"
## BASIS. CARNEGIE MELLON UNIVERSITY MAKES NO WARRANTIES OF ANY KIND,
## EITHER EXPRESSED OR IMPLIED, AS TO ANY MATTER INCLUDING, BUT NOT
## LIMITED TO, WARRANTY OF FITNESS FOR PURPOSE OR MERCHANTABILITY,
## EXCLUSIVITY, OR RESULTS OBTAINED FROM USE OF THE
## MATERIAL. CARNEGIE MELLON UNIVERSITY DOES NOT MAKE ANY WARRANTY OF
## ANY KIND WITH RESPECT TO FREEDOM FROM PATENT, TRADEMARK, OR
## COPYRIGHT INFRINGEMENT.
##
## Released under a GNU-Lesser GPL 3.0-style license, please see
## LICENSE.txt or contact permission@sei.cmu.edu for full terms.
##
## [DISTRIBUTION STATEMENT A] This material has been approved for
## public release and unlimited distribution.  Please see Copyright
## notice for non-US Government use and distribution.
##
## Carnegie Mellon(R) and CERT(R) are registered in the U.S. Patent
## and Trademark Office by Carnegie Mellon University.
##
## DM18-0325
## @OPENSOURCE_LICENSE_END@
## ------------------------------------------------------------------------
## Authors: Brian Trammell
## ------------------------------------------------------------------------

ACLOCAL_AMFLAGS = -I m4

SUBDIRS = src include
pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libfixbuf.pc

include doxygen.am

MOSTLYCLEANFILES = $(DX_CLEANFILES)
DISTCLEANFILES = $(RELEASES_XML)

RELEASES_XML = doc/releases.xml


dist-hook: docs copy-doxygen-doc

docs: make-doc-path doxygen-doc subdir-docs $(RELEASES_XML)

make-doc-path:
	test -d $(top_builddir)/doc/html || $(MKDIR_P) $(top_builddir)/doc/html

subdir-docs:
	cd $(top_builddir)/src && $(MAKE) docs

copy-doxygen-doc:
	cp -pR doc/html $(distdir)/doc

RUN_NEWS2XHTML = \
 srcdir='' ; \
 test -f ./doc/news2xhtml.pl || srcdir=$(srcdir)/ ; \
 if $(AM_V_P) ; then \
 echo "$(PERL) $${srcdir}doc/news2xhtml.pl $(PACKAGE_TARNAME) < '$<' > '$@'" ; \
 else echo "  GEN     " $@ ; fi ; \
 $(PERL) $${srcdir}doc/news2xhtml.pl $(PACKAGE_TARNAME) < "$<" > "$@" || \
 { rm "$@" ; exit 1 ; }

$(RELEASES_XML): NEWS
	@$(RUN_NEWS2XHTML)

EXTRA_DIST = \
     Doxyfile.in \
     libfixbuf.spec.in \
     LICENSE.txt \
     doc/Doxyhead.html \
     doc/Doxyfoot.html \
     doc/DoxygenLayout.xml \
     doc/add-header.pl \
     doc/doxygen.css \
     doc/news2xhtml.pl
