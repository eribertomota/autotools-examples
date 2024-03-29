# -*- autoconf -*-
# Process this file with autoconf to produce a configure script.

# Copyright (C) 1991, 1993-2008 Free Software Foundation, Inc.

# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

dnl Written by Jim Meyering.

AC_PREREQ(2.61)

# Make inter-release version strings look like, e.g., v6.9-219-g58ddd, which
# indicates that it is built from the 219th delta (in _some_ repository)
# following the v6.9 tag, and that 58ddd is a prefix of the commit SHA1.
AC_INIT([dc3dd], [7.2.646], [dc3dd@dc3.mil])
AC_CONFIG_SRCDIR([src/dc3dd.c])

AC_CONFIG_AUX_DIR(build-aux)
AC_CONFIG_HEADERS([lib/config.h:lib/config.hin])

AM_INIT_AUTOMAKE

AC_PROG_CC_STDC
AM_PROG_CC_C_O
AC_PROG_CPP
AC_PROG_GCC_TRADITIONAL
AC_PROG_RANLIB
AC_PROG_LN_S
gl_EARLY
gl_INIT
coreutils_MACROS
DC3_HDPARM

AC_FUNC_FORK

optional_bin_progs=
AC_CHECK_FUNCS(uname,
	gl_ADD_PROG([optional_bin_progs], [uname]))
AC_CHECK_FUNCS(chroot,
	gl_ADD_PROG([optional_bin_progs], [chroot]))
AC_CHECK_FUNCS(gethostid,
	gl_ADD_PROG([optional_bin_progs], [hostid]))

gl_WINSIZE_IN_PTEM

AC_MSG_CHECKING(whether localtime caches TZ)
AC_CACHE_VAL(utils_cv_localtime_cache,
[if test x$ac_cv_func_tzset = xyes; then
AC_RUN_IFELSE([AC_LANG_SOURCE([[#include <time.h>
#if STDC_HEADERS
# include <stdlib.h>
#endif
extern char **environ;
void unset_TZ (void)
{
  char **from, **to;
  for (to = from = environ; (*to = *from); from++)
    if (! (to[0][0] == 'T' && to[0][1] == 'Z' && to[0][2] == '='))
      to++;
}
int main()
{
  time_t now = time ((time_t *) 0);
  int hour_GMT0, hour_unset;
  if (putenv ("TZ=GMT0") != 0)
    exit (1);
  hour_GMT0 = localtime (&now)->tm_hour;
  unset_TZ ();
  hour_unset = localtime (&now)->tm_hour;
  if (putenv ("TZ=PST8") != 0)
    exit (1);
  if (localtime (&now)->tm_hour == hour_GMT0)
    exit (1);
  unset_TZ ();
  if (localtime (&now)->tm_hour != hour_unset)
    exit (1);
  exit (0);
}]])],
[utils_cv_localtime_cache=no],
[utils_cv_localtime_cache=yes],
[# If we have tzset, assume the worst when cross-compiling.
utils_cv_localtime_cache=yes])
else
	# If we lack tzset, report that localtime does not cache TZ,
	# since we can't invalidate the cache if we don't have tzset.
	utils_cv_localtime_cache=no
fi])dnl
AC_MSG_RESULT($utils_cv_localtime_cache)
if test $utils_cv_localtime_cache = yes; then
  AC_DEFINE(LOCALTIME_CACHE, 1, [FIXME])
fi

# SCO-ODT-3.0 is reported to need -los to link programs using initgroups
AC_CHECK_FUNCS(initgroups)
if test $ac_cv_func_initgroups = no; then
  AC_CHECK_LIB(os, initgroups)
fi

AC_CHECK_FUNCS(syslog)
if test $ac_cv_func_syslog = no; then
  # syslog is not in the default libraries.  See if it's in some other.
  for lib in bsd socket inet; do
    AC_CHECK_LIB($lib, syslog, [AC_DEFINE(HAVE_SYSLOG, 1, [FIXME])
      LIBS="$LIBS -l$lib"; break])
  done
fi

AC_CACHE_CHECK([for 3-argument setpriority function],
  [utils_cv_func_setpriority],
  [AC_LINK_IFELSE(
    [AC_LANG_PROGRAM(
       [[#include <sys/time.h>
	 #include <sys/resource.h>
       ]],
       [[setpriority (0, 0, 0);]])],
    [utils_cv_func_setpriority=yes],
    [utils_cv_func_setpriority=no])])
if test $utils_cv_func_setpriority = no; then
  AC_CHECK_FUNCS([nice])
fi
case $utils_cv_func_setpriority,$ac_cv_func_nice in
*yes*)
  gl_ADD_PROG([optional_bin_progs], [nice])
esac

AC_DEFUN([coreutils_DUMMY_1],
[
  AC_REQUIRE([gl_READUTMP])
  if test $ac_cv_header_utmp_h = yes || test $ac_cv_header_utmpx_h = yes; then
    gl_ADD_PROG([optional_bin_progs], [who])
    gl_ADD_PROG([optional_bin_progs], [users])
    gl_ADD_PROG([optional_bin_progs], [pinky])
  fi
])
coreutils_DUMMY_1

