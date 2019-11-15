## -*- Makefile -*-
## Makefile for a2ps' etc library directory.

ogonkifydir=$(datadir)/ogonkify
libpath = $(pkgdatadir)/sheets:$(pkgdatadir)/ps:$(pkgdatadir)/encoding:$(pkgdatadir)/afm:$(ogonkifydir)/afm:$(pkgdatadir)/ppd:$(pkgdatadir)/fonts:$(ogonkifydir)/fonts:$(pkgdatadir)

pkgdata_DATA = README

dsysconf = $(DESTDIR)$(sysconfdir)

EXTRA_DIST = README.in

all-local: a2ps.cfg

install-data-local: a2ps.cfg
	$(mkinstalldirs) $(dsysconf)
	@if test -r $(dsysconf)/$(PACKAGE).cfg; then \
	  if cmp $(dsysconf)/$(PACKAGE).cfg $(top_builddir)/etc/$(PACKAGE).cfg 2> /dev/null ; then \
	     echo "$(dsysconf)/$(PACKAGE).cfg has not changed"; \
	  else \
	     echo;	\
	     echo "*******************";	\
	     echo "* Warning: $(dsysconf)/$(PACKAGE).cfg exist."; \
	     echo "* It has been moved as $(dsysconf)/$(PACKAGE).cfg.old"; \
	     echo "*******************";	\
	     echo; \
	     mv $(dsysconf)/$(PACKAGE).cfg $(dsysconf)/$(PACKAGE).cfg.old; \
	     $(INSTALL_DATA) $(top_builddir)/etc/$(PACKAGE).cfg $(dsysconf)/$(PACKAGE).cfg ; \
	  fi \
	else \
	  $(INSTALL_DATA) $(top_builddir)/etc/$(PACKAGE).cfg $(dsysconf)/$(PACKAGE).cfg; \
	fi
	@test -r $(dsysconf)/a2ps-site.cfg || \
	  $(INSTALL_DATA) $(top_builddir)/etc/a2ps-site.cfg $(dsysconf)/a2ps-site.cfg ;

uninstall-local:
	rm -f $(dsysconf)/$(PACKAGE).cfg $(dsysconf)/$(PACKAGE)-site.cfg

DISTCLEANFILES = a2ps.cfg README

# Building the correct a2ps.cfg
a2ps.cfg: a2ps_cfg Makefile
	sed "s!@libpath@!$(libpath)!" a2ps_cfg > a2ps.cfg

# Building a time stamp to know the version.
README: README.in Makefile
	sed "s!@date@!`date`!g;s!@version@!$(VERSION)!g"	\
	$(srcdir)/README.in > README
