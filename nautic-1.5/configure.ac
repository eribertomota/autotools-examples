#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.65])
AC_INIT([nautic], [1.2], [gio.enas@alice.it])
AM_INIT_AUTOMAKE([nautic], [1.2])
AC_CONFIG_SRCDIR([sofam.h])
AC_CONFIG_HEADERS([config.h])

# Checks for programs.
AC_PROG_CXX
AC_PROG_CC

#PKG_CHECK_MODULES([WXWIDGETS], [gtk+-2.0 >= 1.3.5 libwxgtk2.8-0 >= 1.8.4 libwxbase2.8-0 >= 1.8.4])
# Checks for libraries.
AM_OPTIONS_WXCONFIG
reqwx=1.8.0
AM_PATH_WXCONFIG($reqwx, wxWin=1)
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
#AC_CHECK_LIB([libwx_gtk2u_xrc-2.8.so.0  libwx_gtk2u_html-2.8.so.0  libwx_gtk2u_qa-2.8.so.0 libwx_gtk2u_adv-2.8.so.0
#              libwx_gtk2u_core-2.8.so.0 libwx_baseu_xml-2.8.so.0  libwx_baseu_net-2.8.so.0 libwx_baseu-2.8.so.0 libstdc++.so.6
#              libm.so.6 libgomp.so.1 libgcc_s.so.1 libpthread.so.0 libc.so.6])
# Checks for header files.
AC_CHECK_HEADERS([memory.h stdlib.h string.h wx.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_TYPE_SIZE_T

# Checks for library functions.
AC_CHECK_FUNCS([floor memset pow sqrt])

AC_OUTPUT(Makefile src/Makefile info/Makefile data/Makefile man/Makefile icon/Makefile)
