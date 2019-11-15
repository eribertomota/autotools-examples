INCLUDES =					\
	-I$(top_srcdir)				\
	-I$(top_builddir)			\
	$(EDS_BACKEND_CFLAGS)			

%.eplug: %.eplug.in
	sed -e 's|\@PLUGINDIR\@|$(plugindir)|' $< > $@

plugin_DATA = org-gnome-planner-source.eplug
plugin_LTLIBRARIES = liborg-gnome-planner-source.la


liborg_gnome_planner_source_la_SOURCES = planner-source.c
liborg_gnome_planner_source_la_LDFLAGS = -module -avoid-version
liborg_gnome_planner_source_la_LIBADD =	 $(EDS_BACKEND_LIBS)

EXTRA_DIST = org-gnome-planner-source.eplug.in
