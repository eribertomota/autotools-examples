SUBDIRS = .

sbin_PROGRAMS = cpu

cpu_LDADD = \
 $(top_builddir)/src/util/libcputil.la

cpu_SOURCES = \
 cpu.c

CONFIGDIR = @sysconfdir@
CONFIGFILE = $(CONFIGDIR)/cpu.conf
AM_CFLAGS = -DCONFIGFILE=\"$(CONFIGFILE)\"
