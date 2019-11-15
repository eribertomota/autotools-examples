noinst_LTLIBRARIES = libfiles.la

libfiles_la_SOURCES = \
	ControlFileHandling.cpp ControlFileContent.cpp JobLogFile.cpp \
	ControlFileHandling.h   ControlFileContent.h   JobLogFile.h
libfiles_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
