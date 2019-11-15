# don't build libgstroke if GTK is not available
if HAVE_LIBGTK
GSTROKE_SUBDS = libgstroke
else
GSTROKE_SUBDS = 
endif

SUBDIRS = libstroke $(GSTROKE_SUBDS) tests doc javastroke 

EXTRA_DIST = COPYRIGHT CREDITS README.javastroke README.libgstroke

m4datadir=$(datadir)/aclocal
m4data_DATA=libstroke.m4 libgstroke.m4

MOSTLYCLEANFILES = core *~
CLEANFILES = core *~
DISTCLEANFILES = core *~
MAINTAINERCLEANFILES = core *~

