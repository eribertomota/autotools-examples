noinst_LTLIBRARIES = libjobs.la

libjobs_la_SOURCES = \
	CommFIFO.cpp JobsList.cpp GMJob.cpp JobDescriptionHandler.cpp \
	ContinuationPlugins.cpp DTRGenerator.cpp \
	CommFIFO.h   JobsList.h   GMJob.h   JobDescriptionHandler.h   \
	ContinuationPlugins.h   DTRGenerator.h
libjobs_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
libjobs_la_LIBADD = \
	$(top_builddir)/src/libs/data-staging/libarcdatastaging.la \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(DBCXX_LIBS)
