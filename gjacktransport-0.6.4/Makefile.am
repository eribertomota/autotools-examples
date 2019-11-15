## Process this file with automake to produce Makefile.in

SUBDIRS = src po

man_MANS = doc/gjacktransport.1 doc/gjackclock.1 

EXTRA_DIST = \
	autogen.sh \
	po/messages.pot \
	pixmaps/gjacktransport.png \
	pixmaps/gjackclock.png \
	doc/gjacktransport.1 \
	doc/gjackclock.1 \
	gjackclock.desktop \
	gjacktransport.desktop

DISTCLEAN = \
	po/messages.pot \
	intltool-extract \
	intltool-merge \
	intltool-update

install-data-local:
	@$(NORMAL_INSTALL)
	$(INSTALL) -d $(DESTDIR)$(datadir)/pixmaps/
	$(INSTALL_DATA) $(srcdir)/pixmaps/gjacktransport.png $(DESTDIR)$(datadir)/pixmaps/
	$(INSTALL_DATA) $(srcdir)/pixmaps/gjackclock.png $(DESTDIR)$(datadir)/pixmaps/
	$(INSTALL) -d $(DESTDIR)$(sysconfdir)
	$(INSTALL_DATA) $(srcdir)/src/gjacktransportrc $(DESTDIR)$(sysconfdir)
	$(INSTALL_DATA) $(srcdir)/src/gjackclockrc $(DESTDIR)$(sysconfdir)

uninstall-local:
	rm -vf $(DESTDIR)$(datadir)/pixmaps/gjackclock.png
	rm -vf $(DESTDIR)$(datadir)/pixmaps/gjacktransport.png

po/messages.pot:
	xgettext --keyword=_ -o po/messages.pot src/*.c
