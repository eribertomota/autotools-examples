AM_CFLAGS = @LIBGAVL_CFLAGS@

if HAVE_MMX
mmx_libs = mmx/libgavl_mmx.la mmxext/libgavl_mmxext.la
mmx_subdirs = mmx mmxext
else
mmx_libs = 
mmx_subdirs =
endif

if HAVE_SSE
sse_libs = sse/libgavl_sse.la
sse_subdirs = sse
else
sse_libs = 
sse_subdirs =
endif

if HAVE_SSE2
sse2_libs = sse2/libgavl_sse2.la
sse2_subdirs = sse2
else
sse2_libs = 
sse2_subdirs =
endif

if HAVE_SSE3
sse3_libs = sse3/libgavl_sse3.la
sse3_subdirs = sse3
else
sse3_libs = 
sse3_subdirs =
endif

if HAVE_3DNOW
threednow_libs = 3dnow/libgavl_3dnow.la
threednow_subdirs = 3dnow
else
threednow_libs = 
threednow_subdirs =
endif


SUBDIRS = hq c libgdither libsamplerate $(mmx_subdirs) \
$(sse_subdirs) \
$(sse2_subdirs) \
$(sse3_subdirs) \
$(threednow_subdirs)

lib_LTLIBRARIES= libgavl.la
#noinst_LTLIBRARIES = libgavl.la

libgavl_la_SOURCES = \
absdiff.c \
arith128.c \
audioconverter.c \
audioformat.c \
audioframe.c \
audiooptions.c \
blend.c \
colorchannel.c \
colorspace.c \
compression.c \
cputest.c \
deinterlace.c \
deinterlace_blend.c \
deinterlace_copy.c \
deinterlace_scale.c \
dsp.c \
dsputils.c \
frametable.c \
interleave.c \
memcpy.c \
metadata.c \
mix.c \
peakdetector.c \
psnr.c \
rectangle.c \
sampleformat.c \
samplerate.c \
scale.c \
scale_context.c \
scale_kernels.c \
scale_table.c \
ssim.c \
time.c \
timecode.c \
timer.c \
transform.c \
transform_context.c \
transform_table.c \
video.c \
videoformat.c \
videoframe.c \
videooptions.c \
volume.c

noinst_HEADERS = \
csp_packed_packed.h  \
csp_packed_planar.h  \
csp_planar_packed.h  \
csp_planar_planar.h \
ssim_tab.h

AM_LDFLAGS = -export-symbols-regex gavl -version-info \
@LTVERSION_CURRENT@:@LTVERSION_REVISION@:@LTVERSION_AGE@ \
@LIBGAVL_LDFLAGS@

libgavl_la_LIBADD = \
@GMERLIN_DEP_LIBS@ \
$(mmx_libs) \
$(sse_libs) \
$(sse2_libs) \
$(sse3_libs) \
$(threednow_libs) \
c/libgavl_c.la \
hq/libgavl_hq.la \
libgdither/libgdither.la \
libsamplerate/libsamplerate.la \
@LIBGAVL_LIBS@ \
-lm

EXTRA_DIST=Makefile.am.in
