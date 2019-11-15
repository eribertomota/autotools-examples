## Process this file with automake to produce Makefile.in

# The package version
VERSION = @VERSION@

# The library interface
INTERFACE = 2

slibdir = @slibdir@
localedir = $(datadir)/locale

noinst_HEADERS = db-compat.h netgroup.h nss_db.h

INCLUDES = @DB_CFLAGS@ -D_GNU_SOURCE \
	-I../intl -DLOCALEDIR=\"$(localedir)\"

EXTRA_DIST = libnss_db.map

slib_LTLIBRARIES = libnss_db.la
libnss_db_la_SOURCES = db-alias.c db-ethers.c db-netgrp.c db-grp.c db-proto.c \
	db-pwd.c db-rpc.c db-service.c db-spwd.c db-compat.c db-open.c
EXTRA_libnss_db_la_SOURCES = libnss_db.map db-XXX.c \
	files-ethers.c files-grp.c files-parse.c files-proto.c files-pwd.c \
	files-rpc.c files-service.c files-spwd.c
libnss_db_la_LDFLAGS = -version-info $(INTERFACE) \
	 -Wl,--version-script=$(srcdir)/libnss_db.map
libnss_db_la_DEPENDENCIES = libnss_db.map
libnss_db_la_LIBADD = @DB_LIBS@ -lnss_files

bin_PROGRAMS = makedb
makedb_SOURCES = makedb.c db-compat.c
makedb_LDADD = @DB_LIBS@ @INTLLIBS@

# To mimmick the old glibc installation as closely as possible, we
# shuffle the installed library and the links to it around a bit,
# removing all traces from libtool in the process.
install-data-local:
	$(mkinstalldirs) $(DESTDIR)$(libdir)
	rm $(DESTDIR)$(slibdir)/libnss_db.la
	rm $(DESTDIR)$(slibdir)/libnss_db.so
	mv $(DESTDIR)$(slibdir)/libnss_db.so.$(INTERFACE).0.0 \
		$(DESTDIR)$(slibdir)/libnss_db-$(VERSION).so
	rm $(DESTDIR)$(slibdir)/libnss_db.so.$(INTERFACE)
	$(top_srcdir)/rellns-sh $(DESTDIR)$(slibdir)/libnss_db-$(VERSION).so \
		$(DESTDIR)$(slibdir)/libnss_db.so.$(INTERFACE)
	rm -f $(DESTDIR)$(libdir)/libnss_db.so
	$(top_srcdir)/rellns-sh \
		$(DESTDIR)$(slibdir)/libnss_db.so.$(INTERFACE) \
		$(DESTDIR)$(libdir)/libnss_db.so
