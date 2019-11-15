# A brief demonstration of using Automake with Libtool. -*-Makefile-*-
#
# NOTE: Don't forget that in the libtool distribution, files in this
# directory are distributed by the demo_distfiles variable in the top
# level Makefile.
AUTOMAKE_OPTIONS = foreign

EXTRA_DIST = 

#tclpath::
	#echo ${ENABLE_TCL}

#if ENABLE_TCL
#SEL_BIB = libstroke.la libstroke_tcl.la
#else
#SEL_BIB = libstroke.la
#endif
#
#SEL_FIB =
#if ENABLE_TCL
#libstroke_tcl_la_SOURCES = tcl.c stroke.c
#SEL_FIB = libstroke_tcl.la
#endif
#SEL_FIB = $(SEL_FIB) libstroke.la
#
#lib_LTLIBRARIES = $(SEL_FIB)

lib_LTLIBRARIES = libstroke.la
#libstroke_tcl_la_LDFLAGS = -ltcl -version-info 0:5:0
libstroke_la_SOURCES = stroke.c stroke.h

libstroke_la_LDFLAGS = -version-info 0:5:0

include_HEADERS = stroke.h

INCLUDES = -I$(top_srcdir)/libstroke @X_CFLAGS@  

EXTRA_DIST = 

MOSTLYCLEANFILES = core *~ 
CLEANFILES = core *~ 
DISTCLEANFILES = core *~ 
MAINTAINERCLEANFILES = core *~ 

# Unfortunately, in order to test libtool thoroughly, we need access
# to its private directory.
objdir = `sed -n -e 's/^objdir=\"\(.*\)\"$$/\1/p' ./libtool`

