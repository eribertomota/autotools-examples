SUBDIRS = schema
pkglib_LTLIBRARIES = libmcctls.la

libmcctls_la_SOURCES = PayloadTLSStream.cpp MCCTLS.cpp \
                       ConfigTLSMCC.cpp PayloadTLSMCC.cpp \
                       GlobusSigningPolicy.cpp DelegationSecAttr.cpp \
                       DelegationCollector.cpp \
                       BIOMCC.cpp BIOGSIMCC.cpp \
                       PayloadTLSStream.h   MCCTLS.h   \
                       ConfigTLSMCC.h   PayloadTLSMCC.h   \
                       GlobusSigningPolicy.h   DelegationSecAttr.h   \
                       DelegationCollector.h \
                       BIOMCC.h   BIOGSIMCC.h
libmcctls_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
libmcctls_la_LIBADD = \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/crypto/libarccrypto.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) 
libmcctls_la_LDFLAGS = -no-undefined -avoid-version -module
