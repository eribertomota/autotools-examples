bin_PROGRAMS = ffe

AM_CPPFLAGS = $(LIBGCRYPT_CFLAGS)
LDADD = $(LIBGCRYPT_LIBS)

AM_CFLAGS = -I..

ffe_SOURCES = ffe.c xmalloc.c parserc.c execute.c endian.c level.c anonymize.c
noinst_HEADERS = ffe.h
