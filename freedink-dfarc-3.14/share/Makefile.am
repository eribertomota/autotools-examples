dist_man_MANS = man/man1/dfarc.1 man/man1/freedink-dfarc.1

# Desktop build system inspired by:
# - intltool documentation
# - gnochm
# - gdebi
# - djvulibre

pixmapsdir = $(datarootdir)/pixmaps
dist_pixmaps_DATA = pixmaps/dfarc.png

@INTLTOOL_DESKTOP_RULE@
@INTLTOOL_XML_RULE@

desktopfiles = freedink-dfarc.desktop freedink-mime.xml

# Force building desktop files (even if we don't install them through
# a _DATA primary)
all-local: $(desktopfiles)

EXTRA_DIST = README freedink-dfarc.desktop.in freedink-mime.xml.in
DISTCLEANFILES = $(desktopfiles)


if HAVE_XDG
# xdg-utils introduced at:
# http://kapo-cpp.blogspot.com/2008/02/register-your-own-mime-type-on-free.html
mimetype = application-x-dmod
install-data-local:
#	Take new MimeType for .dmod into account
	$(XDG_ICON_RESOURCE) install --context mimetypes --size 32	\
		$(srcdir)/pixmaps/dfarc.png $(mimetype)
	$(XDG_MIME) install freedink-mime.xml
	$(XDG_DESKTOP_MENU) install freedink-dfarc.desktop

uninstall-local:
	$(XDG_ICON_RESOURCE) uninstall --context mimetypes --size 32	\
		$(mimetype)
	$(XDG_MIME) uninstall freedink-mime.xml
	$(XDG_DESKTOP_MENU) uninstall freedink-dfarc.desktop
else
# This is used for distro packages, and supports DESTDIR
# Note: Debian now automatically *triggers* desktop-file-utils and mime-support
install-data-local:
	$(mkdir_p) "$(DESTDIR)$(datarootdir)/applications"
	$(mkdir_p) "$(DESTDIR)$(datarootdir)/mime/packages"
	$(mkdir_p) "$(DESTDIR)${datarootdir}/icons/hicolor/32x32/mimetypes"
	$(INSTALL_DATA) "$(srcdir)/pixmaps/dfarc.png"						\
		"$(DESTDIR)${datarootdir}/icons/hicolor/32x32/mimetypes/application-x-dmod.png"
	$(INSTALL_DATA) "freedink-dfarc.desktop" "$(DESTDIR)$(datarootdir)/applications/"
	$(INSTALL_DATA) "freedink-mime.xml" "$(DESTDIR)$(datarootdir)/mime/packages/"
#	Run these in your postinst script:
#	update-icon-caches
#	# or gtk-update-icon-cache
#	update-desktop-database
#	update-mime-database $(datarootdir)/mime
uninstall-local:
	rm -f "$(DESTDIR)$(datarootdir)/applications/freedink-dfarc.desktop"
	rm -f "$(DESTDIR)${datarootdir}/icons/hicolor/32x32/mimetypes/application-x-dmod.png"
	rm -f "$(DESTDIR)$(datarootdir)/mime/packages/freedink-mime.xml"
#	Run these in your postrm script:
#	gtk-update-icon-cache
#	update-desktop-database
#	update-mime-database $(datarootdir)/mime
endif
