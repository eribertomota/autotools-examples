## Process this file with automake to produce Makefile.in

VERSION = @VERSION@

SUBDIRS = src po

EXTRA_DIST = \
	autogen.sh

install-data-local:
	@$(NORMAL_INSTALL)
	if test -d $(srcdir)/pixmaps; then \
	   $(mkinstalldirs) $(DESTDIR)$(datadir)/pixmaps/gadmin-bind; \
	   for pixmap in $(srcdir)/pixmaps/*; do \
	     if test -f $$pixmap; then \
	        $(INSTALL_DATA) $$pixmap $(DESTDIR)$(datadir)/pixmaps/gadmin-bind; \
	     fi \
	   done \
	fi;
	if test -d $(DESTDIR)$(datadir)/pixmaps; then \
	   cp pixmaps/gadmin-bind.png $(DESTDIR)$(datadir)/pixmaps/; \
	fi;
	if test -f $(DESTDIR)$(bindir)/consolehelper && test ! -f $(DESTDIR)$(bindir)/gadmin-bind; then \
	   ln -s $(DESTDIR)$(bindir)/consolehelper $(DESTDIR)$(bindir)/gadmin-bind; \
	fi;
	if test -d $(DESTDIR)$(sysconfdir)/pam.d; then \
	   cp etc/pam.d/gadmin-bind $(DESTDIR)$(sysconfdir)/pam.d/; \
	fi;
	if test -d $(DESTDIR)$(sysconfdir)/security/console.apps; then \
	   cp etc/security/console.apps/gadmin-bind $(DESTDIR)$(sysconfdir)/security/console.apps/; \
	fi;   
	if test -d $(DESTDIR)$(datadir)/applications; then \
	   cp desktop/gadmin-bind.desktop $(DESTDIR)$(datadir)/applications/; \
	fi ;
	if test ! -d $(DESTDIR)$(datadir)/doc/gadmin-bind; then \
	   $(mkinstalldirs) $(DESTDIR)$(datadir)/doc/gadmin-bind; \
	fi;
	if test -d $(DESTDIR)$(datadir)/doc/gadmin-bind; then \
	   cp AUTHORS $(DESTDIR)$(datadir)/doc/gadmin-bind/; \
	   cp README $(DESTDIR)$(datadir)/doc/gadmin-bind/; \
	   cp ChangeLog $(DESTDIR)$(datadir)/doc/gadmin-bind/; \
	   cp COPYING $(DESTDIR)$(datadir)/doc/gadmin-bind/; \
	fi;
	@echo ""
	@echo "Start GAdmin-BIND by typing gadmin-bind in a terminal"
	@echo "or start it from the menu."
	@echo ""
	@echo "Send bugreports, comments or questions to magnus-swe@telia.com"
	@echo ""

dist-hook:
	if test -d pixmaps; then \
	  mkdir $(DESTDIR)$(distdir)/pixmaps; \
	  for pixmap in pixmaps/*; do \
	    if test -f $$pixmap; then \
	      cp -p $$pixmap $(DESTDIR)$(distdir)/pixmaps; \
	    fi \
	  done \
	fi
