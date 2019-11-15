#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.61)
AC_INIT([ffe], [0.3.9], [tjsa@iki.fi])
AC_CONFIG_SRCDIR([src/ffe.c])
AC_CONFIG_HEADER([config.h])
AC_CONFIG_AUX_DIR([config])
AC_GNU_SOURCE
AM_INIT_AUTOMAKE

AC_SUBST([VERSION])
ISODATE=`date +%Y-%m-%d`
AC_SUBST([ISODATE])

SHELL_CMD="/bin/sh"
AC_SUBST([SHELL_CMD])

AC_CANONICAL_HOST
AC_DEFINE_UNQUOTED([HOST],["$host"],[Host type.])
AC_DEFINE_UNQUOTED([BUILD_DATE],["$ISODATE"],[Build date.])
AC_DEFINE_UNQUOTED([SHELL_CMD],["$SHELL_CMD"],[Define to the shell for command substitution and input preprosessing.])

# Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL

# Checks for libraries.
# when compiling for mingw32 the AM_PATH_LIBGCRYPT gives false positive
if test "x$cross_compiling" = xno; then
    AM_PATH_LIBGCRYPT([],[AC_DEFINE(HAVE_WORKING_LIBGCRYPT, 1, [Define to 1 if gcrypt is working.])],[])
fi


# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([fcntl.h features.h error.h errno.h getopt.h regex.h signal.h gcrypt.h printf.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_INLINE
AC_C_CONST
AC_TYPE_PID_T
AC_SYS_LARGEFILE
AC_SYS_LONG_FILE_NAMES
AC_CHECK_TYPE([regex_t],[AC_DEFINE(HAVE_REGEX, 1, [Define to 1 if regex functions are available])],,[#if HAVE_REGEX_H
#include <regex.h>
#endif])
AC_TYPE_INT16_T
AC_TYPE_INT32_T
AC_TYPE_INT64_T
AC_TYPE_INT8_T
AC_TYPE_SIZE_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T
AC_TYPE_UINT8_T


# Checks for library functions.
AC_FUNC_FORK
AC_CHECK_FUNCS([atexit dup2 pipe tempnam setenv putenv setmode strcasecmp sigaction parse_printf_format])
AC_CHECK_FUNCS([strchr strdup strerror strstr getline getopt_long regcomp strncasecmp strcasestr])

AC_CONFIG_FILES([Makefile
                 doc/Makefile
                 src/Makefile])
AC_OUTPUT
