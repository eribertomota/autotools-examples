 
# # svn info
# # $Author: morongo $
# # $Date: 2009-01-11 17:17:03 +0100 (dom, 11 ene 2009) $
# # $HeadURL: https://jaula.svn.sourceforge.net/svnroot/jaula/tags/jaula-1.4.0/jaula/Makefile.am $
# # $Id: Makefile.am 45 2009-01-11 16:17:03Z morongo $
# # $Revision: 45 $

VERSION_INFO = @VERSION_INFO@

SUBDIRS = .

# # base data directory
datarootdir = @datarootdir@

# # AM_CPPFLAGS removed as required for bug 1827161
# # AM_CPPFLAGS =-Wall

# # Suggested by libtool
ACLOCAL_AMFLAGS=-I m4

lib_LTLIBRARIES = libjaula.la

include_HEADERS = jaula.h

pkginclude_HEADERS = jaula_bad_data_type.h \
jaula_exception.h \
jaula_lexan_error.h \
jaula_lexan.h \
jaula_name_duplicated.h \
jaula_no_error.h \
jaula_parse.h \
jaula_syntax_error.h \
jaula_value.h \
jaula_value_array.h \
jaula_value_boolean.h \
jaula_value_complex.h \
jaula_value_null.h \
jaula_value_number.h \
jaula_value_number_int.h \
jaula_value_object.h \
jaula_value_string.h

libjaula_la_SOURCES = $(pkginclude_HEADERS) \
jaula_bad_data_type.cc \
jaula_exception.cc \
jaula_lexan_error.cc \
jaula_name_duplicated.cc \
jaula_no_error.cc \
jaula_parse.cc \
jaula_syntax_error.cc \
jaula_value.cc \
jaula_value_array.cc \
jaula_value_boolean.cc \
jaula_value_complex.cc \
jaula_value_null.cc \
jaula_value_number.cc \
jaula_value_number_int.cc \
jaula_value_object.cc \
jaula_value_string.cc

# # Define flex files as non-distributable to avoid distribution of flex
# #generated sources.
nodist_libjaula_la_SOURCES = jaula_lexan.ll

# # As flex files are actually required, they are included in a separate
# # statement
EXTRA_DIST = jaula_lexan.ll

libjaula_la_LDFLAGS = -version-info $(VERSION_INFO)

clean-local:
	$(RM) jaula_lexan.cc

distclean-local:
	$(RM) jaula_lexan.cc

# # EOF $Id: Makefile.am 45 2009-01-11 16:17:03Z morongo $
