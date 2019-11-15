# Process this file with autoconf to produce a configure script.

# PARTIMAGE (Partition Image): tool which saves and restores a partition
# Copyright (C) 2000-2007 Fracois Dupoux
# Copyright (C) 2000-2007 Franck Ladurelle

AC_REVISION([[$Revision: 1.4 $]])

AC_PREREQ(2.59c)

AC_INIT([partimage], [0.6.9])
AC_DEFINE([PACKAGE_NETPROTOVER], "PiMgNet001", [Define the version of the network protocol])

AC_CANONICAL_SYSTEM
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE([1.6 dist-bzip2])
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])
AM_CONFIG_HEADER([config.h])

AC_DEFINE(ENABLE_NLS, 1, [Enable translations])

# Translations system
AM_GNU_GETTEXT_VERSION([0.14.4])
AM_GNU_GETTEXT([external])

AC_PROG_LIBTOOL
AC_ISC_POSIX
AC_PROG_CC
AM_PROG_CC_STDC
AC_HEADER_STDC
AC_PROG_AWK
AC_PROG_CXX
AC_PROG_CPP
AC_PROG_INSTALL
AC_PROG_LN_S

dnl defined for files > 2GB
AC_DEFINE([_GNU_SOURCE], 1, [Defined to have O_LARGEFILE under Linux])
AC_SYS_LARGEFILE

dnl Try to extract to an external m4 file
dnl Test files
AC_DEFUN([AC_TEST_FILES],
[
    ac_file_found=yes
    for f in $1; do
	if test ! -f $2/$f; then
    	   ac_file_found=no
	   break;
	fi
    done

    if test "$ac_file_found" = "yes" ; then
	ifelse([$3], , :,[$3])
    else
	ifelse([$4], , :,[$4])
    fi
])

dnl Checks for os/architecture specificities.
case "$target_os" in

  linux*)
    AC_DEFINE([OS_LINUX], 1, [Define to 1 if OS is Linux])
    AC_CHECK_LIB([pthread], [pthread_create], [],
       AC_MSG_ERROR([*** pthread library (libpthread) not found]))
    ;;
  freebsd*)
    AC_MSG_WARN([Partimage not yet fully ported to BSDish])
    AC_DEFINE([OS_FBSD], 1, [Define to 1 if OS is FreeBSD])
    CPPFLAGS="$CPPFLAGS -I../../intl -I/usr/local/include"
    CPPFLAGS="$CPPFLAGS -I../../src/client/fs"
    CPPFLAGS="$CPPFLAGS -I/usr/include/slang"
    PARTIMAGE_LDFLAGS="$PARTIMAGE_LDFLAGS -pthread"
    LIBS="$LIBS -L/usr/local/lib"
    ;;
  *)
    AC_MSG_ERROR([Unsupported system type $target_os])
    ;;
esac

dnl Check for libraries.
AC_ARG_ENABLE(efence,
    [--enable-efence Enable linking with libefence Memory Debugger],
    efence_support=$enableval,
    efence_support=no
)
if test "$efence_support" = "yes" ; then
  AC_CHECK_LIB([efence], [EF_Print], [], AC_MSG_ERROR([*** efence library \
  	(libefence) not found]))
fi
AC_CHECK_LIB([bz2], [BZ2_bzopen], [],
   AC_MSG_ERROR([*** bzip2 library (libbz2) not found or too old: version 1.0.0 or more recent is need]))
AC_CHECK_LIB([newt], [newtCenteredWindow], [],
   AC_MSG_ERROR([*** newt library (libnewt) not found]))
AC_CHECK_LIB([z], [gzwrite], [],
   AC_MSG_ERROR([*** gzip library (libz) not found]))

