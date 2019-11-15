# aclocal Path
ACLOCAL_AMFLAGS = -I m4

if HAVE_GMERLIN
gmerlin_subdirs = plugins
else
gmerlin_subdirs =
endif

if HAVE_DOXYGEN
DOC_SUBDIRS = doc
else
DOC_SUBDIRS =
endif

SUBDIRS = lib $(gmerlin_subdirs) tests include m4 po utils $(DOC_SUBDIRS)

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = gmerlin_avdec.pc

EXTRA_DIST = config.rpath  autogen.sh cvs_clean.sh gmerlin_avdec.pc.in gmerlin_avdec.spec.in cpuinfo.sh make_potfiles
