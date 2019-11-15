# Process this file with autoconf to produce a configure script.
#
# XPLC - Cross-Platform Lightweight Components
# Copyright (C) 2000-2002, Pierre Phaneuf
# Copyright (C) 2002-2004, Net Integration Technologies, Inc.
#
#
# This library is free software; you can redistribute it and/or modify
# it under the terms of the GNU Lesser General Public License as
# published by the Free Software Foundation; either version 2.1 of the
# License, or (at your option) any later version.
#
# This library is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# Lesser General Public License for more details.
#
# You should have received a copy of the GNU Lesser General Public
# License along with this library; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307
# USA

AC_INIT(XPLC, 0.3.13, pp@ludusdesign.com)
AC_REVISION($Id: configure.ac,v 1.41 2005/10/31 23:19:35 pphaneuf Exp $)

AC_CANONICAL_HOST

AC_ARG_ENABLE(debug,
              AC_HELP_STRING([--enable-debug],
                             [debugging options]))

AC_ARG_ENABLE(fatal-warnings,
              AC_HELP_STRING([--enable-fatal-warnings],
                             [turn warnings into errors]))

AC_ARG_ENABLE(optimization,
              AC_HELP_STRING([--disable-optimization],
                             [optimization options]))

AC_ARG_ENABLE(warnings,
              AC_HELP_STRING([--disable-warnings],
                             [extra warnings]))

AC_ARG_ENABLE(unstable,
              AC_HELP_STRING([--enable-unstable],
                             [allow unstable interfaces in stable version]))

AC_ARG_ENABLE(rtti,
              AC_HELP_STRING([--enable-rtti],
                             [C++ run-time type identification (compiler)]))

AC_ARG_ENABLE(exceptions,
              AC_HELP_STRING([--enable-exceptions],
                             [C++ exceptions (compiler)]))

AC_ARG_ENABLE(pic,
              AC_HELP_STRING([--disable-pic],
                             [generation of position-independent code]))

AC_ARG_ENABLE(loader,
              AC_HELP_STRING([--disable-loader],
                             [dynamic loading]))

AC_ARG_WITH(dlopen,
            AC_HELP_STRING([--with-dlopen],
                           [dlopen]))

AC_ARG_WITH(dyld,
            AC_HELP_STRING([--with-dyld],
                           [dyld]))

AC_ARG_WITH(libuuid,
            AC_HELP_STRING([--with-libuuid],
                           [libuuid]))

AC_CONFIG_SRCDIR([include/xplc/xplc.h])

AC_LANG(C++)

AC_PROG_CC
AC_PROG_CXX
AC_PROG_INSTALL
AC_PROG_LN_S

AC_HEADER_DIRENT
AC_CHECK_HEADERS([limits.h])

AC_CHECK_PROGS([CVS2CL], [cvs2cl.pl cvs2cl], [no])

case "$host_os" in
darwin*|rhapsody*)
    so_style=darwin
    ;;
*)
    so_style=sysv
    ;;
esac

# Make sure we link in libc.
LDFLAGS="$LDFLAGS -lc"

if test "$with_dlopen" != "no"; then
    AC_CHECK_HEADERS(dlfcn.h)
    AC_SEARCH_LIBS(dlopen, dl, with_dlopen=$ac_cv_search_dlopen, with_dlopen=no)
    test "$with_dlopen" = "none required" && with_dlopen=
    test "$with_dlopen" = "no" || AC_DEFINE(WITH_DLOPEN, 1, [Define if you have dlopen.])
fi

if test "$with_dyld" != "no"; then
    AC_CHECK_HEADERS(mach-o/dyld.h)
    AC_SEARCH_LIBS(NSCreateObjectFileImageFromFile, System, with_dyld=$ac_cv_search_NSCreateObjectFileImageFromFile, with_dyld=no)
    test "$with_dyld" = "none required" && with_dyld=
    test "$with_dyld" = "no" || AC_DEFINE(WITH_DYLD, 1, [Define if you have dyld.])
fi

# dyld not really supported yet
if test "$with_dlopen" = "no" && test "$with_dyld" = "no"; then
    enable_loader=no
fi

if test "$enable_loader" != "no"; then
    AC_DEFINE(ENABLE_LOADER, 1, [Define if you want to enable dynamic loading.])
fi

dnl Do some checks for uuid/ since no native library is available
with_uuid=no
if test "$with_uuid" == "no" && test "$with_libuuid" != "no"; then
    AC_CHECK_HEADERS(uuid/uuid.h,
		     AC_CHECK_LIB(uuid, uuid_unparse,
				  with_uuid=-luuid))
