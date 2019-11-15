INCLUDES = 				\
	-I$(top_srcdir)			\
	-I$(top_srcdir)/src		\
	$(PYTHON_INCLUDES)		\
	$(PYGTK_CFLAGS)			\
	$(PLANNER_CFLAGS)

pkgpythondir = $(pythondir)
pkgpyexecdir = $(pyexecdir)

pkgpyexec_LTLIBRARIES = planner.la plannerui.la

planner_la_CFLAGS = -Wno-missing-declarations -Wno-missing-prototypes
planner_la_LDFLAGS = -module -avoid-version -export-symbols-regex initplanner
planner_la_LIBADD = $(LIBPLANNER_LIBS) $(top_builddir)/libplanner/libplanner-1.la
planner_la_SOURCES = plannermodule.c
nodist_planner_la_SOURCES = planner.c

plannerui_la_CFLAGS = -Wno-missing-declarations -Wno-missing-prototypes
plannerui_la_LDFLAGS = -module -avoid-version -export-symbols-regex initplannerui
plannerui_la_LIBADD = $(PLANNER_LIBS) $(top_builddir)/libplanner/libplanner-1.la
plannerui_la_SOURCES = planneruimodule.c
nodist_plannerui_la_SOURCES = plannerui.c

CLEANFILES = planner.c plannerui.c

EXTRA_DIST = 				\
	planner.override		\
	planner.defs			\
	planner-types.defs		\
	planner-arg-types.py		\
					\
	plannerui.override		\
	plannerui.defs			\
	plannerui-types.defs

planner.c: planner.defs planner-types.defs planner.override
	( cd $(srcdir) && $(PYGOBJECT_CODEGEN) \
	    --override $*.override \
            --load-types planner-arg-types.py \
            --register $(PYGTK_DEFSDIR)/gtk-types.defs \
	    --prefix $* $*.defs ) > gen-$*.c \
	&& cp gen-$*.c $*.c \
	&& rm -f gen-$*.c

plannerui.c: plannerui.defs plannerui-types.defs plannerui.override
	( cd $(srcdir) && $(PYGOBJECT_CODEGEN) \
	    --override $*.override \
            --load-types planner-arg-types.py \
            --register $(PYGTK_DEFSDIR)/gtk-types.defs \
            --register planner-types.defs \
	    --prefix $* $*.defs ) > gen-$*.c \
	&& cp gen-$*.c $*.c \
	&& rm -f gen-$*.c
