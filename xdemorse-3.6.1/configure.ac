#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT([xdemorse], [3.6.1], [nkcyham@yahoo.com])
AM_INIT_AUTOMAKE
AC_CONFIG_SRCDIR([src/main.c])
AC_CONFIG_HEADERS([config.h])
AM_MAINTAINER_MODE

# Set CFLAGS if not set in environment
AC_MSG_CHECKING([whether configure should try to set CFLAGS])
if test "x${CFLAGS+set}" = xset; then
   enable_cflags_setting=no
else
   enable_cflags_setting=yes
fi
AC_MSG_RESULT($enable_cflags_setting)
test "x$enable_cflags_setting" = xyes && CFLAGS=""

# Checks for programs.
AC_PROG_CXX
AC_PROG_CC
AC_PROG_MAKE_SET

# Checks for libraries.
pkg_modules="gtk+-3.0 >= 3.22.0"
PKG_CHECK_MODULES(PACKAGE, [$pkg_modules])
AC_SUBST(PACKAGE_CFLAGS)
AC_SUBST(PACKAGE_LIBS)
AC_CHECK_LIB([asound], [snd_pcm_open])
AC_CHECK_LIB([pthread], [pthread_create])
AC_CHECK_LIB([perseus-sdr], [perseus_init])
AC_CHECK_LIB([m], [cos])
AC_CHECK_LIB([gmodule-2.0], [g_module_open])

# Coditional compilation of sources
AM_CONDITIONAL([USE_LIBPERSEUS_SDR],[grep HAVE_LIBPERSEUS_SDR confdefs.h > /dev/null])

# Internationalization tools
AM_GNU_GETTEXT_VERSION([0.19.8])
GETTEXT_PACKAGE=xdemorse
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED([GETTEXT_PACKAGE], ["$GETTEXT_PACKAGE"], [Gettext package.])
AM_GNU_GETTEXT
PROGRAMNAME_LOCALEDIR=[${datadir}/locale]
AC_SUBST(PROGRAMNAME_LOCALEDIR)

# Add the languages which your application supports here.
ALL_LINGUAS=""
AM_GNU_GETTEXT

# Checks for header files.
AC_CHECK_HEADERS([fcntl.h libintl.h stdlib.h string.h termios.h unistd.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_CHECK_FUNCS([memset sqrt strstr])

AC_CONFIG_FILES([Makefile
				 src/Makefile
				 po/Makefile.in])
AC_OUTPUT
