## Process this file with automake to produce Makefile.in

if HAVE_LIBGTK
GSTROKETEST = gnome_stroke_test
else
GSTROKETEST = 
endif


noinst_PROGRAMS = stroke_test $(GSTROKETEST)  #gstroke_conf

# don't forget all *.h files */
stroke_test_SOURCES = stroke_test.c  #gstroke_conf.c
gnome_stroke_test_SOURCES = gnome_stroke_test.c

INCLUDES = -I$(top_srcdir)/libstroke -I$(top_srcdir)/libgstroke \
		@X_CFLAGS@ @GTK_CFLAGS@

stroke_test_LDADD = ../libstroke/libstroke.la @X_LDFLAGS@
gnome_stroke_test_LDADD = ../libgstroke/libgstroke.la @GTK_LIBS@
#gstroke_conf_LDADD = ../libstroke/libgstroke.la @X_LDFLAGS@

EXTRA_DIST = stroke_test.tcl 

MOSTLYCLEANFILES = core *~ 
CLEANFILES = core *~ 
DISTCLEANFILES = core *~ 
MAINTAINERCLEANFILES = core *~ 

