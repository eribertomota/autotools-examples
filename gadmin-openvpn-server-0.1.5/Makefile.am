## Process this file with automake to produce Makefile.in

VERSION = @VERSION@

SUBDIRS = src po

EXTRA_DIST = \
	autogen.sh

install-data-local:
	@$(NORMAL_INSTALL)
	if test -d $(srcdir)/pixmaps; then \
	   $(mkinstalldirs) $(DESTDIR)$(datadir)/pixmaps/gadmin-openvpn-server; \
	   for pixmap in $(srcdir)/pixmaps/*; do \
	     if test -f $$pixmap; then \
	        $(INSTALL_DATA) $$pixmap $(DESTDIR)$(datadir)/pixmaps/gadmin-openvpn-server; \
	     fi \
	   done \
	fi;
	if test -d $(DESTDIR)$(datadir)/pixmaps; then \
	   cp pixmaps/gadmin-openvpn-server.png $(DESTDIR)$(datadir)/pixmaps/; \
	fi;
	if test -f $(DESTDIR)$(bindir)/consolehelper && test ! -f $(DESTDIR)$(bindir)/gadmin-openvpn-server; then \
	   ln -s $(DESTDIR)$(bindir)/consolehelper $(DESTDIR)$(bindir)/gadmin-openvpn-server; \
	fi;
	@echo "Failsafe for a mixed environment"
	if test -f $(DESTDIR)/usr/local/bin/consolehelper && test ! -f $(DESTDIR)/usr/local/bin/gadmin-openvpn-server; then \
	   ln -s $(DESTDIR)/usr/local/bin/consolehelper $(DESTDIR)/usr/local/bin/gadmin-openvpn-server; \
	fi;
	if test -d $(DESTDIR)$(sysconfdir)/pam.d; then \
	   cp etc/pam.d/gadmin-openvpn-server $(DESTDIR)$(sysconfdir)/pam.d/; \
	fi;
	if test -d $(DESTDIR)$(sysconfdir)/security/console.apps; then \
	   cp etc/security/console.apps/gadmin-openvpn-server $(DESTDIR)$(sysconfdir)/security/console.apps/; \
	fi;   
	if test -d $(DESTDIR)$(datadir)/applications; then \
	   cp desktop/gadmin-openvpn-server.desktop $(DESTDIR)$(datadir)/applications/; \
	fi;
	if test ! -d $(DESTDIR)$(datadir)/doc/gadmin-openvpn-server; then \
	   $(mkinstalldirs) $(DESTDIR)$(datadir)/doc/gadmin-openvpn-server; \
	   cp AUTHORS $(DESTDIR)$(datadir)/doc/gadmin-openvpn-server/; \
	   cp README $(DESTDIR)$(datadir)/doc/gadmin-openvpn-server/; \
	   cp ChangeLog $(DESTDIR)$(datadir)/doc/gadmin-openvpn-server/; \
	   cp COPYING $(DESTDIR)$(datadir)/doc/gadmin-openvpn-server/; \
	fi;
	if test ! -d $(DESTDIR)$(sysconfdir)/gadmin-openvpn; then \
	   $(mkinstalldirs) $(DESTDIR)$(sysconfdir)/gadmin-openvpn; \
	fi;
	@echo ""
	@echo "Start GAdmin-OpenVPN-Server by typing gadmin-openvpn-server in a terminal"
	@echo "or start it from the desktop menu."
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
