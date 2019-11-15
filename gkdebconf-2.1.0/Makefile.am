AUTOMAKE_OPTIONS = foreign

gsettings_SCHEMAS = org.debian.gkdebconf.gschema.xml
EXTRA_DIST = $(gsettings_SCHEMAS)
@GSETTINGS_RULES@

DISTCLEANFILES = *~ po/*.gmo

SUBDIRS = po src scripts pixmaps man docs
DIST_SUBDIRS = $(SUBDIRS)
