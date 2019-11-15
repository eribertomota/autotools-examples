DISTDIRS = input output

if ENABLE_CLI

bin_PROGRAMS = drumgizmo dgvalidator

drumgizmo_LDADD = $(JACK_LIBS) $(top_srcdir)/src/libdg.la

drumgizmo_LDFLAGS =

drumgizmo_CXXFLAGS = \
	-I$(top_srcdir)/src -I$(top_srcdir)/getoptpp \
	-I$(top_srcdir)/hugin -DWITH_HUG_MUTEX -DWITH_HUG_FILTER \
	$(JACK_CFLAGS) $(SSEFLAGS)

drumgizmo_CFLAGS = -DWITH_HUG_MUTEX -DWITH_HUG_FILTER

drumgizmo_SOURCES = \
	drumgizmoc.cc \
	enginefactory.cc \
	$(top_srcdir)/hugin/hugin.c \
	$(top_srcdir)/hugin/hugin_filter.c

if HAVE_INPUT_DUMMY
drumgizmo_SOURCES += input/inputdummy.cc
drumgizmo_CXXFLAGS += -DHAVE_INPUT_DUMMY
endif # HAVE_INPUT_DUMMY

if HAVE_INPUT_TEST
drumgizmo_SOURCES += input/test.cc
drumgizmo_CXXFLAGS += -DHAVE_INPUT_TEST
endif # HAVE_INPUT_TEST

if HAVE_INPUT_MIDIFILE
drumgizmo_CXXFLAGS += $(SMF_CFLAGS)
drumgizmo_LDADD += $(SMF_LIBS)
drumgizmo_SOURCES += input/midifile.cc
drumgizmo_CXXFLAGS += -DHAVE_INPUT_MIDIFILE
endif # HAVE_INPUT_MIDIFILE

if HAVE_INPUT_JACKMIDI
drumgizmo_SOURCES += input/jackmidi.cc
drumgizmo_CXXFLAGS += -DHAVE_INPUT_JACKMIDI
endif # HAVE_INPUT_JACKMIDI

if HAVE_OUTPUT_DUMMY
drumgizmo_SOURCES += output/outputdummy.cc
drumgizmo_CXXFLAGS += -DHAVE_OUTPUT_DUMMY
endif # HAVE_OUTPUT_DUMMY

if HAVE_OUTPUT_WAVFILE
drumgizmo_SOURCES += output/wavfile.cc
drumgizmo_CXXFLAGS += -DHAVE_OUTPUT_WAVFILE
endif # HAVE_OUTPUT_WAVFILE

if HAVE_OUTPUT_ALSA
drumgizmo_CXXFLAGS += $(ALSA_CFLAGS)
drumgizmo_LDFLAGS += $(ALSA_LIBS)
drumgizmo_SOURCES += output/alsa.cc
drumgizmo_CXXFLAGS += -DHAVE_OUTPUT_ALSA
endif # HAVE_OUTPUT_ALSA

if HAVE_OUTPUT_JACKAUDIO
drumgizmo_CXXFLAGS += $(JACK_CFLAGS)
drumgizmo_LDFLAGS += $(JACK_LIBS)
drumgizmo_SOURCES += output/jackaudio.cc
drumgizmo_CXXFLAGS += -DHAVE_OUTPUT_JACKAUDIO
endif # HAVE_OUTPUT_JACKAUDIO

if HAVE_OUTPUT_OSS
drumgizmo_SOURCES += output/oss.cc
drumgizmo_CXXFLAGS += -DHAVE_OUTPUT_OSS
endif # HAVE_OUTPUT_OSS

if HAVE_INPUT_OSSMIDI
drumgizmo_SOURCES += input/ossmidi.cc
drumgizmo_CXXFLAGS += -DHAVE_INPUT_OSSMIDI
endif # HAVE_INPUT_OSSMIDI


# Only compile jackclient.cc if at least one of the jack modules are included.
if HAVE_OUTPUT_JACKAUDIO
drumgizmo_SOURCES += jackclient.cc
else
if HAVE_INPUT_JACKMIDI
drumgizmo_SOURCES += jackclient.cc
endif #  HAVE_INPUT_JACKMIDI
endif # HAVE_OUTPUT_JACKAUDIO

EXTRA_DIST = \
	jackclient.h \
	enginefactory.h \
	input/inputdummy.h \
	input/test.h \
	input/jackmidi.h \
	input/midifile.h \
	input/ossmidi.h \
	output/alsa.h \
	output/jackaudio.h \
	output/outputdummy.h \
	output/oss.h \
	output/wavfile.h

dgvalidator_LDADD = $(JACK_LIBS) $(top_srcdir)/src/libdg.la

dgvalidator_LDFLAGS =

dgvalidator_CXXFLAGS = \
	-I$(top_srcdir)/src -I$(top_srcdir)/getoptpp \
	-I$(top_srcdir)/hugin -DWITH_HUG_MUTEX -DWITH_HUG_FILTER \
	$(SSEFLAGS)

dgvalidator_CFLAGS = -DWITH_HUG_MUTEX -DWITH_HUG_FILTER

dgvalidator_SOURCES = \
	dgvalidator.cc \
	$(top_srcdir)/hugin/hugin.c \
	$(top_srcdir)/hugin/hugin_filter.c

endif # ENABLE_CLI
