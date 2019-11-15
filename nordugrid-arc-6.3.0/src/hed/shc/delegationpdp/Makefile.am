SUBDIRS = schema

noinst_LTLIBRARIES = libdelegationpdp.la

libdelegationpdp_la_SOURCES = DelegationPDP.cpp DelegationPDP.h
libdelegationpdp_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libdelegationpdp_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la
