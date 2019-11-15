AC_PREREQ(2.53)
AC_INIT(qwo, 0.5, http://www.nongnu.org/qwo/)
AM_INIT_AUTOMAKE()
AM_CONFIG_HEADER(config.h)
AM_MAINTAINER_MODE

PKG_PROG_PKG_CONFIG([0.20])

AC_ISC_POSIX
AC_PROG_CC
AC_PROG_CC_STDC
AC_STDC_HEADERS

AC_CHECK_LIB(X11, XOpenDisplay)

AC_CHECK_LIB(Xext, XShapeQueryExtension)

AC_CHECK_LIB(Xtst, XTestFakeKeyEvent)

dnl Check for imlib2 library

AC_CHECK_LIB(Imlib2, imlib_create_image)

dnl Check for libconfig

AC_ARG_ENABLE([config], AS_HELP_STRING([--disable-config],
			  [build without config file support]), [enable_config=$enableval],
			  [enable_config=yes])

if test x$enable_config != xno; then
PKG_CHECK_MODULES([LIBCONFIG], [libconfig],
				  [AC_DEFINE(HAVE_LIBCONFIG, 1, Use libconfig)
					PKG_CHECK_MODULES([LIBCONFIG_NEWER_1_3_2], [libconfig >= 1.3.2],
				  AC_DEFINE(LIBCONFIG_LOOKUP_RETURN_CODE, 1, Is libconfig > 1.3.2),
				  AC_DEFINE(LIBCONFIG_LOOKUP_RETURN_CODE, 0, Is libconfig > 1.3.2))],
				  [echo "libconfig not found" ;])

CFLAGS="$CFLAGS $LIBCONFIG_CFLAGS"
LIBS="$LIBS $LIBCONFIG_LIBS"

fi

dnl Check for help2man

AC_CHECK_PROGS([HELP2MAN], [help2man], [NONE])

if test x"$HELP2MAN" = xNONE; then
	AC_MSG_WARN(["cannot find help2man."])
	AC_MSG_WARN(["You will not be able to generate the manpage."])
fi
AM_CONDITIONAL([HAVE_HELP2MAN], [test x"$HELP2MAN" != xNONE])
AC_SUBST([HELP2MAN])

AC_CONFIG_FILES([
Makefile
src/Makefile
data/Makefile
data/qwo.desktop
data/qwo_control
])

AC_OUTPUT
