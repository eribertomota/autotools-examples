gmerlin_plugindir = @gmerlin_plugindir@

INCLUDES = -I$(top_srcdir)/include

AM_LDFLAGS = @GMERLIN_PLUGIN_LDFLAGS@ -avoid-version -module
AM_CFLAGS = @GMERLIN_DEP_CFLAGS@ @AVFORMAT_CFLAGS@ @AVCODEC_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"

gmerlin_plugin_LTLIBRARIES = \
e_ffmpeg_video.la \
e_ffmpeg_audio.la \
e_ffmpeg.la

common_sources = ffmpeg_common.c codecs.c

e_ffmpeg_video_la_SOURCES = e_ffmpeg_video.c $(common_sources)
e_ffmpeg_video_la_LIBADD  = @GMERLIN_DEP_LIBS@ @AVFORMAT_LIBS@

e_ffmpeg_audio_la_SOURCES = e_ffmpeg_audio.c $(common_sources)
e_ffmpeg_audio_la_LIBADD  = @GMERLIN_DEP_LIBS@ @AVFORMAT_LIBS@

e_ffmpeg_la_SOURCES = e_ffmpeg.c $(common_sources)
e_ffmpeg_la_LIBADD  = @GMERLIN_DEP_LIBS@ @AVFORMAT_LIBS@

noinst_HEADERS = ffmpeg_common.h params.h
