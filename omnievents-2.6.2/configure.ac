#                            Package   : omniEvents
# configure.ac               Created   : 2003/10/31
#                            Author    : Alex Tingle
#
#    Copyright (C) 2003-2005 Alex Tingle.
#
#    This file is part of the omniEvents application.
#
#    omniEvents is free software; you can redistribute it and/or
#    modify it under the terms of the GNU Lesser General Public
#    License as published by the Free Software Foundation; either
#    version 2.1 of the License, or (at your option) any later version.
#
#    omniEvents is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
#    Lesser General Public License for more details.
#
#    You should have received a copy of the GNU Lesser General Public
#    License along with this library; if not, write to the Free Software
#    Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
#

# Set up autoheader
AH_BOTTOM([
/* Clean away the PACKAGE_* macros unless they are needed. */
#include "scour.h"
])

# Process this file with autoconf to produce a configure script.
AC_INIT(omniEvents,2.6.2,alex.omnievents@firetree.net)
AC_CONFIG_AUX_DIR(auto)
AC_CONFIG_SRCDIR([src/omniEvents.cc])
AC_CONFIG_HEADER([src/config.h])

ac_omniorbbase="$OMNIORBBASE"

# Checks for programs.
AC_PROG_CXX
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_MAKE_SET

AC_LANG([C++])


# Checks for header files.
AC_FUNC_ALLOCA
AC_HEADER_STDC
AC_CHECK_HEADERS([fcntl.h malloc.h stdlib.h string.h strings.h syslog.h sys/param.h unistd.h process.h signal.h libc.h sys/utsname.h])


# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_C_INLINE
AC_TYPE_SIZE_T


# Checks for C++ features
AC_CXX_NAMESPACES
AC_CXX_HAVE_STL
AC_CXX_STD
AC_CXX_BOOL
AC_CXX_TEMPLATE_REPOSITORY
AC_CXX_PIC_FLAG
AC_CXX_RTTI_FLAG

AC_PROG_CXX_AR
AC_PROG_CXX_LINK_SO_LIB


# Checks for library functions.
AC_FUNC_MALLOC
AC_TYPE_SIGNAL
AC_FUNC_STAT
AC_FUNC_SIGSET
AC_CHECK_FUNCS([gethostname strchr strdup tzset uname getopt on_exit])

# Checks for libraries.

# Corba (Needs to go last, as it sets some libraries that may not run without
# LD_LIBRARY_PATH being set.
AC_CORBA_ORB
AC_CORBA_IDLCOS

# Check for SysV-style init.d directory.
AC_MSG_CHECKING([for SysV-style init.d directory])
if test -d /etc/init.d ; then
  AC_MSG_RESULT([/etc/init.d])
  AC_SUBST(INSTALL_ETC,/etc)
elif test -d /sbin/init.d ; then
  AC_MSG_RESULT([/sbin/init.d])
  AC_SUBST(INSTALL_ETC,/sbin)
else
  AC_MSG_RESULT([no. Using default /etc/init.d])
  AC_SUBST(INSTALL_ETC,/etc)
fi

# Check for SysV-style /etc/default or BSD style /etc/sysconfig directories.
AC_MSG_CHECKING([for SysV or BSD-style config directory])
if test -d /etc/default ; then
  AC_MSG_RESULT([/etc/default])
  AC_SUBST(SYSCONFIG_DIR,/etc/default)
elif test -d /etc/sysconfig ; then
  AC_MSG_RESULT([/etc/sysconfig])
  AC_SUBST(SYSCONFIG_DIR,/etc/sysconfig)
else
  AC_MSG_RESULT([no. Using default /etc/default])
  AC_SUBST(SYSCONFIG_DIR,/etc/default)
fi

if test "x$ac_cv_func_gethostname" = x ; then
  AC_SUBST(HAVE_GETHOSTNAME,no)
else
  AC_SUBST(HAVE_GETHOSTNAME,yes)
fi

# Write a summary of the most important results.
echo             "+-----------------------------------------------------------------------------+"
echo             "| C++       : $CXX"
echo             "| C++ STL   : $ac_cv_cxx_have_stl"
case "$CORBA_ORB" in
  omniORB3) echo "| CORBA ORB : $ac_cv_corba_omniorb3 (omniORB3)" ;;
  omniORB4) echo "| CORBA ORB : $ac_cv_corba_omniorb4 (omniORB4)" ;;
         *) echo "| CORBA ORB : NONE FOUND" ;;
esac
echo             "| omniidl   : $IDL"
if test "x$OMNIORBBASE" != x; then
echo             "+-----------------------------------------------------------------------------+"
  if test "x$OMNIORBBASE" = "x$ac_omniorbbase"; then
    echo         "| NOTE: omniORB search restricted by OMNIORBBASE=$ac_omniorbbase"
    echo         "| To override, try 'unset OMNIORBBASE' or option '--with-omniorb'"
  else
    echo         "| NOTE: omniORB search restricted by --with-omniorb=$OMNIORBBASE"
  fi
fi
echo             "+-----------------------------------------------------------------------------+"

AC_CONFIG_FILES([config.mk etc/init.d/omniorb-eventservice contrib/omniEvents.pc])
AC_OUTPUT
