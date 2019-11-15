SUBDIRS = \
  libogmdvd \
  libogmjob \
  libogmrip \
  avibox \
  dvdcpy

if HAVE_GTK_SUPPORT
SUBDIRS +=      \
  libogmdvd-gtk \
  libogmrip-gtk \
  src
endif

if HAVE_THEORA_SUPPORT
SUBDIRS += \
  theoraenc
endif

if HAVE_SRT_SUPPORT
SUBDIRS += \
  subrip
endif

SUBDIRS += \
  data \
  docs \
  po

EXTRA_DIST= \
  intltool-update.in  \
  intltool-extract.in \
  intltool-merge.in   \
  po/Makefile.in.in   \
  po/POTFILES.in

DISTCLEANFILES = \
  intltool-update  \
  intltool-extract \
  intltool-merge

DISTCHECK_CONFIGURE_FLAGS = --enable-gtk-doc=yes
