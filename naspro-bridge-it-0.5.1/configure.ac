dnl
dnl NASPRO - The NASPRO Architecture for Sound PROcessing
dnl LV2 bridging helper library
dnl
dnl Copyright (C) 2007-2014 Stefano D'Angelo
dnl
dnl See the COPYING file for license conditions.
dnl

AC_PREREQ([2.69])

AC_INIT([NASPRO Bridge it], [0.5.1], [zanga.mail@gmail.com])
AC_COPYRIGHT([Copyright (C) 2007-2014 Stefano D'Angelo])

AC_CONFIG_SRCDIR([src/internal.h])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])

AM_INIT_AUTOMAKE

# Command line options.
AC_MSG_CHECKING([where to put pkg-config's .pc files])
AC_ARG_WITH([pkgconfigdir],
	    AS_HELP_STRING([--with-pkgconfigdir=DIR],
	    [where to put pkg-config's .pc files @<:@LIBDIR/pkgconfig@:>@]),
	    [pkgconfigdir="${withval}"], [pkgconfigdir="${libdir}/pkgconfig"])
AC_SUBST([pkgconfigdir])
AC_MSG_RESULT([$pkgconfigdir])

# Checks for programs.
AC_PROG_CC_C99
AC_LIBTOOL_WIN32_DLL
AC_PROG_LIBTOOL

AC_ARG_VAR([NATURALDOCS], [path to NaturalDocs executable])
AC_CHECK_PROGS([NATURALDOCS], [NaturalDocs naturaldocs])
AM_CONDITIONAL([BUILD_DOC], [test -n "$NATURALDOCS"])

# Checks for libraries.
PKG_CHECK_MODULES([NACORE], [nacore-5 >= 0.4.0])

# Checks for header files.
PKG_CHECK_MODULES([LV2], [lv2 >= 1.0.0])

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

# Output.
LT_CURRENT=3
LT_REVISION=0
LT_AGE=0
AC_SUBST([LT_CURRENT])
AC_SUBST([LT_REVISION])
AC_SUBST([LT_AGE])

AC_CONFIG_FILES([Makefile nabrit-3.pc doc/Makefile include/Makefile \
		 src/Makefile])
AC_OUTPUT
