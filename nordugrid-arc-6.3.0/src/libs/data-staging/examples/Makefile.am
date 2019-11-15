check_PROGRAMS = generator

generator_SOURCES = generator-main.cpp Generator.h Generator.cpp
generator_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
generator_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	../libarcdatastaging.la $(GLIBMM_LIBS)

exampledir = $(pkgdatadir)/examples/sdk
example_DATA = $(generator_SOURCES)

EXTRA_DIST = $(generator_SOURCES)

