noinst_LTLIBRARIES = libarcalg.la
libarcalg_ladir = $(pkgincludedir)/security/ArcPDP/alg
libarcalg_la_HEADERS = AlgFactory.h CombiningAlg.h DenyOverridesAlg.h PermitOverridesAlg.h OrderedAlg.h
libarcalg_la_SOURCES = DenyOverridesAlg.cpp PermitOverridesAlg.cpp OrderedAlg.cpp
libarcalg_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcalg_la_LIBADD = $(top_builddir)/src/hed/libs/common/libarccommon.la
