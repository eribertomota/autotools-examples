# Filename: configure.in

AC_INIT([dgedit], m4_esyscmd([cat version.h | cut -d'"' -f2 | xargs echo -n]))dnl"

AC_CONFIG_SRCDIR([src/dgedit.cc])
AM_INIT_AUTOMAKE

AC_PROG_CXX
#AM_PROG_CC_C_O

AC_PROG_LIBTOOL
AM_PROG_LIBTOOL

AM_CONFIG_HEADER(config.h)
AC_STDC_HEADERS

need_jack=no

dnl ======================
dnl Init pkg-config
dnl ======================
PKG_PROG_PKG_CONFIG(0.23)

HUGIN_PARM="-DDISABLE_HUGIN"
AC_ARG_WITH(debug,  [  --with-debug            Build with debug support])
if test x$with_debug == xyes; then
    AC_MSG_WARN([*** Building with debug support!])
    CXXFLAGS="$CXXFLAGS -Wall -Werror -g"
    HUGIN_PARM=""
fi
CXXFLAGS="$CXXFLAGS $HUGIN_PARM"


dnl ======================
dnl Check for Qt
dnl ======================
PKG_CHECK_MODULES(QT, Qt5Widgets Qt5Core Qt5Gui Qt5Xml >= 5.0)
AC_CHECK_PROGS(QT_MOC, [moc5 moc-qt5 moc], [])
AC_CHECK_PROGS(QT_RCC, [rcc5 rcc-qt5 rcc], [])
AC_CHECK_PROGS(QT_UIC, [uic5 uic-qt5 uic], [])
if (test "$QT_MOC" = ""); then
  AC_MSG_ERROR([QT5 moc is required.])
fi
if (test "$QT_RCC" = ""); then
  AC_MSG_ERROR([QT5 rcc is required.])
fi
if (test "$QT_UIC" = ""); then
  AC_MSG_ERROR([QT5 uic is required.])
fi
CXXFLAGS="$CXXFLAGS -fPIC"
CXXFLAGS="$CXXFLAGS -std=c++14"

dnl ======================
dnl Check for libao
dnl ======================
PKG_CHECK_MODULES(AO, ao >= 0.8.8)

dnl ======================
dnl Check for sndfile
dnl ======================
PKG_CHECK_MODULES(SNDFILE, sndfile >= 1.0.20)

AC_SUBST(CFLAGS)
AC_SUBST(CPPFLAGS)
AC_SUBST(CXXFLAGS)
AC_SUBST(LDFLAGS)

AC_OUTPUT(
	Makefile
	tools/Makefile
	src/Makefile
  icons/Makefile)
