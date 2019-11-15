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
	   cp pixmaps/gadmin-openvpn-client.png $(DESTDIR)$(datadir)/icons/; \
	fi;
	if test -f $(DESTDIR)$(bindir)/consolehelper && test ! -f $(DESTDIR)$(bindir)/gadmin-openvpn-client; then \
	   ln -s $(DESTDIR)$(bindir)/consolehelper $(DESTDIR)$(bindir)/gadmin-openvpn-client; \
	fi;
	@echo "Failsafe for a mixed environment"
	if test -f $(DESTDIR)/usr/local/bin/consolehelper && test ! -f $(DESTDIR)/usr/local/bin/gadmin-openvpn-client; then \
	   ln -s $(DESTDIR)/usr/local/bin/consolehelper $(DESTDIR)/usr/local/bin/gadmin-openvpn-client; \
	fi;
	if test -d $(DESTDIR)$(sysconfdir)/pam.d; then \
	   cp etc/pam.d/gadmin-openvpn-client $(DESTDIR)$(sysconfdir)/pam.d/; \
	fi;
	if test -d $(DESTDIR)$(sysconfdir)/security/console.apps; then \
	   cp etc/security/console.apps/gadmin-openvpn-client $(DESTDIR)$(sysconfdir)/security/console.apps/; \
	fi;   
	if test -d $(DESTDIR)$(datadir)/applications; then \
	   cp desktop/gadmin-openvpn-client.desktop $(DESTDIR)$(datadir)/applications/; \
	fi;
	if test ! -d $(DESTDIR)$(datadir)/doc/gadmin-openvpn-client; then \
	   $(mkinstalldirs) $(DESTDIR)$(datadir)/doc/gadmin-openvpn-client; \
	   cp AUTHORS $(DESTDIR)$(datadir)/doc/gadmin-openvpn-client/; \
	   cp README $(DESTDIR)$(datadir)/doc/gadmin-openvpn-client/; \
	   cp ChangeLog $(DESTDIR)$(datadir)/doc/gadmin-openvpn-client/; \
	   cp COPYING $(DESTDIR)$(datadir)/doc/gadmin-openvpn-client/; \
	fi;
	@echo ""
	@echo "Start GAdmin-OpenVPN-Client by typing gadmin-openvpn-client in a terminal"
	@echo "or start it from the desktop menu."
	@echo ""
	@echo "Send bugreports, comments or questions to magnus-swe@telia.com"
	@echo ""

dist-hook:
	if test -d pixmaps; then \
	  mkdir $(DESTDIR)$(distdir)/icons; \
	  for pixmap in pixmaps/*; do \
	    if test -f $$pixmap; then \
	      cp -p $$pixmap $(DESTDIR)$(distdir)/icons; \
	    fi \
	  done \
	fi
