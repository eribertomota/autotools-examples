noinst_LTLIBRARIES = libdenypdp.la

libdenypdp_la_SOURCES = DenyPDP.cpp DenyPDP.h
libdenypdp_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libdenypdp_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la
