localedir = $(datadir)/locale
if HAVE_GTK
gtk_subdirs=gtk
else
gtk_subdirs=
endif

AM_CFLAGS = -DLOCALE_DIR=\"$(localedir)\"

SUBDIRS = $(gtk_subdirs)

if HAVE_X11
xbin = lqtplay
xman = lqtplay.1
else
xbin =
xman =
endif
noinst_PROGRAMS = test_codec testqt dump_codecs gen_colorspace_tables
# bin_PROGRAMS = $(xbin) qtinfo qtstreamize qtdechunk qtrechunk qtyuv4toyuv qtdump qtrecover lqt_transcode
bin_PROGRAMS = $(xbin) qtinfo qtstreamize qtdechunk qtrechunk qtyuv4toyuv qtdump lqt_transcode qt2text lqtremux
man1_MANS = $(xman)

lqt_transcode_SOURCES=lqt_transcode.c
lqt_transcode_LDADD=@UTIL_LIBADD@ -lm

testqt_SOURCES=testqt.c
testqt_LDADD=@UTIL_LIBADD@ -lm

test_codec_SOURCES=test_codec.c
test_codec_LDADD=@UTIL_LIBADD@

qtinfo_SOURCES=qtinfo.c common.c
qtinfo_LDADD=@UTIL_LIBADD@

qtstreamize_SOURCES=qtstreamize.c
qtstreamize_LDADD=@UTIL_LIBADD@

qtdump_SOURCES=dump.c
qtdump_LDADD=@UTIL_LIBADD@

qt2text_SOURCES=qt2text.c
qt2text_LDADD=@UTIL_LIBADD@

gen_colorspace_tables_sources=gen_colorspace_tables.c

qtdechunk_SOURCES=dechunk.c
qtdechunk_LDADD=@UTIL_LIBADD@

dump_codecs_SOURCES=dump_codecs.c
dump_codecs_LDADD=@UTIL_LIBADD@

qtrechunk_SOURCES=rechunk.c
qtrechunk_LDADD=@UTIL_LIBADD@

lqtremux_SOURCES=lqtremux.c
lqtremux_LDADD=@UTIL_LIBADD@

# qtrecover_SOURCES=recover.c
# qtrecover_LDADD=@UTIL_LIBADD@

qtyuv4toyuv_SOURCES=yuv4toyuv.c
qtyuv4toyuv_LDADD=@UTIL_LIBADD@

lqtplay_SOURCES=lqtplay.c common.c
lqtplay_LDADD=@UTIL_LIBADD@ @X_LIBS@ -lXaw -lXt @X_PRE_LIBS@ -lXext \
	-lXv @GL_LIBS@ -lX11 @X_EXTRA_LIBS@ -lm @ALSA_LIBS@ @SNDIO_LIBS@ \
	@OSSAUDIO_LIBS@

INCLUDES = -I$(top_srcdir)/include \
	    -I$(top_builddir)/include/quicktime \
	    @X_CFLAGS@ @ALSA_CFLAGS@

EXTRA_DIST=lqtplay.1 cpuinfo.c recover.c
noinst_HEADERS = common.h
