include $(top_srcdir)/misc/Makefile.common

AM_CFLAGS   = $(DEFAULT_OCFLAGS) $(X_CFLAGS) $(VISIBILITY_FLAG)
AM_CPPFLAGS += -DXINE_LIBRARY_COMPILE

EXTRA_DIST = ppcasm_string.S ppc_asm.tmpl

noinst_HEADERS = ppcasm_string.h mangle.h xine_mmx.h yuv2rgb.h yuv2rgb_private.h

noinst_LTLIBRARIES = libxineutils.la

if ARCH_PPC
if !HOST_OS_DARWIN
pppc_files = ppcasm_string.S
endif
endif

noinst_LTLIBRARIES += libyuv2rgb.la
libyuv2rgb_la_SOURCES = yuv2rgb.c yuv2rgb_mmx.c yuv2rgb_mlib.c
libyuv2rgb_la_CFLAGS = $(AM_CFLAGS) $(MLIB_CFLAGS)
libyuv2rgb_la_LIBADD = $(MLIB_LIBS)
YUV_LIB = libyuv2rgb.la

libxineutils_la_SOURCES = $(pppc_files) \
	cpu_accel.c \
	color.c \
	copy.c \
	list.c \
	memcpy.c \
	monitor.c \
	utils.c \
	xine_check.c \
	xine_mutex.c \
	xmllexer.c \
	xine_buffer.c \
	xmlparser.c \
	array.c \
	sorted_array.c \
	pool.c \
	ring_buffer.c

libxineutils_la_LIBADD = $(YUV_LIB)

if !WIN32
noinst_PROGRAMS = xmltest
xmltest_SOURCES = xmllexer.c xmlparser.c
xmltest_CFLAGS = -DLOG -DXINE_XML_PARSER_TEST $(AM_CFLAGS)
endif
