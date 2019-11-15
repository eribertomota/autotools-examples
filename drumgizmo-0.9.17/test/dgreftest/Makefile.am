if ENABLE_CLI
if HAVE_INPUT_MIDIFILE

bin_PROGRAMS = dgreftest

dgreftest_LDADD = $(PTHREAD_LIBS) $(JACK_LIBS) \
	$(SMF_LIBS) $(top_srcdir)/src/libdg.la

dgreftest_LDFLAGS =

dgreftest_CXXFLAGS = $(SNDFILE_CXXFLAGS) $(PTHREAD_CFLAGS) \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/hugin -DWITH_HUG_MUTEX -DWITH_HUG_FILTER \
	$(JACK_CFLAGS) $(SSEFLAGS) $(SMF_CFLAGS) $(FLOAT_STORE)

dgreftest_CFLAGS = -DWITH_HUG_MUTEX -DWITH_HUG_FILTER

dgreftest_SOURCES = \
	dgreftest.cc \
	midiinputengine.cc \
	wavfileoutputengine.cc \
	compareoutputengine.cc \
	$(top_srcdir)/hugin/hugin.c \
	$(top_srcdir)/hugin/hugin_filter.c

endif # HAVE_INPUT_MIDIFILE

EXTRA_DIST = \
	midiinputengine.h \
	wavfileoutputengine.h \
	compareoutputengine.h

endif # ENABLE_CLI
