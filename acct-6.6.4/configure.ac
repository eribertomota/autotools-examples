dnl/*
dnl    Copyright (C) 2009, 2010, 2011, 2013, 2014,2017
dnl    Markus Gothe <nietzsche@lysator.liu.se>
dnl
dnl    This program is free software: you can redistribute it and/or modify
dnl    it under the terms of the GNU General Public License as
dnl    published by the Free Software Foundation, either version 3 of the
dnl    License, or (at your option) any later version.
dnl
dnl    This program is distributed in the hope that it will be useful,
dnl    but WITHOUT ANY WARRANTY; without even the implied warranty of
dnl    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
dnl    GNU General Public License for more details.
dnl
dnl    You should have received a copy of the GNU General Public License
dnl    along with this program.  If not, see <http://www.gnu.org/licenses/>.
dnl */


dnl $Id: configure.ac 97 2017-04-05 21:10:58Z nihilus $
dnl Process this file with autoconf to produce a configure script.

dnl init autoconf
AC_REQ(2.63)
AC_INIT([acct],[6.6.4],[nietzsche@lysator.liu.se])
dnl AH_HEADER
AC_CONFIG_HEADERS([config.h:config.h.in])
AC_CONFIG_SRCDIR([ac.c])
AC_CONFIG_AUX_DIR([.])
AC_REQUIRE_AUX_FILE([install-sh])
AC_CANONICAL_BUILD
AC_CANONICAL_HOST
AC_CANONICAL_TARGET

dnl macros for automake
AM_INIT_AUTOMAKE([gnu 1.11 check-news dist-bzip2 std-options subdir-objects])

dnl Set it in C99-mode
AC_SYS_INTERPRETER
AC_USE_SYSTEM_EXTENSIONS
dnl GNUlib
gl_EARLY
gl_INIT

AC_PROG_CC_C99
dnl AC_PROG_CPP
AC_REQUIRE_CPP
AC_PROG_CC_C_O
AC_PROG_CXX
AC_C_FLEXIBLE_ARRAY_MEMBER
AC_C_VARARRAYS
AC_PROG_CC
AC_PROG_CXX
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_PROG_CPP
AC_PROG_AWK

if test "x$GCC" = "xyes"; then
 CFLAGS="${CFLAGS} -Wall -Wmissing-prototypes"
fi

AC_HEADER_STDC
AC_PROG_CC_STDC
AC_PROG_CC_C89
AC_PROG_GCC_TRADITIONAL
AC_PROG_INSTALL

LT_PREREQ([2.4])
LT_INIT([dlopen win32-dll])
AC_SUBST([LIBTOOL_DEPS])

dnl /usr/bin/doxygen
AC_PATH_PROG(DOXYGEN, doxygen, "")
AM_CONDITIONAL(CONFIG_DOXYGEN, [test ! -z "$DOXYGEN"])

dnl C-stuff

AC_C_CONST
AC_C_INLINE
AC_C_RESTRICT
AC_C_VOLATILE
AC_SYS_POSIX_TERMIOS
AC_SYS_LARGEFILE

dnl
dnl Functions
dnl

dnl AM_GNU_GETTEXT
AC_FUNC_ERROR_AT_LINE
AC_FUNC_FSEEKO
AC_FUNC_ALLOCA
AC_FUNC_LSTAT_FOLLOWS_SLASHED_SYMLINK
AC_FUNC_MALLOC
AC_FUNC_MKTIME
AC_FUNC_REALLOC
AC_FUNC_OBSTACK
AC_FUNC_STRERROR_R
AC_CHECK_FUNCS([getcwd getpagesize inet_ntoa isascii localtime_r memmove memset pathconf rmdir strcasecmp strchr strdup strerror strtol uname])
AC_CHECK_FUNC(snprintf, AC_DEFINE(HAVE_SNPRINTF, 1, [Define if your system has the SNPRINTF system call.]))
AC_CHECK_FUNC(__builtin_unreachable, AC_DEFINE(HAVE_UNREACHBLE, 1, [Define if your compiler support __builtin_unreachable().]))

dnl
dnl Headers
dnl

AC_HEADER_TIME
AC_HEADER_STDBOOL
AC_HEADER_DIRENT
AC_CHECK_HEADERS([OS.h arpa/inet.h fcntl.h inttypes.h libintl.h limits.h locale.h malloc.h netdb.h netinet/in.h stddef.h stdint.h stdlib.h string.h sys/param.h sys/socket.h sys/time.h unistd.h utmp.h utmpx.h wchar.h errno.h])

dnl
dnl find out where various programs reside on this system
dnl

