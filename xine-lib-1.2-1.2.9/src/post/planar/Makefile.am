include $(top_builddir)/misc/Makefile.plugins
include $(top_srcdir)/misc/Makefile.common

AM_CFLAGS   = $(VISIBILITY_FLAG)
AM_CPPFLAGS +=
AM_LDFLAGS  =

if ENABLE_POSTPROC
pp_module_sources = pp.c
pp_module_libs = $(POSTPROC_LIBS)
pp_module_deps = $(POSTPROC_DEPS)
pp_module_cflags = $(FFMPEG_CFLAGS) $(POSTPROC_CFLAGS)
endif

noinst_LTLIBRARIES = libpost_planar_asm.la
libpost_planar_asm_la_SOURCES = noise.c
libpost_planar_asm_la_CFLAGS  = $(O1_CFLAGS) -fomit-frame-pointer $(AM_CFLAGS)
libpost_planar_asm_la_LIBADD  = 

xinepost_LTLIBRARIES = xineplug_post_planar.la
xineplug_post_planar_la_SOURCES = planar.c invert.c expand.c fill.c boxblur.c \
                                  eq.c eq2.c \
                                  denoise3d.c unsharp.c $(pp_module_sources)
xineplug_post_planar_la_LIBADD  = $(XINE_LIB) $(pp_module_libs) -lm $(PTHREAD_LIBS) $(LTLIBINTL) $(noinst_LTLIBRARIES)
xineplug_post_planar_la_DEPS = $(pp_module_deps)
xineplug_post_planar_la_CFLAGS  = $(DEFAULT_OCFLAGS) $(AM_CFLAGS) $(pp_module_cflags)
xineplug_post_planar_la_LDFLAGS = $(AM_LDFLAGS) $(xineplug_ldflags) $(IMPURE_TEXT_LDFLAGS)
