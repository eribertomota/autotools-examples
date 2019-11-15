AM_CPPFLAGS = $(GTKMM_CFLAGS) $(GTK_CFLAGS) $(GIG_CFLAGS)
DEFS = -DLOCALEDIR=\"$(datadir)/locale\" @DEFS@

if HAVE_GTK3
wraplabel =
else
wraplabel = wrapLabel.cc wrapLabel.hh
endif

if MAC
mac_src = MacHelper.h MacHelper.mm
mac_ld = -framework Foundation -framework AppKit
else
mac_src =
mac_ld =
endif

SUBDIRS = gfx

pkglib_LTLIBRARIES = libgigedit.la
libgigedit_la_SOURCES = \
	global.h \
	Settings.cpp Settings.h \
	compat.cpp compat.h \
	gigedit.cpp gigedit.h \
	mainwindow.cpp mainwindow.h \
	regionchooser.cpp regionchooser.h \
	dimregionchooser.cpp dimregionchooser.h \
	dimregionedit.cpp dimregionedit.h \
	paramedit.cpp paramedit.h \
	dimensionmanager.cpp dimensionmanager.h \
	CombineInstrumentsDialog.cpp CombineInstrumentsDialog.h \
	midirules.cpp midirules.h \
	scripteditor.cpp scripteditor.h \
	scriptslots.cpp scriptslots.h \
	ReferencesView.cpp ReferencesView.h \
	MacroEditor.cpp MacroEditor.h \
	MacrosSetup.cpp MacrosSetup.h \
	ManagedWindow.cpp ManagedWindow.h \
	$(wraplabel) $(mac_src)
libgigedit_la_LIBADD = \
	$(GTKMM_LIBS) $(GTK_LIBS) $(GIG_LIBS) $(SNDFILE_LIBS) gfx/libgigeditgfx.la
libgigedit_la_CXXFLAGS = \
	$(SNDFILE_CFLAGS)
libgigedit_la_LDFLAGS = \
	-version-info @SHARED_VERSION_INFO@ @SHLIB_VERSION_ARG@ -no-undefined \
	$(mac_ld)

bin_PROGRAMS = gigedit
gigedit_SOURCES = main.cpp
gigedit_LDADD = libgigedit.la $(SIGC_LIBS) $(GTK_LIBS) $(GTKMM_LIBS)
if WINDOWS
gigedit_LDFLAGS = -mwindows
endif
