AM_CXXFLAGS = \
	$(FAM_CFLAGS)                                   \
	$(GNUBIFF_DEP_CFLAGS)                           \
	$(GNOME_DEP_CFLAGS)                             \
	-Wall -pedantic -export-dynamic

AM_CFLAGS = \
	$(AM_CXXFLAGS)                                  \
	-ansi

AM_CPPFLAGS = \
	-DGNUBIFF_LOCALEDIR=\""$(datadir)/locale"\"		\
	-DGNUBIFF_DATADIR=\""$(pkgdatadir)"\"			\
	-DGNUBIFF_ICONDIR=\""$(datadir)/pixmaps"\"		\
	-DGNUBIFF_UIDIR=\""$(datadir)/gnome-2.0/ui"\"	\
	-DREAL_DATADIR=\""$(datadir)"\"					\
	-D_GNU_SOURCE

bin_PROGRAMS = gnubiff

gnome_sources =  \
	ui-applet-gnome.cc 		ui-applet-gnome.h

common_sources = \
	biff.cc					biff.h					\
	\
	mailbox.cc				mailbox.h				\
	header.cc				header.h				\
	socket.cc				socket.h				\
	support.cc				support.h				\
	nls.h											\
	decoding.cc				decoding.h				\
	local.cc				local.h					\
	file.cc					file.h					\
	imap4.cc				imap4.h					\
	maildir.cc				maildir.h				\
	mh.cc					mh.h					\
	mh_basic.cc				mh_basic.h				\
	mh_sylpheed.cc			mh_sylpheed.h			\
	pop.cc					pop.h					\
	apop.cc					apop.h					\
	pop3.cc					pop3.h					\
	\
	option.cc				option.h				\
	options.cc				options.h				\
	gnubiff_options.cc		gnubiff_options.h		\
	\
	gui.cc					gui.h					\
	ui-applet.cc			ui-applet.h				\
	ui-applet-gtk.cc 		ui-applet-gtk.h			\
	ui-applet-gui.cc		ui-applet-gui.h			\
	ui-applet-systray.cc	ui-applet-systray.h		\
	ui-preferences.cc 		ui-preferences.h		\
	ui-authentication.cc	ui-authentication.h		\
	ui-certificate.cc		ui-certificate.h		\
	ui-properties.cc		ui-properties.h			\
	gtk_image_animation.cc	gtk_image_animation.h 	\
	ui-popup.cc				ui-popup.h				\
	\
	signals.cc				signals.h				\
	\
	eggtrayicon.c			eggtrayicon.h


gnubiff_SOURCES      = $(common_sources) gnubiff.cc
gnubiff_LDADD        = $(INTLLIBS) $(GNUBIFF_DEP_LIBS) $(FAM_LIBS)
panelappletdir       = `pkg-config --variable=libpanel_applet_dir libpanel-applet`
panelapplet_in_files =
panelapplet_DATA     =
uidir			     = $(datadir)/gnome-2.0/ui
ui_DATA              = 

##
## Additional files and directories for the gnome panel frontend
##
if USE_GNOME
gnubiff_applet_libdir          = $(pkglibdir)
gnubiff_applet_lib_LTLIBRARIES = libgnubiff-applet.la
libgnubiff_applet_la_SOURCES   = $(common_sources) $(gnome_sources)
libgnubiff_applet_la_CPPFLAGS  = $(AM_CPPFLAGS) -DGNOMELOCALEDIR=\""$(localedir)"\" -DUSE_GNOME
libgnubiff_applet_la_LIBADD    = $(gnubiff_LDADD) $(GNOME_DEP_LIBS)
libgnubiff_applet_la_LDFLAGS   = $(gnubiff_LDFLAGS) -module -avoid-version

panelapplet_in_files += org.gnome.panel.applet.GnubiffApplet.panel-applet.in
panelapplet_DATA     += $(panelapplet_in_files:.panel-applet.in=.panel-applet)
ui_DATA		         += GNOME_gnubiffApplet.xml
endif

$(panelapplet_in_files): $(panelapplet_in_files:.panel-applet.in=.panel-applet.in.in)
	sed -e "s|\@LOCATION\@|$(pkglibdir)/libgnubiff-applet.so|" \
	    -e "s|\@PKGDATADIR\@|$(pkgdatadir)|" $< > $@

# Following rule should be provided by intltool (INTLTOOL_PANEL_APPLET_RULE)
%.panel-applet: %.panel-applet.in $(INTLTOOL_MERGE) $(wildcard $(top_srcdir)/po/*po) ; $(INTLTOOL_MERGE) $(top_srcdir)/po $< $@ -d -u -c $(top_builddir)/po/.intltool-merge-cache

##
## Files not yet (or not always) covered that must be included when creating
## a package for distribution
##
EXTRA_DIST = \
	org.gnome.panel.applet.GnubiffApplet.panel-applet.in.in	\
	GNOME_gnubiffApplet.xml				\
	gnubiff.schemas						\
	$(gnome_sources)

##
## Created files to be deleted when executing "make distclean"
##
DISTCLEANFILES = \
	org.gnome.panel.applet.GnubiffApplet.panel-applet.in \
	org.gnome.panel.applet.GnubiffApplet.panel-applet

