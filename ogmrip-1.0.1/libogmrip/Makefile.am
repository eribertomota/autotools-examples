lib_LTLIBRARIES =   \
  libogmrip.la      \
  libogmrip-lavc.la \
  libogmrip-mplayer.la

libogmrip_la_SOURCES =      \
  ogmrip-audio-codec.c      \
  ogmrip-chapters.c         \
  ogmrip-codec.c            \
  ogmrip-container.c        \
  ogmrip-dvdcpy.c           \
  ogmrip-edl.c              \
  ogmrip-encoding.c         \
  ogmrip-encoding-manager.c \
  ogmrip-file.c             \
  ogmrip-fs.c               \
  ogmrip-hardsub.c          \
  ogmrip-keyfile-settings.c \
  ogmrip-novideo.c          \
  ogmrip-options.c          \
  ogmrip-player.c           \
  ogmrip-plugin.c           \
  ogmrip-settings.c         \
  ogmrip-subp-codec.c       \
  ogmrip-version.c          \
  ogmrip-video-codec.c

libogmrip_ladir = \
  $(includedir)/ogmrip

libogmrip_la_HEADERS =      \
  ogmrip-audio-codec.h      \
  ogmrip-chapters.h         \
  ogmrip-codec.h            \
  ogmrip-container.h        \
  ogmrip-dvdcpy.h           \
  ogmrip-edl.h              \
  ogmrip-encoding.h         \
  ogmrip-encoding-manager.h \
  ogmrip-enums.h            \
  ogmrip-file.h             \
  ogmrip-fs.h               \
  ogmrip-hardsub.h          \
  ogmrip-keyfile-settings.h \
  ogmrip-novideo.h          \
  ogmrip-options.h          \
  ogmrip-player.h           \
  ogmrip-plugin.h           \
  ogmrip-settings.h         \
  ogmrip-subp-codec.h       \
  ogmrip-version.h          \
  ogmrip-video-codec.h      \
  ogmrip.h

libogmrip_la_LDFLAGS = \
  -version-info $(OGMRIP_LT_VERSION)

libogmrip_la_LIBADD = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  $(top_builddir)/libogmjob/libogmjob.la \
  $(LIBXML_LIBS) $(OGMRIP_LIBS)

#
# Common
#

libogmrip_mplayer_la_SOURCES = \
  ogmrip-mplayer.c
  
libogmrip_mplayer_la_LDFLAGS = \
  -version-info $(OGMRIP_LT_VERSION) \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_mplayer_la_LIBADD = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  $(top_builddir)/libogmjob/libogmjob.la \
  libogmrip.la $(OGMRIP_LIBS)

libogmrip_mplayer_ladir = \
  $(includedir)/ogmrip

libogmrip_mplayer_la_HEADERS = \
  ogmrip-mplayer.h

libogmrip_lavc_la_SOURCES = \
  ogmrip-lavc.c
  
libogmrip_lavc_la_LDFLAGS = \
  -version-info $(OGMRIP_LT_VERSION) \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_lavc_la_LIBADD = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  $(top_builddir)/libogmjob/libogmjob.la \
  libogmrip.la libogmrip-mplayer.la \
  $(OGMRIP_LIBS)

libogmrip_lavc_ladir = \
  $(includedir)/ogmrip

libogmrip_lavc_la_HEADERS = \
  ogmrip-lavc.h

#
# Video Codecs
#

video_codecsdir=$(libdir)/ogmrip/video-plugins

video_codecs_LTLIBRARIES =

video_codecs_HEADERS =

if HAVE_LAVC_SUPPORT
video_codecs_LTLIBRARIES += \
  libogmrip-lavc-mpeg4.la

libogmrip_lavc_mpeg4_la_SOURCES = \
  ogmrip-lavc-mpeg4.c
  
libogmrip_lavc_mpeg4_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_lavc_mpeg4_la_LIBADD = \
  libogmrip.la      \
  libogmrip-lavc.la \
  libogmrip-mplayer.la

video_codecs_HEADERS += \
  ogmrip-lavc-mpeg4.h
endif

if HAVE_XVID_SUPPORT
video_codecs_LTLIBRARIES += \
  libogmrip-xvid.la

libogmrip_xvid_la_SOURCES = \
  ogmrip-xvid.c

libogmrip_xvid_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_xvid_la_LIBADD = \
  libogmrip.la \
  libogmrip-mplayer.la \
	$(OGMRIP_LIBS)

video_codecs_HEADERS += \
  ogmrip-xvid.h
endif

if HAVE_THEORA_SUPPORT
video_codecs_LTLIBRARIES += \
  libogmrip-theora.la

libogmrip_theora_la_SOURCES = \
  ogmrip-theora.c

libogmrip_theora_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_theora_la_LIBADD = \
  $(top_builddir)/libogmjob/libogmjob.la \
  libogmrip.la libogmrip-mplayer.la
endif

if HAVE_X264_SUPPORT
video_codecs_LTLIBRARIES += \
  libogmrip-x264.la

libogmrip_x264_la_SOURCES = \
  ogmrip-x264.c

libogmrip_x264_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_x264_la_LIBADD = \
  libogmrip.la \
  libogmrip-mplayer.la \
	$(OGMRIP_LIBS) -lm

video_codecs_HEADERS += \
  ogmrip-x264.h
endif

#
# Audio Codecs
#

