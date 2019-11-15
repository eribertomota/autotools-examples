AUTOMAKE_OPTIONS = 1.6

DOC_MODULE = ogmdvd

DOC_MAIN_SGML_FILE = ogmdvd.xml

DOC_SOURCE_DIR = ../../../libogmdvd

HFILE_GLOB = $(top_srcdir)/libogmdvd/*.h
CFILE_GLOB = $(top_srcdir)/libogmdvd/*.c

IGNORE_HFILES = ogmdvd.h \
		ogmdvd-priv.h \
		ogmdvd-transport.h \
		ogmdvd-device.h

IGNORE_CFILES = ogmdvd-transport.c \
		ogmdvd-device.c

include $(top_srcdir)/gtk-doc.make

GTKDOC_CFLAGS = \
  $(DBUS_CFLAGS) $(CAM_CFLAGS)

GTKDOC_LIBS = \
  $(DBUS_LIBS) $(CAM_LIBS)
