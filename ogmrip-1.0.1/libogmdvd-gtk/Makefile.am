lib_LTLIBRARIES = \
  libogmdvd-gtk.la

BUILT_SOURCES = \
  ogmdvd-marshal.c \
  ogmdvd-marshal.h

libogmdvd_gtk_la_SOURCES =        \
  ogmdvd-cell-renderer-language.c \
  ogmdvd-chapter-list.c           \
  ogmdvd-drive-chooser.c          \
  ogmdvd-drive-chooser-widget.c   \
  ogmdvd-drive-chooser-dialog.c   \
  ogmdvd-marshal.c                \
  ogmdvd-title-chooser.c          \
  ogmdvd-title-chooser-widget.c

libogmdvd_gtk_ladir = \
  $(includedir)/ogmdvd

libogmdvd_gtk_la_HEADERS =        \
  ogmdvd-cell-renderer-language.h \
  ogmdvd-chapter-list.h           \
  ogmdvd-drive-chooser.h          \
  ogmdvd-drive-chooser-widget.h   \
  ogmdvd-drive-chooser-dialog.h   \
  ogmdvd-marshal.h                \
  ogmdvd-title-chooser.h          \
  ogmdvd-title-chooser-widget.h   \
  ogmdvd-gtk.h

libogmdvd_gtk_la_LDFLAGS = \
  -version-info $(OGMDVD_GTK_LT_VERSION)

libogmdvd_gtk_la_LIBADD = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  $(DVDREAD_LIBS) $(OGMRIP_LIBS) \
  $(GUI_LIBS)

ogmdvd-marshal.h: ogmdvd-marshal.list $(GLIB_GENMARSHAL)
	$(GLIB_GENMARSHAL) $< --header --prefix=ogmdvd_cclosure_marshal > $@

ogmdvd-marshal.c: ogmdvd-marshal.list $(GLIB_GENMARSHAL)
	echo "#include \"ogmdvd-marshal.h\"" > $@ && \
	$(GLIB_GENMARSHAL) $< --body --prefix=ogmdvd_cclosure_marshal >> $@

EXTRA_DIST = \
  ogmdvd-marshal.list

INCLUDES = \
  -I$(top_srcdir)/libogmdvd \
  $(OGMRIP_CFLAGS) $(GUI_CFLAGS)

CLEANFILES = \
  $(BUILT_SOURCES)

