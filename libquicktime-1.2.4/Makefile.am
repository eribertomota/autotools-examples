localedir = $(datadir)/locale
# libquicktime top-level Makefile.am

if HAVE_DOXYGEN
DOC_SUBDIRS = doc
else
DOC_SUBDIRS =
endif

# aclocal Path
ACLOCAL_AMFLAGS = -I m4

SUBDIRS = $(DOC_SUBDIRS) src include plugins utils po

EXTRA_DIST = autogen.sh libquicktime.pc.in cpuinfo.sh config.rpath

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA=libquicktime.pc


DIST_SUBDIRS= \
doc \
src \
include \
plugins \
utils \
po
