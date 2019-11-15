INCLUDES = \
	$(FAM_CFLAGS) \
	$(GNUBIFF_DEP_CFLAGS)							\
	$(GNOME_DEP_CFLAGS)						\
	-DGNUBIFF_LOCALEDIR=\""$(datadir)/locale"\"		\
	-DGNUBIFF_DATADIR=\""$(pkgdatadir)"\"			\
	-DGNUBIFF_ICONDIR=\""$(datadir)/pixmaps"\"		\
	-DGNUBIFF_UIDIR=\""$(datadir)/gnome-2.0/ui"\"	\
	-DREAL_DATADIR=\""$(datadir)"\"					\
	-D_GNU_SOURCE									\
	-Wall -ansi -pedantic -export-dynamic

bin_PROGRAMS = gnubiff

gnome_sources =  \
	ui-applet-gnome.cc 		ui-applet-gnome.h

common_sources = \
	gnubiff.cc										\
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


## In case of compilation problem, just comment next lines
## then autoconf/automake/configure/make
.cc.o:
	@printf "%-40s" "Compiling $<... " 
	@am__fastdepCXX_TRUE@	if $(CXXCOMPILE) -MT $@ -MD -MP -MF "$(DEPDIR)/$*.Tpo" -c -o $@ $<; \
	@am__fastdepCXX_TRUE@	then mv -f "$(DEPDIR)/$*.Tpo" "$(DEPDIR)/$*.Po"; else rm -f "$(DEPDIR)/$*.Tpo"; exit 1; fi
	@AMDEP_TRUE@@am__fastdepCXX_FALSE@	source='$<' object='$@' libtool=no @AMDEPBACKSLASH@
	@AMDEP_TRUE@@am__fastdepCXX_FALSE@	DEPDIR=$(DEPDIR) $(CXXDEPMODE) $(depcomp) @AMDEPBACKSLASH@
	@am__fastdepCXX_FALSE@	$(CXXCOMPILE) -c -o $@ $<
	@echo "[OK]" 

gnubiff$(EXEEXT): $(gnubiff_OBJECTS) $(gnubiff_DEPENDENCIES) 
	@rm -f gnubiff$(EXEEXT)
	@printf "%-40s" "Linking $@ ... "
	$(CXXLINK) $(gnubiff_LDFLAGS) $(gnubiff_OBJECTS) $(gnubiff_LDADD) $(LIBS)
	@echo "[OK]"

## End of section to be commented in case of compilation problem


gnubiff_SOURCES      = $(common_sources)
gnubiff_LDADD        = $(INTLLIBS) $(GNUBIFF_DEP_LIBS) $(FAM_LIBS)
panelappletdir       = `pkg-config --variable=libpanel_applet_dir libpanel-applet`
panelapplet_in_files =
panelapplet_DATA     =
servicedir           = /usr/share/dbus-1/services
service_in_files     = 
service_DATA         =
uidir			     = $(datadir)/gnome-2.0/ui
ui_DATA              = 

##
## Additional files and directories for the gnome panel frontend
##
if USE_GNOME
gnubiff_SOURCES      += $(gnome_sources)
gnubiff_LDADD        += $(GNOME_DEP_LIBS)
panelapplet_in_files += org.gnome.panel.applet.GnubiffApplet.panel-applet.in
panelapplet_DATA     += $(panelapplet_in_files:.panel-applet.in=.panel-applet)
ui_DATA		         += GNOME_gnubiffApplet.xml
service_in_files     += org.gnome.panel.applet.GnubiffApplet_Factory.service.in
service_DATA         += $(service_in_files:.service.in=.service)
endif

$(panelapplet_in_files): $(panelapplet_in_files:.panel-applet.in=.panel-applet.in.in)
	sed -e "s|\@BINDIR\@|$(bindir)|" \
	    -e "s|\@PKGDATADIR\@|$(pkgdatadir)|" $< > $@

# Following rule should be provided by intltool (INTLTOOL_PANEL_APPLET_RULE)
%.panel-applet: %.panel-applet.in $(INTLTOOL_MERGE) $(wildcard $(top_srcdir)/po/*po) ; $(INTLTOOL_MERGE) $(top_srcdir)/po $< $@ -d -u -c $(top_builddir)/po/.intltool-merge-cache

org.gnome.panel.applet.GnubiffApplet_Factory.service: $(service_in_files)
	sed -e "s|\@BINDIR\@|$(bindir)|" $< > $@

##
## Files not yet (or not always) covered that must be included when creating
## a package for distribution
##
EXTRA_DIST = \
	org.gnome.panel.applet.GnubiffApplet_Factory.service.in \
	org.gnome.panel.applet.GnubiffApplet.panel-applet.in.in	\
	GNOME_gnubiffApplet.xml				\
	gnubiff.schemas						\
	$(gnome_sources)

##
## Created files to be deleted when executing "make distclean"
##
DISTCLEANFILES = \
	org.gnome.panel.applet.GnubiffApplet.panel-applet.in \
	org.gnome.panel.applet.GnubiffApplet.panel-applet \
	org.gnome.panel.applet.GnubiffApplet_Factory.service

