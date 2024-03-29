dnl Process this file with autoconf to produce a configure script.

AC_INIT([imagination], [3.4],
		[https://sourceforge.net/p/imagination/bugs/])
AC_CONFIG_SRCDIR([src/imagination.h])
AM_INIT_AUTOMAKE

AC_CONFIG_MACRO_DIRS([m4])

# Enable silent rules if supported
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

AM_MAINTAINER_MODE

AC_ISC_POSIX
AC_PROG_CC
AM_PROG_CC_STDC
AC_HEADER_STDC

AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_INTLTOOL

AC_SEARCH_LIBS([sqrtf], [m], ,AC_MSG_ERROR([Unable to find math library]))

# for plugins
AC_DISABLE_STATIC
AM_PROG_LIBTOOL
LIBTOOL="$LIBTOOL --silent"

pkg_modules="gtk+-2.0 >= 2.14.0 gthread-2.0"
PKG_CHECK_MODULES(PACKAGE, [$pkg_modules])

sox_modules="sox >= 14.2.0"
PKG_CHECK_MODULES(SOX, [$sox_modules])

plugins_modules="cairo >= 1.6 glib-2.0 > 2.18.0"
PKG_CHECK_MODULES(PLUGINS, [$plugins_modules])

# get svn revision
REVISION="r0"
if test "x${REVISION}" = "xr0"
then
	SVN=`which svn 2>/dev/null`
	if test -d ".svn" -a "x${SVN}" != "x" -a -x "${SVN}"
	then
		REVISION=r`$SVN info|grep 'Last Changed Rev'|cut -d' ' -f4`
	fi
fi
if test "x${REVISION}" != "xr0"
then
	# force debug mode for a SVN working copy
	CFLAGS="-g -Wall"
else
	REVISION="-1"
fi
AC_DEFINE_UNQUOTED(REVISION, "$REVISION", [subversion revision number])

AC_SUBST(PACKAGE_CFLAGS)
AC_SUBST(PACKAGE_LIBS)

AC_SUBST(SOX_CFLAGS)
AC_SUBST(SOX_LIBS)

AC_SUBST(PLUGINS_CFLAGS)
AC_SUBST(PLUGINS_LIBS)

GETTEXT_PACKAGE=imagination
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE,"$GETTEXT_PACKAGE", [Gettext package.])

AC_PATH_PROG([XSLTPROC], [xsltproc], [yes])

AM_CONDITIONAL([ENABLE_XSLTPROC], [test x"$enable_xsltproc" = x"yes"])

dnl Add the languages which your application supports here.
ALL_LINGUAS="`sed -e '/^#/d' $srcdir/po/LINGUAS`"
AM_GLIB_GNU_GETTEXT

GTK_VERSION=`$PKG_CONFIG --modversion gtk+-2.0`
SOX_VERSION=`$PKG_CONFIG --modversion sox`

AC_OUTPUT([
Makefile
src/Makefile
transitions/Makefile
doc/Makefile
doc/en/Makefile
doc/en/imagination.xml
doc/en/images/Makefile
doc/fr/Makefile
doc/fr/imagination.xml
doc/fr/images/Makefile
doc/es/Makefile
doc/es/imagination.xml
doc/es/images/Makefile
doc/pt_BR/Makefile
doc/pt_BR/imagination.xml
doc/pt_BR/images/Makefile
po/Makefile.in
icons/Makefile
icons/16x16/Makefile
icons/24x24/Makefile
icons/48x48/Makefile
icons/scalable/Makefile
])

echo ""
echo "Imagination configuration:"
echo "--------------------------"
echo ""
echo "Install in  :       ${prefix}/bin"
echo "GTK version :       ${GTK_VERSION}"
echo "SOX version :       ${SOX_VERSION}"
if test "${REVISION}" != "-1"
then
	echo "SVN revision:       ${REVISION}"
fi
echo ""
