noinst_LTLIBRARIES = librun.la

librun_la_SOURCES = run_plugin.cpp run_plugin.h
librun_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
librun_la_LIBADD = $(DLOPEN_LIBS) -lpthread
