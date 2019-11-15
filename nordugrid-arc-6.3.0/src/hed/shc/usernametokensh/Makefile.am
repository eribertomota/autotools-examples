SUBDIRS = schema

noinst_LTLIBRARIES = libusernametokensh.la

libusernametokensh_la_SOURCES = UsernameTokenSH.cpp UsernameTokenSH.h
libusernametokensh_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libusernametokensh_la_LIBADD = \
	$(top_builddir)/src/hed/libs/ws-security/libarcwssecurity.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la
