#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT(BitStormLite, 0.2q, gxcoo@hotmail.com)
AM_INIT_AUTOMAKE(BitStormLite, 0.2q)

AC_CONFIG_SRCDIR([src/bdict.cpp])
AM_CONFIG_HEADER(config.h)

AC_ARG_ENABLE(debug,
	      [  --enable-debug          turn on debug],
	      CXXFLAGS="$CXXFLAGS -g3 -D_DEBUG=1")

# Checks for programs.
AC_PROG_CXX

GETTEXT_PACKAGE=BitStormLite
AC_SUBST(GETTEXT_PACKAGE)

dnl check gettext
AM_GNU_GETTEXT
AM_GNU_GETTEXT_VERSION([0.16.1])
AM_GNU_GETTEXT([external])
ALL_LINGUAS="zh_CN"

# Checks for libraries.
PKG_CHECK_MODULES(GTK, gtk+-2.0 >= 2.6.0)
AC_SUBST(GTK_CFLAGS)
AC_SUBST(GTK_LIBS)

AC_PATH_PROG(CURL_CONFIG, curl-config, no)
if test "$CURL_CONFIG" = "no" ; then
	AC_MSG_ERROR(the curl-config script installed by libcurl could not be found.  libcurl is required.)
fi
LIBCURL_CHECK_CONFIG

# Checks for header files.
AC_HEADER_DIRENT
AC_HEADER_STDC
AC_CHECK_HEADERS([arpa/inet.h fcntl.h libintl.h locale.h netinet/in.h string.h sys/socket.h sys/time.h unistd.h netdb.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_C_CONST
AC_C_INLINE
AC_TYPE_SIZE_T
AC_HEADER_TIME

# Checks for library functions.
AC_FUNC_CLOSEDIR_VOID
AC_CHECK_FUNCS([ftruncate gettimeofday gethostbyname inet_ntoa memset mkdir socket])

AC_CONFIG_FILES(Makefile src/Makefile po/Makefile.in)
AC_OUTPUT
