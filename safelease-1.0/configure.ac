#
# Copyright 2014 Red Hat, Inc.
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
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA
#
# Refer to the README and COPYING files for full details of the license
#

AC_PREREQ([2.69])
AC_INIT([safelease], [1.0], [devel@ovirt.org])
AM_INIT_AUTOMAKE([1.13 foreign -Wall -Werror])
AC_PROG_CC
AC_CONFIG_SRCDIR([src/safelease.c])
AC_CONFIG_HEADERS([config.h])

AC_CHECK_HEADERS([fcntl.h stdlib.h string.h sys/time.h unistd.h])

AC_C_INLINE
AC_TYPE_OFF_T

AC_CHECK_FUNCS([alarm gettimeofday memset strerror strrchr strtoul strtoull])

AC_SUBST([safeleaselibexecdir], ['${bindir}'])

AC_CONFIG_FILES([Makefile src/Makefile])
AC_OUTPUT

