SUBDIRS = doc

source_h = xsettings-client.h  xsettings-common.h
source_c = xsettings-client.c  xsettings-common.c

INCLUDES = -I $(includedir) $(X_CFLAGS)

libxsincludedir = $(includedir)

lib_LTLIBRARIES      = libXsettings-client.la

libxsinclude_HEADERS = $(source_h)

libXsettings_client_la_SOURCES = $(source_c) $(source_h)

libXsettings_client_la_LIBADD      = @X_LIBS@

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libxsettings-client.pc

EXTRA_DIST = config.h.in \
             gpe-dist.am \
             gpe-tp.am \
             libxsettings-client.pc.in \
			 debian/rules \
			 debian/control \
			 debian/changelog \
			 debian/compat \
			 debian/libxsettings-client-dev.files \
			 debian/libxsettings-client0.files

deb: dist
	-mkdir $(top_builddir)/debian-build
	cd $(top_builddir)/debian-build && tar xzf $(top_builddir)/../$(PACKAGE)-$(VERSION).tar.gz
	cd $(top_builddir)/debian-build/$(PACKAGE)-$(VERSION) && dpkg-buildpackage -rfakeroot
	-rm -rf $(top_builddir)/debian-build/$(PACKAGE)-$(VERSION)
	
include gpe-dist.am
include gpe-tp.am
