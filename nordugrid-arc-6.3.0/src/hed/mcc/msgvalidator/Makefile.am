SUBDIRS = schema

pkglib_LTLIBRARIES = libmccmsgvalidator.la

libmccmsgvalidator_la_SOURCES = MCCMsgValidator.cpp MCCMsgValidator.h
libmccmsgvalidator_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libmccmsgvalidator_la_LIBADD = \
	$(top_builddir)/src/hed/libs/ws-addressing/libarcwsaddressing.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS)
libmccmsgvalidator_la_LDFLAGS  = -no-undefined -avoid-version -module
