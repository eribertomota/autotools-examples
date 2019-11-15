if BUILD_SL

lib_LTLIBRARIES = libplibsl.la libplibsm.la

include_HEADERS = sl.h slPortability.h sm.h

libplibsl_la_SOURCES = \
	slDSP.cxx slSample.cxx slEnvelope.cxx \
	slPlayer.cxx slMODPlayer.cxx slSamplePlayer.cxx \
        slScheduler.cxx slMODdacio.cxx slMODfile.cxx \
        slMODinst.cxx slMODnote.cxx slMODPrivate.h slMODfile.h
libplibsl_la_LIBADD = ../util/libplibul.la
libplibsl_la_LDFLAGS = -version-info 9:5:8

libplibsm_la_SOURCES = slPortability.h smMixer.cxx
libplibsm_la_LDFLAGS = -version-info 9:5:8

INCLUDES = -I$(top_srcdir)/src/util

endif

EXTRA_DIST = sl.dsp

