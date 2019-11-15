SUBDIRS = .

lib_LTLIBRARIES = libcpu_passwd.la

LDADD = $(top_builddir)/src/util/libcputil.la
libcpu_passwd_la_LDFLAGS = @LBFLAGS@

libcpu_passwd_la_SOURCES = \
 commandline.c \
 data.c \
 getid.c \
 passwd.c
