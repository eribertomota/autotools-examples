## Process this file with automake to produce Makefile.in

noinst_HEADERS = cddb.h compat.h

lib_LTLIBRARIES = libcdaudio.la

libcdaudio_la_SOURCES = cddb.c cdindex.c coverart.c data.c changer.c	\
base64.c extra_objs.c

if IRIX
libcdaudio_la_SOURCES += cdaudio-irix.c
else !IRIX
if BEOS
libcdaudio_la_SOURCES += cdaudio-beos.c
else !BEOS
libcdaudio_la_SOURCES += cdaudio.c
endif !BEOS
endif !IRIX

libcdaudio_la_LDFLAGS = -version-info 1:0:0

include_HEADERS = \
	cdaudio.h

# The following rules are customized from the defaults provided by
# Automake so we can change the install name to @cdaudioname@.

install-includeHEADERS: $(include_HEADERS)
	$(mkinstalldirs) $(DESTDIR)$(includedir)
	$(INSTALL_DATA) cdaudio.h $(DESTDIR)$(includedir)/@cdaudioname@.h

uninstall-includeHEADERS:
	rm -f $(DESTDIR)$(includedir)/@cdaudioname@.h

install-libLTLIBRARIES: lib@cdaudioname@.la
	$(mkinstalldirs) $(DESTDIR)$(libdir)
	$(LIBTOOL) --mode=install $(INSTALL) lib@cdaudioname@.la $(DESTDIR)$(libdir)/lib@cdaudioname@.la

all-am: Makefile lib@cdaudioname@.la $(HEADERS)

uninstall-libLTLIBRARIES:
	$(LIBTOOL) --mode=uninstall rm -f $(DESTDIR)$(libdir)/lib@cdaudioname@.la

libcdaudio.la: $(libcdaudio_la_OBJECTS) $(libcdaudio_la_DEPENDENCIES)
	$(LINK) -rpath $(libdir) $(libcdaudio_la_LDFLAGS) $(libcdaudio_la_OBJECTS) $(libcdaudio_la_LIBADD) $(LIBS)

liblibcdaudio.la: $(libcdaudio_la_OBJECTS) $(libcdaudio_la_DEPENDENCIES)
	$(LINK) -rpath $(libdir) $(libcdaudio_la_LDFLAGS) $(libcdaudio_la_OBJECTS) $(libcdaudio_la_LIBADD) $(LIBS)
