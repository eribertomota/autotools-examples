noinst_LIBRARIES = libcurl.a

libcurlincludedir = $(includedir)/SDL

INCLUDES = -I$(top_srcdir)/include -I$(top_builddir)/lib -I$(top_srcdir)/lib

# Makefile.inc provides the CSOURCES and HHEADERS defines
include Makefile.inc

libcurl_a_SOURCES = $(CSOURCES) $(HHEADERS)

WIN32SOURCES = $(CSOURCES)
WIN32HEADERS = $(HHEADERS) config-win32.h
