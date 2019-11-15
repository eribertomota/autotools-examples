if HAVE_LOCAL_LIBCDIRECTORY
AM_CPPFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/common \
	@LIBCERROR_CPPFLAGS@ \
	@LIBCLOCALE_CPPFLAGS@ \
	@LIBUNA_CPPFLAGS@

noinst_LTLIBRARIES = libcdirectory.la

libcdirectory_la_SOURCES = \
	libcdirectory_definitions.h \
	libcdirectory_error.c libcdirectory_error.h \
	libcdirectory_extern.h \
	libcdirectory_directory.c libcdirectory_directory.h \
	libcdirectory_directory_entry.c libcdirectory_directory_entry.h \
	libcdirectory_libcerror.h \
	libcdirectory_libclocale.h \
	libcdirectory_libuna.h \
	libcdirectory_support.c libcdirectory_support.h \
	libcdirectory_system_string.c libcdirectory_system_string.h \
	libcdirectory_types.h \
	libcdirectory_unused.h \
	libcdirectory_wide_string.c libcdirectory_wide_string.h
endif

MAINTAINERCLEANFILES = \
	Makefile.in

distclean: clean
	/bin/rm -f Makefile

splint:
	@echo "Running splint on libcdirectory ..."
	-splint -preproc -redef $(DEFS) $(DEFAULT_INCLUDES) $(INCLUDES) $(AM_CPPFLAGS) $(libcdirectory_la_SOURCES)

