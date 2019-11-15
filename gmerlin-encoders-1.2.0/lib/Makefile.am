INCLUDES = -I$(top_srcdir)/include

if HAVE_FLAC
flac_libs = libbgflac.la
else
flac_libs =
endif

if HAVE_SHOUT
shout_libs = libbgshout.la
else
shout_libs =
endif


AM_CFLAGS = -DLOCALE_DIR=\"$(localedir)\" @FLAC_CFLAGS@

noinst_LTLIBRARIES = libgmerlin_encoders.la $(flac_libs) $(shout_libs)

libgmerlin_encoders_la_SOURCES = \
id3v1.c \
id3v2.c

libbgflac_la_CFLAGS  = @FLAC_CFLAGS@
libbgflac_la_SOURCES = bgflac.c

libbgshout_la_CFLAGS  = @SHOUT_CFLAGS@
libbgshout_la_SOURCES = bgshout.c
