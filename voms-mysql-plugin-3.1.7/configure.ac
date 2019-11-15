# Process this file with autoconf to produce a configure script.
AC_INIT([VOMS MySQL plugin], [3.1.7])
AC_PREREQ(2.57)
AC_PREFIX_DEFAULT("/")
AC_CONFIG_AUX_DIR([./aux])
AC_CONFIG_SRCDIR([src/dbwrap.h])
AC_CONFIG_MACRO_DIR([m4])

AM_INIT_AUTOMAKE
AM_MAINTAINER_MODE

# Notices.
AC_COPYRIGHT([Copyright (c) 2004-2012 Istituto Nazionale di Fisica Nucleare
See LICENCE file for details
])

#Environment.
WORKDIR=`pwd`
AC_SUBST(WORKDIR)

# Checks for programs.
AC_PROG_CC
AC_PROG_CPP
AC_PROG_CXX
AC_PROG_CXXCPP
AC_PROG_LIBTOOL

# Checks for libraries.
AC_CHECK_LIB([mysqlclient], [main])

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([stdlib.h string.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_C_CONST
AC_C_INLINE
AC_TYPE_SIZE_T

# Checks for library functions.
AC_FUNC_ERROR_AT_LINE
AC_FUNC_STAT
AC_FUNC_STRTOD
AC_CHECK_FUNCS([strtol strtoul strtoull])

if test "x$prefix" = xNONE; then
   mypref=$ac_default_prefix
else
   mypref=$prefix
fi

AC_DEFINE_UNQUOTED(PROGPREFIX, "${mypref}", PROGPREFIX)
PPREFIX=${mypref}
AC_SUBST(PPREFIX)

# MySQL dependency check 
have_mysql=no
AC_MYSQL(have_mysql=yes, have_mysql=no)
AC_MSG_RESULT(["MySQL found $have_mysql"])

AM_CONFIG_HEADER([src/autogen/config.h])

AC_CONFIG_FILES([Makefile
                 config/Makefile
                 src/Makefile
                ])
AC_OUTPUT
