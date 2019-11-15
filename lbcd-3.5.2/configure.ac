dnl Autoconf configuration for lbcd.
dnl
dnl Written by Russ Allbery <eagle@eyrie.org>
dnl Based on work by Larry Schwimmer
dnl Copyright 1996, 1997, 1998, 2003, 2004, 2005, 2006, 2008, 2009, 2012,
dnl     2013, 2014
dnl     The Board of Trustees of the Leland Stanford Junior University
dnl
dnl See LICENSE for licensing terms.

AC_PREREQ([2.64])
AC_INIT([lbcd], [3.5.2], [eagle@eyrie.org])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_LIBOBJ_DIR([portable])
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE([1.11 check-news dist-xz foreign silent-rules subdir-objects
    -Wall -Werror])
AM_MAINTAINER_MODE

dnl Detect unexpanded macros.
m4_pattern_forbid([^_?RRA_])

AC_PROG_CC
RRA_PROG_CC_CLANG
AC_USE_SYSTEM_EXTENSIONS
AC_SYS_LARGEFILE
AM_PROG_CC_C_O
AM_PROG_AR
AC_PROG_INSTALL
AC_PROG_RANLIB

dnl Support installation of systemd unit files.
RRA_WITH_SYSTEMD_UNITDIR

dnl Probes for networking libraries.
AC_SEARCH_LIBS([gethostbyname], [nsl])
AC_SEARCH_LIBS([socket], [socket], ,
    [AC_CHECK_LIB([nsl], [socket], [LIBS="-lnsl -lsocket $LIBS"], [],
        [-lsocket])])

dnl Probes for kernel information libraries.
AC_SEARCH_LIBS([kvm_open], [kvm])
AC_SEARCH_LIBS([kstat_open], [kstat])
AC_CHECK_LIB([mld], [main], [LIBS="$LIBS -lmld"])
AC_SEARCH_LIBS([nlist], [elf])

dnl Probes for general support libraries.
RRA_LIB_SYSTEMD_DAEMON_OPTIONAL

dnl General C library probes.
AC_HEADER_STDBOOL
AC_CHECK_HEADERS([search.h sys/bittypes.h sys/filio.h sys/select.h \
    sys/statvfs.h sys/uio.h sys/time.h sys/vfs.h syslog.h utmp.h utmpx.h])
AC_CHECK_DECLS([snprintf, strlcat, strlcpy, vsnprintf])
RRA_C_C99_VAMACROS
RRA_C_GNU_VAMACROS
AC_TYPE_LONG_LONG_INT
AC_TYPE_UINT8_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_CHECK_TYPES([sig_atomic_t], [], [],
    [#include <sys/types.h>
     #include <signal.h>])
AC_CHECK_TYPES([ssize_t], [], [],
    [#include <sys/types.h>])
RRA_FUNC_SNPRINTF
AC_CHECK_FUNCS([getutent getutxent hsearch setrlimit setsid statvfs])
AC_REPLACE_FUNCS([asprintf daemon mkstemp reallocarray strlcat strlcpy])
AC_REPLACE_FUNCS([strndup])

dnl Additional probes for networking portability and IPv6.
AC_CHECK_DECLS([h_errno], [], [], [#include <netdb.h>])
AC_CHECK_DECLS([inet_aton, inet_ntoa], [], [],
    [#include <sys/types.h>
     #include <netinet/in.h>
     #include <arpa/inet.h>])
AC_CHECK_MEMBERS([struct sockaddr.sa_len], [], [],
    [#include <sys/types.h>
     #include <sys/socket.h>])
AC_CHECK_TYPES([socklen_t], [], [],
    [#include <sys/types.h>
     #include <sys/socket.h>])
AC_CHECK_TYPES([struct sockaddr_in6],
    [AC_DEFINE([HAVE_INET6], [1],
        [Define to 1 if IPv6 library interfaces are available.])], [],
    [#include <sys/types.h>
     #include <netinet/in.h>])
AC_CHECK_TYPES([struct sockaddr_storage],
    [AC_CHECK_MEMBERS([struct sockaddr_storage.ss_family], [], [],
        [#include <sys/types.h>
         #include <sys/socket.h>])], [],
    [#include <sys/types.h>
     #include <sys/socket.h>])
RRA_MACRO_IN6_ARE_ADDR_EQUAL
RRA_MACRO_SA_LEN
RRA_FUNC_INET_NTOA
AC_CHECK_FUNCS([getaddrinfo],
    [RRA_FUNC_GETADDRINFO_ADDRCONFIG],
    [AC_LIBOBJ([getaddrinfo])])
AC_REPLACE_FUNCS([getnameinfo inet_aton inet_ntop])

dnl Enable appropriate warnings.
AM_CONDITIONAL([WARNINGS_GCC], [test x"$GCC" = xyes && test x"$CLANG" != xyes])
AM_CONDITIONAL([WARNINGS_CLANG], [test x"$CLANG" = xyes])

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_FILES([Makefile])
AC_OUTPUT
