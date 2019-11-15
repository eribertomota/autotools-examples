if HAVE_VORBIS
ogg_subdirs = ogg
else
ogg_subdirs =
endif

if HAVE_FLAC
flac_subdirs = flac
else
flac_subdirs =
endif

if HAVE_LAME
lame_subdirs = lame
else
lame_subdirs =
endif

if HAVE_FAAC
faac_subdirs = faac
else
faac_subdirs =
endif

if HAVE_MJPEGTOOLS
mjpeg_subdirs = yuv4mpeg
else
mjpeg_subdirs =
endif

if HAVE_LIBAVFORMAT
ffmpeg_subdirs = ffmpeg
else
ffmpeg_subdirs =
endif

SUBDIRS = \
$(ogg_subdirs) \
$(flac_subdirs) \
$(lame_subdirs) \
$(faac_subdirs) \
$(mjpeg_subdirs) \
$(ffmpeg_subdirs)
