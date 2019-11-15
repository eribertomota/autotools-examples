AUTOMAKE_OPTIONS = 1.6

DOC_MODULE = ogmrip-gtk

DOC_MAIN_SGML_FILE = ogmrip-gtk.xml

DOC_SOURCE_DIR = ../../../libogmrip-gtk

HFILE_GLOB = $(top_srcdir)/libogmrip-gtk/*.h
CFILE_GLOB = $(top_srcdir)/libogmrip-gtk/*.c

IGNORE_HFILES = ogmrip-gtk.h ogmrip-marshal.h

include $(top_srcdir)/gtk-doc.make

GTKDOC_CFLAGS = \
  $(OGMRIP_CFLAGS) $(GUI_CFLAGS) \
  -I$(top_srcdir)/libogmdvd      \
  -I$(top_srcdir)/libogmdvd-gtk  \
  -I$(top_srcdir)/libogmjob      \
  -I$(top_srcdir)/libogmrip      \
  -I$(top_srcdir)/libogmrip-gtk

GTKDOC_LIBS = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  $(top_builddir)/libogmdvd-gtk/libogmdvd-gtk.la \
  $(top_builddir)/libogmjob/libogmjob.la \
  $(top_builddir)/libogmrip/libogmrip.la \
  $(top_builddir)/libogmrip-gtk/libogmrip-gtk.la \
  $(OGMRIP_LIBS) $(HAL_LIBS)

