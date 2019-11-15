noinst_LTLIBRARIES = libarcattr.la
libarcattr_ladir = $(pkgincludedir)/security/ArcPDP/attr
libarcattr_la_HEADERS = AttributeValue.h StringAttribute.h DateTimeAttribute.h X500NameAttribute.h AnyURIAttribute.h BooleanAttribute.h \
                        GenericAttribute.h AttributeProxy.h AttributeFactory.h RequestAttribute.h
libarcattr_la_SOURCES = RequestAttribute.cpp StringAttribute.cpp DateTimeAttribute.cpp X500NameAttribute.cpp AnyURIAttribute.cpp BooleanAttribute.cpp GenericAttribute.cpp
libarcattr_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcattr_la_LIBADD = $(top_builddir)/src/hed/libs/common/libarccommon.la
