SUBDIRS = glade images ui dtd stylesheets mime sql

desktopdir = $(datadir)/applications
desktop_in_files = planner.desktop.in
desktop_DATA = planner.desktop
@INTLTOOL_DESKTOP_RULE@

gsettings_SCHEMAS = org.gnome.Planner.gschema.xml
@GSETTINGS_RULES@

man_MANS = planner.1

EXTRA_DIST = 				\
	$(desktop_in_files)		\
	$(gsettings_SCHEMAS)		\
	$(man_MANS)

CLEANFILES = $(desktop_DATA)
