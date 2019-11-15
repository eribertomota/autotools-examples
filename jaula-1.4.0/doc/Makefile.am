
# # svn info
# # $Author: morongo $
# # $Date: 2009-01-11 17:17:03 +0100 (dom, 11 ene 2009) $
# # $HeadURL: https://jaula.svn.sourceforge.net/svnroot/jaula/tags/jaula-1.4.0/doc/Makefile.am $
# # $Id: Makefile.am 45 2009-01-11 16:17:03Z morongo $
# # $Revision: 45 $

DOXYGEN=@DOXYGEN@

PDFLATEX=@PDFLATEX@

SUBDIRS = .

# # base data directory
datarootdir = @datarootdir@

# # document destination
pkgdocdir=$(datadir)/doc/$(PACKAGE_NAME)

# # Additional documentation (besides doxygen generated files)
pkgdoc_DATA =  api_footer.html json_value_parse.png parser.xmi

EXTRA_DIST = $(pkgdoc_DATA) Doxyfile.in

doc:
	if test -n "$(DOXYGEN)"; then ($(SHELL) -c $(DOXYGEN) || true); fi
	if test -d "latex" -a -n "$(PDFLATEX)"; then (make -C latex || true); fi

all-local:	doc

install-data-local:
	test -n "$(DOXYGEN)" && mkdir -p $(DESTDIR)/$(pkgdocdir)/html
	test -n "$(DOXYGEN)" -a -d html && (\
		for i in `find html -print`; \
		do \
			echo "$(INSTALL_DATA) $$i $(DESTDIR)/$(pkgdocdir)/$$i"; \
			$(INSTALL_DATA) $$i $(DESTDIR)/$(pkgdocdir)/$$i; \
		done)
	test -n "$(DOXYGEN)" -a -f $(PACKAGE_NAME).tag && $(INSTALL_DATA) $(PACKAGE_NAME).tag $(DESTDIR)/$(pkgdocdir)/$(PACKAGE_NAME).tag
	test -n "$(DOXYGEN)" && mkdir -p $(DESTDIR)/$(pkgdocdir)/latex
	test -n "$(DOXYGEN)" -a -d latex && (\
		for i in `find latex -print`; \
		do \
			echo "$(INSTALL_DATA) $$i $(DESTDIR)/$(pkgdocdir)/$$i"; \
			$(INSTALL_DATA) $$i $(DESTDIR)/$(pkgdocdir)/$$i; \
		done)
	test -n "$(DOXYGEN)" -a -f "latex/refman.pdf" && $(INSTALL_DATA) latex/refman.pdf $(DESTDIR)/$(pkgdocdir)/$(PACKAGE_NAME)_API_reference.pdf
	test -n "$(DOXYGEN)" && mkdir -p $(DESTDIR)/$(pkgdocdir)/rtf
	test -n "$(DOXYGEN)" -a -d rtf && (\
		for i in `find rtf -print`; \
		do \
			echo "$(INSTALL_DATA) $$i $(DESTDIR)/$(pkgdocdir)/$$i"; \
			$(INSTALL_DATA) $$i $(DESTDIR)/$(pkgdocdir)/$$i; \
		done)

clean-local:
	$(RM) -r html
	$(RM) -r rtf
	$(RM) -r latex

# # EOF $Id: Makefile.am 45 2009-01-11 16:17:03Z morongo $


