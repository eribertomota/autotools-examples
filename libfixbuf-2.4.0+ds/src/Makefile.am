## Process this file with automake to produce Makefile.in
## ------------------------------------------------------------------------
## Makefile.am (source)
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

lib_LTLIBRARIES = libfixbuf.la

WARN_CFLAGS = -Wall

AM_CFLAGS = $(WARN_CFLAGS) $(DEBUG_CFLAGS) $(SPREAD_CFLAGS) $(GLIB_CFLAGS)
LDADD = $(GLIB_LDADD) $(SPREAD_LDFLAGS) $(SPREAD_LIBS) $(GLIB_LIBS)

libfixbuf_la_SOURCES =  fbuf.c       fbinfomodel.c fbtemplate.c  fbsession.c \
                        fbconnspec.c fbexporter.c  fbcollector.c fbcollector.h \
                        fblistener.c fbnetflow.c   fbsflow.c     fbxml.c
nodist_libfixbuf_la_SOURCES = $(MAKE_INFOMODEL_OUTPUTS)
libfixbuf_la_LDFLAGS = -version-info $(LIBCOMPAT)

EXTRA_DIST = xml2fixbuf.xslt make-infomodel

SUBDIRS = infomodel

MAKE_INFOMODEL_OUTPUTS = infomodel.c infomodel.h
RUN_MAKE_INFOMODEL = \
  srcdir='' ; \
  test -f ./make-infomodel || srcdir=$(srcdir)/ ; \
  $(PERL) "$${srcdir}make-infomodel" --package $(PACKAGE) \
    $(INFOMODEL_REGISTRY_PREFIXES) \
  || { rm -f $(MAKE_INFOMODEL_OUTPUTS) ; exit 1 ; }

BUILT_SOURCES = $(MAKE_INFOMODEL_OUTPUTS)
if ENABLE_TOOLS
BUILT_SOURCES += ipfixDump.h
endif
CLEANFILES = $(BUILT_SOURCES)

infomodel.c : infomodel.h
infomodel.h : make-infomodel Makefile
	$(AM_V_GEN)$(RUN_MAKE_INFOMODEL)

bin_PROGRAMS =
man1_MANS =
if ENABLE_TOOLS
bin_PROGRAMS += ipfixDump
man1_MANS += ipfixDump.1
endif

PODFILES = ipfixDump.pod
HTMLFILES = ipfixDump.html
EXTRA_DIST += $(PODFILES) ipfixDump.h.in
CLEANFILES += $(man1_MANS) $(HTMLFILES)

ipfixDump_SOURCES = ipfixDump.c ipfixDumpPrint.c
nodist_ipfixDump_SOURCES = ipfixDump.h
#ipfixDump_CPPFLAGS = $(AM_CPPFLAGS) -DVERSION='"$(VERSION)"' -DCERT_IPFIX_PATH='"$(pkgdatadir)"'
ipfixDump_LDADD = libfixbuf.la $(LDADD)

IPFIXDUMP_H_SED = sed \
  -e 's|@FIXBUF_PACKAGE_NAME[@]|$(PACKAGE)|g' \
  -e 's|@FIXBUF_PACKAGE_VERSION[@]|$(PACKAGE_VERSION)|g' \
  -e 's|@FIXBUF_PACKAGE_DATADIR[@]|$(pkgdatadir)|g'

MAKE_IPFIXDUMP_H = \
  srcdir='' ; \
  test -f "./$@.in" || srcdir=$(srcdir)/ ; \
  $(IPFIXDUMP_H_SED) "$${srcdir}$@.in" > $@ || { rm -f $@ ; exit 1 ; }

ipfixDump.h: ipfixDump.h.in Makefile
	$(AM_V_GEN)$(MAKE_IPFIXDUMP_H)

FIXBUF_POD2MAN_ARGS = --center='$(PACKAGE_NAME)' --release='$(PACKAGE_VERSION)' --date='$(BUILD_DATE)'
FIXBUF_POD2HTML_ARGS = --noindex --nopoderrors

dist_pkgdata_DATA =
noinst_DATA =
if ENABLE_TOOLS
dist_pkgdata_DATA += cert_ipfix.xml
noinst_DATA += share/$(PACKAGE)/cert_ipfix.xml
endif

SYMLINK_CERT_IPFIX = \
  target="$?" ; \
  expr "x$${target}" : "x/" >/dev/null || target="../../$${target}" ; \
  { test -d share/$(PACKAGE) || $(MKDIR_P) share/$(PACKAGE) ; } && \
  { cd share/$(PACKAGE) && $(LN_S) "$${target}" cert_ipfix.xml ; }

share/$(PACKAGE)/cert_ipfix.xml: cert_ipfix.xml
	$(AM_V_GEN)$(SYMLINK_CERT_IPFIX)

CLEANFILES += $(noinst_DATA)


if ENABLE_TOOLS
TOOLS_DOCS = tools-docs
endif

RUN_POD2HTML = \
  add_header=$(top_builddir)/doc/add-header.pl ; \
  test -f "$${add_header}" || add_header="$(top_srcdir)/doc/add-header.pl" ; \
  { $(POD2HTML) $(FIXBUF_POD2HTML_ARGS) --title="$*" \
    --infile="$<" --outfile="$@" && \
    $(PERL) "$${add_header}" "$@" ; } || { rm -f "$@" ; exit 1 ; }

.pod.1:
	$(AM_V_GEN)$(POD2MAN) $(FIXBUF_POD2MAN_ARGS) --section=1 $< $@

.pod.html:
	$(AM_V_GEN)$(RUN_POD2HTML)

docs: $(TOOLS_DOCS)

tools-docs: $(HTMLFILES)
	@test -d $(top_builddir)/doc/html || $(MKDIR_P) $(top_builddir)/doc/html
	cp -p $(HTMLFILES) $(top_builddir)/doc/html

CLEAN_HTML = \
  dir='$(top_builddir)/doc/html' ; \
  files='$(HTMLFILES)' ; \
  test -z "$$files" \
  || { test ! -d "$$dir" && test ! -f "$$dir" && test ! -r "$$dir" ; } \
  || { cd "$$dir" && rm -f $$files ; }

mostlyclean-local:
	$(CLEAN_HTML)
	rm -f pod2htm*.tmp

.PHONY: docs tools-docs
