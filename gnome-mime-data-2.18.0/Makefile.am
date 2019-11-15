SUBDIRS = man po

pkgconfigdir = $(datadir)/pkgconfig
pkgconfig_DATA = gnome-mime-data-2.0.pc

NULL=

keys_in_files = gnome-vfs.keys.in
keys_files = $(keys_in_files:.keys.in=.keys)
@INTLTOOL_KEYS_RULE@

mimedir = $(datadir)/mime-info
mime_DATA = $(keys_files) gnome-vfs.mime

applicationsdir = $(datadir)/application-registry
applications_DATA = gnome-vfs.applications

sysconf_DATA = gnome-vfs-mime-magic

EXTRA_DIST =					\
	autogen.sh				\
	check-mime.pl				\
	gnome-mime-data.spec			\
	gnome-mime-data-zip.in			\
	gnome-mime-data-2.0.pc.in		\
	intltool-extract.in			\
	intltool-merge.in			\
	intltool-update.in			\
	$(keys_in_files) $(mime_DATA) $(sysconf_DATA) $(applications_DATA)

CLEANFILES = $(keys_files)

DISTCLEANFILES = \
  intltool-extract \
  intltool-merge \
  intltool-update
