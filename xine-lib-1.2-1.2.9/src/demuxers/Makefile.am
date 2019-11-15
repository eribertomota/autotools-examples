include $(top_builddir)/misc/Makefile.plugins
include $(top_srcdir)/misc/Makefile.common

AM_CFLAGS  = $(DEFAULT_OCFLAGS) $(VISIBILITY_FLAG)
AM_LDFLAGS = $(xineplug_ldflags)

noinst_LTLIBRARIES = libasfheader.la
libasfheader_la_SOURCES = asfheader.c

##
# IMPORTANT:
# ---------
# All of xine demuxer plugins should be named like the scheme "xineplug_dmx_"

noinst_HEADERS = asfheader.h qtpalette.h group_games.h group_audio.h \
		 group_video.h id3.h ebml.h matroska.h demux_matroska.h \
		 iff.h flacutils.h  real_common.h

if ENABLE_ASF
asf_module = xineplug_dmx_asf.la
endif

if ENABLE_MNG
mng_module = xineplug_dmx_mng.la
endif

if ENABLE_MODPLUG
modplug_module = xineplug_dmx_modplug.la
endif

if BUILD_DMX_IMAGE
image_module = xineplug_dmx_image.la
endif

xineplug_LTLIBRARIES = \
	$(asf_module) \
	$(mng_module) \
	$(image_module) \
	$(modplug_module) \
	xineplug_dmx_games.la \
	xineplug_dmx_audio.la \
	xineplug_dmx_video.la \
	xineplug_dmx_fli.la \
	xineplug_dmx_pva.la \
	xineplug_dmx_slave.la \
	xineplug_dmx_nsv.la \
	xineplug_dmx_playlist.la

xineplug_dmx_video_la_SOURCES = group_video.c \
				demux_avi.c demux_iff.c \
				demux_elem.c demux_mpeg_block.c demux_mpeg.c \
				demux_mpeg_pes.c demux_ts.c \
				demux_vc1es.c demux_qt.c demux_real.c demux_flv.c \
				demux_rawdv.c demux_yuv_frames.c demux_yuv4mpeg2.c \
				demux_matroska.c demux_matroska-chapters.c ebml.c
xineplug_dmx_video_la_CFLAGS = $(AM_CFLAGS)
xineplug_dmx_video_la_CPPFLAGS = $(AM_CPPFLAGS) $(ZLIB_CPPFLAGS)
xineplug_dmx_video_la_LIBADD = $(XINE_LIB) $(LTLIBINTL) $(ZLIB_LIBS)

xineplug_dmx_asf_la_SOURCES = demux_asf.c
xineplug_dmx_asf_la_LIBADD = $(XINE_LIB) $(LTLIBINTL) $(LTLIBICONV) libasfheader.la

xineplug_dmx_fli_la_SOURCES = demux_fli.c
xineplug_dmx_fli_la_LIBADD = $(XINE_LIB)

xineplug_dmx_mng_la_SOURCES = demux_mng.c
xineplug_dmx_mng_la_LIBADD = $(XINE_LIB) $(ZLIB_LIBS) $(MNG_LIBS)
xineplug_dmx_mng_la_CPPFLAGS = $(AM_CPPFLAGS) $(ZLIB_CPPFLAGS)

xineplug_dmx_pva_la_SOURCES = demux_pva.c
xineplug_dmx_pva_la_LIBADD = $(XINE_LIB)

xineplug_dmx_games_la_SOURCES = group_games.c demux_eawve.c \
				demux_idcin.c demux_ipmovie.c demux_roq.c \
				demux_vqa.c demux_wc3movie.c demux_str.c \
				demux_film.c demux_smjpeg.c demux_4xm.c \
				demux_vmd.c
xineplug_dmx_games_la_LIBADD = $(XINE_LIB) $(LTLIBINTL)

xineplug_dmx_audio_la_SOURCES = group_audio.c demux_aud.c demux_aiff.c \
				demux_cdda.c demux_mpgaudio.c \
				demux_realaudio.c demux_snd.c demux_voc.c \
				demux_vox.c demux_wav.c demux_ac3.c id3.c \
				demux_aac.c demux_flac.c \
				demux_mpc.c demux_dts.c demux_shn.c \
				demux_tta.c
xineplug_dmx_audio_la_LIBADD = $(XINE_LIB) $(LTLIBINTL)

xineplug_dmx_modplug_la_SOURCES = demux_mod.c
xineplug_dmx_modplug_la_LIBADD = $(XINE_LIB) $(LIBMODPLUG_LIBS)
xineplug_dmx_modplug_la_CFLAGS = $(AM_CFLAGS) $(LIBMODPLUG_CFLAGS)

xineplug_dmx_slave_la_SOURCES = demux_slave.c
xineplug_dmx_slave_la_LIBADD = $(XINE_LIB)

xineplug_dmx_image_la_SOURCES = demux_image.c
xineplug_dmx_image_la_LIBADD = $(XINE_LIB)

xineplug_dmx_nsv_la_SOURCES = demux_nsv.c
xineplug_dmx_nsv_la_LIBADD = $(XINE_LIB)

xineplug_dmx_playlist_la_SOURCES = demux_playlist.c
xineplug_dmx_playlist_la_LIBADD = $(XINE_LIB) $(LTLIBINTL)