dnl Search for headers, add path to CPPFLAGS if found 
AC_DEFUN([AC_SEARCH_HEADERS], 
[
    AC_MSG_CHECKING("for $1") 
    ac_hdr_found=no
    for p in $2; do
	AC_TEST_FILES($1, $p, 
	    [ 
     	       ac_hdr_found=yes
	       break
	    ]
	)
    done 
    if test "$ac_hdr_found" = "yes" ; then
 	CPPFLAGS="$CPPFLAGS -I$p"
        AC_MSG_RESULT( [($p) yes] ) 
	ifelse([$3], , :,[$3])
    else
        AC_MSG_RESULT("no") 
	ifelse([$4], , :,[$4])
    fi
])
dnl end of code to extract

CPPFLAGS="$CPPFLAGS -Wno-deprecated"

dnl SSL support.
AC_ARG_ENABLE(ssl, 
     [--disable-ssl       Don't compile ssl mode],
   SSL=$enableval,
   SSL=yes
)
AC_ARG_WITH(ssl-headers,
    [--with-ssl-headers=DIR  SSL Include files location],
  SSL_HDR_DIR="$withval"
  CPPFLAGS="$CPPFLAGS -I$withval"
)
AC_ARG_WITH(ssl-lib,
    [--with-ssl-lib=DIR  SSL Library location],
  LIBS="$LIBS -L$withval"
)

dnl SLang location
AC_ARG_WITH(slang-headers,
    [--with-slang-headers=DIR  SLang Include files location],
  CPPFLAGS="$CPPFLAGS -I$withval"
)

dnl options for developers
dnl Don't remove the comma, it's required.
AC_ARG_ENABLE(devel,
    [--enable-devel Enable developpers options (debug, ...)],
    AC_DEFINE([DEVEL_SUPPORT], 1, [Define to 1 to enable Developpers support])
    ,
)
     
dnl Want to use PAM?
AC_ARG_ENABLE(pam,
    [--enable-pam Enable PAM to authenticate users],
   pamsupport=$enableval,
   pamsupport=no
)

dnl Static executables?
AC_ARG_ENABLE(all-static,
    [--enable-all-static     build static binaries],
  allstatic=$enableval,
  allstatic=no
)

if test "$allstatic" = "yes"; then
  PARTIMAGE_LDFLAGS="$PARTIMAGE_LDFLAGS -all-static"
  PARTIMAGED_LDFLAGS="$PARTIMAGED_LDFLAGS -all-static"
  AC_SUBST(PARTIMAGE_LDFLAGS)
  AC_SUBST(PARTIMAGED_LDFLAGS)
  LIBS="$LIBS /usr/lib/libslang.a /usr/lib/libnewt.a /usr/lib/libdl.a"

  if test "$SSL" = "yes"; then
    LIBS="$LIBS /usr/lib/libssl.a /usr/lib/libcrypto.a"
  fi
fi


dnl Check for header files.
AC_CHECK_HEADERS(fcntl.h strings.h limit.h malloc.h strings.h unistd.h)
AC_CHECK_HEADERS(pthread.h crypt.h shadow.h mntent.h)
AC_CHECK_HEADERS(sys/param.h sys/statfs.h sys/mount.h)
AC_CHECK_HEADERS(getopt.h, [],
   AC_MSG_WARN([getopt.h not found: only short parameter can be used on cmdline])
)


dnl Check for typedefs, structures and compiler characteristics.
AC_C_CONST
AC_C_INLINE
AC_TYPE_SIZE_T
AC_STRUCT_TM

dnl Check for library functions.
AC_FUNC_SETPGRP
AC_CHECK_FUNCS(getwd strerror strdup atoll strtoll setpgid)
AC_CHECK_FUNCS(fstat64 fstatfs64 open64)
dnl getcwd, putenv, strdup have already been checked.

dnl with-log-dir option.
AC_ARG_WITH(log-dir,
  [  --with-log-dir=PATH     logfiles [/var/log]],
    LOGDIR=$with_log_dir, LOGDIR=/var/log)
    AC_SUBST(LOGDIR)

dnl Check for types sizes. (not required anymore ? -> use u8 to u64)
AC_CHECK_SIZEOF(char, 1)
AC_CHECK_SIZEOF(short, 2)
AC_CHECK_SIZEOF(int, 4)
AC_CHECK_SIZEOF(long int, 4)
AC_CHECK_SIZEOF(unsigned long long, 8)

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([stdint.h stdlib.h stdio.h string.h strings.h getopt.h sys/types.h])

dnl Check for PAM.
if test "$pamsupport" = "yes"; then
  AC_CHECK_LIB([pam], [pam_start], [],
       AC_MSG_ERROR([*** pam library (libpam) not found]))
  AC_CHECK_LIB([dl], [dlopen], [],
       AC_MSG_ERROR([*** dl library (libdl) not found]))
  AC_DEFINE([HAVE_PAM], 1, [Define if you have PAM support on your system])
fi

dnl Check for SSL.
if test "$SSL" = "yes"; then

  AC_MSG_RESULT()
  AC_PATH_PROG(opensslpath, openssl)
  if test x$opensslpath = x ; then
    AC_MSG_WARN([openssl is required for building partimaged certificates.])
    AC_MSG_WARN([Use --disable-ssl if you don't want to install openssl.])
  fi
  AC_SUBST(opensslpath)

  AC_CHECKING([ for SSL Library and Header files ... ])
  AC_SEARCH_HEADERS(rsa.h crypto.h x509.h pem.h ssl.h err.h,
    $SSL_HDR_DIR /usr/include/ssl /usr/include/openssl /usr/include,
    [  AC_CHECK_LIB(crypto, CRYPTO_free, [LIBS="$LIBS -lcrypto"],
        AC_MSG_ERROR([ Required for SSL Crypto Library not found. ])
      )
       AC_CHECK_LIB(ssl, SSL_CTX_new,
        [
          LIBS="$LIBS -lssl"
          AC_DEFINE([HAVE_SSL], 1, [Define to 1 if you have SSL support])
        ],
        AC_MSG_ERROR([ SSL Library not found. ])
      )
    ], 
    AC_MSG_ERROR([ SSL Headers not found. ])
  )
fi

dnl Client must login.
dnl Don't remove the comma, it's required.
AC_ARG_ENABLE(login,
    [--disable-login   Clients needn't to login when connecting partimaged],
  ,
  [AC_DEFINE([MUST_LOGIN], 1,
      [Define to 1 if you want users to login before using partimaged])
   AC_CHECK_LIB([crypt], [crypt], [],
      AC_MSG_ERROR([*** crypt library (libcrypt) not found]))
  ]
)   

dnl Server changes euid to 'partimag'
dnl Don't remove the comma, it's required.
AC_ARG_ENABLE(cheuid,
    [--disable-cheuid   Server doesn't change euid to 'partimag'],
  ,
  AC_DEFINE([MUST_CHEUID], 1,
     [Define to 1 if you want partimaged to drop privilieges on start])
)

dnl with-debug-level option.
AC_ARG_WITH(debug-level,
  [  --with-debug-level=X    default debut level used to write the debug logfile [1]],
   DEFAULT_DEBUG_LEVEL=$with_debug_level, DEFAULT_DEBUG_LEVEL=1
)
AC_SUBST(DEFAULT_DEBUG_LEVEL)

dnl SYSCONFDIR substitution
if test "${sysconfdir}" = "\${prefix}/etc" ; then
  if test "${prefix}" = "NONE" ; then
    SYSCONFDIR=["$ac_default_prefix/etc"]
  else
    SYSCONFDIR=["${prefix}/etc"]
  fi
else
  SYSCONFDIR=[${sysconfdir}]
fi
AC_SUBST(SYSCONFDIR)

AC_CONFIG_FILES([Makefile src/Makefile src/shared/Makefile src/shared/pathnames.h 
                 src/client/Makefile src/client/fs/Makefile src/server/Makefile 
		 m4/Makefile po/Makefile.in])

AC_OUTPUT
