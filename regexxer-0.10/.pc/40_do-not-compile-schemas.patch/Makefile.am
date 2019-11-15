## Copyright (c) 2004-2007  Daniel Elstner  <daniel.kitta@gmail.com>
##
## This file is part of regexxer.
##
## regexxer is free software; you can redistribute it and/or modify
## it under the terms of the GNU General Public License as published by
## the Free Software Foundation; either version 2 of the License, or
## (at your option) any later version.
##
## regexxer is distributed in the hope that it will be useful,
## but WITHOUT ANY WARRANTY; without even the implied warranty of
## MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
## GNU General Public License for more details.
##
## You should have received a copy of the GNU General Public License
## along with regexxer; if not, write to the Free Software Foundation, Inc.,
## 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA

## This project does not use recursive make, but a single toplevel Makefile
## to build the entire tree (excluding the po subdirectory as gettext comes
## with its own build system).  Read Peter Miller's excellent paper to learn
## why recursive make invocations are both slow and error-prone:
## http://members.pcug.org.au/~millerp/rmch/recu-make-cons-harm.html

AUTOMAKE_OPTIONS = subdir-objects
ACLOCAL_AMFLAGS  = -I m4 ${ACLOCAL_FLAGS}
DISTCHECK_CONFIGURE_FLAGS = --disable-schemas-install --enable-warnings=fatal

SUBDIRS = po

bin_PROGRAMS = src/regexxer

src_regexxer_SOURCES =		\
	src/completionstack.cc \
	src/completionstack.h \
	src/controller.cc	\
	src/controller.h	\
	src/filebuffer.cc	\
	src/filebuffer.h	\
	src/filebufferundo.cc	\
	src/filebufferundo.h	\
	src/fileio.cc		\
	src/fileio.h		\
	src/fileshared.cc	\
	src/fileshared.h	\
	src/filetree.cc		\
	src/filetree.h		\
	src/filetreeprivate.cc	\
	src/filetreeprivate.h	\
	src/globalstrings.h	\
	src/main.cc		\
	src/mainwindow.cc	\
	src/mainwindow.h	\
	src/miscutils.h		\
	src/prefdialog.cc	\
	src/prefdialog.h	\
	src/sharedptr.h		\
	src/signalutils.cc	\
	src/signalutils.h	\
	src/statusline.cc	\
	src/statusline.h	\
	src/stringutils.cc	\
	src/stringutils.h	\
	src/translation.cc	\
	src/translation.h	\
	src/undostack.cc	\
	src/undostack.h		\
	src/settings.h

nodist_src_regexxer_SOURCES =	\
	ui/stockimages.h

# The location of the gettext catalogs as defined by intltool.
rxlocaledir = $(prefix)/$(DATADIRNAME)/locale

global_defs = -DREGEXXER_LOCALEDIR=\""$(rxlocaledir)"\" -DREGEXXER_PKGDATADIR=\""$(pkgdatadir)"\"
AM_CPPFLAGS = $(global_defs) -I$(top_builddir) $(REGEXXER_MODULES_CFLAGS) $(REGEXXER_WARNING_FLAGS)

src_regexxer_LDADD        = $(REGEXXER_MODULES_LIBS) $(INTLLIBS)

dist_pkgdata_DATA   = ui/mainwindow.ui ui/prefdialog.ui

iconthemedir        = $(datadir)/icons/hicolor
appicondir          = $(iconthemedir)/48x48/apps
dist_appicon_DATA   = ui/regexxer.png

gsettingsschema_in_files    = ui/org.regexxer.gschema.xml.in
gsettingsschema_DATA = ui/org.regexxer.gschema.xml

desktop_in_files    = ui/regexxer.desktop.in
desktopdir          = $(datadir)/applications
desktop_DATA        = ui/regexxer.desktop

dist_intltool       = intltool-extract.in intltool-merge.in intltool-update.in
stockimages         = ui/stock_save_all_16.png ui/stock_save_all_24.png

dist_noinst_DATA    = $(stockimages) $(dist_intltool) $(desktop_in_files) $(gsettingsschema_in_files)
dist_noinst_SCRIPTS = autogen.sh

BUILT_SOURCES       = $(nodist_src_regexxer_SOURCES)
CLEANFILES          = $(nodist_src_regexxer_SOURCES) $(desktop_DATA) $(gsettingsschema_DATA)
DISTCLEANFILES      = intltool-extract intltool-merge intltool-update

pixbuf_csource      = $(GDK_PIXBUF_CSOURCE) --raw
update_icon_cache   = $(GTK_UPDATE_ICON_CACHE) --ignore-theme-index --force

@INTLTOOL_DESKTOP_RULE@
@INTLTOOL_XML_NOMERGE_RULE@

install-data-hook: install-update-icon-cache
	$(GLIB_COMPILE_SCHEMAS) $(gsettingsschemadir)
#$(gsettingsupdateschemacache) $(gsettingsschemadir)

uninstall-hook: uninstall-update-icon-cache

dist-hook: dist-changelog

# Note that this rule creates the ui/ build directory as a side effect.
# This works just fine because the target is in BUILT_SOURCES and thus
# built before everything else.  Otherwise a special ui/.dirstamp rule
# would be necessary.
ui/stockimages.h: $(stockimages)
	@mkdir ui >/dev/null 2>&1 || test -d ui
	@build_list='--build-list'; \
	list='$(stockimages)'; for file in $$list; do \
	  name=`expr "X/$$file" : '.*[\\/]\([^.]*\)' | sed 'y/-/_/'`; \
	  dir=; test -f "$$file" || dir='$(srcdir)/'; \
	  build_list="$$build_list $$name $$dir$$file"; \
	done; \
	echo " $(pixbuf_csource) $$build_list >$@"; \
	$(pixbuf_csource) $$build_list >$@

dist-changelog:
	@if test -r "$(top_srcdir)/.git"; then \
	  if git --git-dir="$(top_srcdir)/.git" --work-tree="$(top_srcdir)" \
		log --date=short --pretty='format:%cd  %an  <%ae>%n%n%s%n%n%b%n' \
	  | sed	-e '/^[12]...-[01].-[0123].  [^<>]*  <[^<>]*>$$/,/^$$/ b' \
		-e '/[^	 ]/,/^[	 ]*$$/! d' \
		-e 's/^[	 ]*/	/' \
		-e 's/^[	 ]*$$//' >.ChangeLog.tmp; \
	  then mv -f .ChangeLog.tmp "$(top_distdir)/ChangeLog"; \
	  else rm -f .ChangeLog.tmp; exit 1; fi; \
	fi
install-update-icon-cache:
	@$(POST_INSTALL)
	test -n "$(DESTDIR)" || $(update_icon_cache) "$(iconthemedir)"

uninstall-update-icon-cache:
	@$(POST_UNINSTALL)
	test -n "$(DESTDIR)" || $(update_icon_cache) "$(iconthemedir)"

.PHONY: dist-changelog \
	install-update-icon-cache uninstall-update-icon-cache

.DELETE_ON_ERROR:
