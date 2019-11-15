#
# Most of this configure script was ripped from pidgin or the
# pidgin-encryption configure script, thanks guys ;)
#

AC_INIT(src/extendedprefs.c)
AC_PREREQ([2.50])

EXTPREFS_VERSION="0.7"
AM_INIT_AUTOMAKE([pidgin-extprefs], $EXTPREFS_VERSION, 'no-define')
AC_DEFINE_UNQUOTED(EXTPREFS_VERSION, "$EXTPREFS_VERSION", [pidgin-extprefs Version])

AC_PATH_PROG(sedpath, sed)
#
# Our header
#

AH_TOP([ /* our header */
#ifndef _EXTPREFS_CONFIG_H
#define _EXTPREFS_CONFIG_H
])
AH_BOTTOM([
#endif /* _EXTPREFS_CONFIG_H */
])

#
# Look for the C compiler
#
CFLAGS_save="$CFLAGS"
AC_PROG_CC
CFLAGS="$CFLAGS_save"

AC_ARG_ENABLE(debug,   [  --enable-debug          compile with debugging support],,enable_debug=no)

if test "x$enable_debug" = "xyes" ; then
	DEBUG_CFLAGS="$DEBUG_CFLAGS"
	AC_DEFINE(DEBUG, 1, [Define if debugging is enabled.])
fi

AC_SUBST(DEBUG_CFLAGS)

if test "x$GCC" = "xyes"; then
	CFLAGS="$CFLAGS -Wall -g3"
fi
AC_SUBST(CFLAGS)

#
# Check for Pidgin
#

PKG_CHECK_MODULES(PURPLE, purple >= 2.0.0,
[
   AC_DEFINE(HAVE_PURPLE, 1, [Define if we've found purple.])
])
PKG_CHECK_MODULES(PIDGIN, pidgin >= 2.0.0,
[
   AC_DEFINE(HAVE_PIDGIN, 1, [Define if we've found pidgin.])
])

AC_SUBST(PURPLE_CFLAGS)
AC_SUBST(PIDGIN_CFLAGS)

#
# check for GTK+ and glib
#

AM_PATH_GLIB_2_0(2.0.0,,AC_MSG_ERROR([
*** GLib 2.0 is required to build pidgin-extprefs; please make sure you have
*** the GLib development headers installed. The latest version of GLib is 
*** always available at http://www.gtk.org/.]))
AC_SUBST(GLIB_CFLAGS)

AM_PATH_GTK_2_0(2.0.0,,AC_MSG_ERROR([
*** GTK+ 2.0 is required to build pidgin-extprefs; please make sure you have
*** the GTK+ development headers installed. The latest version of GTK+ is 
*** always available at http://www.gtk.org/.]))
AC_SUBST(GTK_CFLAGS)

#
# Check if plugins are enabled
#
want_plugins=yes
AM_CONDITIONAL(PLUGINS, test "$want_plugins" = "yes")

#
# Setup libtool
#
AM_PROG_LIBTOOL
LIBTOOL="$LIBTOOL --silent"

#
# Finish up
#
AM_CONFIG_HEADER(pre_config.h)
AC_OUTPUT([Makefile
		   src/Makefile
		  ])

echo;
echo Configuration complete
echo;
echo Debugging enabled..............: $enable_debug
echo;
eval eval echo Extended Preferences will be installed in $libdir.
if eval eval test ! -e ${bindir}/pidgin ; then
	echo;
        echo "Warning: Pidgin is not installed in $prefix.  Plugin may not"
        echo "         be installed to a loadable location."
fi

echo;
echo configure complete, now type \'make\' to compile
echo;
