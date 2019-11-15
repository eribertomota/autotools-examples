bin_PROGRAMS = \
  ogmrip

ogmrip_SOURCES = \
  ogmrip-crop-dialog.c      \
  ogmrip-gconf.c            \
  ogmrip-main.c             \
  ogmrip-marshal.c          \
  ogmrip-options-dialog.c   \
  ogmrip-pref-dialog.c      \
  ogmrip-profile-editor.c   \
  ogmrip-profiles.c         \
  ogmrip-profiles-dialog.c  \
  ogmrip-progress-dialog.c  \
  ogmrip-queue-dialog.c     \
  ogmrip-spell-dialog.c     \
  ogmrip-update-dialog.c    \
  ogmrip-audio-options.c    \
  ogmrip-subp-options.c

EXTRA_DIST = \
  ogmrip-crop-dialog.h      \
  ogmrip-gconf.h            \
  ogmrip-marshal.h          \
  ogmrip-marshal.list       \
  ogmrip-options-dialog.h   \
  ogmrip-pref-dialog.h      \
  ogmrip-profile-editor.h   \
  ogmrip-profiles.h         \
  ogmrip-profiles-dialog.h  \
  ogmrip-progress-dialog.h  \
  ogmrip-queue-dialog.h     \
  ogmrip-spell-dialog.h     \
  ogmrip-update-dialog.h    \
  ogmrip-audio-options.h    \
  ogmrip-subp-options.h

if MAINTAINER_MODE
DEBUG_CFLAGS = \
  -DG_ENABLE_DEBUG
endif

ogmrip_LDADD = \
  $(top_builddir)/libogmdvd/libogmdvd.la          \
  $(top_builddir)/libogmdvd-gtk/libogmdvd-gtk.la  \
  $(top_builddir)/libogmjob/libogmjob.la          \
  $(top_builddir)/libogmrip/libogmrip.la          \
  $(top_builddir)/libogmrip-gtk/libogmrip-gtk.la  \
  $(OGMRIP_LIBS)  $(GUI_LIBS) $(ENCHANT_LIBS)     \
  $(DBUS_LIBS) $(DVDREAD_LIBS) $(LIBNOTIFY_LIBS)

BUILT_SOURCES = \
  ogmrip-marshal.c \
  ogmrip-marshal.h

ogmrip-marshal.h: ogmrip-marshal.list $(GLIB_GENMARSHAL)
	$(GLIB_GENMARSHAL) $< --header --prefix=ogmrip_cclosure_marshal > $@

ogmrip-marshal.c: ogmrip-marshal.list $(GLIB_GENMARSHAL)
	echo "#include \"ogmrip-marshal.h\"" > $@ && \
	$(GLIB_GENMARSHAL) $< --body --prefix=ogmrip_cclosure_marshal >> $@

INCLUDES = \
  $(DEBUG_CFLAGS)     \
  $(DBUS_CFLAGS)      \
  $(OGMRIP_CFLAGS)    \
  $(GUI_CFLAGS)       \
  $(ENCHANT_CFLAGS)   \
  $(LIBNOTIFY_CFLAGS) \
  -I$(top_srcdir)/libogmdvd     \
  -I$(top_srcdir)/libogmdvd-gtk \
  -I$(top_srcdir)/libogmjob     \
  -I$(top_srcdir)/libogmrip     \
  -I$(top_builddir)/libogmrip   \
  -I$(top_srcdir)/libogmrip-gtk \
  -DOGMRIP_DATA_DIR=\""$(datadir)"\"

CLEANFILES = $(BUILT_SOURCES) *~ *.bak

