#
# Copyright (c) 2001, 2002, 2003 Thorsten Kukuk <kukuk@suse.de>
#
AUTOMAKE_OPTIONS = 1.7 gnits
MAINT_CHARSET = latin1
#
INSTALL_PROGRAM = @INSTALL_PROGRAM@ -s -m 555

localedir = $(datadir)/locale

INCLUDES = -I$(top_srcdir)/lib -I$(top_srcdir) -I$(top_builddir) -I$(srcdir)

DEFS = @DEFS@ -DLOCALEDIR=\"$(localedir)\" -DYPBINDIR=\"$(libexecdir)\" \
	-DCONFDIR=\"$(sysconfdir)\" -DYPMAPDIR=\"/var/yp\" \
	-DUSE_FQDN=@USE_FQDN@

CLEANFILES = *~

EXTRA_DIST = ${MANS}

man_MANS = yphelper.8

libexec_PROGRAMS = yphelper

yphelper_SOURCES = yphelper.c

yphelper_LDADD = $(top_builddir)/lib/libyp.a @LIBDBM@
