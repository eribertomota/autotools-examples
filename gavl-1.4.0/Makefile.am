if HAVE_DOXYGEN
DOC_SUBDIRS = doc
else
DOC_SUBDIRS =
endif

SUBDIRS = gavl src include m4 utils $(DOC_SUBDIRS)

# aclocal Path
ACLOCAL_AMFLAGS = -I m4


pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = gavl.pc

EXTRA_DIST=autogen.sh \
cvs_clean.sh \
gavl.spec.in \
gavl.pc.in \
cpuinfo.sh
