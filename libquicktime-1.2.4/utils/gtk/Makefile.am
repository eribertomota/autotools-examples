localedir = $(datadir)/locale
INCLUDES = -I$(top_srcdir)/include
AM_CFLAGS = @GTK_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"

bin_PROGRAMS = libquicktime_config

libquicktime_config_SOURCES = lqt_gtk.c lqt_gtk.h libquicktime_config.c

libquicktime_config_LDADD = @GTK_LIBS@ @GTKUTIL_LIBADD@

