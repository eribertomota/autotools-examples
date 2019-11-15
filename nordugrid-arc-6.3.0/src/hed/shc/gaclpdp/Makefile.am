noinst_LTLIBRARIES = libgaclpdp.la

libgaclpdp_la_SOURCES = GACLRequest.cpp GACLRequest.h \
	GACLPolicy.cpp GACLPolicy.h \
	GACLEvaluator.cpp GACLEvaluator.h \
	GACLPDP.cpp GACLPDP.h
libgaclpdp_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libgaclpdp_la_LIBADD = $(top_builddir)/src/hed/libs/common/libarccommon.la
