INCLUDES = 							\
	-I$(top_srcdir)						\
	-I$(top_srcdir)/src					\
	-I$(top_builddir)					\
	-I$(top_builddir)/src					\
	$(PLANNER_CFLAGS) $(WARN_CFLAGS)			\
	-DG_LOG_DOMAIN=\"Planner\"				\
	-DPREFIX=\""$(prefix)"\"				\
	-DSYSCONFDIR=\""$(sysconfdir)"\"			\
	-DLIBDIR=\""$(libdir)"\"				\
	-DDATADIR=\""$(datadir)"\"

if HAVE_PYTHON_PLUGIN
INCLUDES += $(PYTHON_INCLUDES) $(PYGOBJECT_CFLAGS)
endif

bin_PROGRAMS = planner 
planner_SOURCES = \
	planner-main.c
planner_LDFLAGS = -export-dynamic
planner_LDADD = \
	libplannerapp.la

# Create a convenience library to link our tests against
noinst_LTLIBRARIES = libplannerapp.la
libplannerapp_la_LIBADD = $(top_builddir)/libplanner/libplanner-1.la \
                            $(PLANNER_LIBS) -lm

libplannerapp_la_SOURCES = 			\
	$(built_sources)		\
	eel-canvas-rect.c		\
	eel-canvas-rect.h		\
	dummy-canvas-item.c		\
	dummy-canvas-item.h		\
	planner-application.c		\
	planner-application.h		\
	planner-assignment-model.c	\
	planner-assignment-model.h	\
	planner-conf.h                  \
	planner-conf-gconf.c            \
	planner-calendar.c		\
	planner-calendar-dialog.c	\
	planner-calendar-dialog.h	\
	planner-calendar.h		\
	planner-calendar-selector.c	\
	planner-calendar-selector.h	\
	planner-canvas-line.c		\
	planner-canvas-line.h		\
	planner-cell-renderer-date.c	\
	planner-cell-renderer-date.h	\
	planner-cell-renderer-list.c	\
	planner-cell-renderer-list.h	\
	planner-cell-renderer-popup.c	\
	planner-cell-renderer-popup.h	\
	planner-cmd-manager.c		\
	planner-cmd-manager.h		\
	planner-column-dialog.c		\
	planner-column-dialog.h		\
	planner-day-type-dialog.c	\
	planner-day-type-dialog.h	\
	planner-default-week-dialog.c	\
	planner-default-week-dialog.h	\
	planner-format.c		\
	planner-format.h		\
	planner-group-dialog.c		\
	planner-group-dialog.h		\
	planner-group-model.c		\
	planner-group-model.h		\
	planner-list-model.c		\
	planner-list-model.h		\
	planner-phase-dialog.c		\
	planner-phase-dialog.h		\
	planner-plugin.c		\
	planner-plugin.h		\
	planner-plugin-loader.c		\
	planner-plugin-loader.h		\
	planner-popup-button.c		\
	planner-popup-button.h		\
	planner-popup-entry.c		\
	planner-popup-entry.h		\
	planner-predecessor-model.c	\
	planner-predecessor-model.h	\
	planner-print-dialog.c		\
	planner-print-dialog.h		\
	planner-print-job.c		\
	planner-print-job.h		\
	planner-project-properties.c	\
	planner-project-properties.h	\
	planner-property-dialog.c	\
	planner-property-dialog.h	\
	planner-property-model.c	\
	planner-property-model.h	\
	planner-resource-cmd.c		\
	planner-resource-cmd.h		\
	planner-resource-dialog.c	\
	planner-resource-dialog.h	\
	planner-resource-input-dialog.c	\
	planner-resource-input-dialog.h	\
	planner-scale-utils.c		\
	planner-scale-utils.h		\
	planner-sidebar.c		\
	planner-sidebar.h		\
	planner-table-print-sheet.c	\
	planner-table-print-sheet.h	\
	planner-task-cmd.c		\
	planner-task-cmd.h		\
	planner-task-date-widget.c	\
	planner-task-date-widget.h	\
	planner-task-dialog.c		\
	planner-task-dialog.h		\
	planner-task-input-dialog.c	\
	planner-task-input-dialog.h	\
	planner-util.c			\
	planner-util.h			\
	planner-view.c			\
	planner-view.h			\
	planner-window.c		\
	planner-window.h		\
	planner-working-time-dialog.c	\
	planner-working-time-dialog.h	\
	valgrind.h			\
	$(gantt_task_source)		\
	$(task_source)			\
	$(resource_source)		\
	$(usage_source)

gantt_task_source = 			\
	planner-gantt-background.c	\
	planner-gantt-background.h	\
	planner-gantt-header.c		\
	planner-gantt-header.h		\
	planner-gantt-model.c		\
	planner-gantt-model.h		\
	planner-task-tree.c		\
	planner-task-tree.h		\
	planner-task-popup.c 		\
	planner-task-popup.h		\
	planner-relation-arrow.c	\
	planner-relation-arrow.h	\
	planner-gantt-chart.c		\
	planner-gantt-chart.h		\
	planner-gantt-print.c		\
	planner-gantt-print.h		\
	planner-gantt-row.c		\
	planner-gantt-row.h		\
	planner-gantt-view.c		\
	planner-gantt-view.h		\
	planner-task-view.c		\
	planner-task-view.h

