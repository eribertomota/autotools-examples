dnl configure.ac
dnl
dnl Copyright (C) 2001-2003 Tim Stadelmann
dnl
dnl This program is free software; you can redistribute it and/or modify
dnl it under the terms of the GNU General Public License as published by
dnl the Free Software Foundation; either version 2, or (at your option)
dnl any later version.
dnl
dnl This program is distributed in the hope that it will be useful,
dnl but WITHOUT ANY WARRANTY; without even the implied warranty of
dnl MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
dnl GNU General Public License for more details.
dnl
dnl You should have received a copy of the GNU General Public License
dnl along with this program; if not, write to the Free Software Foundation,
dnl Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.  

dnl Initialization

AC_INIT
AC_CONFIG_SRCDIR(config.h.in)
AC_CONFIG_HEADERS([config.h])
AM_INIT_AUTOMAKE(hotswap, 0.4.0)
AC_SUBST(VERSION)
ISODATE=`date +%Y-%m-%d`
AC_SUBST(ISODATE)

AM_GNU_GETTEXT([external])

dnl Options

AC_ARG_ENABLE(kde-frontend,
  AC_HELP_STRING([--disable-kde-frontend],
    [do not build the KDE frontend]))

AC_ARG_ENABLE(motif-frontend,
  AC_HELP_STRING([--disable-motif-frontend],
    [do not build the Motif frontend]))

if test "$enable_kde_frontend" != "no"; then
  AC_CONFIG_SUBDIRS(kde-frontend) 
fi

if test "$enable_motif_frontend" != "no"; then
  AC_CONFIG_SUBDIRS(motif-frontend) 
fi

dnl Check for programs.

AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_MAKE_SET

dnl Check for libraries.

AM_PATH_XML2(2.3.4,
  RCFILE="rcfile.o"
  AC_DEFINE(HAVE_LIBXML2, [], [Define if you have libxml2.])
  )
AC_SUBST(RCFILE)

dnl Check for header files.

AC_HEADER_STDC
AC_CHECK_HEADERS([sys/ioctl.h sys/mount.h])

dnl Declare output files.

AC_CONFIG_FILES([Makefile]
		[src/Makefile]
		[po/Makefile.in]
		[m4/Makefile]
		[doc/Makefile])
AC_OUTPUT
