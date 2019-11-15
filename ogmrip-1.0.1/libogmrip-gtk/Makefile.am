lib_LTLIBRARIES = \
  libogmrip-gtk.la

libogmrip_gtk_la_SOURCES =       \
  ogmrip-chapter-list.c          \
  ogmrip-chooser-list.c          \
  ogmrip-gconf-settings.c        \
  ogmrip-helper.c                \
  ogmrip-options-plugin.c        \
  ogmrip-source-chooser.c        \
  ogmrip-source-chooser-widget.c

libogmrip_gtk_ladir = \
  $(includedir)/ogmrip

libogmrip_gtk_la_HEADERS =       \
  ogmrip-chapter-list.h          \
  ogmrip-chooser-list.h          \
  ogmrip-gconf-settings.h        \
  ogmrip-helper.h                \
  ogmrip-options-plugin.h        \
  ogmrip-source-chooser.h        \
  ogmrip-source-chooser-widget.h \
  ogmrip-gtk.h

libogmrip_gtk_la_LDFLAGS = \
  -version-info $(OGMRIP_GTK_LT_VERSION)

libogmrip_gtk_la_LIBADD = \
  $(top_builddir)/libogmdvd/libogmdvd.la \
  $(top_builddir)/libogmdvd-gtk/libogmdvd-gtk.la  \
  $(top_builddir)/libogmjob/libogmjob.la \
  $(top_builddir)/libogmrip/libogmrip.la \
  $(DVDREAD_LIBS) $(OGMRIP_LIBS) $(GUI_LIBS)

#
# Options
#

options_plugindir=$(libdir)/ogmrip/options-plugins

options_plugin_LTLIBRARIES = \
  libogmrip-lavc-options.la  \
  libogmrip-x264-options.la \
  libogmrip-xvid-options.la

libogmrip_lavc_options_la_SOURCES = \
  ogmrip-lavc-options.c

libogmrip_lavc_options_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip-gtk/.libs

libogmrip_lavc_options_la_LIBADD = \
  $(top_builddir)/libogmrip/libogmrip.la \
  $(top_builddir)/libogmrip/libogmrip-lavc.la \
  libogmrip-gtk.la $(OGMRIP_LIBS) $(GUI_LIBS)

libogmrip_xvid_options_la_SOURCES = \
  ogmrip-xvid-options.c

libogmrip_xvid_options_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip-gtk/.libs

libogmrip_xvid_options_la_LIBADD = \
  $(top_builddir)/libogmrip/libogmrip.la \
  libogmrip-gtk.la $(OGMRIP_LIBS) $(GUI_LIBS)

libogmrip_x264_options_la_SOURCES = \
  ogmrip-x264-options.c

libogmrip_x264_options_la_LDFLAGS = \
  -export-dynamic -module -avoid-version \
  -L$(top_builddir)/libogmrip-gtk/.libs

libogmrip_x264_options_la_LIBADD = \
  $(top_builddir)/libogmrip/libogmrip.la \
  libogmrip-gtk.la $(OGMRIP_LIBS) $(GUI_LIBS)

#
# Misc
#

INCLUDES = \
  $(OGMRIP_CFLAGS) $(GUI_CFLAGS) \
  -I$(top_srcdir)/libogmdvd      \
  -I$(top_srcdir)/libogmdvd-gtk  \
  -I$(top_srcdir)/libogmjob      \
  -I$(top_srcdir)/libogmrip      \
  -DOGMRIP_LIB_DIR=\""$(libdir)"\"   \
  -DOGMRIP_DATA_DIR=\""$(datadir)"\"

CLEANFILES = \
  $(BUILT_SOURCES)

