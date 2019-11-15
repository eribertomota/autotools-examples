lib_LTLIBRARIES = \
  libogmdvd.la

libogmdvd_la_SOURCES = \
  ogmdvd-audio.c   \
  ogmdvd-contrib.c \
  ogmdvd-device.c  \
  ogmdvd-disc.c    \
  ogmdvd-drive.c   \
  ogmdvd-labels.c  \
  ogmdvd-monitor.c \
  ogmdvd-parser.c  \
  ogmdvd-priv.c    \
  ogmdvd-reader.c  \
  ogmdvd-stream.c  \
  ogmdvd-subp.c    \
  ogmdvd-title.c   \
  ogmdvd-transport.c

libogmdvd_la_HEADERS = \
  ogmdvd-audio.h   \
  ogmdvd-disc.h    \
  ogmdvd-drive.h   \
  ogmdvd-enums.h   \
  ogmdvd-labels.h  \
  ogmdvd-monitor.h \
  ogmdvd-parser.h  \
  ogmdvd-reader.h  \
  ogmdvd-stream.h  \
  ogmdvd-subp.h    \
  ogmdvd-title.h   \
  ogmdvd-types.h   \
  ogmdvd.h

libogmdvd_la_LDFLAGS = \
  -version-info $(OGMDVD_LT_VERSION)

libogmdvd_la_LIBADD = \
  $(OGMRIP_LIBS) $(DVDREAD_LIBS) $(CAM_LIBS)

libogmdvd_ladir = \
  $(includedir)/ogmdvd

EXTRA_DIST = \
  ogmdvd-contrib.h   \
  ogmdvd-device.h    \
  ogmdvd-transport.h \
  ogmdvd-priv.h

INCLUDES = \
  $(OGMRIP_CFLAGS)

