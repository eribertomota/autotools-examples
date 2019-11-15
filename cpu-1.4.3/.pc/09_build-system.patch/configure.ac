AC_PREREQ(2.52)
AC_INIT(cpu, 1.4.3, cpu-users@lists.sourceforge.net, cpu)
AM_INIT_AUTOMAKE(cpu, 1.4.3)
AM_CONFIG_HEADER(src/include/config.h)

dnl Checks for programs.
AC_PROG_AWK
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_PROG_LIBTOOL

AC_FUNC_CHOWN
AC_FUNC_LSTAT
AC_TYPE_UID_T

AC_CHECK_HEADERS(stdint.h crypt.h sys/time.h errno.h fcntl.h limits.h sys/param.h strings.h)

dnl Check system type
case "$host_os" in
linux*)
     AC_DEFINE(LINUX,1,[This is a Linux system])
     ;;
freebsd*)
     AC_DEFINE_UNQUOTED(SOMEBSD,1,[This is a BSD system])
     CFLAGS="-pthread $CFLAGS"
     ;;
openbsd*)
     AC_DEFINE_UNQUOTED(SOMEBSD,1,[This is a BSD system])
     CFLAGS="-pthread $CFLAGS"
     ;;
netbsd*)
     AC_DEFINE_UNQUOTED(SOMEBSD,1,[This is a BSD system])
     CFLAGS="-pthread $CFLAGS"
     ;;
*solaris*)
     AC_DEFINE_UNQUOTED(SOLARIS,1,[This is a Solaris system])
     AC_DEFINE_UNQUOTED(_REENTRANT,1,[Need with solaris or errno doesnt work])
     AC_CHECK_LIB(resolv, res_init)
     ;;
*arm-linux*)
     AC_DEFINE(LINUX,1,[This is a Linux system])
     CFLAGS="-D_REENTRANT -fPIC -pipe $CFLAGS"
     ;;
*)
     AC_MSG_RESULT(Unrecognised OS $host_os)
     AC_DEFINE_UNQUOTED(OTHEROS,1,[Some strange OS])
     AC_MSG_RESULT(otheros)
     ;;
esac

AM_PROG_LIBTOOL

AC_CHECK_LIB(dl, dlopen)
AC_CHECK_LIB(crypt, crypt)

developer=false
AC_MSG_CHECKING([if developer options are wanted])
AC_ARG_ENABLE(developer,
	      AC_HELP_STRING([--enable-developer],
			     [Turn on developer warnings and debugging (default=no)]),
[
AC_MSG_RESULT(yes)
AC_DEFINE(DEVELOPER, 1,
	[Define if you are a developer])
developer=true
CFLAGS="$CFLAGS -Wall -Wno-sign-compare -Werror -ggdb"
],
[
AC_MSG_RESULT(no)
CFLAGS="$CFLAGS -w"
])

debug=false
AC_MSG_CHECKING([if debugging options are wanted])
AC_ARG_ENABLE(debug,
	      AC_HELP_STRING([--enable-debug],
			     [Turn on debugging (default=no)]),
[
AC_MSG_RESULT(yes)
AC_DEFINE(DEBUG, 1,
	[Define if you are debugging])
debug=true
CFLAGS="$CFLAGS -Wall -ggdb"
],
[
AC_MSG_RESULT(no)
])

