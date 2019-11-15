LIBTOOLFLAGS=--silent

man_MANS=man/kateenc.1 man/katedec.1 man/katalyzer.1 man/KateDJ.1

# dependency to get doc to be built
noinst_DATA = .doc-dummy-target

install-data-local:
	$(mkinstalldirs) $(DESTDIR)$(docdir)
	for dir in $(top_srcdir)/doc/html; do \
	  if test -d "$$dir"; then \
	    b=`basename $$dir`; \
	    $(mkinstalldirs) $(DESTDIR)$(docdir)/$$b; \
	    for f in "$$dir/"*; do \
	      $(INSTALL_DATA) "$$f" "$(DESTDIR)$(docdir)/$$b"; \
            done \
	  fi \
	done
	for f in README AUTHORS COPYING THANKS ChangeLog; do \
	  $(INSTALL_DATA) $(top_srcdir)/$$f $(DESTDIR)$(docdir); \
	done

uninstall-local:
	rm -rf $(DESTDIR)$(docdir)

distclean-local:
	if test -d html; then rm -rf html; fi
	if test -d latex; then rm -rf latex; fi
	if test -f .doc-dummy-target; then rm -f .doc-dummy-target; fi

if HAVE_DOXYGEN
.doc-dummy-target: kate.doxygen
	doxygen kate.doxygen
	touch .doc-dummy-target
else
.doc-dummy-target:
	echo "doxygen not found, cannot build docs"
endif

dist-hook: .doc-dummy-target
	cp -fR * $(distdir)
	rm -f $(distdir)/doc/kate.doxygen
	for f in man/kateenc.1 man/katedec.1 man/katalyzer.1; do \
	  if test -f "$(distdir)/doc/$$f"; then rm -f "$(distdir)/doc/$$f"; fi \
	done

.PHONY: force-doc
force-doc: rm-doc-dummy-target .doc-dummy-target

.PHONY: rm-doc-dummy-target
rm-doc-dummy-target:
	rm -f .doc-dummy-target

