target_test = test

check_PROGRAMS = $(target_test)

AM_CXXFLAGS = \
 -I$(top_srcdir)/inc \
 -I$(top_srcdir)/src \
 -I$(top_srcdir)/qa/helper \
 $(BOOST_CFLAGS) \
 $(EPOXY_CFLAGS) \
 $(GLM_CFLAGS) \
 $(DEBUG_CXXFLAGS) \
 $(LIBGLTF_CXXFLAGS) \
 $(X11_CFLAGS) \
 $(GL_CFLAGS) \
 $(LIBPNG_CFLAGS)

test_LDFLAGS = -L../../src/.libs
test_LDADD = \
 ../../src/.libs/libgltf-@GLTF_MAJOR_VERSION@.@GLTF_MINOR_VERSION@.la \
 $(EPOXY_LIBS) \
 $(CPPUNIT_LIBS) \
 $(X11_LIBS) \
 $(GL_LIBS) \
 $(LIBPNG_LIBS)

test_SOURCES = \
 APITest.cpp \
 APITest.h \
 ../helper/OpenGLContext.cpp \
 ../helper/OpenGLContext.h \
 ../helper/PNGHelper.cpp \
 ../helper/PNGHelper.h \
 UnitTester.cpp

TESTS = $(target_test)

