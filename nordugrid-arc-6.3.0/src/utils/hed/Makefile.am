bin_PROGRAMS = wsdl2hed arcplugin

man_MANS = wsdl2hed.1 arcplugin.1

wsdl2hed_SOURCES = wsdl2hed.cpp schemaconv.cpp schemaconv.h \
	common.cpp simpletype.cpp complextype.cpp
wsdl2hed_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
wsdl2hed_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS)

arcplugin_SOURCES = arcplugin.cpp
arcplugin_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
arcplugin_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS)
