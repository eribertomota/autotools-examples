dnl Process this file with autoconf to produce a configure script.



dnl Some intro checks and defines
AC_INIT(Ample,AMPLE_VERSION,david@2gen.com)
AC_REVISION ($Id: configure.ac,v 1.14 2003/11/25 09:28:27 alphix Exp $)
AC_PREREQ(2.50)
AC_CONFIG_SRCDIR(src/ample.c)
AC_CONFIG_HEADER(config.h)

PACKAGE=ample
AMPLE_MAJOR_VERSION=0
AMPLE_MINOR_VERSION=5
AMPLE_MICRO_VERSION=7

AMPLE_VERSION=\"$AMPLE_MAJOR_VERSION.$AMPLE_MINOR_VERSION.$AMPLE_MICRO_VERSION\"
AC_DEFINE_UNQUOTED(AMPLE_VERSION,$AMPLE_VERSION,[Define program version])



dnl Checks for programs.
AC_PROG_CC
AC_PROG_MAKE_SET
AC_PROG_INSTALL



dnl Checks for libraries.
dnl from aclocal.m4
AC_CHECK_SOCKET_LIBS



dnl Checks for header files.
AC_HEADER_DIRENT
AC_HEADER_STDC
AC_HEADER_SYS_WAIT
AC_CHECK_HEADERS([arpa/inet.h errno.h fcntl.h limits.h netinet/in.h stdlib.h \
		  string.h sys/socket.h unistd.h getopt.h signal.h stdint.h \
		  netdb.h])



dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_SIZE_T
AC_TYPE_OFF_T
AC_TYPE_PID_T
AC_TYPE_SIGNAL
dnl from aclocal.m4
AC_TYPE_SOCKLEN_T



dnl Checks for library functions.
AC_FUNC_VPRINTF
AC_CHECK_FUNCS([getcwd inet_ntoa memset socket strcasecmp alarm strchr strdup strerror strncasecmp strrchr strtol])
AC_FUNC_FORK
AC_FUNC_MALLOC



dnl Checks for conditionals

dnl Does the combination of tcpwrappers and syslog options make sense?
AC_ARG_ENABLE(libwrap, AC_HELP_STRING([--enable-libwrap],[Use tcpd wrappers]))
AC_ARG_ENABLE(syslog, AC_HELP_STRING([--disable-syslog],[Disable the use of syslog]))
AC_MSG_CHECKING([libwrap/sysconf interoperability])
if test "x$enable_libwrap" = "xyes" -a "x$enable_syslog" = "xno" ; then
	dnl syslog disabled, libwrap enabled
	AC_MSG_ERROR([you can't enable libwrap and disable syslog])
elif test "x$enable_libwrap" = "xyes" ; then
	dnl syslog enabled, libwrap enabled
	AC_MSG_RESULT([ok])
	AC_CHECK_HEADERS([syslog.h],,[AC_MSG_ERROR([syslog enabled but syslog header not found])])
	dnl from aclocal.m4	
	AC_LIB_WRAP
elif test "x$enable_syslog" != "xno" ; then
	dnl syslog enabled, libwrap disabled
	AC_MSG_RESULT([ok])
	AC_CHECK_HEADERS([syslog.h],,AC_MSG_ERROR([syslog enabled but syslog header not found]))
else
	dnl syslog disabled, libwrap disabled
	AC_MSG_RESULT([ok])
fi

dnl Do we want to log to a special facility?
AC_MSG_CHECKING([log facility])
AC_ARG_ENABLE(facility, AC_HELP_STRING([--enable-facility=ARG],[Syslog to ARG instead of LOG_DAEMON]))
if test "x$enable_facility" = "xyes" ; then
	AC_MSG_ERROR([you have to give an option to --enable-facility])
elif test "x$enable_facility" = "xno" -o "x$enable_facility" = "x"; then
	AC_DEFINE_UNQUOTED(LOG_FACILITY, LOG_DAEMON, [Log facility to use with syslog])
else
	AC_DEFINE_UNQUOTED(LOG_FACILITY, $enable_facility, [Log facility to use with syslog])
fi
AC_MSG_RESULT([ok])

dnl Done
echo
echo "Creating files"
AC_OUTPUT([Makefile src/Makefile docs/Makefile])
echo



dnl Pretty-print status message
echo "+----------------------------------------+"
echo "|              SUCCESS                   |"
echo "+----------------------------------------+"
echo "  Ample has been configured, you should"
echo "  now type 'make' to compile Ample."
echo
echo "+----------------------------------------+"
echo "|          YOUR CONFIGURATION            |"
echo "+----------------------------------------+"

echo "  Version:      $AMPLE_MAJOR_VERSION.$AMPLE_MINOR_VERSION.$AMPLE_MICRO_VERSION"

if test "x$enable_syslog" = "xno" ; then
	echo "  Syslog:       disabled"
	echo "  Libwrap:      disabled"
elif test "x$enable_libwrap" = "xyes" ; then
	echo "  Syslog:       enabled"
	echo "  Libwrap:      enabled"
else
	echo "  Syslog:       enabled"
	echo "  Libwrap:      disabled"
fi	

if test "x$enable_facility" != "xno" -a "x$enable_facility" != "x"; then
	echo "  Log facility: $enable_facility"
fi

echo

