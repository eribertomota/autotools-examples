AUTOMAKE_OPTIONS = 1.6

DOC_MODULE = ogmdvd-gtk

DOC_MAIN_SGML_FILE = ogmdvd-gtk.xml

DOC_SOURCE_DIR = ../../../libogmdvd-gtk

HFILE_GLOB = $(top_srcdir)/libogmdvd-gtk/*.h
CFILE_GLOB = $(top_srcdir)/libogmdvd-gtk/*.c

include $(top_srcdir)/gtk-doc.make

GTKDOC_CFLAGS = \
  $(OGMRIP_CFLAGS) $(GUI_CFLAGS) \
  -I$(top_srcdir)/libogmdvd      \
  -I$(top_srcdir)/libogmdvd-gtk

GTKDOC_LIBS = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  $(top_builddir)/libogmdvd-gtk/libogmdvd-gtk.la \
  $(OGMRIP_LIBS)

