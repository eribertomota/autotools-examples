noinst_LTLIBRARIES = libarcpolicy.la
libarcpolicy_ladir = $(pkgincludedir)/security/ArcPDP/policy
libarcpolicy_la_HEADERS = Policy.h
libarcpolicy_la_SOURCES = Policy.cpp
libarcpolicy_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcpolicy_la_LIBADD =  $(top_builddir)/src/hed/libs/common/libarccommon.la
