HGTAG = 'usermode-$(VERSION)'
VENDOR=redhat

EXTRA_DIST = 	\
	dummy.h \
	consolehelper.8.in \
	sample/README sample/shutdown sample/wrapped.console \
	sample/wrapped.pamd \
	userhelper.8.in \
	userhelper_context \
	userinfo.desktop.in \
	usermount.desktop.in \
	userpasswd.desktop.in

SUBDIRS=po

AM_CPPFLAGS = -DLOCALEDIR='"$(localedir)"'
AM_CFLAGS = $(SN_CFLAGS) $(GTK_CFLAGS) $(LIBUSER_CFLAGS)
BINDIR_CPPFLAGS = -DBINDIR='"$(bindir)"'
PIXMAPDIR_CPPFLAGS = -DPIXMAPDIR='"$(pixmapdir)"'
SBINDIR_CPPFLAGS = -DSBINDIR='"$(sbindir)"'

bin_PROGRAMS = userinfo usermount userpasswd consolehelper consolehelper-gtk \
	pam-panel-icon
sbin_PROGRAMS = userhelper
noinst_PROGRAMS = test-userdialog
dist_man_MANS = consolehelper-gtk.8 pam-panel-icon.1 \
	userinfo.1 usermount.1 userpasswd.1
man_MANS = consolehelper.8 userhelper.8

pixmapdir = $(datadir)/pixmaps
dist_pixmap_DATA = keys.xpm status_lock.png status_unlocked.png user_icon.png \
	password.png disks.png keyring.png badge-small.png

noinst_LIBRARIES = liblib.a

install-data-local: userinfo.desktop usermount.desktop userpasswd.desktop
	mkdir -p $(DESTDIR)$(datadir)/applications
	for i in userinfo.desktop usermount.desktop userpasswd.desktop; do \
		desktop-file-install --vendor=$(VENDOR)			   \
			--dir=$(DESTDIR)$(datadir)/applications		   \
			$(top_builddir)/$$i;				   \
	done

uninstall-local:
	-rm -f $(DESTDIR)$(datadir)/applications/$(VENDOR)-userinfo.desktop   \
	       $(DESTDIR)$(datadir)/applications/$(VENDOR)-usermount.desktop  \
	       $(DESTDIR)$(datadir)/applications/$(VENDOR)-userpasswd.desktop

CLEANFILES = $(man_MANS)
DISTCLEANFILES =            \
	userinfo.desktop    \
	usermount.desktop   \
	userpasswd.desktop


debug-install:
	$(INSTALL) -m4711 userhelper $(sbindir)/
	$(INSTALL)  -m755 consolehelper $(bindir)/
	$(INSTALL)  -m755 consolehelper-gtk $(bindir)/
	$(INSTALL)  -m755 userinfo          $(bindir)/
	$(INSTALL)  -m755 usermount         $(bindir)/
	$(INSTALL)  -m755 userpasswd        $(bindir)/

dist_pkgdata_DATA = usermode.ui

@INTLTOOL_DESKTOP_RULE@

userhelper_SOURCES = userhelper.c userhelper.h shvar.c shvar.h
userhelper_CPPFLAGS = $(AM_CPPFLAGS) -DSYSCONFDIR='"$(sysconfdir)"'
userhelper_LDADD = liblib.a $(LIBUSER_LIBS) $(GLIB_LIBS) $(PAM_LIBS) \
	$(SELINUX_LIBS) $(EFENCE_LIBS)

userinfo_SOURCES = userinfo.c
userinfo_CPPFLAGS = $(AM_CPPFLAGS) $(PIXMAPDIR_CPPFLAGS) $(SBINDIR_CPPFLAGS) \
	-DPKGDATADIR='"$(pkgdatadir)"'
userinfo_LDADD = liblib.a $(SN_LIBS) $(GTK_LIBS) $(EFENCE_LIBS)

usermount_SOURCES = usermount.c
usermount_CPPFLAGS = $(AM_CPPFLAGS) $(PIXMAPDIR_CPPFLAGS)
usermount_LDADD = liblib.a $(GTK_LIBS) -lblkid $(EFENCE_LIBS)

userpasswd_SOURCES = userpasswd.c
userpasswd_CPPFLAGS = $(AM_CPPFLAGS) $(SBINDIR_CPPFLAGS)
userpasswd_LDADD = liblib.a $(SN_LIBS) $(GTK_LIBS) $(EFENCE_LIBS)

consolehelper_SOURCES = consolehelper-nox.c
consolehelper_CPPFLAGS = $(AM_CPPFLAGS) $(BINDIR_CPPFLAGS) $(SBINDIR_CPPFLAGS)
consolehelper_LDADD = $(GLIB_LIBS) $(EFENCE_LIBS)

consolehelper_gtk_SOURCES = consolehelper.c
consolehelper_gtk_CPPFLAGS = $(AM_CPPFLAGS) $(SBINDIR_CPPFLAGS)
consolehelper_gtk_LDADD = liblib.a $(SN_LIBS) $(GTK_LIBS) $(EFENCE_LIBS)

pam_panel_icon_SOURCES = pam-panel-icon.c gsmclient.c gsmclient.h props.c \
	props.h
pam_panel_icon_CPPFLAGS = $(AM_CPPFLAGS) $(BINDIR_CPPFLAGS) \
	$(PIXMAPDIR_CPPFLAGS) -DGETTEXT_PACKAGE=\"$(PACKAGE)\"
pam_panel_icon_LDADD = $(GTK_LIBS) $(X_LIBS) -lICE -lSM $(EFENCE_LIBS)

test_userdialog_SOURCES = test-userdialog.c
test_userdialog_LDADD = liblib.a $(GTK_LIBS) $(EFENCE_LIBS)

liblib_a_SOURCES = userdialogs.c userdialogs.h userhelper-messages.c \
	userhelper-messages.h userhelper-wrap.c userhelper-wrap.h
liblib_a_CPPFLAGS = $(AM_CPPFLAGS) $(PIXMAPDIR_CPPFLAGS)

consolehelper.8: $(srcdir)/consolehelper.8.in Makefile
	sed 's,@''BINDIR@,$(bindir),g' < $(srcdir)/consolehelper.8.in > $@

userhelper.8: $(srcdir)/userhelper.8.in Makefile
	sed 's,@''SYSCONFDIR@,$(sysconfdir),g' < $(srcdir)/userhelper.8.in > $@

tag:
	cd $(top_srcdir); hg tag $(HGTAG)

forcetag:
	cd $(top_srcdir); hg tag -f $(HGTAG)

archive:
	rm -fr /tmp/$(PACKAGE)-export-tmp
	hg clone -r $(HGTAG) $(abs_top_srcdir) /tmp/$(PACKAGE)-export-tmp
	cd /tmp/$(PACKAGE)-export-tmp; ./autogen.sh ; \
		./configure --sysconfdir=/etc --prefix=/usr; make dist
	mv /tmp/$(PACKAGE)-export-tmp/$(PACKAGE)-$(VERSION).tar.xz .
	rm -fr /tmp/$(PACKAGE)-export-tmp
