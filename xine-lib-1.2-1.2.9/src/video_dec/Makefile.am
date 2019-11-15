SUBDIRS = \
	libmpeg2 \
	libmpeg2new \
	libvdpau

include $(top_builddir)/misc/Makefile.plugins
include $(top_srcdir)/misc/Makefile.common

AM_CFLAGS  = $(DEFAULT_OCFLAGS) $(VISIBILITY_FLAG)
AM_LDFLAGS = $(xineplug_ldflags)

EXTRA_DIST = foovideo.c
noinst_HEADERS = group_raw.h

if ENABLE_IMAGEMAGICK
image_module = xineplug_decode_image.la
endif

if ENABLE_GDK_PIXBUF
gdkpixbuf_module = xineplug_decode_gdk_pixbuf.la
endif

if ENABLE_LIBJPEG
libjpeg_module = xineplug_decode_libjpeg.la
endif

if ENABLE_OPENHEVC
libopenhevc_module = xineplug_decode_libopenhevc.la
endif

if ENABLE_VPX
libvpx_module = xineplug_decode_libvpx.la
endif

if ENABLE_MMAL
libmmal_module = xineplug_decode_libmmal.la
endif

xineplug_LTLIBRARIES = $(image_module) \
	$(gdkpixbuf_module) \
	$(libjpeg_module) \
	$(theora_module) \
	$(libopenhevc_module) \
	$(libvpx_module) \
	$(libmmal_module) \
	xineplug_decode_rawvideo.la

xineplug_decode_rawvideo_la_SOURCES = group_raw.c bitplane.c rgb.c yuv.c
xineplug_decode_rawvideo_la_LIBADD = $(XINE_LIB) $(LTLIBINTL)

xineplug_decode_image_la_SOURCES = image.c
xineplug_decode_image_la_LIBADD = $(XINE_LIB) $(DYNAMIC_LD_LIBS) $(WAND_LIBS)
xineplug_decode_image_la_CFLAGS = $(AM_CFLAGS) $(WAND_CFLAGS)

xineplug_decode_gdk_pixbuf_la_SOURCES = gdkpixbuf.c
xineplug_decode_gdk_pixbuf_la_LIBADD = $(XINE_LIB) $(DYNAMIC_LD_LIBS) $(GDK_PIXBUF_LIBS)
xineplug_decode_gdk_pixbuf_la_CFLAGS = $(AM_CFLAGS) $(GDK_PIXBUF_CFLAGS)

xineplug_decode_libjpeg_la_SOURCES = libjpeg.c
xineplug_decode_libjpeg_la_LIBADD = $(XINE_LIB) $(JPEG_LIBS) $(LTLIBINTL)
xineplug_decode_libjpeg_la_CFLAGS = $(AM_CFLAGS) $(JPEG_CFLAGS)

xineplug_decode_libopenhevc_la_SOURCES = libopenhevc.c
xineplug_decode_libopenhevc_la_LIBADD = $(XINE_LIB) $(OPENHEVC_LIBS) -lm
xineplug_decode_libopenhevc_la_CFLAGS = $(AM_CFLAGS) $(OPENHEVC_CFLAGS)
xineplug_decode_libopenhevc_la_LDFLAGS = $(AM_LDFLAGS) -Wl,-Bsymbolic

xineplug_decode_libvpx_la_SOURCES = libvpx.c
xineplug_decode_libvpx_la_LIBADD = $(XINE_LIB) $(VPX_LIBS)
xineplug_decode_libvpx_la_CFLAGS = $(AM_CFLAGS) $(VPX_CFLAGS)

xineplug_decode_libmmal_la_SOURCES = mmal.c
xineplug_decode_libmmal_la_LIBADD = $(XINE_LIB) $(PTHREAD_LIBS) $(MMAL_LIBS)
xineplug_decode_libmmal_la_CFLAGS = $(AM_CFLAGS) $(MMAL_CFLAGS)
xineplug_decode_libmmal_la_LDFLAGS = $(AM_LDFLAGS) $(MMAL_LDFLAGS)