AC_PATH_PROGS(SYS_LAST, last, echo, /bin /etc /sbin /usr/bin /usr/etc /usr/sbin /usr/ucb /usr/local/bin /usr/local/etc /usr/local/sbin )
AC_PATH_PROGS(SYS_LASTCOMM, lastcomm, echo, /bin /etc /sbin /usr/bin /usr/etc /usr/sbin /usr/ucb /usr/local/bin /usr/local/etc /usr/local/sbin )
AC_PATH_PROGS(SYS_AC, ac, echo, /bin /etc /sbin /usr/bin /usr/etc /usr/sbin /usr/ucb /usr/local/bin /usr/local/etc /usr/local/sbin )
AC_PATH_PROGS(SYS_SA, sa, echo, /bin /etc /sbin /usr/bin /usr/etc /usr/sbin /usr/ucb /usr/local/bin /usr/local/etc /usr/local/sbin )

dnl
dnl Check for stat.st_rdev
dnl

AC_CHECK_MEMBERS([struct stat.st_rdev])

dnl
dnl find out what fields are valid in utmp.h
dnl

AC_CHECK_MEMBERS([struct utmpx.ut_host],,,[$utmp_includes])
AC_CHECK_MEMBERS([struct utmp.ut_host],,,[$utmp_includes])

dnl
dnl
dnl

AC_ARG_ENABLE([linux-multiformat],
	      AS_HELP_STRING([--enable-linux-multiformat],[support various predefined linux acct file formats 
			     instead of the one defined in <sys/acct.h>]),
	      [],
	      [
		case $target_os in
		*linux*)
			enable_linux_multiformat=yes
			;;
		*)
			enable_linux_multiformat=no 
			;;
		esac
	      ]
	      )

