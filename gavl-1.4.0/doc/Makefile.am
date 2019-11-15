EXTRA_DIST=Doxyfile.in mainpage.incl

apiref:
	doxygen Doxyfile

html: apiref 

all: html

install-data-local:
	test -z "$(DESTDIR)$(docdir)/apiref" || $(mkdir_p) "$(DESTDIR)$(docdir)/apiref"
	$(INSTALL_DATA) apiref/* $(DESTDIR)$(docdir)/apiref

CLEANFILES = gavl.tags

clean-local:
	-rm -rf apiref

uninstall-local:
	-rm -rf "$(DESTDIR)$(docdir)/apiref"
