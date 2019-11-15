# A brief demonstration of using Automake with Libtool. -*-Makefile-*-
#
# NOTE: Don't forget that in the libtool distribution, files in this
# directory are distributed by the demo_distfiles variable in the top
# level Makefile.
AUTOMAKE_OPTIONS = foreign

#SEL_BIB = libgstroke.la

lib_LTLIBRARIES = libgstroke.la
libgstroke_la_SOURCES = gnome-stroke.c gnome-stroke-draw.c gstroke.h

libgstroke_la_LDFLAGS = -version-info 0:5:0 -lgtk

include_HEADERS = gstroke.h

noinst_HEADERS = gstroke-internal.h

INCLUDES = @GTK_CFLAGS@
LDADD    = @GTK_LIBS@

EXTRA_DIST = 

MOSTLYCLEANFILES = core *~ 
CLEANFILES = core *~ 
DISTCLEANFILES = core *~ 
MAINTAINERCLEANFILES = core *~ 

# Unfortunately, in order to test libtool thoroughly, we need access
# to its private directory.
objdir = `sed -n -e 's/^objdir=\"\(.*\)\"$$/\1/p' ./libtool`

