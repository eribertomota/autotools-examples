if HAVE_LOCAL_LIBFWPS
AM_CPPFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/common \
	@LIBCERROR_CPPFLAGS@ \
	@LIBCTHREADS_CPPFLAGS@ \
	@LIBCDATA_CPPFLAGS@ \
	@LIBCNOTIFY_CPPFLAGS@ \
	@LIBUNA_CPPFLAGS@ \
	@LIBFDATETIME_CPPFLAGS@ \
	@LIBFGUID_CPPFLAGS@ \
	@LIBFOLE_CPPFLAGS@ \
	@PTHREAD_CPPFLAGS@

noinst_LTLIBRARIES = libfwps.la

libfwps_la_SOURCES = \
	libfwps_codepage.h \
	libfwps_definitions.h \
	libfwps_extern.h \
	libfwps_error.c libfwps_error.h \
	libfwps_format_class_identifier.c libfwps_format_class_identifier.h \
	libfwps_libcerror.h \
	libfwps_libcnotify.h \
	libfwps_libfguid.h \
	libfwps_libfole.h \
	libfwps_libuna.h \
	libfwps_property_identifier.c libfwps_property_identifier.h \
	libfwps_storage.c libfwps_storage.h \
	libfwps_support.c libfwps_support.h \
	libfwps_types.h \
	libfwps_unused.h \
	libfwps_value.c libfwps_value.h
endif

MAINTAINERCLEANFILES = \
	Makefile.in

distclean: clean
	/bin/rm -f Makefile

splint:
	@echo "Running splint on libfwps ..."
	-splint -preproc -redef $(DEFS) $(DEFAULT_INCLUDES) $(INCLUDES) $(AM_CPPFLAGS) $(libfwps_la_SOURCES)

