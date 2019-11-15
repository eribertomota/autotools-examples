dnl
dnl NASPRO - The NASPRO Architecture for Sound PROcessing
dnl Portable runtime library
dnl
dnl Copyright (C) 2007-2014 Stefano D'Angelo
dnl
dnl See the COPYING file for license conditions.
dnl

AC_PREREQ([2.69])

AC_INIT([NASPRO core],[0.5.1], [zanga.mail@gmail.com])
AC_COPYRIGHT([Copyright (C) 2007-2014 Stefano D'Angelo])

AC_CONFIG_SRCDIR([src/internal.h])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])

AC_CANONICAL_HOST

AM_INIT_AUTOMAKE

# Command line options.
AC_MSG_CHECKING([where to put pkg-config's .pc files])
AC_ARG_WITH([pkgconfigdir],
	    AS_HELP_STRING([--with-pkgconfigdir=DIR],
	    [where to put pkg-config's .pc files @<:@LIBDIR/pkgconfig@:>@]),
	    [pkgconfigdir="${withval}"], [pkgconfigdir="${libdir}/pkgconfig"])
AC_SUBST([pkgconfigdir])
AC_MSG_RESULT([$pkgconfigdir])

# Checks for programs.
AC_PROG_CC_C99
AC_LIBTOOL_WIN32_DLL
AC_PROG_LIBTOOL

AC_ARG_VAR([NATURALDOCS], [path to NaturalDocs executable])
AC_CHECK_PROGS([NATURALDOCS], [NaturalDocs naturaldocs])
AM_CONDITIONAL([BUILD_DOC], [test -n "$NATURALDOCS"])

# Checks for libraries.
win32=no
case "$host_os" in
	mingw*)
		THREAD_FLAGS="-mthreads"
		win32=yes
		;;
	haiku*)
		THREAD_FLAGS=""
		;;
	*)
		THREAD_FLAGS="-pthread"
		;;
esac
AC_SUBST([THREAD_FLAGS])
AM_CONDITIONAL([WIN32], [test $win32 = yes])

# Checks for header files.
AC_CHECK_HEADERS([math.h], , [AC_MSG_ERROR([C math library header not found.])])
if test $win32 = yes ; then
	AC_CHECK_HEADERS([windows.h], ,
			 [AC_MSG_ERROR([Missing required header files.])])
else
	AC_CHECK_HEADERS([pthread.h langinfo.h dlfcn.h sys/types.h unistd.h \
			  dirent.h semaphore.h], ,
			 [AC_MSG_ERROR([Missing required header files.])])
fi

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.
AC_SEARCH_LIBS([logl], [m], , [AC_MSG_ERROR([C math library not found.])])
if test $win32 = yes ; then
	AC_SEARCH_LIBS([_configthreadlocale],
		       [msvcrt msvcr90 msvcr90d msvcr100], ,
		       [AC_MSG_ERROR([Missing recent enough C library..])])
else
	AC_SEARCH_LIBS([dlopen], [dl], ,
		       [AC_MSG_ERROR([Dynamic loading library not found.])])
	AC_CHECK_FUNCS([fpathconf dirfd], ,
		       [AC_MSG_ERROR([Missing needed functions.])])
fi

# Output.
LT_CURRENT=5
LT_REVISION=2
LT_AGE=0
AC_SUBST([LT_CURRENT])
AC_SUBST([LT_REVISION])
AC_SUBST([LT_AGE])

AC_CONFIG_FILES([Makefile nacore-5.pc doc/Makefile include/Makefile \
		 src/Makefile src/posix/Makefile src/win32/Makefile])
AC_OUTPUT
