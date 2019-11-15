noinst_LTLIBRARIES = libauth.la libaccess.la libmap.la

libauth_la_SOURCES = auth.h auth.cpp auth_subject.cpp auth_file.cpp \
	auth_voms.cpp auth_plugin.cpp
libauth_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(GLOBUS_IO_CFLAGS) \
	$(LCMAPS_CFLAGS) $(AM_CXXFLAGS)
libauth_la_LIBADD = ../misc/libmisc.la ../run/librun.la ../conf/libconf.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la

libaccess_la_SOURCES = identity.cpp identity.h \
	identity_dn.cpp identity_dn.h identity_voms.cpp identity_voms.h \
	permission.cpp permission.h  \
	object_access.cpp object_access.h
libaccess_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(GLOBUS_IO_CFLAGS) \
	$(LCMAPS_CFLAGS) $(AM_CXXFLAGS)
libaccess_la_LIBADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(XML_LIBS)

libmap_la_SOURCES = unixmap.h unixmap.cpp unixmap_lcmaps.cpp \
	simplemap.h simplemap.cpp
libmap_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(GLOBUS_IO_CFLAGS) \
	$(LCMAPS_CFLAGS) $(AM_CXXFLAGS)
libmap_la_LIBADD = libauth.la $(top_builddir)/src/hed/libs/common/libarccommon.la
