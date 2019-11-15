EXTRA_DIST = *.png faq.sgml index.sgml
DOC_MODULE=partimage-user-doc
DOC_MAIN_SGML_FILE=index.sgml
DOC_FAQ_SGML_FILE=faq.sgml
HTML_DIR=$(prefix)/share/doc/partimage-doc/html

html: 
	sgml2html $(DOC_MAIN_SGML_FILE)
	sgml2html $(DOC_FAQ_SGML_FILE)

install-data-local: html
	$(mkinstalldirs) $(HTML_DIR)
	-for file in $(srcdir)/*.html $(srcdir)/*.sgml $(srcdir)/*.png; do \
		basefile=`basename $$file`; \
		$(INSTALL_DATA) $(srcdir)/$$file $(HTML_DIR)/$$basefile; \
	done

uninstall-local:
	-rm -f $(HTML_DIR)/*.html
	-rm -r $(HTML_DIR)/*.sgml
	-rm -r $(HTML_DIR)/*.png
	
