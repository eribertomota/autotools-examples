pkglib_LTLIBRARIES = libcandypond.la

libcandypond_la_SOURCES = CandyPond.h CandyPond.cpp \
                             CandyPondGenerator.h CandyPondGenerator.cpp
libcandypond_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
libcandypond_la_LIBADD = \
	../a-rex/grid-manager/libgridmanager.la \
	../a-rex/delegation/libdelegation.la \
	$(top_builddir)/src/hed/libs/infosys/libarcinfosys.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS)
libcandypond_la_LDFLAGS = -no-undefined -avoid-version -module
