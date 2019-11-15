dnl Process the file with autoconf to generate configure script
dnl Gopal Narayanan <gopal@astro.umass.edu> Apr 27, 2001.
dnl
dnl Updated version number, added CFLAGS - Claudio, May 05, 2002
dnl Modified for use with mingw32, added some more checks - Claudio, May 11, 2002

AC_INIT(src)dnl
AM_INIT_AUTOMAKE(transcalc,0.14)dnl
AM_CONFIG_HEADER(config.h)dnl
dnl try to adopt the new autoconf features
dnl AC_CONFIG_HEADERS(config.h)

dnl Check for programs
AC_PROG_AWK
AC_PROG_CC dnl check for the c compiler
AC_PROG_LN_S

dnl you should add CFLAGS="" here, 'cos it is set to -g by PROG_CC
CFLAGS="-ggdb -O2 -Wall"

AC_CANONICAL_HOST
dnl checks for win32 platforms
AC_MSG_CHECKING([for some Win32 platform])
case "$host" in
  *-*-mingw*|*-*-cygwin*)
    platform_win32=yes
    ;;
  *)
    platform_win32=no
    ;;
esac
AC_MSG_RESULT([$platform_win32])
if test "$platform_win32" = "yes"; then
dnl  AC_DEFINE(PLATFORM_WIN32)
  AC_DEFINE([PLATFORM_WIN32], 1, [Compiling for Win32 platform])
fi

AC_MSG_CHECKING([for native Win32])
case "$host" in
  *-*-mingw*)
    os_win32=yes
    PATHSEP=';'
    ;;
  *)
    os_win32=no
    PATHSEP=':'
    ;;
esac
AC_MSG_RESULT([$os_win32])
AC_SUBST(PATHSEP)
if test "$os_win32" = "yes"; then
dnl   AC_DEFINE(OS_WIN32)
  AC_DEFINE([OS_WIN32], 1, [Check for native Win32])
fi
 
if test "$os_win32" = "yes"; then
  AC_CHECK_PROG(ms_librarian, lib.exe, yes, no)
fi
AM_CONDITIONAL(MS_LIB_AVAILABLE, test x$ms_librarian = xyes)

dnl check for a BSD compatible install 
AC_PROG_INSTALL 
AC_HEADER_STDC

dnl Check for GTK+
if test x$os_win32 = xyes; then
  dnl On Win32, use the gtk-1-3-win32-production branch of GTK+
  dnl which really is like GTK+ 1.2.7 or thereabouts, API-wise.
  PKG_CHECK_MODULES(GTK, gtk+-1.3-win32-production >= 1.3.0)
  dnl and fresh GLib.
  PKG_CHECK_MODULES(GLIB, glib-2.0 >= 1.3.9)
else
  AM_PATH_GTK_2_0(2.2.0,,
    AC_MSG_ERROR(transcalc needs GTK 2.2.0 or higher))

  dnl Quick hack to deny non GTK 1.2
dnl  if (expr $gtk_config_major_version \> 1) > /dev/null; then
dnl    AC_MSG_ERROR(transcalc needs GTK 1.2.7 or higher)
dnl  fi
dnl  if (expr $gtk_config_minor_version \> 2) > /dev/null; then
dnl    AC_MSG_ERROR(transcalc needs GTK 1.2.7 or higher)
dnl  fi
fi

if test x$os_win32 = xyes; then
  case "$CC $CFLAGS " in
    *[[\ \	]]-fnative-struct[[\ \	]]*) ;;
    *) CFLAGS="$CFLAGS -fnative-struct" ;;
  esac
fi

dnl check for libraries
dnl AM_PATH_GTK(1.2.7,,AC_MSG_ERROR(transcalc needs GTK 1.2.7 or higher))dnl

dnl Check for the 'sin' function in -lm:
AC_CHECK_LIB(m, sin)

dnl
dnl Locate the imlib library
dnl
dnl AM_PATH_GDK_IMLIB(1.9.5, AC_DEFINE(HAVE_IMLIB))
dnl As of GTK2.0, we do not need GDK_IMLIB anymore
dnl remove the next three lines
dnl AM_PATH_GDK_IMLIB(1.9.5, AC_DEFINE([HAVE_IMLIB], 1, [Check for Imlib]))
dnl AC_SUBST(GDK_IMLIB_LIBS)
dnl AC_SUBST(GDK_IMLIB_CFLAGS)


dnl Checks for GDK_IMLIB
dnl AC_PATH_PROG(imlibpath, imlib-config)
dnl AC_MSG_CHECKING(for gdk_imlib)
dnl IMLIB_CFLAGS=`$imlibpath --cflags-gdk 2>/dev/null`
dnl IMLIB_LDFLAGS=`$imlibpath --libs-gdk 2>/dev/null`
dnl if test "_$IMLIB_CFLAGS" = _ ; then
dnl dnl   AC_MSG_ERROR([not found, GDK_IMLIB is required. Please consult the
dnl dnl   INSTALL for 
dnl dnl information.])
dnl      AC_MSG_RESULT([**not found, GDK_IMLIB is recommended to show the
dnl      images. Will not load any images.**])
dnl else
dnl    AC_MSG_RESULT(ok)
dnl      LIBS="$LIBS $IMLIB_LDFLAGS"
dnl    CFLAGS="$CFLAGS $IMLIB_CFLAGS"
dnl    AC_DEFINE(HAVE_IMLIB)
dnl    HAVE_IMLIB=`$imlibpath --version`
dnl fi

dnl Checks for header files.
AC_CHECK_HEADERS([stdlib.h string.h sys/wait.h unistd.h pwd.h])

dnl Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_PID_T
AC_HEADER_TIME
AC_CHECK_FUNCS(strcpy bcopy)

# Checks for library functions.
AC_FUNC_FNMATCH
AC_FUNC_MALLOC
AC_FUNC_STAT
# asinh, acosh and atanh seems to be missing from mingw32 (?)
AC_CHECK_FUNCS([floor pow sqrt asinh acosh atanh])

dnl Find the X11 include and library directories
AC_PATH_X
AC_PATH_XTRA

AC_OUTPUT(Makefile
src/Makefile
images/Makefile
examples/Makefile
docs/Makefile)

AC_MSG_RESULT([

$PACKAGE-$VERSION is now configured for $host

  Source directory:     $srcdir
  Installation prefix:  $prefix
  C compiler:           $CC $XTRA_CFLAGS $CFLAGS

])

