bin_PROGRAMS = eject volname
eject_SOURCES = eject.c
volname_SOURCES = volname.c

if USE_NLS
SUBDIRS = po
endif

AM_CPPFLAGS = -DDEFAULTDEVICE=\"$(DEFAULTDEVICE)\" -DGETOPTLONG
AM_CFLAGS = -Wall $(RPM_OPT_FLAGS)

man_MANS = eject.1 volname.1
EXTRA_DIST = $(man_MANS) PORTING PROBLEMS bootstrap eject-$(VERSION).lsm eject-$(VERSION).spec debian/changelog debian/control debian/copyright debian/dirs debian/files debian/rules debian/substvars po/*.pot po/*.po po/Makefile i18n.h
