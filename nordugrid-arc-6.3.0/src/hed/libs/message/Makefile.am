DIST_SUBDIRS = test
SUBDIRS = $(TEST_DIR)

lib_LTLIBRARIES = libarcmessage.la

libarcmessage_ladir = $(pkgincludedir)/message
libarcmessage_la_HEADERS = SOAPEnvelope.h   PayloadRaw.h   PayloadSOAP.h   \
	PayloadStream.h   MCC_Status.h   MCC.h   Service.h   Plexer.h   \
	MessageAttributes.h   Message.h   SOAPMessage.h   MessageAuth.h   \
	SecAttr.h   MCCLoader.h   SecHandler.h
libarcmessage_la_SOURCES = SOAPEnvelope.cpp PayloadRaw.cpp PayloadSOAP.cpp \
	PayloadStream.cpp MCC_Status.cpp MCC.cpp Service.cpp Plexer.cpp \
	MessageAttributes.cpp Message.cpp SOAPMessage.cpp MessageAuth.cpp \
	SecAttr.cpp MCCLoader.cpp SecHandler.cpp
libarcmessage_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcmessage_la_LIBADD = \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS)
libarcmessage_la_LDFLAGS  = -version-info 3:0:0
