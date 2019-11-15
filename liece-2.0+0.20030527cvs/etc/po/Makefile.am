localedir = $(pkgdatadir)/locale

pofiles = $(wildcard *.po)
mofiles = $(pofiles:%.po=%.mo)

EXTRA_DIST = $(pofiles)

all: $(mofiles)
%.mo: %.po
	msgfmt -o $@ $<

install-data-local: $(mofiles)
	@$(NORMAL_INSTALL)
	$(mkinstalldirs) $(DESTDIR)$(localedir)
	@list='$(mofiles)'; for p in $$list; do \
	  lang=`basename $$p | sed s/\.mo//`; \
	  $(mkinstalldirs) $(DESTDIR)$(localedir)/$$lang; \
	  $(mkinstalldirs) $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES; \
	  if test -f $(srcdir)/$$p; then \
	    echo " $(INSTALL_DATA) $(srcdir)/$$p $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES/liece.mo"; \
	    $(INSTALL_DATA) $(srcdir)/$$p $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES/liece.mo; \
	  else if test -f $$p; then \
	    echo " $(INSTALL_DATA) $$p $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES/liece.mo"; \
	    $(INSTALL_DATA) $$p $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES/liece.mo; \
	  fi; fi; \
	done
