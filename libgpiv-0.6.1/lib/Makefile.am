ENABLE_CAM	= @ENABLE_CAM@
ENABLE_TRIG	= @ENABLE_TRIG@
RTA_TOPDIR	= @RTA_TOPDIR@
ENABLE_MPI	= @ENABLE_MPI@
AUTOMAKE_OPTIONS 	= gnu
SOURCES			= genpar.c					\
			cam.c cam_par.c 				\
			trig.c trig_par.c 				\
			img.c img_utils.c				\
			imgproc.c imgproc_deform.c imgproc_par.c	\
			io.c io_png.c io_raw.c io_hdf.c io_dav.c 	\
			utils.c utils_alloc.c				\
			piv.c piv_par.c piv_utils.c 			\
			valid.c valid_par.c				\
			post.c post_par.c post_utils.c			\
			my_utils.c my_utils.h

if BUILD_MPI

lib_LTLIBRARIES 	= libgpiv_mpi.la
libgpiv_mpi_la_SOURCES	= $(SOURCES)
INCLUDES 		= -I$(top_srcdir)/include \
@GLIB_CFLAGS@ \
-I@RTA_TOPDIR@/include
LDADD           	= @GLIB_LIBS@
libgpiv_mpi_la_LDFLAGS 	= \
        -version-info $(LT_CURRENT):$(LT_REVISION):$(LT_AGE)

else

lib_LTLIBRARIES 	= libgpiv.la
libgpiv_la_SOURCES	= $(SOURCES)
INCLUDES                = -I$(top_srcdir)/include \
@GLIB_CFLAGS@ \
-I@RTA_TOPDIR@/include
LDADD                   = @GLIB_LIBS@
libgpiv_la_LDFLAGS      = \
        -version-info $(LT_CURRENT):$(LT_REVISION):$(LT_AGE)

endif

AM_CFLAGS		= @ENABLE_CAM@ @ENABLE_TRIG@ @ENABLE_MPI@

EXTRA_DIST                = 	Makefile.in
MAINTAINERCLEANFILES      = 	Makefile.in
