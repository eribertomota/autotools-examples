dnl  Copyright (C) 2009, 2012, 2014, 2015 Timothy Richard Musson
dnl
dnl  This program is free software; you can redistribute it and/or modify
dnl  it under the terms of the GNU General Public License as published by
dnl  the Free Software Foundation; either version 2, or (at your option)
dnl  any later version.
dnl
dnl  This program is distributed in the hope that it will be useful,
dnl  but WITHOUT ANY WARRANTY; without even the implied warranty of
dnl  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
dnl  GNU General Public License for more details.
dnl
dnl  You should have received a copy of the GNU General Public License
dnl  along with this program; if not, write to the Free Software
dnl  Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA
dnl  02111-1307, USA.


AC_INIT([GNU gxmessage], 3.4.3)
AC_CONFIG_SRCDIR([gxmessage.c])
AM_INIT_AUTOMAKE

AC_PREREQ(2.52)

AM_MAINTAINER_MODE

AM_CONFIG_HEADER(config.h)

AC_ISC_POSIX
AC_PROG_CC
AM_PROG_CC_STDC
AC_HEADER_STDC

AM_GLIB_GNU_GETTEXT
IT_PROG_INTLTOOL([0.50.0])

GETTEXT_PACKAGE=gxmessage
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE, "$GETTEXT_PACKAGE", [gettext package])

AC_SUBST(PACKAGE_CFLAGS)
AC_SUBST(PACKAGE_LIBS)

PKG_CHECK_MODULES(PACKAGE, gtk+-3.0 >= 3.4.0)

AC_OUTPUT([
doc/Makefile
po/Makefile.in
Makefile
])

