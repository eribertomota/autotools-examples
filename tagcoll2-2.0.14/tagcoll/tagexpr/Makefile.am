## Process this file with automake to produce Makefile.in

tagexprincludedir = $(includedir)/tagcoll-$(VERSION)/tagcoll/tagexpr

tagexprinclude_HEADERS = \
		TagexprParser.h

noinst_LTLIBRARIES = libtagexpr.la
libtagexpr_la_SOURCES = \
		TagexprParser.cc \
		Tagexpr_parser_y.yy Tagexpr_parser_l.ll

if NO_FMEMOPEN
libtagexpr_la_SOURCES += \
		fmemopen.c \
		fmemopen.h
endif

AM_CPPFLAGS = -I$(top_srcdir) $(LIBWIBBLE_DEFS)

AM_YFLAGS = -d
