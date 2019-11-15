#
# misc. data files
#
dist_pkgdata_DATA = qwo.desktop qworc normal.png caps.png extra.png

#
# desktop integration: .desktop file
#
desktopdir = $(datadir)/applications
dist_desktop_DATA = qwo.desktop

if HAVE_HELP2MAN
dist_man_MANS = qwo.1
endif

qwo.1:
	help2man -n "An input method for touchscreen" -s 1 -N -o qwo.1\
		$(top_builddir)/src/qwo