dmalloc=false
AC_MSG_CHECKING([if malloc debugging is wanted])
AC_ARG_WITH(dmalloc,
	    AC_HELP_STRING([--with-dmalloc=PFX],
		 	   [use dmalloc as in, http://www.dmalloc.com/dmalloc.tar.gz]),
[ dnl ACTION-IF-GIVEN
  AC_MSG_RESULT(yes)
  if test "$with_dmalloc" != "yes"; then
    LDFLAGS="$LDFLAGS -L$with_dmalloc/lib"
    CPPFLAGS="$CPPFLAGS -I$with_dmalloc/include"
  fi
  AC_CHECK_LIB(dmalloc, dmalloc_debug,
   [
    LIBS="$LIBS -ldmalloc"
    CFLAGS="$CFLAGS -ggdb"
   ],
   [
    AC_MSG_ERROR(could not find dmalloc_debug in libdmalloc, is it installed?)
   ])
  AC_CHECK_HEADERS([dmalloc.h], [], AC_MSG_ERROR(Could not find dmalloc.h))
  AC_DEFINE(HAVE_DMALLOC,1,
	[Define if using the dmalloc debugging malloc package])
  dmalloc=true
],
[ dnl ACTION-IF-NOT-GIVEN
  AC_MSG_RESULT(no)
])

libcrack=false
AC_MSG_CHECKING(for cracklib support)
AC_ARG_WITH(libcrack,
	    AC_HELP_STRING(--with-libcrack=PFX,
	       [use cracklib as in
http://www.crypticide.org/users/alecm/security]),
[ dnl ACTION-IF-GIVEN
  AC_MSG_RESULT(yes)
  if test "$with_libcrack" != "yes"; then
    LDFLAGS="$LDFLAGS -L$with_libcrack/lib"
    CPPFLAGS="$CPPFLAGS -I$with_libcrack/include"
  fi
  AC_CHECK_LIB(crack, FascistCheck,,
   [
    AC_MSG_ERROR(could not find FascistCheck in libcrack, is it installed?)
   ])
  AC_CHECK_HEADERS([crack.h],, AC_MSG_ERROR(Could not find crack.h))
  libcrack=true
],
[ dnl ACTION-IF-NOT-GIVEN
  AC_MSG_RESULT(no)
])

ldap=false
tls=false
AC_MSG_CHECKING(where ldap development files are)
AC_ARG_WITH(ldap,
	    AC_HELP_STRING([--with-ldap=PFX], [Base of ldap files]),
[ dnl ACTION-IF-GIVEN
     AC_MSG_RESULT("$with_ldap")
if test "$with_ldap" != "yes"; then
     LDFLAGS="$LDFLAGS -L$with_ldap/lib"
     CPPFLAGS="$CPPFLAGS -I$with_ldap/include"
fi
     AC_CHECK_LIB(lber, main)
     AC_CHECK_LIB(ldap, main, [], AC_MSG_ERROR(Could not find libldap))
     AC_CHECK_HEADERS([lber.h], [], AC_MSG_ERROR(Could not find lber.h))
     AC_CHECK_HEADERS([ldap.h], [], AC_MSG_ERROR(Could not find ldap.h),
[#if HAVE_LBER_H
#include <lber.h>
#endif
])
     ldap=true
     AC_CHECK_FUNCS(ldap_initialize ldap_start_tls_s, tls=true,
		    AC_MSG_NOTICE([TLS Support is unavailable]))
],
[ dnl ACTION-IF-NOT-GIVEN
     AC_CHECK_LIB(lber, main)
     AC_CHECK_LIB(ldap, main, [], AC_MSG_ERROR(Could not find libldap))
     AC_CHECK_HEADERS([lber.h], [], AC_MSG_ERROR(Could not find lber.h))
     AC_CHECK_HEADERS([ldap.h], [], AC_MSG_ERROR(Could not find ldap.h),
[#if HAVE_LBER_H
#include <lber.h>
#endif
])
     ldap=true
     AC_CHECK_FUNCS(ldap_initialize ldap_start_tls_s, tls=true,
     		    AC_MSG_NOTICE([TLS Support is unavailable]))
])

flatfile=false
AC_MSG_CHECKING([whether to build flatfile support])
AC_ARG_WITH(flatfile,
	      AC_HELP_STRING([--with-flatfile],
			     [Turn on flatfile support]),
[
if test "$developer" = "false"
then
	flatfile=false
	AC_MSG_RESULT(Only developers can build flatfile support)
else

	AC_MSG_RESULT(yes)
	flatfile=true
fi
],
[
AC_MSG_RESULT(no)
])

AC_HEADER_DIRENT
AC_HEADER_STDC
AC_HEADER_TIME

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_PID_T
AC_TYPE_SIZE_T
AC_HEADER_TIME
AC_STRUCT_TM
AC_CHECK_TYPES([bool])

dnl Checks for library functions.
AC_FUNC_MEMCMP
AC_FUNC_MMAP
AC_TYPE_SIGNAL
AC_FUNC_STRFTIME
AC_FUNC_VPRINTF
AC_FUNC_FORK
AC_FUNC_SELECT_ARGTYPES
AC_FUNC_MALLOC
AC_FUNC_STAT
AC_FUNC_CLOSEDIR_VOID
AC_CHECK_FUNCS(bzero strstr memset strcasecmp strdup getpass gettimeofday mkdir rmdir strchr)
AC_FUNC_ALLOCA

AM_CONDITIONAL(HAVE_LDAP, test x$ldap = xtrue)
AM_CONDITIONAL(HAVE_PASSWD, test x$flatfile = xtrue)

AC_CONFIG_FILES(Makefile
doc/Makefile
doc/man/Makefile
src/Makefile
src/util/Makefile
src/main/Makefile
src/plugins/Makefile
src/plugins/ldap/Makefile
src/plugins/passwd/Makefile
)
AC_OUTPUT

AC_MSG_NOTICE([NOTICE: Support for the following will be built:])
AC_MSG_NOTICE([        DMALLOC: $dmalloc])
AC_MSG_NOTICE([        DEVELOPER: $developer])
AC_MSG_NOTICE([        DEBUG: $debug])
AC_MSG_NOTICE([        LIBCRACK: $libcrack])
AC_MSG_NOTICE([        LDAP: $ldap])
AC_MSG_NOTICE([           TLS: $tls])
AC_MSG_NOTICE([        FLATFILE: $flatfile])
