if HAVE_GTK_SUPPORT

uidir = $(datadir)/ogmrip
ui_DATA = ogmrip-ui.xml

gladedir = $(datadir)/ogmrip
glade_DATA = ogmrip-crop.glade           \
             ogmrip-main.glade           \
             ogmrip-options.glade        \
             ogmrip-pref.glade           \
             ogmrip-profile-editor.glade \
             ogmrip-profiles.glade       \
             ogmrip-progress.glade       \
             ogmrip-queue.glade          \
             ogmrip-update.glade         \
             ogmrip-spell.glade          \
             ogmrip-lavc.glade           \
             ogmrip-x264.glade           \
             ogmrip-xvid.glade

pixmapdir = $(datadir)/pixmaps
pixmap_DATA = ogmrip.png

profilesdir = $(datadir)/ogmrip/profiles
profilesfile = profiles.xml.in
profiles_DATA = $(profilesfile:.xml.in=.xml)
@INTLTOOL_XML_RULE@

desktopdir  = $(datadir)/applications
desktopfile = ogmrip.desktop.in
desktop_DATA = $(desktopfile:.desktop.in=.desktop)
@INTLTOOL_DESKTOP_RULE@

schemasdir  = $(GCONF_SCHEMA_FILE_DIR)
schemasfile = ogmrip.schemas.in
schemas_DATA = $(schemasfile:.schemas.in=.schemas)
@INTLTOOL_SCHEMAS_RULE@

if GCONF_SCHEMAS_INSTALL
install-data-local:
	-GCONF_CONFIG_SOURCE=$(GCONF_SCHEMA_CONFIG_SOURCE) \
      $(GCONFTOOL) --makefile-install-rule $(srcdir)/$(schemas_DATA)
endif # GCONF_SCHEMAS_INSTALL

endif # HAVE_GTK_SUPPORT

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = ogmrip.pc     \
                 ogmrip-gtk.pc \
                 ogmdvd.pc     \
                 ogmdvd-gtk.pc \
                 ogmjob.pc

EXTRA_DIST =      \
  $(ui_DATA)      \
  $(glade_DATA)   \
  $(pixmap_DATA)  \
  $(profilesfile) \
  $(desktopfile)  \
  $(schemasfile)

CLEANFILES = \
  *.gladep   \
  *.bak

DISTCLEANFILES = \
  ogmrip.desktop \
  ogmrip.schemas \
  profiles.xml

