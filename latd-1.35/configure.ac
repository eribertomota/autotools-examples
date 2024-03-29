dnl Process this file with autoconf to produce a configure script.

dnl Checks that we are given a good source directory.
AC_INIT([latd], [1.35])
AC_CONFIG_SRCDIR([latcp.cc])
AM_INIT_AUTOMAKE

dnl Checks for programs.
AC_PROG_CC
AC_PROG_CXX
AC_PROG_CPP
AC_PROG_INSTALL
AC_PROG_MAKE_SET

AC_SUBST(INTERFACE)
AC_SUBST(LIBUTIL)

dnl Checks for headers.
AC_CHECK_HEADERS(sys/ioctl.h sys/sockio.h sys/socketio.h sys/filio.h \
 pty.h termios.h libutil.h util.h mcheck.h netinet/ether.h net/if_ether.h)

dnl Checks for struct ether_header.
AC_CHECK_HEADERS(net/if_ether.h net/ethernet.h)
AC_MSG_CHECKING([for struct ether_header])
AC_TRY_COMPILE([
#include <sys/types.h>
#include <sys/socket.h>
#include <net/if.h>
#ifdef HAVE_NET_IF_ETHER_H
#include <net/if_ether.h>
#endif /* HAVE_NET_IF_ETHER_H */
#ifdef HAVE_NET_ETHERNET_H
#include <net/ethernet.h>
#endif /* HAVE_NET_ETHERNET_H */
], [
  struct ether_header the_ether_header;
  unsigned int ethertype;
  ethertype = the_ether_header.ether_type;
], , AC_MSG_ERROR([cannot find struct ether_header]))
AC_MSG_RESULT(yes)

dnl Checks for our network access type.
latd_raw_type=
AC_CHECK_HEADER(netpacket/packet.h, [latd_raw_type=linux])	
if test x$latd_raw_type = x; then
  AC_CHECK_HEADER(net/bpf.h, [latd_raw_type=bpf])
fi
case x$latd_raw_type in
xbpf)
  AC_CHECK_HEADERS(net/if_dl.h)
  AC_MSG_CHECKING([for AF_LINK support])
  AC_EGREP_CPP(_latd_has_af_link,
[
#include <sys/socket.h>
#ifdef AF_LINK
_latd_has_af_link
#endif
], [
  AC_MSG_RESULT(yes)
  AC_DEFINE(HAVE_AF_LINK)
], [
  AC_MSG_RESULT(no)
])
  ;;
xlinux)
  AC_CHECK_HEADERS(features.h)
  ;;
*)
  ;;
esac
AC_MSG_CHECKING([for raw Ethernet access method])
if test x$latd_raw_type = x; then
  AC_MSG_ERROR([can't find any raw Ethernet access method])
fi
AC_MSG_RESULT($latd_raw_type)
INTERFACE=interfaces-$latd_raw_type.o

dnl Checks for sockaddr.sa_len - only needed for BPF access
if test "x$latd_raw_type" = "xbpf"; then
  AC_MSG_CHECKING([for sockaddr.sa_len])
  AC_TRY_COMPILE([
  #include <sys/types.h>
  #include <sys/socket.h>
  ],[
  struct sockaddr sa;
  sa.sa_len = 5;
  ], AC_DEFINE(HAVE_SOCKADDR_SA_LEN))
  AC_MSG_RESULT(yes)
fi

dnl Configure the use of openpty.
AC_ARG_ENABLE(openpty,
[  --disable-openpty       don't use the system's openpty function [do]],
, [enable_openpty=yes])
if test "x$enable_openpty" = "xyes"; then
  openpty_found=
  AC_CHECK_FUNCS(openpty, openpty_found=yes)
  if test "x$openpty_found" = "x"; then
    AC_CHECK_LIB(util, openpty, openpty_found=yes)
    if test "x$openpty_found" = "xyes"; then
      AC_DEFINE(HAVE_OPENPTY)
      LIBUTIL=-lutil
    fi
  fi
fi

dnl Configuring the login program
withval=
AC_ARG_WITH(login,
[  --with-login            program to use for logins (defaults to local "login")	])
if test "x$withval" = "x"; then
  if test -f /bin/login; then
    withval="/bin/login"
  elif test -f /usr/bin/login; then
    withval="/usr/bin/login"
  fi
fi
AC_DEFINE_UNQUOTED(LOGIN_BIN, "$withval")

dnl Configure "llogin -p" locking
AC_ARG_ENABLE(devlocking,
[  --disable-devlocking         disable llogin device locking using flock],
[ ], [enable_devlocking=yes])
if test "x$enable_devlocking" = "xno"; then
  CXXFLAGS="${CXXFLAGS-} -DDISABLE_DEVICE_LOCKING"
fi

dnl Configure the latcp socket.
LATCPSOCK=/var/run/latcp
AC_ARG_WITH(latcp_socket,
[  --with-latcp-socket=SOCK  set the socket for latcp to SOCK [/var/run/latcp]],
[ ], [with_latcp_socket=yes])
case x$with_latcp_socket in
  xyes | xno | x) ;;
  *) LATCPSOCK=$with_latcp_socket ;;
esac
AC_DEFINE_UNQUOTED(LATCP_SOCKNAME, "$LATCPSOCK")

dnl Configure the llogin socket.
LLOGINSOCK=/var/run/latlogin
AC_ARG_WITH(llogin_socket,
[  --with-llogin-socket=SOCK set the socket for llogin to SOCK [/var/run/latlogin]],
[ ], [with_llogin_socket=yes])
case x$with_llogin_socket in
  xyes | xno | x) ;;
  *) LLOGINSOCK=$with_llogin_socket ;;
esac
AC_DEFINE_UNQUOTED(LLOGIN_SOCKNAME, "$LLOGINSOCK")


dnl Disable default login service
AC_ARG_ENABLE(defservice,
[  --disable-defservice         disable default login service],
[ ], [enable_defservice=yes])
if test "x$enable_defservice" = "xyes"; then
  CXXFLAGS="${CXXFLAGS-} -DENABLE_DEFAULT_SERVICE"
fi

dnl Configure debugging and/or warnings.
AC_ARG_ENABLE(debug,
[  --enable-debug         compile debuggable programs],
[enable_debug=yes])
if test "x$enable_debug" = "xyes"; then
  CXXFLAGS="${CXXFLAGS-} -g3 -O0 -DVERBOSE_DEBUG -DNO_FORK"
fi

AC_ARG_ENABLE(warnings,
[  --disable-warnings      don't compile with warnings turned on],
[ ], [enable_warnings=yes])
if test "x$enable_warnings" = "xyes" -a "x$GCC" = "xyes"; then
  CXXFLAGS="${CXXFLAGS-} -W"
fi

dnl Writes files.
AC_OUTPUT(Makefile)

