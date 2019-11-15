## Process this file with automake to produce Makefile.in.

gmerlin_plugindir = @gmerlin_plugindir@

INCLUDES = -I$(top_srcdir)/include


if HAVE_CDIO
cdio_modules = i_vcd.la
cdio_cflags = @CDIO_CFLAGS@

if HAVE_DVDREAD
dvdread_modules = i_dvd.la
else
dvdread_modules =
endif

else
cdio_modules =
cdio_cflags =
endif

if HAVE_LINUXDVB
dvb_modules = i_dvb.la
else
dvb_modules =
endif

AM_CFLAGS = @OPT_CFLAGS@ @GMERLIN_CFLAGS@ $(cdio_cflags) -DLOCALE_DIR=\"$(localedir)\"

AM_LDFLAGS = -avoid-version -module @GMERLIN_PLUGIN_LDFLAGS@
# AM_LDFLAGS = -avoid-version -module
gmerlin_plugin_LTLIBRARIES = \
i_avdec.la \
$(cdio_modules) \
$(dvdread_modules) \
$(dvb_modules)

noinst_HEADERS = avdec_common.h

i_avdec_la_SOURCES = i_avdec.c avdec_common.c
i_avdec_la_LIBADD = $(top_builddir)/lib/libgmerlin_avdec.la @GMERLIN_LIBS@

i_vcd_la_SOURCES = i_vcd.c avdec_common.c
i_vcd_la_LIBADD = $(top_builddir)/lib/libgmerlin_avdec.la @GMERLIN_LIBS@

i_dvd_la_SOURCES = i_dvd.c avdec_common.c
i_dvd_la_LIBADD = $(top_builddir)/lib/libgmerlin_avdec.la @GMERLIN_LIBS@

i_dvb_la_SOURCES = i_dvb.c avdec_common.c
i_dvb_la_LIBADD = $(top_builddir)/lib/libgmerlin_avdec.la @GMERLIN_LIBS@
