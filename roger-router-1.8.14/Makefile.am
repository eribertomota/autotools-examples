SUBDIRS = libroutermanager roger roger-cli po doc

AM_DISTCHECK_CONFIGURE_FLAGS = \
	--disable-werror

EXTRA_DIST = \
	autogen.sh \
	org.tabos.roger.desktop.in \
	roger.appdata.xml.in \
	remove-settings.sh \
	share/roger-cups \
	share/roger-fax.ppd \
	share/install-fax.sh \
	win32/setup-mingw.sh \
	win32/settings.ini \
	win32/printer.nsh \
	win32/roger.nsi.in \
	win32/roger.ico \
	win32/themes/Adwaita/gtk-3.0/gtk.css \
	win32/themes/Adwaita/gtk-3.0/gtk.gresource \
	win32/themes/Adwaita/gtk-3.0/settings.ini \
	win32/printer/ghostpdf.inf \
	win32/printer/ghostpdf.ppd \
	win32/patches/portaudio.patch \
	win32/patches/spandsp-0.0.6.patch

sharedir = $(datadir)/roger
share_DATA = \
	share/roger-cups\
	share/roger-fax.ppd\
	share/install-fax.sh

noinst_HEADERS = config.h

DISTCLEANFILES = intltool-extract intltool-merge intltool-update org.tabos.roger.desktop roger.appdata.xml

appsdir = $(datadir)/applications
apps_in_files = org.tabos.roger.desktop.in
apps_DATA = $(apps_in_files:.desktop.in=.desktop)

appdatadir = $(datadir)/appdata
appdata_in_files = roger.appdata.xml.in
appdata_DATA = $(appdata_in_files:.xml.in=.xml)

@INTLTOOL_XML_RULE@
@INTLTOOL_DESKTOP_RULE@
