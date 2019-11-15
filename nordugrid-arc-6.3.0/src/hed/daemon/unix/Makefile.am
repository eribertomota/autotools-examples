noinst_LTLIBRARIES = libdaemon.la

libdaemon_la_SOURCES = daemon.cpp main_unix.cpp daemon.h
libdaemon_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libdaemon_la_LIBADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(SYSTEMD_DAEMON_LIBS)
