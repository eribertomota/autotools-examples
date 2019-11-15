noinst_LTLIBRARIES = libconf.la

libconf_la_SOURCES = \
  GMConfig.h GMConfig.cpp \
  CoreConfig.cpp CoreConfig.h \
  UrlMapConfig.cpp UrlMapConfig.h \
  CacheConfig.cpp CacheConfig.h \
  StagingConfig.cpp StagingConfig.h
libconf_la_CXXFLAGS = -I$(top_srcdir)/include \
  $(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
