version_info = -version-info $(LT_CURRENT):$(LT_REVISION):$(LT_AGE)


lib_LTLIBRARIES = libgltf-@GLTF_MAJOR_VERSION@.@GLTF_MINOR_VERSION@.la
libgltf_@GLTF_MAJOR_VERSION@_@GLTF_MINOR_VERSION@_includedir = $(includedir)/libgltf-@GLTF_MAJOR_VERSION@.@GLTF_MINOR_VERSION@
libgltf_@GLTF_MAJOR_VERSION@_@GLTF_MINOR_VERSION@_include_HEADERS = \
 $(top_srcdir)/inc/libgltf.h \
 $(top_srcdir)/inc/types.h

AM_CXXFLAGS = -I$(top_srcdir)/inc $(BOOST_CFLAGS) $(EPOXY_CFLAGS) $(GLM_CFLAGS) $(DEBUG_CXXFLAGS) $(LIBGLTF_CXXFLAGS)

libgltf_@GLTF_MAJOR_VERSION@_@GLTF_MINOR_VERSION@_la_LIBADD = $(BOOST_LIBS) $(EPOXY_LIBS) $(GLM_LIBS)
libgltf_@GLTF_MAJOR_VERSION@_@GLTF_MINOR_VERSION@_la_LDFLAGS = $(version_info) -export-dynamic -no-undefined
libgltf_@GLTF_MAJOR_VERSION@_@GLTF_MINOR_VERSION@_la_SOURCES = \
 Camera.cpp \
 Camera.h \
 Common.cpp \
 Common.h \
 Font.cpp \
 Font.h \
 FPSCounter.cpp \
 FPSCounter.h \
 libgltf.cpp \
 LoadScene.cpp \
 LoadScene.h \
 NumberBitmap.h \
 NumberBitmap.cpp \
 RenderScene.cpp \
 RenderScene.h \
 Shaders.cpp \
 Shaders.h \
 Texture.cpp \
 Texture.h \
 TimeFunction.cpp \
 TimeFunction.h \
 types.cpp

distclean-local :
	@echo
