#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

# Copyright (c) 2002  Leon Bottou and Yann Le Cun. (DjVuLibre-3.5)
# Copyright (c) 2001  AT&T (DjVuLibre-3.5)
# Copyright (C) 2007, 2008, 2009, 2014  Sylvain Beucler

# This file is part of GNU FreeDink

# GNU FreeDink is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3 of the License, or
# (at your option) any later version.

# GNU FreeDink is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program.  If not, see
# <http://www.gnu.org/licenses/>.

AC_PREREQ(2.61)
AC_INIT([DFArc],[3.14],[bug-freedink@gnu.org])
AC_CONFIG_AUX_DIR(autotools)
AC_CONFIG_HEADER([config.h])
AM_INIT_AUTOMAKE([gnits dist-zip])
# Terse output - use V=1 for verbose output
AM_SILENT_RULES(yes)

# Define $host $host_os + distributes config.guess and config.sub
AC_CANONICAL_HOST

# We use wxWidget's internal gettext-compatible functions, calling
# AM_PO_SUBDIRS directly (otherwise GETTEXT wants intl/ and such):
##AM_GNU_GETTEXT()
AM_PO_SUBDIRS()
# This one is for .desktop files:
# Note: IT_PROG_INTLTOOL quits if intltool/gettext dependency isn't satisfied :/
AC_SUBST(GETTEXT_PACKAGE, $PACKAGE_TARNAME)
IT_PROG_INTLTOOL(0.31, no-xml)

