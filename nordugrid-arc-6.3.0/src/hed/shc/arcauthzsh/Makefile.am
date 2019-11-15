SUBDIRS = schema

noinst_LTLIBRARIES = libarcauthzsh.la

libarcauthzsh_la_SOURCES = ArcAuthZ.cpp ArcAuthZ.h
libarcauthzsh_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcauthzsh_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la
