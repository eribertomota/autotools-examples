#
# $Id: configure.ac,v 1.3 2003/08/19 13:40:06 telka Exp $
#
# Copyright (C) 2002, 2003 ETC s.r.o.
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either version 2
# of the License, or (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA
# 02111-1307, USA.
#
# Written by Marcel Telka <marcel@telka.sk>, 2002, 2003.
#

AC_INIT(libbrux,0.1)

AC_PREREQ(2.54)

AC_CONFIG_AUX_DIR(../tools)

AM_INIT_AUTOMAKE

AC_CONFIG_FILES(
	Makefile
	po/Makefile.in
)

AM_MAINTAINER_MODE

AM_CONFIG_HEADER(config.h)

AC_GNU_SOURCE

AM_GNU_GETTEXT(external)
AM_GNU_GETTEXT_VERSION(0.12.1)

AC_PROG_CC
AC_PROG_RANLIB

AC_ARG_WITH(include,
	AC_HELP_STRING([--with-include=PATH], [Path to the openwince includes]),
	openwince_inc="$withval")

AC_CACHE_CHECK([for the openwince includes], openwince_includes_path, [
	openwince_includes_path="no"
	for openwince_include in $openwince_inc /usr/include/openwince /usr/local/include/openwince; do
		if test -f "$openwince_include/common.h"; then
			openwince_includes_path="$openwince_include"
			break
		fi
	done
])
if test "$openwince_includes_path" = "no"; then
	AC_MSG_ERROR([The openwince include package not found.])
fi
CPPFLAGS="$CPPFLAGS -I$openwince_includes_path -I$openwince_includes_path/device -I$openwince_includes_path/arm"

CFLAGS="$CFLAGS -Wall"
CPPFLAGS="$CPPFLAGS -I\$(top_srcdir)/../include"

AC_OUTPUT
