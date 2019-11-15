SUBDIRS = schema

if ARGUS_ENABLED
pkglib_LTLIBRARIES = libidentitymap.la libarguspdpclient.la libarguspepclient.la
else
pkglib_LTLIBRARIES = libidentitymap.la libarguspdpclient.la
endif

libidentitymap_la_SOURCES = IdentityMap.cpp SimpleMap.cpp \
                            IdentityMap.h   SimpleMap.h
libidentitymap_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libidentitymap_la_LIBADD = \
	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS) 
libidentitymap_la_LDFLAGS = -no-undefined -avoid-version -module

if ARGUS_ENABLED
libarguspepclient_la_SOURCES = ArgusPEPClient.cpp ArgusPEPClient.h
libarguspepclient_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(ARGUS_CFLAGS) $(AM_CXXFLAGS)
libarguspepclient_la_LIBADD = \
	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS) $(ARGUS_LIBS)
libarguspepclient_la_LDFLAGS = -no-undefined -avoid-version -module
endif

libarguspdpclient_la_SOURCES = ArgusPDPClient.cpp ArgusPDPClient.h ArgusXACMLConstant.h
libarguspdpclient_la_CXXFLAGS = -I$(top_srcdir)/include \
        $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarguspdpclient_la_LIBADD = \
        $(top_builddir)/src/hed/libs/security/libarcsecurity.la \
        $(top_builddir)/src/hed/libs/message/libarcmessage.la \
        $(top_builddir)/src/hed/libs/loader/libarcloader.la \
        $(top_builddir)/src/hed/libs/common/libarccommon.la \
        $(top_builddir)/src/hed/libs/credential/libarccredential.la \
        $(top_builddir)/src/hed/libs/communication/libarccommunication.la \
        $(GLIBMM_LIBS) $(LIBXML2_LIBS)
libarguspdpclient_la_LDFLAGS = -no-undefined -avoid-version -module

