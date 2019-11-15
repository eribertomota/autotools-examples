SUBDIRS = icons po styles

EXTRA_DIST = gnu-emacs-user-config.in
DISTCLEANFILES = gnu-emacs-user-config
pkgdata_DATA = gnu-emacs-user-config
gnu-emacs-user-config: gnu-emacs-user-config.in
	sed 's!@pkgdatadir@!$(pkgdatadir)!g' $< > $@
	chmod +x $@

package:
install-package: package
	$(MAKE) pkgdatadir=$(PACKAGEDIR)/etc/$(PACKAGE) install
