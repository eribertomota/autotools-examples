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

AC_INIT([regexxer], [0.10], [http://regexxer.sourceforge.net/bugs], [regexxer],
        [http://regexxer.sourceforge.net/])
AC_PREREQ([2.59])

AC_CONFIG_SRCDIR([ui/regexxer.desktop.in])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_HEADERS([config.h])

AM_INIT_AUTOMAKE([1.10 -Wall gnu no-define nostdinc check-news dist-xz no-dist-gzip])
AC_ARG_VAR([ACLOCAL_FLAGS], [aclocal flags, e.g. -I <macro dir>])

AC_PROG_CC
AC_PROG_CXX

IT_PROG_INTLTOOL([0.35])
AC_SUBST([GETTEXT_PACKAGE], [regexxer])
AM_GNU_GETTEXT_VERSION([0.11])
AM_GLIB_GNU_GETTEXT

PKG_CHECK_MODULES([REGEXXER_MODULES],
                  [gtkmm-3.0 >= 3.0.0 glibmm-2.4 >= 2.27.94
                  gtksourceviewmm-3.0 >= 2.91.5])

DK_PKG_PATH_PROG([GDK_PIXBUF_CSOURCE], [gdk-pixbuf-2.0], [gdk-pixbuf-csource])
DK_PKG_PATH_PROG([GTK_UPDATE_ICON_CACHE], [gtk+-2.0], [gtk-update-icon-cache])

GLIB_GSETTINGS

AC_LANG([C++])

DK_ARG_ENABLE_WARNINGS([REGEXXER_WARNING_FLAGS],
                       [-Wall -w1 -Wno-long-long],
                       [-pedantic -Wall -Wextra -w1 -Wno-long-long],
                       [G GDK GTK PANGO ATK GLIBMM GDKMM ATKMM GTKMM])

AC_CONFIG_FILES([Makefile po/Makefile.in])
AC_OUTPUT
