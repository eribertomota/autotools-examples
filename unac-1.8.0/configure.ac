#
# Copyright (C) 2000, 2001, 2002, 2003 Loic Dachary <loic@senga.org>
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
# Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
#
AC_INIT(config.h.in)
VERSION=`cat ${srcdir}/.version`
MAJOR_VERSION=[`expr $VERSION : '\([0-9][0-9]*\)'`]
AC_SUBST(MAJOR_VERSION)
MINOR_VERSION=[`expr $VERSION : '[0-9][0-9]*\.\([0-9][0-9]*\)'`]
AC_SUBST(MINOR_VERSION)
MICRO_VERSION=[`expr $VERSION : '[0-9][0-9]*\.[0-9][0-9]*\.\([0-9][0-9]*\)'`]
AC_SUBST(MICRO_VERSION)
AM_INIT_AUTOMAKE([unac], $VERSION, nosubst)
AC_PREREQ(2.50)

AM_CONFIG_HEADER(config.h)

AC_PROG_MAKE_SET

dnl
dnl Unicode version used by unac, as published at http://www.unicode.org/Public/
dnl
UNICODE_VERSION=4.0.0
AC_SUBST(UNICODE_VERSION)

AC_PROG_CC
AC_AIX
AC_COMPILE_WARNINGS

AM_PROG_LIBTOOL

AC_PATH_PROG(PERL, perl, /usr/bin/perl)
AC_PATH_PROG(SH, sh, /bin/sh)

AM_MAINTAINER_MODE

AM_ICONV

AC_CHECK_FUNCS(iconv_open,,AC_MSG_ERROR([
iconv_open not found try to install replacement from
http://www.gnu.org/software/libiconv/
ftp://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.9.1.tar.gz]))

AC_CHECK_FUNCS(vsnprintf)

AC_LIBSOURCES(getopt.c)
AC_CHECK_FUNCS(getopt_long,,[AC_LIBOBJ(getopt)])

AC_CONFIG_FILES([builder], [chmod +x builder])
AC_CONFIG_FILES([t_unac], [chmod +x t_unac])
AC_CONFIG_FILES([Makefile unac.pc unac.spec])
AC_OUTPUT
