gmerlin_plugindir = @gmerlin_plugindir@

INCLUDES = -I$(top_srcdir)/include

AM_LDFLAGS = @GMERLIN_PLUGIN_LDFLAGS@ -avoid-version -module
AM_CFLAGS = @MJPEGTOOLS_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"

gmerlin_plugin_LTLIBRARIES = e_yuv4mpeg.la e_mpegvideo.la e_mpegaudio.la e_mpeg.la

e_yuv4mpeg_la_SOURCES  = e_yuv4mpeg.c y4m_common.c
e_yuv4mpeg_la_LIBADD = @GMERLIN_DEP_LIBS@ @MJPEGTOOLS_LIBS@


e_mpegvideo_la_SOURCES  = e_mpegvideo.c y4m_common.c mpv_common.c
e_mpegvideo_la_LIBADD = @GMERLIN_DEP_LIBS@ @MJPEGTOOLS_LIBS@

e_mpegaudio_la_SOURCES  = e_mpegaudio.c mpa_common.c
# e_mpegaudio_la_LIBADD = @GMERLIN_DEP_LIBS@ @MJPEGTOOLS_LIBS@

e_mpeg_la_SOURCES = e_mpeg.c mpa_common.c y4m_common.c mpv_common.c
e_mpeg_la_LIBADD = @GMERLIN_DEP_LIBS@ @MJPEGTOOLS_LIBS@

noinst_HEADERS = y4m_common.h mpv_common.h mpa_common.h

