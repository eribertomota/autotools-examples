SUBDIRS = code file_formats headers unix_kit

lib_LTLIBRARIES = libsnappea.la

libsnappea_la_SOURCES = dummy.c
libsnappea_la_LDFLAGS = -version-info 0:0:0 -no-undefined
libsnappea_la_LIBADD = ./code/libcode.la ./unix_kit/libunixkit.la

readmedir = $(pkgdocdir)/Kernel

readme_DATA = ReadMe

EXTRA_DIST = detab.c makefile-client
