noinst_PROGRAMS = plugingui rcgen
noinst_LTLIBRARIES = libdggui.la

# If you add a file here, remember to add it to plugin/Makefile.mingw32.in
RES = \
	resources/bg.png \
	resources/bypass_button.png \
	resources/font.png \
	resources/fontemboss.png \
	resources/help_button.png \
	resources/knob.png \
	resources/logo.png \
	resources/png_error \
	resources/progress.png \
	resources/pushbutton.png \
	resources/sidebar.png \
	resources/slider.png \
	resources/stddev_horizontal.png \
	resources/stddev_horizontal_disabled.png \
	resources/stddev_vertical.png \
	resources/stddev_vertical_disabled.png \
	resources/switch_back_off.png \
	resources/switch_back_on.png \
	resources/switch_front.png \
	resources/tab.png \
	resources/thinlistbox.png \
	resources/topbar.png \
	resources/toplogo.png \
	resources/vertline.png \
	resources/widget.png \
	../ABOUT \
	../AUTHORS \
	../BUGS \
	../COPYING

resource_data.cc : rcgen $(RES)
	./rcgen $(RES) > resource_data.cc

libdggui_la_CPPFLAGS = \
	$(GUI_CPPFLAGS) \
	-I$(top_srcdir)/hugin \
	-I$(top_srcdir)/src \
	-DWITH_HUG_MUTEX $(PTHREAD_CFLAGS) \
	-DLODEPNG_NO_COMPILE_ENCODER \
	-DLODEPNG_NO_COMPILE_DISK \
	-DLODEPNG_NO_COMPILE_ANCILLARY_CHUNKS \
	-DLODEPNG_NO_COMPILE_ERROR_TEXT \
	-DLODEPNG_NO_COMPILE_CPP

libdggui_la_CFLAGS =

libdggui_la_LIBTOOLFLAGS=--tag=CC

libdggui_la_LIBADD = \
	$(GUI_LIBS) $(PTHREAD_LIBS)

# If you add a file here, remember to add it to plugin/Makefile.mingw32.in
nodist_libdggui_la_SOURCES = \
	abouttab.cc \
	bleedcontrolframecontent.cc \
	button.cc \
	button_base.cc \
	checkbox.cc \
	colour.cc \
	combobox.cc \
	dialog.cc \
	directory.cc \
	diskstreamingframecontent.cc \
	drumkitframecontent.cc \
	drumkittab.cc \
	eventhandler.cc \
	filebrowser.cc \
	font.cc \
	frame.cc \
	helpbutton.cc \
	humanizerframecontent.cc \
	humaniservisualiser.cc \
	image.cc \
	imagecache.cc \
	knob.cc \
	label.cc \
	layout.cc \
	led.cc \
	lineedit.cc \
	listbox.cc \
	listboxbasic.cc \
	listboxthin.cc \
	maintab.cc \
	mainwindow.cc \
	painter.cc \
	pixelbuffer.cc \
	pluginconfig.cc \
	powerbutton.cc \
	progressbar.cc \
	resamplingframecontent.cc \
	resource.cc \
	resource_data.cc \
	sampleselectionframecontent.cc \
	scrollbar.cc \
	slider.cc \
	stackedwidget.cc \
	statusframecontent.cc \
	tabbutton.cc \
	tabwidget.cc \
	textedit.cc \
	texture.cc \
	texturedbox.cc \
	timingframecontent.cc \
	toggle.cc \
	tooltip.cc \
	utf8.cc \
	verticalline.cc \
	visualizerframecontent.cc \
	widget.cc \
	window.cc \
	lodepng/lodepng.cpp

if ENABLE_X11
nodist_libdggui_la_SOURCES += \
	nativewindow_x11.cc
endif

if ENABLE_WIN32
nodist_libdggui_la_SOURCES += \
	nativewindow_win32.cc
endif

if ENABLE_COCOA
nodist_libdggui_la_SOURCES += \
	nativewindow_cocoa.mm

libdggui_la_OBJCXXFLAGS = \
	-fblocks
endif

if ENABLE_PUGL_X11
nodist_libdggui_la_SOURCES += \
	nativewindow_pugl.cc \
	$(top_srcdir)/pugl/pugl/pugl_x11.c

libdggui_la_CPPFLAGS += \
	-I$(top_srcdir)/pugl

libdggui_la_CFLAGS += \
	-std=c99
endif

if ENABLE_PUGL_WIN32
nodist_libdggui_la_SOURCES += \
	nativewindow_pugl.cc \
	$(top_srcdir)/pugl/pugl/pugl_win.cpp

libdggui_la_CPPFLAGS += \
	-I$(top_srcdir)/pugl
endif

if ENABLE_PUGL_COCOA
nodist_libdggui_la_SOURCES += \
	nativewindow_pugl.cc \
	$(top_srcdir)/pugl/pugl/pugl_osx.m

libdggui_la_CPPFLAGS += \
	-I$(top_srcdir)/pugl
endif

plugingui_LDADD = libdggui.la $(top_srcdir)/src/libdg.la

plugingui_CXXFLAGS = \
	$(GUI_CPPFLAGS) \
	$(SNDFILE_CXXFLAGS) \
	$(PTHREAD_CFLAGS) \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin

plugingui_CFLAGS = $(plugingui_CXXFLAGS)

plugingui_SOURCES = \
	testmain.cc \
	$(top_srcdir)/hugin/hugin.c

rcgen_SOURCES = rcgen.cc

EXTRA_DIST = \
	$(nodist_libdggui_la_SOURCES) \
	$(RES) \
	abouttab.h \
	bleedcontrolframecontent.h \
	button.h \
	button_base.h \
	canvas.h \
	checkbox.h \
	colour.h \
	combobox.h \
	dialog.h \
	directory.h \
	diskstreamingframecontent.h \
	drawable.h \
	drumkitframecontent.h \
	drumkittab.h \
	eventhandler.h \
	filebrowser.h \
	font.h \
	frame.h \
	guievent.h \
	helpbutton.h \
	humaniservisualiser.h \
	humanizerframecontent.h \
	image.h \
	imagecache.h \
	knob.h \
	label.h \
	labeledcontrol.h \
	layout.h \
	led.h \
	lineedit.h \
	listbox.h \
	listboxbasic.h \
	listboxthin.h \
	maintab.h \
	mainwindow.h \
	nativewindow.h \
	nativewindow_cocoa.h \
	nativewindow_pugl.h \
	nativewindow_win32.h \
	nativewindow_x11.h \
	painter.h \
	pixelbuffer.h \
	pluginconfig.h \
	powerbutton.h \
	progressbar.h \
	resamplingframecontent.h \
	resource.h \
	resource_data.h \
	sampleselectionframecontent.h \
	scrollbar.h \
	slider.h \
	stackedwidget.h \
	statusframecontent.h \
	tabbutton.h \
	tabwidget.h \
	textedit.h \
	texture.h \
	texturedbox.h \
	timingframecontent.h \
	toggle.h \
	tooltip.h \
	utf8.h \
	verticalline.h \
	visualizerframecontent.h \
	widget.h \
	window.h
