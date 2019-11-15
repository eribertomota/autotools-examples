gmerlin_plugindir = @gmerlin_plugindir@

INCLUDES = -I$(top_srcdir)/include

AM_LDFLAGS = @GMERLIN_PLUGIN_LDFLAGS@ -avoid-version -module

if HAVE_THEORAENC
theoraenc_plugins = e_theora.la

if HAVE_SHOUT
shout_plugins = b_ogg.la
bgshout_libs    = $(top_builddir)/lib/libbgshout.la @SHOUT_LIBS@
else
shout_plugins =
endif

else
theoraenc_plugins =
shout_plugins =
endif

if HAVE_SPEEX
speex_plugins = e_speex.la
speex_sources = speex.c
else
speex_plugins =
speex_sources =
endif

if HAVE_FLAC
flac_plugins = e_flacogg.la
flac_sources = flac.c
bgflac_libs    = $(top_builddir)/lib/libbgflac.la @FLAC_LIBS@
else
flac_plugins =
flac_sources =
endif

gmerlin_plugin_LTLIBRARIES = \
e_vorbis.la \
$(theoraenc_plugins) \
$(speex_plugins) \
$(flac_plugins) \
$(shout_plugins)


AM_CFLAGS = -DLOCALE_DIR=\"$(localedir)\"

e_vorbis_la_CFLAGS = @VORBIS_CFLAGS@ $(AM_CFLAGS)
e_vorbis_la_SOURCES = e_vorbis.c vorbis.c ogg_common.c
e_vorbis_la_LIBADD = @GMERLIN_DEP_LIBS@ $(top_builddir)/lib/libgmerlin_encoders.la @VORBISENC_LIBS@ @VORBIS_LIBS@ 

e_flacogg_la_CFLAGS = @OGG_CFLAGS@ @FLAC_CFLAGS@ $(AM_CFLAGS)
e_flacogg_la_SOURCES = e_flacogg.c flac.c ogg_common.c
e_flacogg_la_LIBADD = @GMERLIN_DEP_LIBS@ $(top_builddir)/lib/libgmerlin_encoders.la $(bgflac_libs) @OGG_LIBS@

e_theora_la_CFLAGS = @THEORAENC_CFLAGS@ @VORBIS_CFLAGS@ @SPEEX_CFLAGS@ @FLAC_CFLAGS@ $(AM_CFLAGS) $(AM_CFLAGS)
e_theora_la_SOURCES = e_theora.c vorbis.c $(speex_sources) $(flac_sources) theora.c ogg_common.c
e_theora_la_LIBADD = @GMERLIN_DEP_LIBS@ $(top_builddir)/lib/libgmerlin_encoders.la @VORBISENC_LIBS@ @VORBIS_LIBS@ @THEORAENC_LIBS@ @THEORADEC_LIBS@ @SPEEX_LIBS@ $(bgflac_libs)

b_ogg_la_CFLAGS = @THEORAENC_CFLAGS@ @THEORADEC_LIBS@ @VORBIS_CFLAGS@ @SPEEX_CFLAGS@  $(AM_CFLAGS)
b_ogg_la_SOURCES = b_ogg.c vorbis.c $(speex_sources) theora.c ogg_common.c
b_ogg_la_LIBADD = @GMERLIN_DEP_LIBS@ $(top_builddir)/lib/libgmerlin_encoders.la @VORBISENC_LIBS@ @VORBIS_LIBS@ @THEORAENC_LIBS@ @THEORADEC_LIBS@ @SPEEX_LIBS@ $(bgshout_libs)

e_speex_la_CFLAGS = @SPEEX_CFLAGS@ $(AM_CFLAGS)
e_speex_la_SOURCES = e_speex.c speex.c ogg_common.c
e_speex_la_LIBADD = @GMERLIN_DEP_LIBS@ $(top_builddir)/lib/libgmerlin_encoders.la @SPEEX_LIBS@ @OGG_LIBS@ 

noinst_HEADERS = ogg_common.h
