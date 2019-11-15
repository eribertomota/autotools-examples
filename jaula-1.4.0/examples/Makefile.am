 
# # svn info
# # $Author: morongo $
# # $Date: 2009-01-11 17:17:03 +0100 (dom, 11 ene 2009) $
# # $HeadURL: https://jaula.svn.sourceforge.net/svnroot/jaula/tags/jaula-1.4.0/examples/Makefile.am $
# # $Id: Makefile.am 45 2009-01-11 16:17:03Z morongo $
# # $Revision: 45 $

SUBDIRS = .

# # base data directory
datarootdir = @datarootdir@

# # Suggested by libtool
ACLOCAL_AMFLAGS=-I m4

# -Wall option removed as required for bug 1827161
AM_CPPFLAGS = -I $(top_srcdir)/jaula

# # document destination
pkgdocdir=$(datadir)/doc/$(PACKAGE_NAME)

# # JSON data examples will be installed with the documentation
pkgdoc_DATA = example1.json example2.json example3.json malformed_example3.json

# # Include examples in software distribution
EXTRA_DIST = $(pkgdoc_DATA)

# # lextst will not be installed anywhere
noinst_PROGRAMS = lextst

# # jparse will be installed in standard binaries directory
bin_PROGRAMS = jparse

# # lextst generation directives
lextst_SOURCES = lextst.cc
lextst_LDADD = $(top_builddir)/jaula/libjaula.la
lextst_LDFLAGS = -static

# # jparse generation directives
jparse_SOURCES = jparse.cc
jparse_LDADD = $(top_builddir)/jaula/libjaula.la
# # jparse_LDFLAGS = -static

# # EOF $Id: Makefile.am 45 2009-01-11 16:17:03Z morongo $
