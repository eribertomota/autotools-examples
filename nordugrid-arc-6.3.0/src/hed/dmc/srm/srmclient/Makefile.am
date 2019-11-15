noinst_LTLIBRARIES = libsrmclient.la 

libsrmclient_la_SOURCES = SRMClient.cpp   SRMClient.h   \
                          SRM1Client.cpp  SRM1Client.h  \
                          SRM22Client.cpp SRM22Client.h \
                          SRMURL.cpp      SRMURL.h      \
                          SRMInfo.cpp     SRMInfo.h     \
                          SRMClientRequest.h
libsrmclient_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
