SUBDIRS = .

lib_LTLIBRARIES = libcpu_ldap.la

LDADD = $(top_builddir)/src/util/libcputil.la
libcpu_ldap_la_LDFLAGS = @LDFLAGS@

libcpu_ldap_la_SOURCES = \
 ldap_errors.c \
 commandline.c \
 cat.c \
 user.c \
 group.c \
 ld.c \
 ldap.c
