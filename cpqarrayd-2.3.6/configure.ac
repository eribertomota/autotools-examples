# Process this file with autoconf to produce a configure script.
AC_INIT([cpqarrayd], [2.1], [spark@knoware.nl])
AC_CONFIG_SRCDIR([cpqarrayd.c])
AM_INIT_AUTOMAKE

AM_CONFIG_HEADER(config.h)

# Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_AWK
AC_PROG_MAKE_SET

# Checks for libraries.

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([arpa/inet.h fcntl.h netdb.h netinet/in.h stdlib.h string.h sys/ioctl.h sys/socket.h sys/time.h syslog.h unistd.h])

dnl Check for directory with kernel source...
AC_MSG_CHECKING(for directory with kernel source)
AC_ARG_WITH(kernel,
  [  --with-kernel=dir       give the directory with kernel sources]
  [                        [/usr/src/linux]],
  kerneldir="$withval",
  if test -d "/lib/modules/`uname -r`/build" -o -L "/lib/modules/`uname -r`/build"; then
    kerneldir="/lib/modules/`uname -r`/build"
  else
    kerneldir="/usr/src/linux"
  fi
)
if test -d "$kerneldir" -o -L "$kerneldir"; then
  AC_MSG_RESULT(found $kerneldir )
else
  AC_MSG_ERROR(Kernel source directory not found)
fi

CONFIG_KERNEL_SOURCE="$kerneldir"
AC_SUBST(CONFIG_KERNEL_SOURCE)

CPQARRAY_INC="-I$CONFIG_KERNEL_SOURCE/drivers/block -I$CONFIG_KERNEL_SOURCE/include"

CFLAGS="$CFLAGS $CPQARRAY_INC"
CPPFLAGS="$CPPFLAGS $CPQARRAY_INC"

dnl Check for compile.h (2.6.x kernels only?
AC_CHECK_HEADERS(linux/compiler.h)
                                                                       
dnl Check Headers
dnl AC_CHECK_HEADERS(ida_ioctl.h ida_cmd.h cpqarray.h,, 
dnl   AC_MSG_ERROR(You need to have the SmartArray driver in the kernel.))

dnl Check version of SmartArray driver
dnl AC_MSG_CHECKING(SmartArray driver version)
dnl AC_EGREP_HEADER(blk_cnt, ida_ioctl.h,AC_MSG_RESULT(ok), 
dnl   AC_MSG_ERROR(You need to have the SmartArray driver version 1.0.1 or higher installed.))

dnl Check for CCISS header file
dnl AC_CHECK_HEADERS(linux/cciss_ioctl.h,,
dnl   AC_MSG_ERROR(You need to have the CCISS driver in the kernel.))

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

# Checks for library functions.
AC_FUNC_FORK
AC_PROG_GCC_TRADITIONAL
AC_FUNC_MALLOC
AC_CHECK_FUNCS([dup2 gethostbyname gethostname memset strerror])

# Check for snmp support
SNMPSUPPORT=1
AC_ARG_ENABLE(snmptrap,
  AC_HELP_STRING([--disable-snmptrap],[Disable support for sending snmptraps]),
  [ SNMPSUPPORT= ],
)

if test "$SNMPSUPPORT" = 1 ; then
  AC_CHECK_LIB(crypto,HMAC,,)
  AC_CHECK_LIB(netsnmp,snmp_open,,AC_MSG_ERROR([net-snmp is required for snmptrap option]))
  AC_DEFINE(HAVE_SNMPTRAP,1,"HAVE_SNMPTRAP")
fi

AC_CONFIG_FILES([Makefile
                 scripts/Makefile])
AC_OUTPUT