AS_IF([test "x$enable_linux_multiformat" = "xyes"],
      AC_DEFINE(LINUX_MULTIFORMAT, 1, [Define to use "linux-acct.h" instead of <sys/acct.h>])
      DUMP_ACCT_PROG=dump-acct
      ACCTON_PROG=accton
      LASTCOMM_PROG=lastcomm
      SA_PROG=sa
      ACCTON_MAN=accton.8
      LASTCOMM_MAN=lastcomm.1
      SA_MAN=sa.8
      AC_DEFINE(HAVE_ACUTIME, 1, [Define if <sys/acct.h> has the AC_UTIME field.])
      AC_DEFINE(ACUTIME_COMPT, 1, [Define if <sys/acct.h>'s AC_UTIME field is a COMP_T.])
      AC_DEFINE(HAVE_ACSTIME, 1, [Define if <sys/acct.h> has the AC_STIME field.])
      AC_DEFINE(ACSTIME_COMPT, 1, [Define if <sys/acct.h>'s AC_STIME field is a COMP_T.])
      AC_DEFINE(HAVE_ACETIME, 1, [Define if <sys/acct.h> has the AC_ETIME field.])
      AC_DEFINE(HAVE_ACIO, 1, [Define if <sys/acct.h> has the AC_IO field.])
      AC_DEFINE(ACIO_COMPT, 1, [Define if <sys/acct.h>'s AC_IO field is a COMP_T.])
      AC_DEFINE(HAVE_ACMEM, 1, [Define if <sys/acct.h> has the AC_MEM field.])
      AC_DEFINE(ACMEM_COMPT, 1, [Define if <sys/acct.h>'s AC_MEM field is a COMP_T.])
      AC_DEFINE(HAVE_PAGING, 1, [Define if <sys/acct.h> has the AC_MINFLT, AC_MAJFLT and AC_SWAPS fields.])
      AC_DEFINE(ACMINFLT_COMPT, 1, [Define if <sys/acct.h>'s AC_MINFLT field is a COMP_T.])
      AC_DEFINE(ACMAJFLT_COMPT, 1, [Define if <sys/acct.h>'s AC_MAJFLT field is a COMP_T.])
      AC_DEFINE(ACSWAPS_COMPT, 1, [Define if <sys/acct.h>'s AC_SWAPS field is a COMP_T.])
      AC_DEFINE(HAVE_COMP_T, 1, [Define if <sys/acct.h> uses the COMP_T type.])
      , [
dnl
dnl figure out where acct.h lives
dnl and whether fields are int/comp_t
dnl
AC_CHECK_HEADER(sys/acct.h,
		AC_DEFINE(HAVE_SYS_ACCT_H, ,[Define if you have the <sys/acct.h> header file.])
		DUMP_ACCT_PROG=dump-acct
		ACCTON_PROG=accton
		LASTCOMM_PROG=lastcomm
		SA_PROG=sa
		ACCTON_MAN=accton.8
		LASTCOMM_MAN=lastcomm.1
		SA_MAN=sa.8
		AC_EGREP_HEADER(ac_utime, sys/acct.h, 
			AC_DEFINE(HAVE_ACUTIME, 1, [Define if <sys/acct.h> has the AC_UTIME field.])
			AC_EGREP_HEADER(comp_t.*ac_utime, sys/acct.h,AC_DEFINE(ACUTIME_COMPT, 1, [Define if <sys/acct.h>'s AC_UTIME field is a COMP_T.]))
		)
		AC_EGREP_HEADER(ac_stime, sys/acct.h,
				AC_DEFINE(HAVE_ACSTIME, 1, [Define if <sys/acct.h> has the AC_STIME field.])
				AC_EGREP_HEADER(comp_t.*ac_stime, sys/acct.h,
						AC_DEFINE(ACSTIME_COMPT, 1, [Define if <sys/acct.h>'s AC_STIME field is a COMP_T.]))
		)
		AC_EGREP_HEADER(ac_etime, sys/acct.h,
				AC_DEFINE(HAVE_ACETIME, 1, [Define if <sys/acct.h> has the AC_ETIME field.])
				AC_EGREP_HEADER(comp_t.*ac_etime, sys/acct.h,
						AC_DEFINE(ACETIME_COMPT, 1, [Define if <sys/acct.h>'s AC_ETIME field is a COMP_T.]))
		)
		AC_EGREP_HEADER(ac_io, sys/acct.h,
				AC_DEFINE(HAVE_ACIO, 1, [Define if <sys/acct.h> has the AC_IO field.])
				AC_EGREP_HEADER(comp_t.*ac_io, sys/acct.h,
						AC_DEFINE(ACIO_COMPT, 1, [Define if <sys/acct.h>'s AC_IO field is a COMP_T.]))
		)
		AC_EGREP_HEADER(ac_mem, sys/acct.h,
				AC_DEFINE(HAVE_ACMEM, 1, [Define if <sys/acct.h> has the AC_MEM field.])
				AC_EGREP_HEADER(comp_t.*ac_mem, sys/acct.h,
						AC_DEFINE(ACMEM_COMPT, 1, [Define if <sys/acct.h>'s AC_MEM field is a COMP_T.]))
		)
		AC_EGREP_HEADER(ac_minflt, sys/acct.h,
				AC_EGREP_HEADER(ac_majflt, sys/acct.h,
						AC_EGREP_HEADER(ac_swaps, sys/acct.h,
								AC_DEFINE(HAVE_PAGING, 1, [Define if <sys/acct.h> has the AC_MINFLT, AC_MAJFLT and AC_SWAPS fields.])
								AC_EGREP_HEADER(comp_t.*ac_minflt, sys/acct.h,
									AC_DEFINE(ACMINFLT_COMPT, 1, [Define if <sys/acct.h>'s AC_MINFLT field is a COMP_T.]))
								AC_EGREP_HEADER(comp_t.*ac_mayflt, sys/acct.h,
									AC_DEFINE(ACMAJFLT_COMPT, 1, [Define if <sys/acct.h>'s AC_MAJFLT field is a COMP_T.]))
								AC_EGREP_HEADER(comp_t.*ac_swaps, sys/acct.h,
									AC_DEFINE(ACSWAPS_COMPT, 1, [Define if <sys/acct.h>'s AC_SWAPS field is a COMP_T.]))
						)
				)
		)
		AC_EGREP_HEADER([comp_t],[sys/acct.h],[AC_DEFINE(HAVE_COMP_T, 1, Define if <sys/acct.h> uses the COMP_T type.)])
  ) ]
)

dnl types
AC_TYPE_PID_T dnl for sys/acct.h
AC_TYPE_UID_T dnl same as above
AC_TYPE_OFF_T
AC_TYPE_UID_T
AC_TYPE_INT32_T
AC_TYPE_MODE_T
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T
AC_CHECK_TYPES([ptrdiff_t])


AC_DIAGNOSE([obsolete],[your code may safely assume C89 semantics that RETSIGTYPE is void.
Remove this warning and the `AC_CACHE_CHECK' when you adjust the code.])dnl
AC_CACHE_CHECK([return type of signal handlers],[ac_cv_type_signal],[AC_COMPILE_IFELSE(
[AC_LANG_PROGRAM([#include <sys/types.h>
#include <signal.h>
],
		 [return *(signal (0, 0)) (0) == 1;])],
		   [ac_cv_type_signal=int],
		   [ac_cv_type_signal=void])])
AC_DEFINE_UNQUOTED([RETSIGTYPE],[$ac_cv_type_signal],[Define as the return type of signal handlers
		    (`int' or `void').])


AC_C_BIGENDIAN(AC_DEFINE(BYTEORDER,0x80,
			 [0x80 for big-endian, 0x00 for little-endian.]),
               AC_DEFINE(BYTEORDER,0x00,
			 [0x80 for big-endian, 0x00 for little-endian.]),)
echo checking for kitchen sink... You find a ring in the sink!

dnl Substitute program names for automake
AC_SUBST(DUMP_ACCT_PROG)
AC_SUBST(ACCTON_PROG)
AC_SUBST(LASTCOMM_PROG)
AC_SUBST(SA_PROG)

dnl Substitute manual page names for automake
AC_SUBST(ACCTON_MAN)
AC_SUBST(LASTCOMM_MAN)
AC_SUBST(SA_MAN)

dnl Dump the makefiles and etc.
AC_CONFIG_FILES([Makefile lib/Makefile files.h version.h])
AC_OUTPUT
