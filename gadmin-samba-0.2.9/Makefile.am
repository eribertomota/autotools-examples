## Process this file with automake to produce Makefile.in

VERSION = @VERSION@

SUBDIRS = src po

EXTRA_DIST = \
	autogen.sh

install-data-local:
	@$(NORMAL_INSTALL)
	if test -d $(srcdir)/pixmaps; then \
	   $(mkinstalldirs) $(DESTDIR)$(datadir)/icons; \
	   for pixmap in $(srcdir)/pixmaps/*; do \
	     if test -f $$pixmap; then \
	        $(INSTALL_DATA) $$pixmap $(DESTDIR)$(datadir)/icons; \
	     fi \
	   done \
	fi;
	if test -d $(DESTDIR)$(datadir)/icons; then \
	   cp $(srcdir)/pixmaps/gadmin-samba.png $(DESTDIR)$(datadir)/icons/; \
	fi;
	if test -f $(DESTDIR)$(bindir)/consolehelper && test ! -f $(DESTDIR)$(bindir)/gadmin-samba; then \
	   ln -s $(DESTDIR)$(bindir)/consolehelper $(DESTDIR)$(bindir)/gadmin-samba; \
	fi;
	@echo "Failsafe for a mixed environment"
	if test -f $(DESTDIR)/usr/local/bin/consolehelper && test ! -f $(DESTDIR)/usr/local/bin/gadmin-samba; then \
	   ln -s $(DESTDIR)/usr/local/bin/consolehelper $(DESTDIR)/usr/local/bin/gadmin-samba; \
	fi;
	if test -d $(DESTDIR)$(sysconfdir)/pam.d; then \
	   cp etc/pam.d/gadmin-samba $(DESTDIR)$(sysconfdir)/pam.d/; \
	fi;
	if test -d $(DESTDIR)$(sysconfdir)/security/console.apps; then \
	   cp etc/security/console.apps/gadmin-samba $(DESTDIR)$(sysconfdir)/security/console.apps/; \
	fi;   
	if test -d $(DESTDIR)$(datadir)/applications; then \
	   cp desktop/gadmin-samba.desktop $(DESTDIR)$(datadir)/applications/; \
	fi;
	if test ! -d $(DESTDIR)$(datadir)/doc/gadmin-samba; then \
	   $(mkinstalldirs) $(DESTDIR)$(datadir)/doc/gadmin-samba; \
	fi;
	if test -d $(DESTDIR)$(datadir)/doc/gadmin-samba; then \
	   cp AUTHORS $(DESTDIR)$(datadir)/doc/gadmin-samba/; \
	   cp README $(DESTDIR)$(datadir)/doc/gadmin-samba/; \
	   cp ChangeLog $(DESTDIR)$(datadir)/doc/gadmin-samba/; \
	   cp COPYING $(DESTDIR)$(datadir)/doc/gadmin-samba/; \
	fi;
	if test ! -d $(DESTDIR)$(sysconfdir)/gadmin-samba; then \
	   $(mkinstalldirs) $(DESTDIR)$(sysconfdir)/gadmin-samba; \
	fi;
	if test -d $(DESTDIR)$(bindir) && test ! -f $(DESTDIR)$(bindir)/gadmin-samba-pdf; then \
	   cp scripts/gadmin-samba-pdf $(bindir)/; \
	fi;
	@echo ""
	@echo "Start GADMIN-SAMBA by typing gadmin-samba in a terminal"
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
