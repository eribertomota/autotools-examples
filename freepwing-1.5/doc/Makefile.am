pkgdoc_DATA = freepwing.html freepwing.css

EXTRA_DIST = freepwing.html.in freepwing.css html-include html-split html-toc
CLEANFILES = *.html

install-data-hook:
	for i in $(pkgdoc_DATA); do \
	    base="`echo $$i | sed -e 's/\.html//'`"; \
	    for j in $$base-[0-9][0-9].html; do \
		test -r $$j || continue; \
		echo " $(INSTALL_DATA) '$$j' '$(DESTDIR)$(pkgdocdir)/$$j'"; \
		$(INSTALL_DATA) "$$j" "$(DESTDIR)$(pkgdocdir)/$$j"; \
	    done; \
	done

uninstall-hook:
	for i in $(pkgdoc_DATA); do \
	    base="`echo $$i | sed -e 's/\.html//'`"; \
	    rm -f "$(DESTDIR)$(pkgdocdir)"/$$base-*.html; \
	done

version.html:
	rm -f $@
	echo $(VERSION) > version.html

freepwing.html: freepwing-cat.html
	rm -f $@
	$(PERL) $(srcdir)/html-split -p freepwing -l h1 -Z -w 2 \
	    freepwing-cat.html

freepwing-cat.html: $(srcdir)/freepwing.html.in version.html toc.html
	rm -f $@
	$(PERL) $(srcdir)/html-include -o $@ $(srcdir)/freepwing.html.in

toc.html: $(srcdir)/freepwing.html.in
	rm -f $@
	$(PERL) $(srcdir)/html-toc -M h3 $(srcdir)/freepwing.html.in > $@
