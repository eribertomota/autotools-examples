SUBDIRS = attr fn policy alg

noinst_LTLIBRARIES = libarcpdp.la
libarcpdp_ladir = $(pkgincludedir)/security/ArcPDP
libarcpdp_la_HEADERS = Source.h EvaluationCtx.h Evaluator.h Response.h \
	Request.h RequestItem.h Result.h EvaluatorLoader.h PolicyParser.h \
	PolicyStore.h
libarcpdp_la_SOURCES = Source.cpp Evaluator.cpp EvaluatorLoader.cpp \
	PolicyParser.cpp PolicyStore.cpp
libarcpdp_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcpdp_la_LIBADD = \
	attr/libarcattr.la fn/libarcfn.la \
	policy/libarcpolicy.la alg/libarcalg.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS)
