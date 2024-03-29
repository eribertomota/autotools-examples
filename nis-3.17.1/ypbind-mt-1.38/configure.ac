dnl Process this file with autoconf to produce a configure script.
AC_INIT([ypbind-mt], [1.38])
AC_CONFIG_SRCDIR([src/ypbind-mt.c])
AM_INIT_AUTOMAKE
AC_CONFIG_HEADERS(config.h)
AC_SUBST(PACKAGE)
AC_SUBST(VERSION)
AM_GNU_GETTEXT_REQUIRE_VERSION(0.0.0)

AC_CANONICAL_HOST

dnl Checks for programs.
AC_PROG_CC
dnl If we're using gcc, we want warning flags
test -n "$GCC" && WARNFLAGS="-Wall"
#test -n "$GCC" && WARNFLAGS="-W -Wall -Wbad-function-cast -Wcast-align -Winline -Wmissing-declarations -Wmissing-prototypes -Wnested-externs -Wpointer-arith -Wshadow -Wstrict-prototypes -Wundef -Werror"
AC_SUBST(WARNFLAGS)
AC_ISC_POSIX
AC_PROG_INSTALL
AC_PROG_MAKE_SET
AC_PROG_RANLIB

AM_WITH_DMALLOC
AM_WITH_EFENCE

dnl Check for SLP support for finding yppserv
AC_ARG_ENABLE([slp],
   AC_HELP_STRING([--disable-slp],[Disable SLP support]))

AC_CHECK_HEADERS([slp.h])

SLP_LIBS=""
if test "$enable_slp" \!= "no"
then
  AC_CHECK_LIB(slp,SLPReg,SLP_LIBS="-lslp",SLP_LIBS="")
  if test -n "$SLP_LIBS" -a x$ac_cv_header_slp_h != xno
  then
    AC_DEFINE(USE_SLP, 1, [Enable SLP support])
  fi
fi
AC_SUBST(SLP_LIBS)

dnl Checks for libraries.
AC_CHECK_LIB(nsl, yp_get_default_domain)
AC_CHECK_LIB(socket, bind)
AC_CHECK_LIB(pthread, pthread_create)

PKG_CHECK_MODULES([SYSTEMD], [libsystemd >= 209], [USE_SD_NOTIFY=1], [USE_SD_NOTIFY=0])
AC_SUBST(USE_SD_NOTIFY)

AC_ARG_ENABLE([dbus-nm],
   AC_HELP_STRING([--enable-dbus-nm],[Enable DBUS/NetworkManager support]),
	[],[enable_dbus_nm=no])
if test "$enable_dbus_nm" \!= "no"
then
  PKG_CHECK_MODULES(DBUS, dbus-glib-1 >= 0.60)
  AC_SUBST(DBUS_CFLAGS)
  AC_SUBST(DBUS_LIBS)
  PKG_CHECK_MODULES(GLIB, glib-2.0 >= 2.6)
  AC_SUBST(GLIB_CFLAGS)
  AC_SUBST(GLIB_LIBS)
  AC_CHECK_HEADERS([NetworkManager/NetworkManager.h])
  AC_CHECK_HEADERS([NetworkManager/NetworkManagerVPN.h])
  AC_DEFINE(USE_DBUS_NM, 1, [Enable DBUS/NetworkManager support])
fi

dnl The difficult part: could we reconfigure NSS or must we use DNS ?
AC_CHECK_FUNCS(__nss_configure_lookup)
if eval "test \"`echo '$ac_cv_func___nss_configure_lookup'`\" != yes"; then
   AC_CHECK_LIB(resolv, res_gethostbyname)
fi

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

