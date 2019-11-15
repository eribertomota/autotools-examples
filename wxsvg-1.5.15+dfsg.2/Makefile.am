SUBDIRS = src svgview include
ACLOCAL_AMFLAGS = -I m4

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libwxsvg.pc
EXTRA_DIST     = libwxsvg.pc.in
man_MANS       = svgview.1

run: all
	$(MAKE) -C svgview run
