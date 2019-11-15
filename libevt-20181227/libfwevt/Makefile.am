if HAVE_LOCAL_LIBFWEVT
AM_CPPFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/common \
	@LIBCERROR_CPPFLAGS@ \
	@LIBCTHREADS_CPPFLAGS@ \
	@LIBCDATA_CPPFLAGS@ \
	@LIBCNOTIFY_CPPFLAGS@ \
	@LIBFDATETIME_CPPFLAGS@ \
	@LIBFGUID_CPPFLAGS@ \
	@LIBFVALUE_CPPFLAGS@ \
	@LIBUNA_CPPFLAGS@ \
	@PTHREAD_CPPFLAGS@

noinst_LTLIBRARIES = libfwevt.la

libfwevt_la_SOURCES = \
	fwevt_template.h \
	libfwevt_channel.c libfwevt_channel.h \
	libfwevt_debug.c libfwevt_debug.h \
	libfwevt_definitions.h \
	libfwevt_extern.h \
	libfwevt_error.c libfwevt_error.h \
	libfwevt_event.c libfwevt_event.h \
	libfwevt_libcdata.h \
	libfwevt_libcerror.h \
	libfwevt_libcnotify.h \
	libfwevt_libfguid.h \
	libfwevt_libfvalue.h \
	libfwevt_libuna.h \
	libfwevt_keyword.c libfwevt_keyword.h \
	libfwevt_level.c libfwevt_level.h \
	libfwevt_manifest.c libfwevt_manifest.h \
	libfwevt_map.c libfwevt_map.h \
	libfwevt_opcode.c libfwevt_opcode.h \
	libfwevt_provider.c libfwevt_provider.h \
	libfwevt_support.c libfwevt_support.h \
	libfwevt_task.c libfwevt_task.h \
	libfwevt_template.c libfwevt_template.h \
	libfwevt_types.h \
	libfwevt_unused.h \
	libfwevt_xml_document.c libfwevt_xml_document.h \
	libfwevt_xml_tag.c libfwevt_xml_tag.h \
	libfwevt_xml_template_value.c libfwevt_xml_template_value.h \
	libfwevt_xml_token.c libfwevt_xml_token.h
endif

MAINTAINERCLEANFILES = \
	Makefile.in

distclean: clean
	/bin/rm -f Makefile

splint:
	@echo "Running splint on libfwevt ..."
	-splint -preproc -redef $(DEFS) $(DEFAULT_INCLUDES) $(INCLUDES) $(AM_CPPFLAGS) $(libfwevt_la_SOURCES)