AC_MSG_CHECKING(ut_host in struct utmp)
AC_CACHE_VAL(su_cv_func_ut_host_in_utmp,
[AC_LINK_IFELSE([AC_LANG_PROGRAM([[#include <sys/types.h>
#include <utmp.h>]], [[struct utmp ut; return !sizeof ut.ut_host;]])],
  [su_cv_func_ut_host_in_utmp=yes],
  [su_cv_func_ut_host_in_utmp=no])])
AC_MSG_RESULT($su_cv_func_ut_host_in_utmp)
if test $su_cv_func_ut_host_in_utmp = yes; then
  have_ut_host=1
  AC_DEFINE(HAVE_UT_HOST, 1, [FIXME])
fi

if test -z "$have_ut_host"; then
  AC_MSG_CHECKING(ut_host in struct utmpx)
  AC_CACHE_VAL(su_cv_func_ut_host_in_utmpx,
  [AC_LINK_IFELSE([AC_LANG_PROGRAM([[#include <sys/types.h>
#include <utmpx.h>]], [[struct utmpx ut; return !sizeof ut.ut_host;]])],
    [su_cv_func_ut_host_in_utmpx=yes],
    [su_cv_func_ut_host_in_utmpx=no])])
  AC_MSG_RESULT($su_cv_func_ut_host_in_utmpx)
  if test $su_cv_func_ut_host_in_utmpx = yes; then
    AC_DEFINE(HAVE_UTMPX_H, 1, [FIXME])
    AC_DEFINE(HAVE_UT_HOST, 1, [FIXME])
  fi
fi

GNULIB_BOOT_TIME([gl_ADD_PROG([optional_bin_progs], [uptime])])

AC_SYS_POSIX_TERMIOS()
gl_HEADER_TIOCGWINSZ_NEEDS_SYS_IOCTL

if test $ac_cv_sys_posix_termios = yes; then
  gl_ADD_PROG([optional_bin_progs], [stty])

  AC_MSG_CHECKING(whether termios.h needs _XOPEN_SOURCE)
  AC_CACHE_VAL(su_cv_sys_termios_needs_xopen_source,
  [AC_EGREP_CPP(yes, [#include <termios.h>
#ifdef IUCLC
yes
#endif], su_cv_sys_termios_needs_xopen_source=no,
   AC_EGREP_CPP(yes, [#define _XOPEN_SOURCE
#include <termios.h>
#ifdef IUCLC
yes
#endif], su_cv_sys_termios_needs_xopen_source=yes,
   su_cv_sys_termios_needs_xopen_source=no))])
  AC_MSG_RESULT($su_cv_sys_termios_needs_xopen_source)
  test $su_cv_sys_termios_needs_xopen_source = yes &&
    AC_DEFINE(TERMIOS_NEEDS_XOPEN_SOURCE, 1, [FIXME])

  AC_MSG_CHECKING(c_line in struct termios)
  AC_CACHE_VAL(su_cv_sys_c_line_in_termios,
  [AC_LINK_IFELSE([AC_LANG_PROGRAM([[#if TERMIOS_NEEDS_XOPEN_SOURCE
#define _XOPEN_SOURCE
#endif
#include <sys/types.h>
#include <termios.h>]], [[struct termios t; return !sizeof t.c_line;]])],
    [su_cv_sys_c_line_in_termios=yes],
    [su_cv_sys_c_line_in_termios=no])])
  AC_MSG_RESULT($su_cv_sys_c_line_in_termios)
  test $su_cv_sys_c_line_in_termios = yes \
    && AC_DEFINE(HAVE_C_LINE, 1, [FIXME])
fi

# FIXME: note that this macro appears above, too.
# I'm leaving it here for now.  This whole thing needs to be modernized...
gl_WINSIZE_IN_PTEM

gl_HEADER_TIOCGWINSZ_IN_TERMIOS_H

if test $gl_cv_sys_tiocgwinsz_needs_termios_h = no && \
   test $gl_cv_sys_tiocgwinsz_needs_sys_ioctl_h = no; then
  AC_MSG_CHECKING(TIOCGWINSZ in sys/pty.h)
  AC_CACHE_VAL(su_cv_sys_tiocgwinsz_in_sys_pty_h,
  [AC_LINK_IFELSE([AC_LANG_PROGRAM([[#include <sys/types.h>
#ifdef WINSIZE_IN_PTEM
# include <sys/stream.h>
# include <sys/ptem.h>
#endif
#include <sys/ioctl.h>
#include <sys/tty.h>
#include <sys/pty.h>]], [[int x = TIOCGWINSZ;]])],
    [su_cv_sys_tiocgwinsz_in_sys_pty_h=yes],
    [su_cv_sys_tiocgwinsz_in_sys_pty_h=no])])
  AC_MSG_RESULT($su_cv_sys_tiocgwinsz_in_sys_pty_h)

  test $su_cv_sys_tiocgwinsz_in_sys_pty_h = yes \
      && AC_DEFINE(GWINSZ_IN_SYS_PTY, 1,
                   [Define if your system defines TIOCGWINSZ in sys/pty.h.])
fi

# For src/kill.c.
AC_CHECK_DECLS([strsignal, sys_siglist, _sys_siglist, __sys_siglist], , ,
  [AC_INCLUDES_DEFAULT
#include <signal.h>])

cu_LIB_CHECK

# Build df only if there's a point to it.
if test $gl_cv_list_mounted_fs = yes && test $gl_cv_fs_space = yes; then
  gl_ADD_PROG([optional_bin_progs], [df])
fi

############################################################################
mk="$srcdir/src/Makefile.am"
# Extract all literal names from the definition of $(EXTRA_PROGRAMS)
# in $mk but don't expand the variable references.
# Append each literal name to $optional_bin_progs.
v=EXTRA_PROGRAMS
for gl_i in `sed -n '/^'$v' =/,/[[^\]]$/p' $mk \
    | sed 's/^  *//;/^\$.*/d;/^'$v' =/d' \
    | tr -s '\\015\\012\\\\' '  '`; do
  gl_ADD_PROG([optional_bin_progs], $gl_i)
done

# As above, extract literal names from the definition of $(no_install__progs)
# in $mk but don't expand the variable references.
v=no_install__progs
t=`sed -n '/^'$v' =/,/[[^\]]$/p' $mk \
    | sed 's/^  *//;/^\$.*/d;/^'$v' =/d' \
    | tr -s '\\015\\012\\\\' '   '`
# Remove any trailing space.
no_install_progs_default=`echo "$t"|sed 's/ $//'`

# Unfortunately, due to the way autoconf's AS_HELP_STRING works, the list
# of default-not-installed programs, "arch hostname su", must appear in two
# places: in this file below, and in $mk.  Using "$no_install_progs_default"
# below cannot work.  And we can't substitute the names into $mk because
# automake needs the literals, too.
# The compromise is to ensure that the space-separated list extracted
# above matches the literal 2nd argument below.
c="$srcdir/configure.ac"
re='^g''l_INCLUDE_EXCLUDE_PROG(.* [\[\(.*\)\]])'
t=`sed -n '/'"$re"'/{s/'"$re"'/\1/;s/,/ /gp
}' $c`
case $t in
  $no_install_progs_default) ;;
  *) AC_MSG_ERROR([[internal error: g'l_INCLUDE_EXCLUDE_PROG's 2nd arg, $t,
                   does not match the list of default-not-installed programs
		   ($no_install_progs_default) also recorded in $mk]],
		   1) ;;
esac

# Given the name of a variable containing a space-separated list of
# install-by-default programs and the actual list do-not-install-by-default
# programs, modify the former variable to reflect any "do-install" and
# "don't-install" requests.
# I.e., add any program name specified via --enable-install-program=..., and
# remove any program name specified via --enable-no-install-program=...
# Note how the second argument below is a literal, with "," separators.
# That is required due to the way the macro works, and since the
# corresponding ./configure option argument is comma-separated on input.
#gl_INCLUDE_EXCLUDE_PROG([optional_bin_progs], [arch,hostname,su])

# Set INSTALL_SU if su installation has been requested via
# --enable-install-program=su.
AC_SUBST([INSTALL_SU])
case " $optional_bin_progs " in
  *' su '*) INSTALL_SU=yes ;;
  *)        INSTALL_SU=no ;;
esac

MAN=`echo "$optional_bin_progs "|sed 's/ /.1 /g;s/ $//'|tr -d '\\015\\012'`

# Change ginstall.1 to "install.h" in $MAN.
MAN=`for m in $MAN; do test $m = ginstall.1 && m=install.1; echo $m; done \
  | tr '\015\012' ' '; echo`

# Remove [.1, since writing a portable rule for it in man/Makefile.am
# is not practical.  The sed LHS below uses the autoconf quadrigraph
# representing '['.
MAN=`echo "$MAN"|sed 's/\@<:@\.1//'`

OPTIONAL_BIN_PROGS=`echo "$optional_bin_progs "|sed 's/ /\$(EXEEXT) /g;s/ $//'`
AC_SUBST([OPTIONAL_BIN_PROGS])
NO_INSTALL_PROGS_DEFAULT=$no_install_progs_default
AC_SUBST([NO_INSTALL_PROGS_DEFAULT])

# Arrange to rerun configure whenever the file, src/Makefile.am,
# containing the list of program names changes.
CONFIG_STATUS_DEPENDENCIES='$(top_srcdir)/src/Makefile.am'
AC_SUBST([CONFIG_STATUS_DEPENDENCIES])
############################################################################

AM_GNU_GETTEXT([external], [need-formatstring-macros])
AM_GNU_GETTEXT_VERSION([0.15])

DC3_HDPARM_SET

# For a test of uniq: it uses the $LOCALE_FR envvar.
gt_LOCALE_FR

AC_CONFIG_FILES(
  Makefile
  lib/Makefile
  man/Makefile
  po/Makefile.in
  src/Makefile
  )
AC_OUTPUT
