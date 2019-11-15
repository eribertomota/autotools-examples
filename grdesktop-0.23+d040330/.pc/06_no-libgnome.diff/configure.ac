# grdesktop - gtk rdesktop frontend
# Copyright (C) 2002 Thorsten Sauter <tsauter@gmx.net>
#
# $Id: configure.ac,v 1.27 2004/03/30 13:59:11 tsauter Exp $
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
#


dnl Global automake/autoconf files
AC_INIT(src/main.c)
AM_INIT_AUTOMAKE(grdesktop, 0.23)
AM_CONFIG_HEADER(config.h)
AM_MAINTAINER_MODE

dnl Check default compiler options
AC_PROG_CC
AC_PROG_CC_STDC
AC_C_CONST

dnl We need these programs to compile/install grdesktop
AC_PROG_INSTALL
AC_PROG_LN_S
AC_ISC_POSIX

dnl Check local system environment
AC_STDC_HEADERS
AC_HAVE_HEADERS(string.h fcntl.h sys/files.h sys/params.h)

dnl GNU gettext functions
ALL_LINGUAS="de fr es"
AM_GLIB_GNU_GETTEXT
GETTEXT_PACKAGE=$PACKAGE
AC_DEFINE_UNQUOTED([GETTEXT_PACKAGE], ["${GETTEXT_PACKAGE}"], [gettext domain])

dnl Searching for GTK+ 2 includes/libs and export compiler flags
PKG_CHECK_MODULES(GTK2, gtk+-2.0, HAVE_GTK=yes, HAVE_GTK=no)
if test "$HAVE_GTK" = "no"; then
	AC_MSG_ERROR([cannot find GTK+ 2.0!])
fi
AC_SUBST(GTK2_CFLAGS)
AC_SUBST(GTK2_LIBS)

dnl Searching for GNOME 2 includes/libs and export compiler flags
PKG_CHECK_MODULES(GNOME2, libgnomeui-2.0, HAVE_GNOME2=yes, HAVE_GNOME2=no)
if test "$HAVE_GNOME2" = "no"; then
	AC_MSG_ERROR([cannot find GNOME2 2.0!])
fi
AC_SUBST(GNOME2_CFLAGS)
AC_SUBST(GNOME2_LIBS)

AC_PATH_PROG(GCONFTOOL, gconftool-2, no)
if test "$GCONFTOOL" = "no"; then
	AC_MSG_ERROR([cannot find gconf 2.0!])
fi
AM_GCONF_SOURCE_2

AC_CHECK_PROG(rdesktop, rdesktop, "yes", "no")
if test "$rdesktop" = "no"; then
	AC_MSG_WARN([*** rdesktop is required to use grdesktp! ***])
fi

AC_ARG_WITH(keymap-path, AC_HELP_STRING([--with-keymap-path=DIR],
	[search for rdesktop keymap files in DIR/]))
if test "$withval" = ""; then
	AC_MSG_WARN([--with-keymap-path called without argument - will use default])
	AC_SUBST(kbpath, "/usr/local/share/rdesktop/keymaps/")
else
	AC_SUBST(kbpath, $withval)
fi

dnl Generate the Makefiles
AC_OUTPUT([
Makefile \
po/Makefile.in \
help/Makefile \
help/C/Makefile \
doc/Makefile \
src/Makefile \
pixmaps/Makefile
])