audio_codecsdir=$(libdir)/ogmrip/audio-plugins

audio_codecs_LTLIBRARIES = \
  libogmrip-acopy.la  \
  libogmrip-wav.la

libogmrip_acopy_la_SOURCES = \
  ogmrip-acopy.c

libogmrip_acopy_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_acopy_la_LIBADD = \
  libogmrip.la \
  libogmrip-mplayer.la

libogmrip_wav_la_SOURCES = \
  ogmrip-wav.c

libogmrip_wav_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_wav_la_LIBADD = \
  libogmrip.la \
  libogmrip-mplayer.la

if HAVE_MP3_SUPPORT
audio_codecs_LTLIBRARIES += \
  libogmrip-mp3.la

libogmrip_mp3_la_SOURCES = \
  ogmrip-mp3.c

libogmrip_mp3_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_mp3_la_LIBADD = \
  $(top_builddir)/libogmjob/libogmjob.la \
  libogmrip.la libogmrip-mplayer.la
endif

if HAVE_VORBIS_SUPPORT
audio_codecs_LTLIBRARIES += \
  libogmrip-vorbis.la

libogmrip_vorbis_la_SOURCES = \
  ogmrip-vorbis.c

libogmrip_vorbis_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_vorbis_la_LIBADD = \
  $(top_builddir)/libogmjob/libogmjob.la \
  libogmrip.la libogmrip-mplayer.la
endif

if HAVE_AAC_SUPPORT
audio_codecs_LTLIBRARIES += \
  libogmrip-aac.la

libogmrip_aac_la_SOURCES = \
  ogmrip-aac.c

libogmrip_aac_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_aac_la_LIBADD = \
  $(top_builddir)/libogmjob/libogmjob.la \
  libogmrip.la libogmrip-mplayer.la
endif

#
# Subp Codecs
#

subp_codecsdir=$(libdir)/ogmrip/subp-plugins

subp_codecs_LTLIBRARIES = \
  libogmrip-vobsub.la

libogmrip_vobsub_la_SOURCES = \
  ogmrip-vobsub.c

libogmrip_vobsub_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_vobsub_la_LIBADD = \
  $(top_builddir)/libogmjob/libogmjob.la \
  libogmrip.la libogmrip-mplayer.la \
  $(OGMRIP_LIBS)

if HAVE_SRT_SUPPORT
subp_codecs_LTLIBRARIES += \
  libogmrip-srt.la

libogmrip_srt_la_SOURCES = \
  ogmrip-srt.c

libogmrip_srt_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_srt_la_LIBADD = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  libogmrip.la libogmrip-mplayer.la \
  $(OGMRIP_LIBS)
endif

#
# Containers
#

containersdir=$(libdir)/ogmrip/container-plugins

containers_LTLIBRARIES = \
  libogmrip-avi.la

libogmrip_avi_la_SOURCES = \
  ogmrip-avi.c

libogmrip_avi_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_avi_la_LIBADD = \
  $(top_builddir)/libogmjob/libogmjob.la \
  libogmrip.la libogmrip-mplayer.la

if HAVE_OGM_SUPPORT
containers_LTLIBRARIES += \
  libogmrip-ogg.la

libogmrip_ogg_la_SOURCES = \
  ogmrip-ogg.c

libogmrip_ogg_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_ogg_la_LIBADD = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  libogmrip.la \
  $(OGMRIP_LIBS)
endif

if HAVE_MKV_SUPPORT
containers_LTLIBRARIES += \
  libogmrip-mkv.la

libogmrip_mkv_la_SOURCES = \
  ogmrip-mkv.c

libogmrip_mkv_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_mkv_la_LIBADD = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  $(top_builddir)/libogmjob/libogmjob.la \
  libogmrip.la \
  $(OGMRIP_LIBS)
endif

if HAVE_MP4_SUPPORT
containers_LTLIBRARIES += \
  libogmrip-mp4.la

libogmrip_mp4_la_SOURCES = \
  ogmrip-mp4.c

libogmrip_mp4_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_mp4_la_LIBADD = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  libogmrip.la libogmrip-mplayer.la \
  $(OGMRIP_LIBS)
endif

if HAVE_LAVF_SUPPORT
containers_LTLIBRARIES += \
  libogmrip-mov.la 

libogmrip_mov_la_SOURCES = \
  ogmrip-mov.c

libogmrip_mov_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip/.libs

libogmrip_mov_la_LIBADD = \
  $(top_builddir)/libogmjob/libogmjob.la \
  libogmrip.la libogmrip-mplayer.la
endif

#
# Misc
#

EXTRA_DIST = \
  ogmrip-version.h.in

if MAINTAINER_MODE
DEBUG_CFLAGS = \
  -DG_ENABLE_DEBUG
endif

INCLUDES = \
  $(LIBXML_CFLAGS)          \
  $(OGMRIP_CFLAGS)          \
  $(DEBUG_CFLAGS)           \
  -I$(top_srcdir)/libogmjob \
  -I$(top_srcdir)/libogmdvd \
  -DOGMRIP_LIB_DIR=\""$(libdir)"\" \
  -DOGMRIP_DATA_DIR=\""$(datadir)"\"

ogmripincdir = \
  $(includedir)/ogmrip

ogmripinc_DATA = \
  ogmrip-version.h

DISTCLEANFILES = \
  ogmrip-version.h

