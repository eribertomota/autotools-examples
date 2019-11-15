AUTOMAKE_OPTIONS = gnu

AM_CFLAGS = -Wall $(LIBUSB1_CFLAGS)
ACLOCAL_AMFLAGS = -I m4

lib_LTLIBRARIES = libinklevel.la
dist_doc_DATA = NEWS README AUTHORS COPYING ChangeLog
LIBTOOL_DEPS = @LIBTOOL_DEPS@

libtool: $(LIBTOOL_DEPS)
	$(SHELL) ./config.status --recheck


libinklevel_la_SOURCES = libinklevel.c canon.c epson.c hp.c bjnp-io.c \
                         bjnp-debug.c d4lib.c devices.c util.c \
			 libusb-utils.c printer-io.c bjnp.h config.h \
			 epson.h inklevel.h util.h canon.h d4lib.h \
			 hp.h devices.h internal.h \
			 libusb-utils.h printer-io.h \
			 libinklevel.spec libinklevel.spec.in \
			 norpm rpmbuild

include_HEADERS = inklevel.h                         

libinklevel_la_LDFLAGS = -version-info @ABI_VERSION@ $(LIBUSB1_LIBS)

@rpmtarget@
