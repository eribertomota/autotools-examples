#export QT_SELECT=qt5

bin_PROGRAMS = dgedit

dgedit_LDADD = $(SNDFILE_LIBS) $(QT_LIBS) $(AO_LIBS) \
	$(shell ../tools/MocList o ) qrc_dgedit.o

dgedit_CXXFLAGS = -g $(SNDFILE_CXXFLAGS) $(QT_CFLAGS) $(AO_CFLAGS) \
	-DLOCALEDIR='"$(localedir)"'
AM_CXXFLAGS = $(QT_CFLAGS)

dgedit_TRANSLATIONS = \
	ts/dgedit_da.ts \
	ts/dgedit_fr.ts

dgedit_SOURCES = \
	dgedit.cc \
	aboutdialog.cc \
	audioextractor.cc \
	canvas.cc \
	canvastool.cc \
	canvastoollisten.cc \
	canvastoolselections.cc \
	canvastoolthreshold.cc \
	canvaswidget.cc \
	channeldialog.cc \
	channelswidget.cc \
	filelist.cc \
	imageeditor.cc \
	instrumentdialog.cc \
	instrumentwidget.cc \
	itemeditor.cc \
	localehandler.cc \
	mainwindow.cc \
	mipmap.cc \
	player.cc \
	project.cc \
	projectdialog.cc \
	projectrenderer.cc \
	projectserialiser.cc \
	renderdialog.cc \
	samplesorter.cc \
	selection.cc \
	selectioneditor.cc \
	settings.cc \
	volumefader.cc \
	zoomslider.cc

HDRS = \
	aboutdialog.h \
	audioextractor.h \
	canvas.h \
	canvastool.h \
	canvastoollisten.h \
	canvastoolselections.h \
	canvastoolthreshold.h \
	canvaswidget.h \
	channeldialog.h \
	channelswidget.h \
	filelist.h \
	imageeditor.h \
	instrumentdialog.h \
	instrumentwidget.h \
	itemeditor.h \
	localehandler.h \
	mainwindow.h \
	mipmap.h \
	player.h \
	project.h \
	projectdialog.h \
	projectrenderer.h \
	projectserialiser.h \
	renderdialog.h \
	samplesorter.h \
	selection.h \
	selectioneditor.h \
	sleep.h \
	settings.h \
	volumefader.h \
	zoomslider.h

EXTRA_DIST = \
	$(dgedit_TRANSLATIONS) \
	$(HDRS) \
	dgedit.qrc

dgedit_MOC = $(shell ../tools/MocList cc )

BUILT_SOURCES = \
	$(dgedit_MOC) \
	qrc_dgedit.cc \
	$(dgedit_TRANSLATIONS:.ts=.qm)

CLEANFILES = $(BUILT_SOURCES)

qrc_%.cc: %.qrc
	QT_SELECT=qt5 $(QT_RCC) $< > $@

%.moc.cc: %.h
	QT_SELECT=qt5 $(QT_MOC) -o $@ $<

#
# ui files not used in this project...
#%.h: %.ui
#	$(QT_UIC) -o $@ $<
#
#%.cc: %.ui
#	$(QT_UIC) -o $@ -impl $*.h $<

# command for creating .res file from .rc on Win32
%.res: %.rc
	rc $<

%.ts: $(dgedit_SOURCES) $(HDRS)
	QT_SELECT=qt5 lupdate $(dgedit_SOURCES) $(HDRS) -ts $@

%.qm: %.ts
	QT_SELECT=qt5 lrelease $<

dgeditdir = $(localedir)
dgedit_DATA = $(dgedit_TRANSLATIONS:.ts=.qm)
