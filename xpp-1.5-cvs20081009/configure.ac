dnl Process this file with autoconf 2.59+ to produce a configure script.
dnl
dnl configure.in/configure.ac file for XPP
dnl

dnl
dnl init autotools
dnl
AC_INIT([xpp], [1.5], [till.kamppeter@gmx.net])
AC_PREREQ(2.59)
AC_CONFIG_SRCDIR([xppmain.cxx])
AC_CONFIG_HEADERS([config.h])
AM_INIT_AUTOMAKE([foreign])
AM_MAINTAINER_MODE

dnl
dnl Build environment setup
dnl
AC_CANONICAL_BUILD
AC_CANONICAL_HOST
AC_PROG_CXX
AC_LANG([C++])

dnl Generic checks for programs.
dnl <none currently>

dnl Generic library checks
dnl <none currently>

dnl
dnl Checks for X11
dnl
AC_PATH_XTRA
if test x"$X_DISPLAY_MISSING" != x ; then
	AC_MSG_ERROR([Required X11 libraries not found])
fi

dnl
dnl Generic header checks
dnl
AC_HEADER_STDC
if test x"$ac_cv_header_stdc" != x"yes" ; then
	AC_MSG_ERROR([Required system header not found])
fi
AC_SYS_LARGEFILE

dnl
dnl Generic typedef/struct/compiler checks
dnl
AC_HEADER_STDBOOL
AC_C_CONST
AC_C_INLINE

dnl
dnl Check for FLTK...
dnl
dnl This already tells us about *everything* we will need for FLTK
dnl which includes the X11 libs and includes, libm, etc
dnl
AC_ARG_VAR([FLTKCONFIG], [Path to the fltk-config program])
AC_PATH_PROG([FLTKCONFIG], [fltk-config],
	[AC_MSG_ERROR([fltk-config program not found, cannot determine FLTK configuration])] )

AC_ARG_VAR([FLUID], [Path to the FLTK dialog generator "fluid"])
AC_PATH_PROG([FLUID],[fluid],
	[AC_MSG_ERROR([Required FLTK "fluid" tool not found])] )

FLTK_CXXFLAGS=`$FLTKCONFIG --use-images --cxxflags`
FLTK_LDFLAGS=`$FLTKCONFIG --use-images --ldflags`
AC_SUBST(FLTK_CXXFLAGS)
AC_SUBST(FLTK_LDFLAGS)

dnl CXXFLAGS="${FLTK_CXXFLAGS} ${CXXFLAGS}"
dnl LDFLAGS="${FLTK_LDFLAGS} ${LDFLAGS}"
AC_CHECK_HEADERS([FL/Fl.H FL/fl_ask.H], [],
	[AC_MSG_ERROR([Required FLTK headers not found])])
dnl there is no simple way to check for C++ libs right now AFAIK,
dnl since autoconf is too dumb to let us ask it for the correct prototype
dnl and C++ name mangling causes the test to always fail

dnl
dnl Checks for CUPS
dnl

AC_ARG_VAR([CUPSCONFIG], [Path to the cups-config program])
AC_PATH_PROG([CUPSCONFIG], [cups-config],
	[AC_MSG_ERROR([cups-config not found, cannot determine CUPS configuration])] )

CUPS_LIBS=`${CUPSCONFIG} --libs`
CUPS_CFLAGS=`${CUPSCONFIG} --cflags`
CUPS_LDFLAGS=`${CUPSCONFIG} --ldflags`

dnl Clean up after completely braindead cups-config rpath usage
dnl never add default ld.so search dirs to -rpath, ever!
TEMP="${CUPS_LDFLAGS}"
CUPS_LDFLAGS=
for i in ${TEMP} ; do
	if test x"$i" != x"-Wl,-rpath,/usr/lib" ; then
		CUPS_LDFLAGS="${CUPS_LDFLAGS} $i"
	fi
done

AC_SUBST(CUPS_CFLAGS)
AC_SUBST(CUPS_LIBS)
AC_SUBST(CUPS_LDFLAGS)

save_ldflags="${LDFLAGS}"
save_cxxflags="${CXXFLAGS}"
save_libs="${LIBS}"
LDFLAGS="${CUPS_LDFLAGS} ${LDFLAGS}"
CXXFLAGS="${CUPS_CXXFLAGS} ${CXXFLAGS}"
LIBS="${CUPS_LIBS} ${LIBS}"
AC_CHECK_LIB([cups], [httpConnect], [],
	[AC_MSG_ERROR([Required CUPS libraries not found])])
AC_CHECK_HEADERS([cups/cups.h], [],
	[AC_MSG_ERROR([Required CUPS headers not found])])
LDFLAGS="${save_ldflags}"
CXXFLAGS="${save_cxxflags}"
LIBS="${save_libs}"

dnl 
dnl Generic library *function* checks
dnl
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_TYPE_SIGNAL
AC_CHECK_FUNCS([memset strcasecmp strchr strdup strncasecmp strpbrk strrchr strspn strstr])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
