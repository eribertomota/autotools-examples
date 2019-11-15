SUBDIRS = src doc po

desktopdir = $(datadir)/applications
desktop_in_files = gnomad2.desktop.in
desktop_DATA = $(desktop_in_files:.desktop.in=.desktop)
@INTLTOOL_DESKTOP_RULE@

icondir = $(datadir)/pixmaps
icon_DATA = gnomad2-logo.png

applicationsdir = $(datadir)/application-registry
applications_DATA = gnomad2.applications

man_MANS = gnomad2.1

EXTRA_DIST = \
	AUTHORS \
	TODO \
	NEWS \
	README \
	$(desktop_in_files) \
	$(desktop_DATA) \
	$(applications_DATA) \
	$(icon_DATA) \
	intltool-merge.in \
	intltool-update.in \
	intltool-extract.in \
	gnomad2.1 \
	mkinstalldirs
DISTCLEANFILES = \
	po/.intltool-merge-cache \
	$(desktop_DATA) \
	intltool-extract \
	intltool-merge \
	intltool-update