resource_source = 			\
	planner-resource-view.c		\
	planner-resource-view.h

usage_source = 				\
	planner-usage-view.c		\
	planner-usage-view.h		\
	planner-usage-chart.c		\
	planner-usage-chart.h		\
	planner-usage-model.c		\
	planner-usage-model.h		\
	planner-usage-row.c		\
	planner-usage-row.h		\
	planner-usage-tree.c		\
	planner-usage-tree.h


#
# Plugins
#

plugindir = $(libdir)/plugins

if HAVE_GDA
sql_plugin = libsql-plugin.la
libsql_plugin_la_SOURCES = planner-sql-plugin.c
libsql_plugin_la_LIBADD =  $(GDA_LIBS)
libsql_plugin_la_CFLAGS = $(GDA_CFLAGS) -DGDA_VERSION=@GDA_VER@
libsql_plugin_la_LDFLAGS = -avoid-version -module
endif

if HAVE_PYTHON_PLUGIN
python_plugin = libpython-plugin.la
libpython_plugin_la_SOURCES = planner-python-plugin.c
libpython_plugin_la_LDFLAGS = -avoid-version -module
libpython_plugin_la_LIBADD  = $(PYTHON_LIB)
endif

if HAVE_EDS_PLUGIN
eds_plugin = libeds-plugin.la
libeds_plugin_la_SOURCES = planner-eds-plugin.c
libeds_plugin_la_LDFLAGS = -avoid-version -module
libeds_plugin_la_LIBADD  = $(EDS_LIBS)
libeds_plugin_la_CFLAGS  = $(EDS_CFLAGS)
endif

plugin_LTLIBRARIES = 			\
	libhtml-plugin.la		\
	libxmlplanner-plugin.la		\
	libmsp-plugin.la		\
	$(sql_plugin)			\
	$(python_plugin)		\
	$(eds_plugin)

libhtml_plugin_la_SOURCES = planner-html-plugin.c
libhtml_plugin_la_LDFLAGS = -avoid-version -module

libxmlplanner_plugin_la_SOURCES = planner-xml-planner-plugin.c
libxmlplanner_plugin_la_LDFLAGS = -avoid-version -module

libmsp_plugin_la_SOURCES = planner-msp-plugin.c
libmsp_plugin_la_LDFLAGS = -avoid-version -module

planner-marshal.h: Makefile.am planner-marshal.list
	$(GLIB_GENMARSHAL) --prefix=planner_marshal $(srcdir)/planner-marshal.list --header > xgen-gmh \
	&& (cmp -s xgen-gmh planner-marshal.h || cp xgen-gmh planner-marshal.h) \
	&& rm -f xgen-gmh xgen-gmh~

planner-marshal.c: Makefile.am planner-marshal.list
	(echo "#include \"planner-marshal.h\""; $(GLIB_GENMARSHAL) --prefix=planner_marshal $(srcdir)/planner-marshal.list --body) > xgen-gmc \
	&& cp xgen-gmc planner-marshal.c \
	&& rm -f xgen-gmc xgen-gmc~

# do not use BUILT_SOURCES because of weird semantics
# i *think* these should actually be stamp-* files
built_sources = planner-marshal.h planner-marshal.c

$(libplannerapp_la_OBJECTS): $(built_sources)

EXTRA_DIST = planner-marshal.list	\
	     planner-util-win32.c

CLEANFILES = $(built_sources)

-include $(INTROSPECTION_MAKEFILE)
INTROSPECTION_GIRS =
INTROSPECTION_SCANNER_ARGS = --add-include-path=$(srcdir) \
                             --add-include-path=$(top_builddir)/libplanner \
                             --warn-all
INTROSPECTION_COMPILER_ARGS = --includedir=$(srcdir) \
                              --includedir=$(top_builddir)/libplanner

if HAVE_INTROSPECTION
introspection_sources = $(libplannerapp_la_SOURCES)

Planner-1.gir: libplannerapp.la
Planner_1_gir_INCLUDES = GObject-2.0 Gtk-2.0 Mrp-1
Planner_1_gir_CFLAGS = $(INCLUDES) $(top_srcdir)/libplanner
Planner_1_gir_LIBS = libplannerapp.la
Planner_1_gir_FILES = $(introspection_sources)
INTROSPECTION_GIRS += Planner-1.gir

girdir = $(datadir)/planner/gir-1.0
gir_DATA = $(INTROSPECTION_GIRS)

typelibdir = $(libdir)
typelib_DATA = $(INTROSPECTION_GIRS:.gir=.typelib)

CLEANFILES += $(gir_DATA) $(typelib_DATA)
endif
