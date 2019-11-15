dnl Copyright (C) 2013, 2017 Ben Asselstine
dnl 
dnl Copying and distribution of this file, with or without modification,
dnl are permitted in any medium without royalty provided the copyright
dnl notice and this notice are preserved.  This file is offered as-is,
dnl without any warranty.
#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_INIT([licenseutils],[0.0.9],[http://sv.nongnu.org/bugs/?group=licenseutils])
AC_CONFIG_AUX_DIR([build-aux])
AM_INIT_AUTOMAKE
AC_PREREQ(2.60)
AM_CONFIG_HEADER(config.h:config.in)
AC_CONFIG_SRCDIR([src/main.c])

# Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_PROG_LIBTOOL

# Checks for header files.
AC_HEADER_STDC

PROGRAM="licensing"
AC_SUBST(PROGRAM)

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_SIZE_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_REALLOC

gl_EARLY
gl_INIT

libcurl_min_version=7.10.0
libcurl_min_vernum=070A00
AC_CHECK_PROGS(PKG_CONFIG, pkg-config)
if test "X$PKG_CONFIG" = X; then
          AC_MSG_ERROR(Please install pkg-config from http://pkg-config.freedesktop.org/)
fi

LIBCURL_MIN_VERSION=$libcurl_min_version
AC_SUBST(LIBCURL_MIN_VERSION)

AC_ARG_WITH(curl-config, [  --with-curl-config=PATH   Location of libcurl curl-config []], curl_config="$withval", curl_config="")

if test "X$curl_config" != "X" ; then
          AC_MSG_WARN(Ignoring --with-curl-config parameter: using pkg-config now)
fi

AC_MSG_CHECKING(for libcurl)
if $PKG_CONFIG libcurl --exists; then
        :
else
        AC_MSG_RESULT(no - not found)
        AC_MSG_ERROR(Please install version 1.5 or newer)
fi

LIBS="$LIBS `$PKG_CONFIG libcurl --libs`"
CFLAGS="`$PKG_CONFIG libcurl --cflags` $CFLAGS"

PKG_CHECK_MODULES(LIBPNG, [libpng >=  1.2.49])
AC_SUBST(LIBPNG_CFLAGS)
AC_SUBST(LIBPNG_LIBS)

LIBS="$LIBS `$PKG_CONFIG libcurl --libs`"
CFLAGS="`$PKG_CONFIG libcurl --cflags` $CFLAGS"

PKG_CHECK_MODULES(GLIB, [glib-2.0 >= 2.10])
AC_SUBST(GLIB_CFLAGS)
AC_SUBST(GLIB_LIBS)

dnl Internationalization macros.
# to update a to a new version of gettext, run:
# gettextize -f -c
AM_GNU_GETTEXT_VERSION([0.19.8])
AM_GNU_GETTEXT([external])

INTERPRETER=lu-sh
AC_SUBST(INTERPRETER)

AC_SUBST(bash_completiondir)
bash_completiondir=$sysconfdir/bash_completion.d

AC_ARG_WITH([bash-completion],
  AS_HELP_STRING([--with-bash-completion@<:@=DIR@:>@], [install bash_completion conf file (default is yes) - it is possible to specify bash_completion's config file directory (default is SYSCONFDIR/bash_completion.d)]),
  [
    if test "$withval" = "no"; then
      BASH_COMPLETION_DIR=""
    elif test "$withval" = "yes"; then
      BASH_COMPLETION_DIR=$sysconfdir/bash_completion.d
    else
      BASH_COMPLETION_DIR="$withval"
    fi
  ],
  [BASH_COMPLETION_DIR=$sysconfdir/bash_completion.d])

AC_ARG_WITH([bash-completion],
  AS_HELP_STRING([--with-bash-completion@<:@=DIR@:>@], [install bash_completion conf file (default is yes) - it is possible to specify bash_completion's config file directory (default is SYSCONFDIR/bash_completion.d)]),
  [
    if test "$withval" = "no"; then
      BASH_COMPLETION_DIR=""
    elif test "$withval" = "yes"; then
      BASH_COMPLETION_DIR=$sysconfdir/bash_completion.d
    else
      BASH_COMPLETION_DIR="$withval"
    fi
  ],
  [BASH_COMPLETION_DIR=$sysconfdir/bash_completion.d])

AC_SUBST(BASH_COMPLETION_DIR)
bash_completiondir="${BASH_COMPLETION_DIR}"
AM_CONDITIONAL(USE_BASH_COMPLETION, test "${BASH_COMPLETION_DIR}" != "")

dnl GNU help2man creates man pages from --help output; in many cases, this
dnl is sufficient, and obviates the need to maintain man pages separately.
dnl However, this means invoking executables, which we generally cannot do
dnl when cross-compiling, so we test to avoid that (the variable
dnl "cross_compiling" is set by AC_PROG_CC).
AS_IF([test $cross_compiling = no], [
  AM_MISSING_PROG([HELP2MAN], [help2man])
], [
  HELP2MAN=:
])

m4_include([styles.ac])
echo "supported comment styles: $enable_commenting_styles"

AC_PROG_CXX
PKG_CHECK_MODULES(SRCHILITE, [source-highlight >= 3.0.0])
AC_SUBST(SRCHILITE_CFLAGS)
AC_SUBST(SRCHILITE_LIBS)

eval LICENSEUTILS_DATADIR="$datadir/licenseutils"
AC_SUBST(LICENSEUTILS_DATADIR)

eval eval DATADIR="$datadir"
AC_SUBST(DATADIR)

AC_CONFIG_FILES([Makefile po/Makefile.in
                 lib/Makefile
                 lang-files/Makefile
                 src/Makefile
                 src/lu-sh
                 src/notice
                 doc/Makefile
                 doc/version.texi
                 tests/Makefile
                 tests/boilerplate/Makefile
                 tests/cbb/Makefile
                 tests/choose/Makefile
                 tests/comment/Makefile
                 tests/copyright/Makefile
                 tests/extra/Makefile
                 tests/png-apply/Makefile
                 tests/prepend/Makefile
                 tests/preview/Makefile
                 tests/project/Makefile
                 tests/top/Makefile
                 tests/uncomment/Makefile
		 po/Makefile])
AC_OUTPUT
