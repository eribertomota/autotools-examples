if HAVE_LOCAL_LIBWRC
AM_CPPFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/common \
	@LIBCERROR_CPPFLAGS@ \
	@LIBCDATA_CPPFLAGS@ \
	@LIBCLOCALE_CPPFLAGS@ \
	@LIBCNOTIFY_CPPFLAGS@ \
	@LIBCSPLIT_CPPFLAGS@ \
	@LIBUNA_CPPFLAGS@ \
	@LIBCFILE_CPPFLAGS@ \
	@LIBCPATH_CPPFLAGS@ \
	@LIBBFIO_CPPFLAGS@ \
	@LIBFCACHE_CPPFLAGS@ \
	@LIBFDATA_CPPFLAGS@ \
	@LIBFDATETIME_CPPFLAGS@ \
	@LIBFGUID_CPPFLAGS@ \
	@LIBFVALUE_CPPFLAGS@ \
	@LIBFWEVT_CPPFLAGS@ \
	@LIBFWNT_CPPFLAGS@ \
	@PTHREAD_CPPFLAGS@ 

noinst_LTLIBRARIES = libwrc.la

libwrc_la_SOURCES = \
	libwrc_codepage.h \
	libwrc_data_descriptor.c libwrc_data_descriptor.h \
	libwrc_debug.c libwrc_debug.h \
	libwrc_definitions.h \
	libwrc_error.c libwrc_error.h \
	libwrc_extern.h \
	libwrc_io_handle.c libwrc_io_handle.h \
	libwrc_language_entry.c libwrc_language_entry.h \
	libwrc_language_table.c libwrc_language_table.h \
	libwrc_libbfio.h \
	libwrc_libcdata.h \
	libwrc_libcerror.h \
	libwrc_libclocale.h \
	libwrc_libcnotify.h \
	libwrc_libfcache.h \
	libwrc_libfdata.h \
	libwrc_libfguid.h \
	libwrc_libfvalue.h \
	libwrc_libfwevt.h \
	libwrc_libfwnt.h \
	libwrc_libuna.h \
	libwrc_manifest.c libwrc_manifest.h \
	libwrc_manifest_values.c libwrc_manifest_values.h \
	libwrc_message_table.c libwrc_message_table.h \
	libwrc_message_table_values.c libwrc_message_table_values.h \
	libwrc_mui.c libwrc_mui.h \
	libwrc_mui_values.c libwrc_mui_values.h \
	libwrc_notify.c libwrc_notify.h \
	libwrc_resource.c libwrc_resource.h \
	libwrc_resource_values.c libwrc_resource_values.h \
	libwrc_stream.c libwrc_stream.h \
	libwrc_support.c libwrc_support.h \
	libwrc_string.c libwrc_string.h \
	libwrc_string_values.c libwrc_string_values.h \
	libwrc_types.h \
	libwrc_unused.h \
	libwrc_version.c libwrc_version.h \
	libwrc_version_values.c libwrc_version_values.h \
	libwrc_wevt_channel.c libwrc_wevt_channel.h \
	libwrc_wevt_event.c libwrc_wevt_event.h \
	libwrc_wevt_keyword.c libwrc_wevt_keyword.h \
	libwrc_wevt_level.c libwrc_wevt_level.h \
	libwrc_wevt_map.c libwrc_wevt_map.h \
	libwrc_wevt_opcode.c libwrc_wevt_opcode.h \
	libwrc_wevt_provider.c libwrc_wevt_provider.h \
	libwrc_wevt_task.c libwrc_wevt_task.h \
	libwrc_wevt_template.c libwrc_wevt_template.h \
	libwrc_wevt_template_definition.c libwrc_wevt_template_definition.h \
	libwrc_wevt_template_values.c libwrc_wevt_template_values.h \
	wrc_data_descriptor.h \
	wrc_message_table_resource.h \
	wrc_mui_resource.h \
	wrc_resource_node.h \
	wrc_version_resource.h
endif

MAINTAINERCLEANFILES = \
	Makefile.in

distclean: clean
	/bin/rm -f Makefile

splint:
	@echo "Running splint on libwrc ..."
	-splint -preproc -redef $(DEFS) $(DEFAULT_INCLUDES) $(INCLUDES) $(AM_CPPFLAGS) $(libwrc_la_SOURCES)

