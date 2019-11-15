dnl Process this file with autoconf to produce a configure script.
AC_INIT
AC_CONFIG_SRCDIR([src/bbmail.cpp])
AM_INIT_AUTOMAKE(bbmail, 0.9.3)

AC_PREFIX_DEFAULT(/usr/local)

dnl get the debug values right
AC_DEFUN(AC_SET_DEBUG,
[
 test "$CXXFLAGS" = "" && CXXFLAGS="-g -Wall -DDEBUG"
 test "$LDFLAGS" = "" && LDFLAGS=""
])

AC_DEFUN(AC_SET_NODEBUG,
[
 test "$CXXFLAGS" = "" && CXXFLAGS="-O2 -Wall"
 test "$LDFLAGS" = "" && LDFLAGS="-s"
])
      

AC_ARG_ENABLE(debug,[  --enable-debug	create debugging code [default=no]],
[
if test $enableval = "no";
 then AC_SET_NODEBUG
 else AC_SET_DEBUG
fi
],
AC_SET_NODEBUG)

dnl Checks for programs.
dnl needed by configure itsself
AC_PROG_CC
AC_PROG_CXX
AC_PROG_CPP
AC_PROG_INSTALL
AC_PROG_RANLIB
AC_HEADER_STDC
AC_CHECK_HEADERS(ctype.h fcntl.h libgen.h locale.h process.h signal.h stdio.h time.h unistd.h sys/param.h sys/select.h sys/stat.h sys/time.h sys/types.h sys/wait.h)
AC_HEADER_TIME

AC_CHECK_FUNCS(setlocale sigaction strftime)

AC_PATH_X
AC_PATH_XTRA

CFLAGS="$CFLAGS $X_CFLAGS"
CXXFLAGS="$CXXFLAGS $X_CFLAGS"
LDFLAGS="$LDFLAGS $X_LIBS $X_PRE_LIBS"
dnl Checks for X libraries.
AC_CHECK_LIB(X11, XOpenDisplay, LDFLAGS="$LDFLAGS -lX11",
             AC_MSG_ERROR(XOpenDisplay not found in -lX11))

dnl Checks for Xextension
SHAPE=
AC_CHECK_LIB(Xext, XMissingExtension, LIBS="$LIBS -lXext"; SHAPE="-DSHAPE",
             AC_MSG_ERROR(XMissingExtension not found in -lXext))
AC_SUBST(SHAPE)

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_HEADER_TIME
AC_STRUCT_TM

dnl Checks for library functions.
AC_CHECK_FUNCS(select strstr)

dnl pkgconfig checks for blackbox library
PKG_CHECK_MODULES(LIBBT, libbt)
CXXFLAGS="$CXXFLAGS $LIBBT_CFLAGS"
LIBS="$LIBS $LIBBT_LIBS"

dnl generate the config header
AM_CONFIG_HEADER(config.h) 

dnl Print results
AC_MSG_RESULT([])
AC_MSG_RESULT([	$PACKAGE version $VERSION configured successfully.])
AC_MSG_RESULT([])
AC_MSG_RESULT([Using '$prefix' for installation.])
AC_MSG_RESULT([Using '$CXX' for C++ compiler.])
AC_MSG_RESULT([Building with '$CXXFLAGS' for C++ compiler flags.])
AC_MSG_RESULT([Building with '$LIBS' for linker flags.])
AC_MSG_RESULT([])

AC_OUTPUT([
Makefile 
src/Makefile 
data/Makefile 
scripts/Makefile
])

dnl fi
