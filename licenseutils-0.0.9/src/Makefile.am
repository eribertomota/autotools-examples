# Copyright (C) 2013, 2014, 2017 Ben Asselstine
# 
# Copying and distribution of this file, with or without modification,
# are permitted in any medium without royalty provided the copyright
# notice and this notice are preserved.  This file is offered as-is,
# without any warranty.
localedir = $(datadir)/locale
EXTRA_DIST=styles.am
bin_SCRIPTS=lu-sh notice
bin_PROGRAMS=licensing lu-comment-extractor
DEFS += -DLOCALEDIR=\"$(localedir)\" -DPROGRAM=\"$(PROGRAM)\" -DBINDIR=\"$(bindir)\" -DINTERPRETER=\"$(INTERPRETER)\" -DINTERPRETER_PATH=\"$(bindir)/$(INTERPRETER)\" @DEFS@
AM_CPPFLAGS = -I$(top_srcdir)/lib -I$(top_builddir)/lib

licensing_SOURCES=main.c opts.c opts.h  licensing.c gettext-more.h \
		  licensing_priv.h gpl.c lgpl.c agpl.c fdl.c boilerplate.c \
		  help.c warranty.c  welcome.c util.c util.h copyright.c \
		  cbb.c comment.c uncomment.c choose.c top.c project.c \
		  apply.c all-permissive.c fsf-permissive.c bsd.c apache.c \
		  mit.c extra.c png-boilerplate.c png-apply.c isc.c styles.c \
		  styles.h comment-style.h prepend.c new-boilerplate.c preview.c \
		  licensing.h gpl.h lgpl.h agpl.h fdl.h boilerplate.h help.h \
		  warranty.h welcome.h copyright.h cbb.h comment.h \
		  uncomment.h choose.h top.h project.h apply.h \
		  all-permissive.h fsf-permissive.h bsd.h apache.h \
		  mit.h extra.h \
		  png-boilerplate.h png-apply.h isc.h prepend.h \
		  new-boilerplate.h preview.h fsf-addresses.c fsf-addresses.h \
		  detect.c detect.h url-downloader.c url-downloader.h \
		  forget.c forget.h mozilla.c mozilla.h tutorial.c tutorial.h \
		  artistic.c artistic.h zlib.c zlib.h eclipse.c eclipse.h
include styles.am

licensing_LDADD= @LIBINTL@ $(top_builddir)/lib/libgnu.la $(GLIB_LIBS) $(LIBPNG_LIBS)

LIBTOOL_DEPS = @LIBTOOL_DEPS@
libtool: $(LIBTOOL_DEPS)
	$(SHELL) ./config.status --recheck

AM_CFLAGS=-Wall $(GLIB_CFLAGS) $(LIBPNG_CFLAGS)

lu_comment_extractor_SOURCES = comment-extractor.cpp
lu_comment_extractor_LDADD = \
    $(SRCHILITE_LIBS)
lu_comment_extractor_CPPFLAGS = $(SRCHILITE_CFLAGS)
lu_comment_extractor_CXXFLAGS = -DLICENSEUTILS_DATADIR='"$(LICENSEUTILS_DATADIR)"'
