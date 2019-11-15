SUBDIRS = . plugins data images

AM_CFLAGS = -I$(top_srcdir)

sharedir = $(datadir)/roger
share_DATA = \
	images/app.png

EXTRA_DIST = $(share_DATA) roger_winres.rc roger.gresource.xml

bin_PROGRAMS = roger

roger_CFLAGS = $(EXTRA_CFLAGS) $(GTK_CFLAGS) $(GMODULE_CFLAGS) -Wall -O2 -g $(PEAS_GTK_CFLAGS) $(SNDFILE_CFLAGS) $(AM_CFLAGS) $(OS_CFLAGS) $(TIFF_CFLAGS)
roger_LDFLAGS = $(EXTRA_LIBS) $(GTK_LIBS) $(GMODULE_LIBS) -export-dynamic $(top_builddir)/libroutermanager/libroutermanager.la $(PEAS_GTK_LIBS) $(SNDFILE_LIBS) $(SPANDSP_LIBS) $(OS_LIBS) $(TIFF_LIBS)

GLIB_COMPILE_RESOURCES = $(shell $(PKG_CONFIG) --variable=glib_compile_resources gio-2.0)

roger_gresource.c: roger.gresource.xml $(shell $(GLIB_COMPILE_RESOURCES) --sourcedir=. --generate-dependencies roger.gresource.xml)
	$(GLIB_COMPILE_RESOURCES) roger.gresource.xml --target=$@ --sourcedir=. --generate-source

roger_gresource.h: roger.gresource.xml $(shell $(GLIB_COMPILE_RESOURCES) --sourcedir=. --generate-dependencies roger.gresource.xml)
	$(GLIB_COMPILE_RESOURCES) roger.gresource.xml --target=$@ --sourcedir=. --generate-header

roger_core_SOURCES =\
	about.c\
	about.h\
	application.c\
	application.h\
	assistant.c\
	assistant.h\
	contacts.c\
	contacts.h\
	contact_edit.c\
	contact_edit.h\
	fax.c\
	fax.h\
	icons.c\
	icons.h\
	journal.c\
	journal.h\
	main.h\
	main_ui.c \
	phone.c\
	phone.h\
	pref.c\
	pref.h\
	pref_action.c\
	pref_action.h\
	pref_audio.c\
	pref_audio.h\
	pref_fax.c \
	pref_fax.h \
	pref_filters.c\
	pref_filters.h\
	pref_plugins.c\
	pref_plugins.h\
	pref_prefix.c\
	pref_prefix.h\
	pref_router.c\
	pref_router.h\
	pref_security.c\
	pref_security.h\
	pref_softphone.c\
	pref_softphone.h\
	pref_misc.c\
	pref_misc.h\
	print.c \
	print.h \
	uitools.c \
	uitools.h \
	roger_gresource.c \
	roger_gresource.h

roger_SOURCES = $(roger_core_SOURCES)

if WIN32
roger_SOURCES +=\
	winmain.c

roger_LDFLAGS += roger_winres.res

BUILT_SOURCES = roger_winres.res

roger_winres.res: roger_winres.rc
	$(WINDRES) -i $< -o $@ -O coff

roger_coredir=$(bindir)
roger_core_LTLIBRARIES = libroger_core.la
libroger_core_la_SOURCES = $(roger_core_SOURCES)
libroger_core_la_CFLAGS = $(roger_CFLAGS)
libroger_core_la_LDFLAGS = $(roger_LDFLAGS) -shared -Wl,--output-def,roger_core.def,--out-implib,roger_core.dll.a -o roger_core.dll -no-undefined -avoid-version
endif

if MACOSX
roger_coredir=$(bindir)
roger_core_LTLIBRARIES = libroger_core.la
libroger_core_la_SOURCES = $(roger_core_SOURCES)
libroger_core_la_CFLAGS = $(roger_CFLAGS)
libroger_core_la_LDFLAGS = $(roger_LDFLAGS) -shared -no-undefined -avoid-version
endif
