SUBDIRS = glade images ui dtd stylesheets mime sql

desktopdir = $(datadir)/applications
desktop_in_files = planner.desktop.in
desktop_DATA = planner.desktop
@INTLTOOL_DESKTOP_RULE@

schemadir = @GCONF_SCHEMA_FILE_DIR@
schema_in_files = planner.schemas.in
schema_DATA = $(schema_in_files:.schemas.in=.schemas)
@INTLTOOL_SCHEMAS_RULE@

man_MANS = planner.1

if GCONF_SCHEMAS_INSTALL
install-data-local:
	GCONF_CONFIG_SOURCE=$(GCONF_SCHEMA_CONFIG_SOURCE) $(GCONFTOOL) --makefile-install-rule $(schema_DATA)
else
install-data-local:
endif

EXTRA_DIST = 				\
	$(desktop_in_files)		\
	$(schema_in_files)		\
	$(man_MANS)

CLEANFILES = $(desktop_DATA)
DISTCLEANFILES = $(schema_DATA)
