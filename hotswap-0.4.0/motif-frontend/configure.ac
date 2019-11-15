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
AM_INIT_AUTOMAKE(xhotswap, 0.4.0)
AC_SUBST(VERSION)
ISODATE=`date +%Y-%m-%d`
AC_SUBST(ISODATE)

AM_GNU_GETTEXT([external])

dnl Check for programs.

AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_MAKE_SET

dnl Check for header files.

AC_HEADER_STDC

dnl Check for system services.

AC_PATH_XTRA
if test "$no_x" = "yes"; then
  AC_MSG_ERROR(This program requires the X Window System.)
fi

TS_PATH_MOTIF_EXTRA
if test "$no_motif" = "yes"; then
  AC_MSG_ERROR(This program requires Motif.)
fi

dnl Declare output files.

AC_CONFIG_FILES([Makefile]
		[src/Makefile]
		[m4/Makefile]
		[doc/Makefile]
		[po/Makefile.in])
AC_OUTPUT
