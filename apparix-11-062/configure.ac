# configure.ac - generated from configure.ac.in by setversion. do not edit
# configure.ac, but edit the master.
# configure.ac - generated from configure.ac.in by setversion. do not edit
# configure.ac, but edit the master.
# $Id: configure.ac.in,v 1.2 2005/10/10 17:53:19 flux Exp $

# Process this file with autoconf to produce a configure script.
AC_PREREQ(2.50)

AC_INIT(apparix, 11-062, mcx-devel@lists.micans.org)
AM_CONFIG_HEADER(config.h)

PACKAGE=$PACKAGE_NAME
VERSION=$PACKAGE_VERSION

AC_CONFIG_SRCDIR([src/apparix.c])
AM_INIT_AUTOMAKE($PACKAGE, $VERSION)
# AM_CONFIG_HEADER(config.h)
# AC_CONFIG_HEADERS([config.h])

# add a `--enable-maintainer-mode' option to `configure'; `maintainer-only' rules turned off by
# default in Makefile.in's
AM_MAINTAINER_MODE

AC_SUBST(PACKAGE)
AC_SUBST(VERSION)

# Checks for programs.
AC_PROG_AWK
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_RANLIB

# Checks for libraries.
# FIXME: Replace `main' with a function in `-lm':
AC_CHECK_LIB([m], [main])

# Checks for header files.
AC_HEADER_STDC
AC_HEADER_SYS_WAIT
AC_CHECK_HEADERS([fcntl.h float.h limits.h stdlib.h string.h ])

AC_CHECK_VA_COPY

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_PID_T

# Checks for library functions.
AC_FUNC_VPRINTF
AC_FUNC_FORK
AC_FUNC_MALLOC
AC_FUNC_MEMCMP
# AC_FUNC_REALLOC
AC_CHECK_FUNCS([dup2 floor memset pow regcomp sqrt strchr strrchr strstr])


# AC_CONFIG_FILES([])
AC_OUTPUT([
  Makefile
  util/Makefile
  src/Makefile
  doc/Makefile
])

