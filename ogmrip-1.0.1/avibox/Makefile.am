bin_PROGRAMS = \
  avibox

avibox_SOURCES = \
  avibox.c   \
  avilib.c   \
  avimisc.c  \
  aud_scan.c \
  platform.c

INCLUDES = \
  -D_LARGEFILE_SOURCE   \
  -D_LARGEFILE64_SOURCE \
  -D_FILE_OFFSET_BITS=64

man_MANS = \
  avibox.1

EXTRA_DIST =  \
  avilib.h    \
  aud_scan.h  \
  platform.h  \
  $(man_MANS)

CLEANFILES = *~ *.bak

