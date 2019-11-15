AUTOMAKE_OPTIONS = 1.6

DOC_MODULE = ogmjob

DOC_MAIN_SGML_FILE = ogmjob.xml

DOC_SOURCE_DIR = ../../../libogmjob

HFILE_GLOB = $(top_srcdir)/libogmjob/*.h
CFILE_GLOB = $(top_srcdir)/libogmjob/*.c

IGNORE_HFILES = ogmjob-marshal.h ogmjob.h

include $(top_srcdir)/gtk-doc.make

GTKDOC_CFLAGS = \
  $(OGMRIP_CFLAGS) \
  -I$(top_srcdir)/libogmjob

GTKDOC_LIBS = \
  $(top_builddir)/libogmjob/libogmjob.la \
  $(OGMRIP_LIBS)

