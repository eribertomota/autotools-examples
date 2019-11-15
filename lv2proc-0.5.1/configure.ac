dnl
dnl NASPRO - The NASPRO Architecture for Sound PROcessing
dnl A simple command line effect processor using LV2 plugins
dnl
dnl Copyright (C) 2011-2014 Stefano D'Angelo
dnl
dnl See the COPYING file for license conditions.
dnl

AC_PREREQ([2.69])

AC_INIT([LV2proc], [0.5.1], [zanga.mail@gmail.com])
AC_COPYRIGHT([Copyright (C) 2011-2014 Stefano D'Angelo])

AC_CONFIG_SRCDIR([src/main.c])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])

AM_INIT_AUTOMAKE

# Command line options.

# Checks for programs.
AC_PROG_CC_C99

# Checks for libraries.
PKG_CHECK_MODULES([SNDFILE], [sndfile])
PKG_CHECK_MODULES([LILV], [lilv-0])

# Checks for header files.
AC_CHECK_HEADERS([math.h], , [AC_MSG_ERROR([C math library header not found.])])

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.
AC_SEARCH_LIBS([roundf], [m], , [AC_MSG_ERROR([C math library not found.])])

# Output.
AC_CONFIG_FILES([Makefile src/Makefile])
AC_OUTPUT
