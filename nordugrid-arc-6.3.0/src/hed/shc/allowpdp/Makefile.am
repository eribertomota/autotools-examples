noinst_LTLIBRARIES = liballowpdp.la

liballowpdp_la_SOURCES = AllowPDP.cpp AllowPDP.h
liballowpdp_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
liballowpdp_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la
