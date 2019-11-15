lib_LTLIBRARIES = libarccredentialstore.la
#noinst_PROGRAMS = test

libarccredentialstore_ladir = $(pkgincludedir)/credentialstore
libarccredentialstore_la_HEADERS = CredentialStore.h ClientVOMS.h ClientVOMSRESTful.h
libarccredentialstore_la_SOURCES = CredentialStore.cpp ClientVOMS.cpp ClientVOMSRESTful.cpp
libarccredentialstore_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS)
libarccredentialstore_la_LIBADD = \
	$(top_builddir)/src/hed/libs/communication/libarccommunication.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS)
libarccredentialstore_la_LDFLAGS  = -version-info 3:0:0

#test_SOURCES = test.cpp
#test_CXXFLAGS = -I$(top_srcdir)/include \
#	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
#test_LDADD = \
#	libarccredentialstore.la \
#	$(top_builddir)/src/hed/libs/common/libarccommon.la \
#	$(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS)
