AUTOMAKE_OPTIONS = 1.6

DOC_MODULE = ogmrip

DOC_MAIN_SGML_FILE = ogmrip.xml

DOC_SOURCE_DIR = ../../../libogmrip

HFILE_GLOB = $(top_srcdir)/libogmrip/*.h
CFILE_GLOB = $(top_srcdir)/libogmrip/*.c

IGNORE_HFILES = ogmrip.h ogmrip-hardsub.h ogmrip-xvid.h ogmrip-x264.h ogmrip-lavc-mpeg4.h

# SCAN_OPTIONS = --ignore-headers="ogmrip-file.h $(IGNORE_HFILES)"

include $(top_srcdir)/gtk-doc.make

GTKDOC_CFLAGS = \
   $(OGMRIP_CFLAGS) \
  -I$(top_srcdir)/libogmdvd \
  -I$(top_srcdir)/libogmjob \
  -I$(top_srcdir)/libogmrip

GTKDOC_LIBS = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  $(top_builddir)/libogmjob/libogmjob.la \
  $(top_builddir)/libogmrip/libogmrip.la \
  $(OGMRIP_LIBS)

