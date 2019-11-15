#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

# Copyright (C) 2007, 2008, 2009, 2010, 2012, 2014  Sylvain Beucler

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
AC_INIT([GNU FreeDink],[109.6],[bug-freedink@gnu.org])
AC_CONFIG_AUX_DIR(autotools)
AC_CONFIG_MACRO_DIR(autotools/m4)
AM_INIT_AUTOMAKE([gnits dist-zip silent-rules])
# Terse output - use V=1 for verbose output
AM_SILENT_RULES(yes)

AC_CONFIG_HEADERS(config.h)
# Define $host $host_os + distributes config.guess and config.sub
AC_CANONICAL_HOST
# Checks for programs.
AC_PROG_CC
AC_PROG_CXX
AC_PROG_LN_S
AC_PROG_MKDIR_P


# Gnulib - configuration in gnulib/m4/gnulib-cache.m4
# Gnulib prefix detected from Makefile.am:ACLOCAL_AMFLAGS
gl_EARLY

AM_CONDITIONAL(ANDROID, test "$host" = "arm-unknown-linux-androideabi")
case "${host}" in *-*-mingw32* | *-*-cygwin* | *-*-windows*) woe=1;; esac
AM_CONDITIONAL(WOE, test x"$woe" = x"1")

# Check if we can fork&exec (for fallback xmessage errors)
AC_CHECK_FUNCS(execlp)
# Check if we've got malloc stats
AC_CHECK_TYPES([struct mallinfo], [], [], [[#include <malloc.h>]])

# gettext
dnl Using [external] because bundling intl/ is deprecated as of 0.18:
AM_GNU_GETTEXT([external])
dnl Not a dependency: only a declaration used by autopoint:
AM_GNU_GETTEXT_VERSION([0.18.1])
dnl Not using ngettext in FreeDink or gnulib as of 2010-11:
dnl AM_GNU_GETTEXT_NEED(need-ngettext)


AC_ARG_VAR([WINDRES], [Resource compiler for woe executables])
AC_CHECK_TOOL(WINDRES, windres)
AM_CONDITIONAL(HAVE_WINDRES, test "$WINDRES" != "")

AC_ARG_VAR([HELP2MAN], [Manpage generator from '--help' output])
AC_PATH_PROG(HELP2MAN, help2man)
if test -z "$HELP2MAN"; then
  AC_MSG_WARN([You may need to install help2man (if you're a developer)])
  # Set HELP2MAN so 'make' errors will be understandable
  HELP2MAN="help2man"
  LACK_HELP2MAN=1
fi


# pkg-config / pkgconf
PKG_PROG_PKG_CONFIG()


AC_ARG_VAR([tests], [run tests])
AC_ARG_ENABLE([tests],
  AS_HELP_STRING([--disable-tests], [run test suite (default is enabled)]),
  [], [enable_tests=yes])
if test x"$enable_tests" = x"yes"; then
  AC_PATH_PROG(CXXTESTGEN, cxxtestgen)
  if test -z "$CXXTESTGEN"; then
    AC_MSG_WARN([Need cxxtestgen to run the testsuite])
    LACK_CXXTESTGEN=1
  fi
fi
AM_CONDITIONAL(HAVE_TESTS, test x"$enable_tests" = x"yes")


AC_ARG_VAR([UPX], [Produce self-decompressing executables (if --enable-upx)])
AC_ARG_ENABLE([upx],
  AS_HELP_STRING([--enable-upx], [compress executables (default is disabled)]),
  [], [enable_upx=no])
if test x"$enable_upx" = x"yes"; then
  AC_PATH_PROG(UPX, upx)
fi
AM_CONDITIONAL(HAVE_UPX, test "$UPX" != "")

# Dynamic and static builds
AC_ARG_ENABLE([static],
  AS_HELP_STRING([--enable-static],[embed SDL and dependencies in the executable (default is disabled)]),
  [], [enable_static=no])
if test x"$enable_static" = x"yes"; then
    case "${host}" in
    # (cf. (autoconf.info)Using System Type) (2002)
    *-*-mingw32* | *-*-cygwin* | *-*-windows*)
        # LIBS is handled by pkg-config and Libs.private/Requires.private
        # We still need to force choosing 'libxxx.a' over 'libxxx.dll.a':
        LDFLAGS="$LDFLAGS -static"
        ;;
    mipsallegrexel-psp-elf)
        # (Only static builds are possible for this architecture AFAIK)
        # Light version, if dependencies are compiled minimaly
        #LIBS="$LIBS -lfreetype -lz"
        # Full version, if planning to support more formats
        LIBS="-lvorbisidec -lfreetype -lpng -ljpeg -lz $LIBS"
        #LIBS="$LIBS -lfreetype -lpng -ltiff -ljpeg -lz -lvorbisfile -lvorbis -logg"
        ;;
    # *nix
    *)
        # The linker doesn't find dependent libs when using .a libs
        #LIBS="$LIBM -ldl $LIBS"
        LIBS="-ldl $LIBS"
        # Strip secondary dependencies added by e.g. fontconfig->libfreetype
        #LDFLAGS="$LDFLAGS -Wl,--as-needed"
        # Actually having freetype is handy, no need to add it for SDL_ttf.
        ;;
    esac
fi


# SDL and core libs
# See BUILD for version requirements
# PACKAGERS: DO *NOT* LOWER THE VERSIONS UNLESS YOU WANT TONS OF BUGS!
PKG_CHECK_MODULES([SDL2], [sdl2 > 2.0.3  SDL2_image > 2.0.0 SDL2_mixer > 2.0.0 SDL2_ttf > 2.0.12 SDL2_gfx >= 1.0.1],
  [CXXFLAGS="$CXXFLAGS $SDL2_CFLAGS"
   CFLAGS="$CXXFLAGS $SDL2_CFLAGS"
   LIBS="$SDL2_LIBS $LIBS"],
  AC_MSG_WARN($SDL2_PKG_ERRORS); LACK_SDL2=1)

case "${host}" in
# (cf. (autoconf.info)Using System Type) (2002)
*-*-msdos* | *-*-go32* | *-*-mingw32* | *-*-cygwin* | *-*-windows* \
| mipsallegrexel-psp-elf \
| arm-unknown-linux-androideabi \
| *-emscripten)
    # Can't search fonts using fontconfig under ms woe
    # Nor under Android or Emscripten (unless we recreate a full fontconfig root? ;))
    use_fontconfig="no"
    ;;
*)
    use_fontconfig="yes"
    ;;
esac
if test x"$use_fontconfig" = x"yes"; then
  PKG_CHECK_MODULES([FONTCONFIG], [fontconfig >= 2.3],
    AC_DEFINE([HAVE_FONTCONFIG], [], [fontconfig library (-lfontconfig)]),
    AC_MSG_WARN($FONTCONFIG_PKG_ERRORS); LACK_FONTCONFIG=1)
  CFLAGS="$CFLAGS $FONTCONFIG_CFLAGS"
  LIBS="$FONTCONFIG_LIBS $LIBS"
fi


# Lengthy Gnulib checks
gl_INIT


# Somewhat optional. Defines matching contants in config.h
# (e.g. HAVE_SDL_FRAMERATE_H). Using a temporary CPPFLAGS to include
# Gnulib's src and build directories ($top_srcdir and $top_builddir
# not present here for some reason). Also sdl-config lacks a
# --cppflags switch so we use SDL_CFLAGS.
# http://lists.gnu.org/archive/html/bug-gnulib/2007-10/msg00157.html
# http://lists.gnu.org/archive/html/bug-gnulib/2007-12/msg00149.html
# https://bugs.freedesktop.org/show_bug.cgi?id=47996
old_CPPFLAGS="$CPPFLAGS"
CPPFLAGS="$CPPFLAGS $SDL_CFLAGS -I${srcdir}/gnulib/lib -I./gnulib/lib"
AC_CHECK_HEADERS(SDL.h SDL2_rotozoom.h SDL_framerate.h SDL_image.h,
  [], AC_MSG_WARN([Could not find necessary SDL libs headers]); LACK_HEADERS=1)
CPPFLAGS="$old_CPPFLAGS"


echo
echo "Errors and warnings recap:"
error=0
warning=0

if test "$LACK_SDL2" = 1; then
  echo "* You need to install the SDL libraries:"
  echo "$SDL2_PKG_ERRORS"
  error=1
fi
if test "$LACK_CXXTESTGEN" = 1; then
  echo "* You need to install the 'cxxtest' testing framework:"
  echo "Could not find 'cxxtestgen'"
  error=1
fi
if test "$USE_NLS" = no; then
  echo "* You need to install the gettext library and enable NLS"
  error=1
fi

if test "$use_fontconfig" = "yes" -a "$LACK_FONTCONFIG" = 1; then
  echo "* You need to install the fontconfig library"
  error=1
fi

if test "$error" = 0 -a "$LACK_HEADERS" = 1; then
  echo "* Warning: You lack some library headers (.h) - see warnings above."
  #error=1
  warning=1
fi

if test "$error" = 0 -a "$LACK_HELP2MAN" = 1; then
  echo -n "* Warning: The 'help2man' utility cannot be found. You won't be able to rebuild manpages"
  echo " (if you modify the source code)"
  warning=1
fi

if test "$enable_upx" = "yes" -a -z "$UPX"; then
  echo "* UPX is explicitely activated (--enable-upx) but cannot be found"
  error=1
fi

if test "$error" = 1; then
  echo
  echo "There are errors - stopping. Please check the reports above."
  echo "If dependencies (such as SDL_gfx) are missing,"
  echo "please check BUILD for distro package names."
  exit 1
elif test "$warning" = 1; then
  echo
  echo "There were warnings - let's continue for now,"
  echo "but please check make sure nothing is missing."
else
  echo "* No errors"
fi
echo


AC_CONFIG_FILES([Makefile gnulib/lib/Makefile gnulib/po/Makefile.in nsis/Makefile po/Makefile.in share/Makefile share/freedink/Makefile src/Makefile src/woeres.rc])

AC_OUTPUT


echo
echo "Options summary:"
echo "* --enable-upx=$enable_upx"
echo "* --enable-static=$enable_static"
echo "* --enable-tests=$enable_tests"
echo
echo "Now you can type 'make' to compile $PACKAGE_STRING"

# TODO : check for GLM
