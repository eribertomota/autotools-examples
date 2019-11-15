dnl
dnl  NASPRO - The NASPRO Architecture for Sound PROcessing
dnl  Common headers for all ino implementations
dnl
dnl  Copyright (C) 2011, 2012 ino development team
dnl
dnl  See the COPYING file for license conditions.
dnl

AC_PREREQ([2.68])

AC_INIT([ino headers], [0.4.0], [zanga.mail@gmail.com])
AC_COPYRIGHT([Copyright (C) 2011, 2012 ino development team])

AC_CONFIG_SRCDIR([lib.h])
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
AC_ARG_VAR([NATURALDOCS], [path to NaturalDocs executable])
AC_CHECK_PROG([NATURALDOCS], [NaturalDocs], [NaturalDocs])
AM_CONDITIONAL([BUILD_DOC], [test -n "$NATURALDOCS"])

# Checks for libraries.

# Checks for header files.

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

# Output.
AC_CONFIG_FILES([Makefile doc/Makefile ino-headers-0.pc])
AC_OUTPUT
