check_PROGRAMS = partial_copy simple_copy

partial_copy_SOURCES = partial_copy.cpp
partial_copy_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
partial_copy_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	../libarcdata.la $(GLIBMM_LIBS)

simple_copy_SOURCES = simple_copy.cpp
simple_copy_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
simple_copy_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	../libarcdata.la $(GLIBMM_LIBS)


check_LTLIBRARIES = libdmcmy.la

libdmcmy_la_SOURCES = DataPointMyProtocol.cpp
libdmcmy_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
libdmcmy_la_LIBADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	../libarcdata.la	$(LIBXML2_LIBS) $(GLIBMM_LIBS)
libdmcmy_la_LDFLAGS = -no-undefined -avoid-version -module


exampledir = $(pkgdatadir)/examples/sdk
example_DATA = partial_copy.cpp simple_copy.cpp DataPointMyProtocol.cpp
