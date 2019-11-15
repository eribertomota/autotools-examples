dnl ##
dnl ##  configure.ac -- Autoconf source for GNU shtool
dnl ##  Copyright (c) 1999-2008 Ralf S. Engelschall <rse@engelschall.com>
dnl ##
dnl ##  This file is part of shtool and free software; you can redistribute
dnl ##  it and/or modify it under the terms of the GNU General Public
dnl ##  License as published by the Free Software Foundation; either version
dnl ##  2 of the License, or (at your option) any later version.
dnl ##
dnl ##  This file is distributed in the hope that it will be useful,
dnl ##  but WITHOUT ANY WARRANTY; without even the implied warranty of
dnl ##  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
dnl ##  General Public License for more details.
dnl ##
dnl ##  You should have received a copy of the GNU General Public License
dnl ##  along with this program; if not, write to the Free Software
dnl ##  Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307,
dnl ##  USA, or contact Ralf S. Engelschall <rse@engelschall.com>.
dnl ##

AC_PREREQ(2.53)
AC_REVISION($1.0$)
AC_INIT(README)

SHTOOL_VERSION_STR="`sh sh.version -l txt -d long VERSION`"
sh sh.echo -e "Configuring %BGNU shtool%b (Portable Shell Tool), version %B${SHTOOL_VERSION_STR}%b"
echo "Copyright (c) 1994-2008 Ralf S. Engelschall <rse@engelschall.com>"
AC_SUBST(SHTOOL_VERSION_STR)

AC_PREFIX_DEFAULT(/usr/local)
AC_SET_MAKE

AC_MSG_CHECKING(for perl interpreter)
PERL=`sh sh.path -m perl`
AC_SUBST(PERL)
AC_MSG_RESULT($PERL)
if test ".$PERL" = .; then
    echo "$0:Error: no perl interpreter found" 1>&2
    exit 1
fi

AC_MSG_CHECKING(for pod2man conversion tool)
perldir=`sh sh.path -d $PERL`
POD2MAN=`sh sh.path -m -p "${perldir}:${PATH}" pod2man`
AC_SUBST(POD2MAN)
AC_MSG_RESULT($POD2MAN)
if test ".$POD2MAN" = .; then
    echo "$0:Error: no pod2man tool found" 1>&2
    exit 1
fi

AC_CONFIG_FILES(Makefile shtoolize)
AC_CONFIG_COMMANDS([adjustment], [chmod a+x shtoolize])
AC_OUTPUT

