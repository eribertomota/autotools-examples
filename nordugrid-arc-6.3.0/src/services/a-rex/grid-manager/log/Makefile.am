noinst_LTLIBRARIES = liblog.la

liblog_la_SOURCES = JobLog.cpp JobLog.h JobsMetrics.cpp JobsMetrics.h HeartBeatMetrics.cpp HeartBeatMetrics.h SpaceMetrics.cpp SpaceMetrics.h
liblog_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
liblog_la_LIBADD = $(top_builddir)/src/hed/libs/common/libarccommon.la
