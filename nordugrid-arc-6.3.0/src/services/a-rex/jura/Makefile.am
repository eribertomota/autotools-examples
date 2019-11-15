pkglibexec_PROGRAMS = jura

if PYTHON_ENABLED
APEL_CLIENT = ssm
else
APEL_CLIENT =
endif

SUBDIRS = $(APEL_CLIENT)

DIST_SUBDIRS = ssm

jura_SOURCES = jura.cpp jura.h UsageReporter.cpp UsageReporter.h \
	Reporter.h ReReporter.cpp ReReporter.h \
	JobLogFile.cpp JobLogFile.h Destinations.cpp Destinations.h \
	Destination.cpp Destination.h LutsDestination.cpp LutsDestination.h \
        ApelDestination.cpp ApelDestination.h CARDestination.cpp CARDestination.h \
        CARAggregation.cpp CARAggregation.h Config.cpp Config.h

jura_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
jura_LDADD = \
	$(top_builddir)/src/hed/libs/communication/libarccommunication.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS)

man_MANS = jura.1
