noinst_LTLIBRARIES = libarcfn.la
libarcfn_ladir = $(pkgincludedir)/security/ArcPDP/fn
libarcfn_la_HEADERS = Function.h FnFactory.h EqualFunction.h MatchFunction.h InRangeFunction.h
libarcfn_la_SOURCES = EqualFunction.cpp MatchFunction.cpp InRangeFunction.cpp
libarcfn_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcfn_la_LIBADD = $(top_builddir)/src/hed/libs/common/libarccommon.la
