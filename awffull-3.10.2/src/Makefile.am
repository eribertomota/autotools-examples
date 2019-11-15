## Makefile.am -- Process this file with automake to produce Makefile.in
###MAINTAINERCLEANFILES = Makefile.in

localedir = $(datadir)/locale

DEFS			= -DETCDIR=\"@ETCDIR@\" @DEFS@
AM_CPPFLAGS		= -DLOCALEDIR=\"$(localedir)\"
noinst_HEADERS          = graphs.h hashtab.h messages.h linklist.h output.h parser.h preserve.h awffull.h common.h gettext.h xmalloc.h segment.h
bin_PROGRAMS            = awffull
awffull_SOURCES    	= graphs.c hashtab.c linklist.c output.c parser.c preserve.c awffull.c options.c css_file.c messages.c xmalloc.c strlcpy.c segment.c

LDADD			= $(LIBINTL)

