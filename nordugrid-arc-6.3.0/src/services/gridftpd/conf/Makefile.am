noinst_LTLIBRARIES = libconf.la

libconf_la_SOURCES = \
	conf_vo.cpp daemon.cpp \
	conf_vo.h   daemon.h
libconf_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(GLOBUS_IO_CFLAGS) $(AM_CXXFLAGS)
