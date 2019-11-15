## Process this file with automake to produce Makefile.in

noinst_DATA = html/index.html libwibble.doxytags

if DO_DOCS
libwibble.doxytags: wibble.dox ../wibble/libwibble.la
	doxygen $<

html/index.html: wibble.dox ../wibble/libwibble.la
	doxygen $<
else
libwibble.doxytags: wibble.dox ../wibble/libwibble.la
	touch $@

html/index.html: wibble.dox ../wibble/libwibble.la
	mkdir html || true
	touch $@
endif

EXTRA_DIST = wibble.dox

CLEANFILES = libwibble.doxytags

clean-local:
	rm -rf html
