dnl Process this file with autoconf to produce a configure script.
dnl Change this to change the version of the package

AC_INIT([libinklevel],[0.9.3])

dnl change this to change the RPM epoch
RPM_EPOCH=1

dnl change this to change the ABI-version

ABI_VERSION=5:0:0

dnl no more configuration after this line

AC_CONFIG_SRCDIR(libinklevel.c)

## Determine hostname & OS
## AC_CANONICAL_HOST
AC_ARG_ENABLE(debug,
	[  --enable-debug          Enable debugging output (default=no)],
	   [ case "${enableval}" in
             yes|"") enabled=yes; 
	     	     AC_DEFINE(DEBUG, 1, [enable debugging output]) ;;
             no) ;;
             *) ;;
    	   esac],
)

## Check for programs
## we want libtool to build our libs
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_MAKE_SET
AC_PROG_LIBTOOL
AC_CONFIG_MACRO_DIR([m4])

## Check if we have rpmbuild, so we can build rpm's
AC_PATH_PROG([RPMBUILD],rpmbuild)
AC_ARG_VAR(RPMBUILD, rpmbuild command)
if test -n "$RPMBUILD"; then
  rpmtarget=$srcdir/rpmbuild
else
  rpmtarget=$srcdir/norpm
fi
AC_SUBST_FILE(rpmtarget)
AC_SUBST(RPMBUILD)

AC_SUBST(BUILD)
AM_INIT_AUTOMAKE
AC_CONFIG_HEADERS([config.h])
AM_PROG_LIBTOOL
AC_PROG_INSTALL
AC_HEADER_STDC
AC_C_CONST
AC_C_VOLATILE
AC_FUNC_SELECT_ARGTYPES
AC_FUNC_SETVBUF_REVERSED
AC_HEADER_SYS_WAIT
AC_HEADER_TIME
AC_PROG_GCC_TRADITIONAL
AC_TYPE_SIGNAL
AC_SUBST(MAKEINDEX)
if test "$MAKEDEPEND" != "no"; then
  DEPEND_RECURSIVE="depend-recursive"
fi

AC_CANONICAL_HOST
case $host_os in
    freebsd* )
        CFLAGS="$CFLAGS -I/usr/local/include"
        LDFLAGS="$LDFLAGS -L/usr/local/lib"
        ;;
esac

## Check for optional  header files
AC_CHECK_HEADERS([ifaddrs.h])

## Check for mandatory header files

AC_CHECK_HEADERS([arpa/inet.h fcntl.h netdb.h netinet/in.h \ 
                 sys/ioctl.h sys/socket.h sys/time.h sys/timeb.h wchar.h ]
                 ,,AC_MSG_ERROR( required header file missing ))

## determine libraries that need to get linked

AC_SEARCH_LIBS([gethostbyname], [nsl])
AC_SEARCH_LIBS([socket], [socket])
AC_SEARCH_LIBS([ftime], [compat])

## Check for availability of optional functions

AC_CHECK_FUNCS([getifaddrs])

## Check for availability of mandatory functions

AC_CHECK_FUNCS([alarm ftime gethostbyaddr gethostbyname gettimeofday inet_ntoa \
               memset select socket strchr strdup strerror strncasecmp strstr \
               gethostname]
               ,,AC_MSG_ERROR( required library function missing ))
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_HEADER_RESOLV

## check for required types 

AC_TYPE_SIZE_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT8_T
AC_DEFINE_UNQUOTED(LINUX,1,[Define value for Linux OS])
case $host in
  *-*-linux*) AC_DEFINE_UNQUOTED(HOST_OS,LINUX,[Host OS])
	      ## check for pkgconfig
	      PKG_PROG_PKG_CONFIG([0.26])

	      ## check for libusb
	      PKG_CHECK_MODULES([LIBUSB1], [libusb-1.0]);;

  *-freebsd*) AC_DEFINE_UNQUOTED(HOST_OS,FREEBSD,[Host OS])
              AC_CHECK_LIB([usb], libusb_init,, AC_MSG_ERROR(Library not found),);;
  *-*-*) AC_MSG_ERROR( Host OS not (yet) supported) ;;
esac

## Variables to be exported

AC_SUBST(LIBTOOL_DEPS)
AC_SUBST(ABI_VERSION)
AC_SUBST(RPM_EPOCH)

AC_SUBST(HOST_OS)
## What files must be generated

AC_CONFIG_FILES([Makefile libinklevel.spec])
AC_OUTPUT