AC_MSG_CHECKING([wether <sys/socket.h> defiens socklen_t])
AC_TRY_COMPILE([#include <sys/socket.h>], [socklen_t sock;],
		 SOCKLEN_T=yes, SOCKLEN_T=no)
if test x"$SOCKLEN_T" = x"yes"; then
   AC_MSG_RESULT(yes)
   AC_DEFINE(HAVE_SOCKLEN_T,1,[Define to 1 if <sys/socket.h> defines socklen_t.])
else
   AC_MSG_RESULT(no)
fi

dnl Checks for header files.
AC_CHECK_HEADERS(paths.h sys/filio.h rpc/svc_soc.h rpc/clnt_soc.h nss.h)

dnl Checks for library functions.
AC_CHECK_FUNCS(getline getdelim vsyslog res_gethostbyname _dns_gethostbyname)

dnl
dnl Check for xsltproc
dnl
enable_man=yes
AC_PATH_PROG([XSLTPROC], [xsltproc])
if test -z "$XSLTPROC"; then
     enable_man=no
fi
AC_PATH_PROG([XMLLINT], [xmllint],[/bin/true])
dnl check for DocBook DTD and stylesheets in the local catalog.
JH_CHECK_XML_CATALOG([-//OASIS//DTD DocBook XML V4.3//EN],
                [DocBook XML DTD V4.3], [], enable_man=no)
JH_CHECK_XML_CATALOG([http://docbook.sourceforge.net/release/xsl/current/manpages/docbook.xsl],
                [DocBook XSL Stylesheets], [], enable_man=no)
AM_CONDITIONAL(ENABLE_REGENERATE_MAN, test x$enable_man != xno)

dnl internationalization macros
AM_GNU_GETTEXT_VERSION
AM_GNU_GETTEXT([external])

dnl By default, don't send a ping to all server at the same time
dnl It doesn't work in the moment
USE_BROADCAST=0

dnl glibc 2.0 needs our patched clnt_udp.c, glibc 2.1 not.
dnl The following check is stupid, since the glibc could be ported to
dnl other platforms in the future, but in the moment, it works.
case "$host_os" in
  linux*libc1)
    dnl send a ping to all server at the same time:
    USE_BROADCAST=1
    AC_LIBOBJ(clnt_udp)
    echo "***"
    echo "***"
    echo "*** ypbind-mt is currently not well tested with Linux libc5."
    echo "*** libc5 is not really threadsafe, and you need a working"
    echo "*** pthread package for it. I'm using linuxthreads 0.7.1 for"
    echo "*** development."
    echo "***"
    echo "***"
    ;;
  linux*|kfreebsd*-gnu*)
    dnl send a ping to all server at the same time:
    USE_BROADCAST=1
    dnl Test, if we have glibc 2.0 or glibc 2.1
	AC_MSG_CHECKING([wether we have glibc 2.1 or later])
	AC_TRY_COMPILE([#include <features.h>], [#if defined(__GLIBC__) && \
	(((__GLIBC__ == 2) && (__GLIBC_MINOR__ > 0)) || (__GLIBC__ > 2))
	#else
	#error Library needs fixed clntudp_call
	#endif], CLNTUDPSRC=yes, CLNTUDPSRC=no)
	if test x"$CLNTUDPSRC" = x"yes"; then
	   AC_MSG_RESULT(yes)
	else
	   AC_MSG_RESULT(no)
	   AC_LIBOBJ(clnt_udp)
	fi
    ;;
  solaris2.6 | solaris2.5.1 | solaris2.5)
    dnl Solaris 2 works without special hacking if it has the pthread library
    ;;
  *)
    echo "***"
    echo "***"
    echo "*** ypbind-mt is currently not tested on this platform."
    echo "*** I don't know if it will work. If it works, please send"
    echo "*** an email to <kukuk@suse.de> and tell me"
    echo "*** that this program will work on the platform"
    echo "*** "$host_cpu-$host_vendor-$host_os", so that I could add it."
    echo "***"
    echo "*** Thanks,"
    echo "***    Thorsten Kukuk"
    echo "***"
    echo "***"
    ;;
esac

AC_SUBST(USE_BROADCAST)

AC_OUTPUT(Makefile lib/Makefile src/Makefile man/Makefile po/Makefile.in)
