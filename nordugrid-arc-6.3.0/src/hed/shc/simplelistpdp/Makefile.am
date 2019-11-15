SUBDIRS = schema

noinst_LTLIBRARIES = libsimplelistpdp.la

libsimplelistpdp_la_SOURCES = SimpleListPDP.cpp SimpleListPDP.h
libsimplelistpdp_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libsimplelistpdp_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la
