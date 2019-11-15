if HAVE_LOCAL_LIBFOLE
AM_CPPFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/common \
	@LIBCERROR_CPPFLAGS@

noinst_LTLIBRARIES = libfole.la

libfole_la_SOURCES = \
	libfole_definitions.h \
	libfole_extern.h \
	libfole_error.c libfole_error.h \
	libfole_libcerror.h \
	libfole_support.c libfole_support.h \
	libfole_types.h \
	libfole_unused.h \
	libfole_value_type.c libfole_value_type.h
endif

MAINTAINERCLEANFILES = \
	Makefile.in

distclean: clean
	/bin/rm -f Makefile

splint:
	@echo "Running splint on libfole ..."
	-splint -preproc -redef $(DEFS) $(DEFAULT_INCLUDES) $(INCLUDES) $(AM_CPPFLAGS) $(libfole_la_SOURCES)

