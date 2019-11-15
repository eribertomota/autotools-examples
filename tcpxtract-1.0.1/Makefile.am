AM_CFLAGS = -D_OFFSET_BITS=64 -D_LARGEFILE_SOURCE
bin_PROGRAMS = tcpxtract
tcpxtract_SOURCES = tcpxtract.c sessionlist.c sessionlist.h util.c util.h confy.y confl.l \
	conf.c conf.h confy.h search.h search.c extract.h extract.c
tcpxtract_LDADD = @LEXLIB@

sysconf_DATA = tcpxtract.conf

man_MANS = tcpxtract.1 

EXTRA_DIST = tcpxtract.conf tcpxtract.1

AM_YFLAGS = -d
