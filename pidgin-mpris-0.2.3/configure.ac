AC_PREREQ(2.59)
AC_INIT(pidgin-mpris, 0.2.3, iacobs@m0n5t3r.info)
AM_INIT_AUTOMAKE
AM_MAINTAINER_MODE

AC_PROG_CC
AC_PROG_INSTALL
AC_DISABLE_STATIC

AM_PROG_LIBTOOL
LIBTOOL="$LIBTOOL --silent"
AC_DEFINE(PURPLE_PLUGINS, 1, ["pidgin_plugin"])

PKG_CHECK_MODULES(pidgin, [pidgin >= 2.0.0])
AC_SUBST(pidgin_CFLAGS)
AC_SUBST(pidgin_LIBS)

PKG_CHECK_MODULES(gtk2, [gtk+-2.0 >= 2.4])
AC_SUBST(gtk2_CFLAGS)
AC_SUBST(gtk2_LIBS)

PKG_CHECK_MODULES(dbus, [dbus-1 >= 0.50])
AC_SUBST(dbus_CFLAGS)
AC_SUBST(dbus_LIBS)

PKG_CHECK_MODULES(dbus_glib, [dbus-glib-1 >= 0.50])
AC_SUBST(dbus_glib_CFLAGS)
AC_SUBST(dbus_glib_LIBS)

PIDGIN_INSTALL="`$PKG_CONFIG pidgin --variable=libdir`/pidgin"
AC_SUBST(PIDGIN_INSTALL)

AC_OUTPUT([
	Makefile
	src/Makefile
])
