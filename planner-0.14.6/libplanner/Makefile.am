INCLUDES = \
	-I$(top_srcdir) \
	-I$(top_srcdir)/libplanner \
	-I$(top_builddir) \
	-I$(top_builddir)/libplanner \
	$(LIBPLANNER_CFLAGS) $(WARN_CFLAGS) \
	-DSTORAGEMODULEDIR=\""$(libdir)/storage-modules"\" \
	-DFILEMODULESDIR=\""$(libdir)/file-modules"\" \
	-DPLUGINDIR=\""$(libdir)/plugins"\"		\
	-DDATADIR=\""$(datadir)/planner"\"

lib_LTLIBRARIES = libplanner-1.la

libplanner_1_la_SOURCES = 			\
	$(built_sources)			\
	mrp-application.c			\
	mrp-assignment.c			\
	mrp-calendar.c				\
	mrp-day.c				\
	mrp-group.c				\
	mrp-object.c				\
	mrp-file-module.c			\
	mrp-file-module.h			\
	mrp-project.c				\
	mrp-resource.c				\
	mrp-storage-module.c			\
	mrp-storage-module-factory.c		\
	mrp-storage-module-factory.h		\
	mrp-task-manager.c			\
	mrp-task-manager.h			\
	mrp-task.c				\
	mrp-relation.c				\
	mrp-types.c				\
	mrp-private.h				\
	mrp-property.c				\
	mrp-time.c				\
	mrp-error.c				\
	mrp-paths-gnome.c

libplannerinclude_HEADERS = 			\
	planner.h				\
	mrp-application.h			\
	mrp-assignment.h			\
	mrp-calendar.h				\
	mrp-day.h				\
	mrp-group.h				\
	mrp-object.h				\
	mrp-project.h				\
	mrp-property.h				\
	mrp-resource.h				\
	mrp-storage-module.h			\
	mrp-task.h				\
	mrp-relation.h				\
	mrp-types.h				\
	mrp-time.h				\
	mrp-error.h				\
	mrp-paths.h

libplanner_1_la_LIBADD = $(LIBPLANNER_LIBS) -lm

libplannerincludedir = $(includedir)/planner-1.0/libplanner


#
# Storage modules
#
storagemoduledir = $(libdir)/storage-modules

if HAVE_GDA
sql_library = libstorage-sql.la
endif

storagemodule_LTLIBRARIES = 			\
	libstorage-mrproject-1.la		\
	$(sql_library)

libstorage_mrproject_1_la_SOURCES = 		\
	mrp-storage-mrproject.c			\
	mrp-storage-mrproject.h			\
	mrp-parser.c				\
	mrp-parser.h

libstorage_mrproject_1_la_LDFLAGS =  -avoid-version -module
libstorage_mrproject_1_la_LIBADD = libplanner-1.la

if HAVE_GDA
libstorage_sql_la_SOURCES = 			\
	mrp-storage-sql.c			\
	mrp-storage-sql.h			\
	mrp-sql.c				\
	mrp-sql.h

libstorage_sql_la_LDFLAGS =  -avoid-version -module
libstorage_sql_la_CFLAGS = $(GDA_CFLAGS) -DGDA_VERSION=@GDA_VER@
libstorage_sql_la_LIBADD =  $(GDA_LIBS) libplanner-1.la
endif

#
# File modules
#
filemoduledir = $(libdir)/file-modules

filemodule_LTLIBRARIES = 			\
	libmrp-xml.la				\
	libmrp-xsl.la

libmrp_xml_la_SOURCES = 			\
	mrp-xml.c				\
	mrp-old-xml.c				\
	mrp-old-xml.h

libmrp_xml_la_CFLAGS = -DDTDDIR=\""$(datadir)/planner/dtd"\"
libmrp_xml_la_LDFLAGS = -avoid-version -module
libmrp_xml_la_LIBADD = libplanner-1.la

libmrp_xsl_la_SOURCES = mrp-xsl.c
libmrp_xsl_la_CFLAGS = 	$(XSLT_CFLAGS) -DSTYLESHEETDIR=\""$(datadir)/planner/stylesheets"\"
libmrp_xsl_la_LDFLAGS = -avoid-version -module
libmrp_xsl_la_LIBADD = $(XSLT_LIBS) libplanner-1.la

mrp-marshal.h: Makefile.am mrp-marshal.list
	$(GLIB_GENMARSHAL) --prefix=mrp_marshal $(srcdir)/mrp-marshal.list --header > xgen-gmh \
	&& (cmp -s xgen-gmh mrp-marshal.h || cp xgen-gmh mrp-marshal.h) \
	&& rm -f xgen-gmh xgen-gmh~

mrp-marshal.c: Makefile.am mrp-marshal.list
	(echo "#include \"mrp-marshal.h\""; $(GLIB_GENMARSHAL) --prefix=mrp_marshal $(srcdir)/mrp-marshal.list --body) > xgen-gmc \
	&& cp xgen-gmc mrp-marshal.c \
	&& rm -f xgen-gmc xgen-gmc~

# do not use BUILT_SOURCES because of weird semantics
# i *think* these should actually be stamp-* files
built_sources = mrp-marshal.h  mrp-marshal.c

$(libplanner_1_la_OBJECTS): $(built_sources)

EXTRA_DIST = mrp-marshal.list

CLEANFILES = $(built_sources)

-include $(INTROSPECTION_MAKEFILE)
INTROSPECTION_GIRS =
INTROSPECTION_SCANNER_ARGS = --add-include-path=$(srcdir) --warn-all
INTROSPECTION_COMPILER_ARGS = --includedir=$(srcdir)

if HAVE_INTROSPECTION
introspection_sources = $(libplannerinclude_HEADERS) $(libplanner_1_la_SOURCES)

Mrp-1.gir: libplanner-1.la
Mrp_1_gir_INCLUDES = GObject-2.0
Mrp_1_gir_CFLAGS = $(INCLUDES)
Mrp_1_gir_LIBS = libplanner-1.la
Mrp_1_gir_FILES = $(introspection_sources)
INTROSPECTION_GIRS += Mrp-1.gir

girdir = $(datadir)/planner/gir-1.0
gir_DATA = $(INTROSPECTION_GIRS)

typelibdir = $(libdir)
typelib_DATA = $(INTROSPECTION_GIRS:.gir=.typelib)

CLEANFILES += $(gir_DATA) $(typelib_DATA)
endif
