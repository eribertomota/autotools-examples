## Process this file with automake to produce Makefile.in

## Created by Anjuta

AM_CPPFLAGS = \
	-DPACKAGE_LOCALE_DIR=\""$(prefix)/$(DATADIRNAME)/locale"\" \
	-DPACKAGE_SRC_DIR=\""$(srcdir)"\" \
	-DPACKAGE_DATA_DIR=\""$(datadir)"\" \
	$(SDL_CFLAGS)

AM_CFLAGS =\
	 -Wall\
	 -O2

bin_PROGRAMS = fische

fische_SOURCES = \
	main.cpp\
	sdlscreen.cpp \
	sdlscreen.h \
	vectorfield.h \
	vectorfield.cpp \
	ringbuffer.h \
	ringbuffer.cpp \
	blurengine.h \
	blurengine.cpp \
	traditional.c \
	traditional.h \
	alsa-samples.cpp \
	alsa-samples.h \
	wavepainter.h \
	wavepainter.cpp \
	analyst.h \
	analyst.cpp \
	configuration.h \
	configuration.cpp \
	samples.h \
	pulseaudio-samples.cpp \
	pulseaudio-samples.h \
	portaudio-samples.cpp \
	portaudio-samples.h \
	driver.h \
	dummyaudio-samples.cpp \
	dummyaudio-samples.h \
	busyindicator.h \
	busyindicator.cpp \	
	vector.h \
	blur.h

fische_LDFLAGS = 

fische_LDADD = \
	$(SDL_LIBS)

