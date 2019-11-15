pkglib_LTLIBRARIES = libmodcredential.la

libmodcredential_la_SOURCES = cred.cpp
libmodcredential_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libmodcredential_la_LIBADD = \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la
libmodcredential_la_LDFLAGS = -no-undefined -avoid-version -module
