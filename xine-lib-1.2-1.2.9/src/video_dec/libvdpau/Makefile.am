include $(top_srcdir)/misc/Makefile.common

AM_CFLAGS = $(DEFAULT_OCFLAGS) $(VISIBILITY_FLAG)
AM_LDFLAGS = $(xineplug_ldflags)

noinst_HEADERS = group_vdpau.h alterh264_decode.h alterh264_bits_reader.h bits_reader.h dpb.h cpb.h h264_parser.h nal.h
EXTRA_DIST = nal.c dpb.c cpb.c h264_parser.c

if ENABLE_VDPAU
vdpau_module = xineplug_decode_vdpau.la
VDPAU_CFLAGS += -D_ISOC99_SOURCE
endif

xineplug_LTLIBRARIES = $(vdpau_module)

xineplug_decode_vdpau_la_SOURCES = group_vdpau.c \
				   alterh264_decode.c \
				   vdpau_h264.c \
				   vdpau_mpeg12.c \
				   vdpau_vc1.c \
				   vdpau_mpeg4.c
xineplug_decode_vdpau_la_CFLAGS = $(AM_CFLAGS) $(VDPAU_CFLAGS)
xineplug_decode_vdpau_la_LIBADD = $(XINE_LIB) $(DYNAMIC_LD_LIBS) -lm
