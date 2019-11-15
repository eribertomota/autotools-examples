INCLUDES = -I$(top_srcdir)

AM_CPPFLAGS = \
  -DPKGDATADIR=\"$(pkgdatadir)\" \
  -DDATADIR=\""$(datadir)"\" -D_GNU_SOURCE

AM_CFLAGS = -Wall -pedantic -std=c99

# add the name of your application
bin_PROGRAMS = qwo

# add the sources to compile for your application
qwo_SOURCES = main.c window.c

MAINTAINERCLEANFILES  = config.h.in Makefile.in

