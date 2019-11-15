## Process this file with automake to produce Makefile.in

# The name of the module.
DOC_MODULE=libplanner

# The top-level SGML file.
DOC_MAIN_SGML_FILE=libplanner-docs.sgml

# The directory containing the source code. Relative to $(srcdir)
DOC_SOURCE_DIR=../../libplanner

# Extra options to pass to gtkdoc-scangobj
SCANGOBJ_OPTIONS=--type-init-func="g_type_init()" 

# Extra options to supply to gtkdoc-scan
#SCAN_OPTIONS=--deprecated-guards="GTK_ENABLE_BROKEN|GTK_DISABLE_DEPRECATED" 

# Extra options to supply to gtkdoc-mkdb
MKDB_OPTIONS=--sgml-mode --output-format=xml

# Extra options to supply to gtkdoc-fixref
#FIXXREF_OPTIONS=--extra-dir=../file-modules/html --extra-dir=../file-modules/html

# Used for dependencies
HFILE_GLOB=$(top_srcdir)/libplanner/*.h
CFILE_GLOB=$(top_srcdir)/libplanner/*.c

# Header files to ignore when scanning
IGNORE_HFILES=  mrp-intl.h 			\
		mrp-marshal.h			\
		mrp-task-manager.h		\
		mrp-storage-module.h		\
		mrp-storage-module-factory.h	\
		mrp-private.h			\
		mrp-file-module.h

# Extra SGML files that are included by $(DOC_MAIN_SGML_FILE)
content_files = 		

# Other files to distribute
extra_files =

# CFLAGS and LDFLAGS for compiling scan program. Only needed
# if $(DOC_MODULE).types is non-empty.
GTKDOC_CFLAGS = 					\
	$(LIBPLANNER_CFLAGS)				\
	-I$(top_srcdir) 				\
	-I$(top_builddir)/libplanner

GTKDOC_LIBS =						\
	$(LIBPLANNER_LIBS)				\
	$(top_builddir)/libplanner/libplanner-1.la


GTKDOC_CC=$(LIBTOOL) --mode=compile $(CC)
GTKDOC_LD=$(LIBTOOL) --mode=link $(CC)

include ../../gtk-doc.make
