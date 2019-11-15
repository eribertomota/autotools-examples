localedir = $(datadir)/locale
EXTRA_DIST = \
mainpage.incl \
api_usage.html \
codecs.html \
hackersguide.txt \
qt4l_building.html \
qt4l_codecs.html \
qt4l_index.html \
qt4l_license.html \
qt4l_opening.html \
qt4l_positioning.html \
qt4l_reading.html \
qt4l_util.html \
qt4l_writing.html \
translatorsguide.txt \
Doxyfile.in

apiref:
	doxygen Doxyfile

html: apiref 

all: html

CLEANFILES = libquicktime.tags

install-data-local:
	test -z "$(DESTDIR)$(docdir)/apiref" || $(mkdir_p) "$(DESTDIR)$(docdir)/apiref"
	$(INSTALL_DATA) apiref/* $(DESTDIR)$(docdir)/apiref


clean-local:
	-rm -rf apiref

uninstall-local:
	-rm -rf "$(DESTDIR)$(docdir)/apiref"