fi
if test "$with_uuid" == "no"; then
    AC_CHECK_SIZEOF(short)
    AC_CHECK_SIZEOF(int)
    AC_CHECK_SIZEOF(long)
    AC_CHECK_SIZEOF(long long)
    SIZEOF_SHORT=$ac_cv_sizeof_short
    SIZEOF_INT=$ac_cv_sizeof_int
    SIZEOF_LONG=$ac_cv_sizeof_long
    SIZEOF_LONG_LONG=$ac_cv_sizeof_long_long
    AC_SUBST(SIZEOF_SHORT)
    AC_SUBST(SIZEOF_INT)
    AC_SUBST(SIZEOF_LONG)
    AC_SUBST(SIZEOF_LONG_LONG)
    AC_CHECK_HEADERS([inttypes.h stdlib.h unistd.h])
    AC_CHECK_HEADERS([net/if.h net/if_dl.h netinet/in.h])
    AC_CHECK_HEADERS([sys/ioctl.h sys/socket.h sys/sockio.h])
    AC_CHECK_FUNCS(srandom)
    AC_CHECK_MEMBER(struct sockaddr.sa_len,
		    AC_DEFINE_UNQUOTED(HAVE_SA_LEN,
				       1,
				       [Define if struct sockaddr contains sa_len]),,
		    [#include <sys/typesDD.h>
	             #include <sys/socket.h>])
    with_uuid=
    with_uuid_static=uuid/libuuid.a
fi

if test "$enable_optimization" != "no"; then
    CFLAGS="$CFLAGS -O2"
fi

if test -z "$enable_debug"; then
    enable_debug=no
fi

if test "$enable_debug" != "no"; then
    CFLAGS="$CFLAGS -ggdb -DDEBUG"
    if test "$enable_debug" != "yes"; then
        CFLAGS="$CFLAGS -DDEBUG_$enable_debug"
    fi
else
    CFLAGS="$CFLAGS -DNDEBUG"
fi

if test "$enable_fatal_warnings" = "yes"; then
    CFLAGS="$CFLAGS -Werror"
fi

if test "$enable_warnings" != "no"; then
    CFLAGS="$CFLAGS -Wall"
    CXXFLAGS="$CXXFLAGS -Woverloaded-virtual"
    if test "$enable_warnings" = "yes"; then
        CXXFLAGS="$CXXFLAGS -Wold-style-cast"
    fi
fi

if test "$enable_rtti" != "yes"; then
    CXXFLAGS="$CXXFLAGS -fno-rtti"
fi

if test "$enable_exceptions" != "yes"; then
    CXXFLAGS="$CXXFLAGS -fno-exceptions"
fi

if test "$enable_pic" != "no"; then
    CFLAGS="$CFLAGS -fpic"
fi

pc_version=
xplcdir_version=
lib_prefix_version=
if test "$(echo $PACKAGE_VERSION | awk -F. '{ print $2 % 2}')" -eq 1; then
    enable_unstable=yes
    pc_version="-${PACKAGE_VERSION}"
    xplcdir_version="/xplc-${PACKAGE_VERSION}"
    lib_prefix_version="../"
fi

if test "$enable_unstable" = "yes"; then
    CFLAGS="$CFLAGS -DUNSTABLE"
fi

CXXFLAGS="$CXXFLAGS $CFLAGS"

AC_SUBST(pc_version)
AC_SUBST(xplcdir_version)
AC_SUBST(lib_prefix_version)
AC_SUBST(enable_loader)
AC_SUBST(with_dlopen)
AC_SUBST(so_style)
AC_SUBST(with_uuid)
AC_SUBST(with_uuid_static)
AC_SUBST(CVS2CL)

AC_CONFIG_FILES([config/config.mk])
AC_CONFIG_FILES([dist/xplc.pc dist/xplc-uninstalled.pc])
AC_CONFIG_FILES([examples/simple-module/Makefile])
AC_CONFIG_FILES([examples/simple-module-user/Makefile])
AC_CONFIG_FILES([uuid/uuid_types.h])
AC_CONFIG_HEADERS([include/autoconf.h])

AC_OUTPUT

if test "$(echo $PACKAGE_VERSION | awk -F. '{ print $2 % 2}')" -eq 1; then
    AC_MSG_WARN([Unstable release, the API might change in the next release.])
fi

if test "$enable_loader" = "no"; then
    AC_MSG_WARN([Dynamic loading is disabled.])
fi

