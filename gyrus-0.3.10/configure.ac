dnl Process this file with autoconf to produce a configure script.

AC_PREREQ(2.52)
AC_INIT([gyrus],[0.3.10],[http://bugzilla.gnome.org/enter_bug.cgi?product=gyrus])

AM_INIT_AUTOMAKE([1.9])
AM_MAINTAINER_MODE

AC_CONFIG_HEADERS([config.h])

dnl check for programs
IT_PROG_INTLTOOL([0.40.0])
AC_ISC_POSIX
AC_PROG_CC
AM_PROG_CC_STDC
AC_HEADER_STDC

AC_PATH_PROG(GLIB_GENMARSHAL, glib-genmarshal)

dnl GNOME 2 force flags

GNOME_COMPILE_WARNINGS(maximum)

GTK_REQUIRED=2.18.0
GIO_REQUIRED=2.22.0
GCONF_REQUIRED=2.0.0
GTK_PRINT_REQUIRED=2.10.0
GNUTLS_REQUIRED=1.0.0

PKG_CHECK_MODULES(GYRUS,
                  gtk+-2.0 >= $GTK_REQUIRED
		  gio-2.0 >= $GIO_REQUIRED
		  gconf-2.0 >= $GCONF_REQUIRED
		  gtk+-unix-print-2.0 >= $GTK_PRINT_REQUIRED)

AC_ARG_ENABLE(gnutls,
              AC_HELP_STRING([--enable-gnutls],
			     [Build with gnutls support (default=no)]),,
			     enable_gnutls=no)
if test "x$enable_gnutls" = "xyes"; then
  PKG_CHECK_MODULES(GNUTLS, gnutls >= $GNUTLS_REQUIRED)
  AC_DEFINE(HAVE_GNUTLS, [], [Defined if we have gnutls])
fi

dnl --enable-tests=(yes|no)
AC_ARG_ENABLE(tests,
              AC_HELP_STRING([--enable-tests],
                             [Enable building test programs (default=no)]),,
              enable_tests=no)
AM_CONDITIONAL(GYRUS_ENABLE_TESTS, test "x$enable_tests" = "xyes")


GYRUS_CFLAGS="$GYRUS_CFLAGS $GNUTLS_CFLAGS -Wall"
GYRUS_LIBS="$GYRUS_LIBS $GNUTLS_LIBS"

AC_SUBST(GYRUS_CFLAGS)
AC_SUBST(GYRUS_LIBS)

dnl Internacionalization macros
GETTEXT_PACKAGE=gyrus
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED([GETTEXT_PACKAGE],["$GETTEXT_PACKAGE"],[Gettext translation domain])

AM_GLIB_GNU_GETTEXT

AC_OUTPUT([
gyrus.desktop.in
Makefile
src/Makefile
src/ui/Makefile
src/pixmaps/Makefile
po/Makefile.in
tests/Makefile
])
