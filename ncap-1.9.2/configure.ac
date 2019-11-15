AC_INIT([ncap], [1.9.2], [info@sie.isc.org])
AC_CANONICAL_TARGET
AM_INIT_AUTOMAKE([1.9 foreign])
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

AC_PROG_CC
AC_PROG_LIBTOOL
AC_PROG_INSTALL

AC_CONFIG_FILES([Makefile])
AC_CONFIG_HEADERS([config.h])

AC_STRUCT_TM
AC_TYPE_INT16_T
AC_TYPE_INT32_T
AC_TYPE_SIGNAL
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T
AC_TYPE_UINT8_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T

AC_SEARCH_LIBS([socket], [socket])
AC_SEARCH_LIBS([gethostbyname], [nsl])
AC_SEARCH_LIBS([clock_gettime], [rt])
AC_SEARCH_LIBS([dlopen], [dl])

AC_FUNC_ALLOCA
AC_FUNC_MALLOC
AC_FUNC_MEMCMP
AC_FUNC_REALLOC
AC_FUNC_SELECT_ARGTYPES
AC_FUNC_STRFTIME
AC_CHECK_FUNCS([alarm clock_gettime gettimeofday isascii memset regcomp dnl
    select socket strcasecmp strchr strdup strerror strrchr strtoul])

AC_HEADER_STDBOOL
AC_HEADER_TIME

AC_CHECK_HEADERS([arpa/inet.h arpa/nameser.h fcntl.h netinet/in_systm.h netinet/in.h dnl
    stddef.h sys/ioctl.h sys/param.h sys/types.h sys/socket.h sys/time.h])

AC_CHECK_HEADERS([net/if.h], [], [],
    [[
#ifdef HAVE_SYS_PARAM_H
# include <sys/param.h>
#endif

#ifdef HAVE_SYS_TYPES_H
# include <sys/types.h>
#endif

#ifdef HAVE_SYS_SOCKET_H
# include <sys/socket.h>
#endif
    ]]
)

AC_CHECK_HEADERS([net/ethernet.h net/ethertypes.h net/if_ether.h dnl
    netinet/if_ether.h netinet/ip.h netinet/ip6.h netinet/tcp.h netinet/udp.h],
    [], [],
    [[
#ifdef HAVE_SYS_PARAM_H
# include <sys/param.h>
#endif

#ifdef HAVE_SYS_TYPES_H
# include <sys/types.h>
#endif

#ifdef HAVE_SYS_SOCKET_H
# include <sys/socket.h>
#endif

#ifdef HAVE_NETINET_IN_SYSTM_H
# include <netinet/in_systm.h>
#endif

#ifdef HAVE_NETINET_IN_H
# include <netinet/in.h>
#endif

#ifdef HAVE_NET_IF_H
# include <net/if.h>
#endif
    ]]
)

AC_CHECK_TYPES([struct ether_header, struct ip, struct ip6_hdr, struct tcphdr,
    struct udphdr], [], AC_MSG_ERROR([struct definition missing.]),
    [[
#ifdef HAVE_SYS_PARAM_H
# include <sys/param.h>
#endif

#ifdef HAVE_SYS_TYPES_H
# include <sys/types.h>
#endif

#ifdef HAVE_SYS_SOCKET_H
# include <sys/socket.h>
#endif

#ifdef HAVE_NETINET_IN_SYSTM_H
# include <netinet/in_systm.h>
#endif

#ifdef HAVE_NETINET_IN_H
# include <netinet/in.h>
#endif

#ifdef HAVE_NETINET_IP_H
# include <netinet/ip.h>
#endif

#ifdef HAVE_NETINET_IP6_H
# include <netinet/ip6.h>
#endif

#ifdef HAVE_NETINET_UDP_H
# include <netinet/udp.h>
#endif

#ifdef HAVE_NETINET_TCP_H
# include <netinet/tcp.h>
#endif

#ifdef HAVE_NET_IF_H
# include <net/if.h>
#endif

#ifdef HAVE_NET_ETHERNET_H
# include <net/ethernet.h>
#endif

#ifdef HAVE_NET_ETHERTYPES_H
# include <net/ethertypes.h>
#endif

#ifdef HAVE_NET_IF_ETHER_H
# include <net/if_ether.h>
#endif

#ifdef HAVE_NETINET_IF_ETHER_H
# include <netinet/if_ether.h>
#endif
    ]]
)

AC_CHECK_MEMBER([struct sockaddr.sa_len],
    AC_DEFINE([HAVE_SA_LEN], [1], [Define to 1 if struct sockaddr has an sa_len member.]),
    [],
    [[
#ifdef HAVE_SYS_TYPES_H
# include <sys/types.h>
#endif

#ifdef HAVE_SYS_SOCKET_H
# include <sys/socket.h>
#endif
    ]]
)


###
### get this out of the way
###
LDFLAGS="$LDFLAGS -L/usr/local/lib"


###
### C compiler checks
###
AC_C_INLINE
AC_C_CONST
AC_C_FLEXIBLE_ARRAY_MEMBER

AC_DEFUN([MYAC_PROG_CC_CFLAGS_OPT],
[AC_MSG_CHECKING([if $CC supports $1])
myac_save_CFLAGS=$CFLAGS
CFLAGS="$myac_save_CFLAGS $1"
_AC_COMPILE_IFELSE([AC_LANG_PROGRAM()],
                   EXTRA_CFLAGS="$EXTRA_CFLAGS $1"
                   AC_MSG_RESULT(yes),
                   [AC_MSG_RESULT(no)])
CFLAGS="$myac_save_CFLAGS"
])

if test "x$GCC" = xyes; then
    EXTRA_CFLAGS="$EXTRA_CFLAGS -Wall -Werror -Wunused -Wshadow -Wcast-qual"
    EXTRA_CFLAGS="$EXTRA_CFLAGS -Wpointer-arith -Wwrite-strings -Wnested-externs"
    EXTRA_CFLAGS="$EXTRA_CFLAGS -Wmissing-noreturn -Wmissing-prototypes -Wbad-function-cast"
    EXTRA_CFLAGS="$EXTRA_CFLAGS -Wbad-function-cast -Wformat-nonliteral"
    MYAC_PROG_CC_CFLAGS_OPT([-Wextra])
    MYAC_PROG_CC_CFLAGS_OPT([-Wswitch-enum])
    case $host in
        *-*-darwin*)
            EXTRA_CFLAGS="$EXTRA_CFLAGS -Wno-unused"
        ;;
    esac
fi

AC_SUBST([EXTRA_CFLAGS])

###
### check for pthreads
###
m4_sinclude(acx_pthread.m4)
ACX_PTHREAD([
    LIBS="$PTHREAD_LIBS $LIBS"
    CFLAGS="$CFLAGS $PTHREAD_CFLAGS"
    CC="$PTHREAD_CC"
])

###
### libpcap
###
m4_sinclude(check_libpcap.m4)

AC_CHECK_HEADER([net/bpf.h],
    AC_CHECK_TYPE([struct bpf_timeval],
        AC_DEFINE([HAVE_BPF_TIMEVAL], [1], [Define to 1 if struct bpf_timeval exists.]),
        [],
        [[
#include <sys/types.h>
#include <net/bpf.h>
        ]]
    )
)

###
### libbind
###
m4_sinclude(check_libbind.m4)

AC_OUTPUT