# Checks for programs.
AC_PROG_CXX
# TODO: error if CXX cannot be found
AC_PROG_LN_S
AC_ARG_VAR([WXGLADE], [Compiler for UI files (.wxg -> .cpp)])
AC_PATH_PROG(WXGLADE, wxglade)
if test x"$WXGLADE" = x""; then
  AC_MSG_WARN([You may need to install wxGlade (if you're a developer)])
  LACK_WXGLADE=1
fi
AM_CONDITIONAL(HAVE_WXGLADE, test "$WXGLADE" != "")

AC_CHECK_TOOL(WINDRES, windres)
AM_CONDITIONAL(HAVE_WINDRES, test "$WINDRES" != "")

AC_ARG_VAR([UPX], [Produce self-decompressing executables (if --enable-upx)])
AC_ARG_ENABLE([upx],
  AS_HELP_STRING([--enable-upx], [compress executables [[default is disabled]]]),
  [], [enable_upx=no])
if test x"$enable_upx" = x"yes"; then
  AC_PATH_PROG(UPX, upx)
fi
AM_CONDITIONAL(HAVE_UPX, test "$UPX" != "")


# Dynamic and static builds
# Dynamic and static builds
AC_ARG_ENABLE([static],
  AS_HELP_STRING([--enable-static],[embed wxWidgets and libbz2 in the executable (mingw32 only) [[default is disabled]]]),
  [], [enable_static=no])

if test x"$enable_static" = x"yes"; then
    case "${host}" in
    # (cf. (autoconf.info)Using System Type)
    # Modified to accept "biplet" instead of "triplet", because at
    # least Debian's MinGW package uses i586-mingw32msvc (instead of
    # i586-pc-mingw32msvc)
    *-*-go32* | *-mingw32* | *-*-cygwin* | *-*-windows*)
        LDFLAGS="$LDFLAGS -static"
        ;;
    esac
fi
# TODO: check with Cygwin + -mno-cygwin



# ----------------------------------------
# Desktop files
# ----------------------------------------
# (inspired by djvulibre's configure.ac)

ac_desktopfiles=yes
AC_ARG_ENABLE(desktopfiles,
    AS_HELP_STRING([--disable-desktopfiles],[Do not install scripts to register icons and menus.]),
    [ac_desktopfiles=$enableval])

# Check for xdg tools
AC_PATH_PROG(XDG_MIME, xdg-mime)
AC_PATH_PROG(XDG_ICON_RESOURCE, xdg-icon-resource)
AC_PATH_PROG(XDG_DESKTOP_MENU, xdg-desktop-menu)
if test -x "${XDG_MIME}" && \
   test -x "${XDG_ICON_RESOURCE}" && \
   test -x "${XDG_DESKTOP_MENU}"
then 
  true
elif test "$ac_desktopfiles" != no ; then
  ac_desktopfiles=no
  AC_MSG_WARN([Cannot find the Xdg Portland tools.
--------------------------------------------------------
*** The scripts to register icons and menus 
*** will not be installed.
--------------------------------------------------------])
fi

AM_CONDITIONAL(HAVE_XDG, test "${ac_desktopfiles}" != "no")


# Checks for libraries.
AC_CHECK_LIB([bz2], [BZ2_compressBlock],,AC_MSG_WARN([You need to install libbz2]); LACK_LIBBZ2=1)

# http://www.wxwidgets.org/wiki/index.php/Autoconf
AM_OPTIONS_WXCONFIG
reqwx=3.0.0
if test x"$enable_static" = x"yes"; then
# Not using $WX_LIBS_STATIC (deprecated anyway) because CFLAGS also
# change, using '--static' instead:
AM_PATH_WXCONFIG($reqwx, [wxWin=1], [wxWin=0], [core], [--static])
else
AM_PATH_WXCONFIG($reqwx, [wxWin=1], [wxWin=0], [core], [])
fi

if test "$wxWin" != 1; then
	AC_MSG_ERROR([
		wxWidgets must be installed on your system.
 
		Please check that wx-config is in path, the directory
		where wxWidgets libraries are installed (returned by
		'wx-config --libs' or 'wx-config --static --libs' command)
		is in LD_LIBRARY_PATH or equivalent variable and
		wxWidgets version is $reqwx or above.
		])
fi
 
CPPFLAGS="$CPPFLAGS $WX_CPPFLAGS"
CXXFLAGS="$CXXFLAGS $WX_CXXFLAGS_ONLY"
CFLAGS="$CFLAGS $WX_CFLAGS_ONLY"
LIBS="$LIBS $WX_LIBS"

# <from autoscan>
# Checks for header files.
AC_HEADER_DIRENT

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_C_CONST
AC_C_INLINE
AC_TYPE_SIZE_T

# Checks for library functions.
#AC_FUNC_MALLOC
AC_HEADER_STDC
AC_FUNC_STAT
AC_CHECK_FUNCS([memset pow])
# </from autoscan>

# Efficient I/O block size (not available under woe) (BZip.cpp)
AC_CHECK_MEMBERS([struct stat.st_blksize])


# Remove mingwm10.dll dependency for static builds
# http://www.sourceware.org/ml/pthreads-win32/2000/msg00141.html
# http://www.thelins.se/johan/2006/11/installing-compressing-and-being.html
if test x"$enable_static" = x"yes"; then
    case "${host}" in
    *-*-go32* | *-mingw32* | *-*-cygwin* | *-*-windows*)
        LIBS="`echo $LIBS | sed 's/-mthreads //'`"
	# Needed for 2.6.4:
        CXXFLAGS="`echo $CXXFLAGS | sed 's/-mthreads //'`"
        ;;
    esac
fi

error=0

if test "$LACK_LIBBZ2" = 1; then
   echo "* Error: you need to install the libbz2 library (for compression)";
   error=1
fi

if test "$enable_upx" = "yes" -a -z "$UPX"; then
  echo "* Error: UPX is explicitely activated (--enable-upx) but cannot be found"
  error=1
fi

if test "$LACK_WXGLADE" = 1; then
   echo "* Warning: you may need to install wxGlade (if you're a developer)";
fi

if test $error -eq 1; then
  exit 1
fi

AC_CONFIG_FILES([Makefile share/Makefile src/Makefile src/woeres.rc po/Makefile.in])
AC_OUTPUT

echo
echo "Options summary:"
echo "* --enable-upx=$enable_upx"
echo "* --enable-static=$enable_static"
echo
echo "Now you can type 'make' to compile $PACKAGE_STRING"
