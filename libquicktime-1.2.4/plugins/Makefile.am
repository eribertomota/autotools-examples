localedir = $(datadir)/locale
# These are always here

base_subdirs = audiocodec \
videocodec \
rtjpeg

if HAVE_LIBJPEG
jpeg_subdirs = mjpeg
else
jpeg_subdirs=
endif

if HAVE_LAME
lame_subdirs = lame
else
lame_subdirs=
endif

if HAVE_LIBDV
dv_subdirs = dv
else
dv_subdirs=
endif

if HAVE_LIBPNG
png_subdirs=png
else
png_subdirs=
endif

if HAVE_VORBIS
vorbis_subdirs=vorbis
else
vorbis_subdirs=
endif

if HAVE_LIBAVCODEC
libavcodec_subdirs=ffmpeg
else
libavcodec=
endif

if HAVE_FAAD2
faad2_subdirs=faad2
else
faad2_subdirs=
endif

if HAVE_FAAC
faac_subdirs=faac
else
faac_subdirs=
endif

if HAVE_X264
x264_subdirs=x264
else
x264_subdirs=
endif

if HAVE_SCHROEDINGER
schroedinger_subdirs=schroedinger
else
schroedinger_subdirs=
endif

SUBDIRS = $(base_subdirs) $(jpeg_subdirs) $(dv_subdirs) \
	$(png_subdirs) $(vorbis_subdirs) $(libavcodec_subdirs) \
        $(lame_subdirs) $(faad2_subdirs) $(faac_subdirs) $(x264_subdirs) \
        $(schroedinger_subdirs)

