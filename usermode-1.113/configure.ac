AC_INIT([usermode], [1.113], [https://pagure.io/usermode], ,
        [https://pagure.io/usermode])
AC_PREREQ([2.63b])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_SRCDIR([userhelper.c])
AC_CONFIG_AUX_DIR([admin])
AM_INIT_AUTOMAKE([no-dist-gzip dist-xz -Wall])
AC_PREFIX_DEFAULT([/usr])

AC_PROG_CC
AM_PROG_CC_C_O
AM_PROG_AR
AC_PROG_RANLIB
AC_PATH_PROG([MOUNT], [mount], [/bin/mount], [/sbin:/bin:/usr/sbin:/usr/bin])
AC_PATH_PROG([UMOUNT], [umount], [/bin/umount], [/sbin:/bin:/usr/sbin:/usr/bin])
AC_PATH_PROG([MKFS], [mkfs], [/sbin/mkfs], [/sbin:/bin:/usr/sbin:/usr/bin])
AC_PATH_PROG([FDFORMAT], [fdformat], [/usr/bin/fdformat],
	     [/sbin:/bin:/usr/sbin:/usr/bin])
AC_DEFINE_UNQUOTED([PATH_MOUNT], ["$MOUNT"], [Path to the mount command])
AC_DEFINE_UNQUOTED([PATH_UMOUNT], ["$UMOUNT"], [Path to the umount command])
AC_DEFINE_UNQUOTED([PATH_FDFORMAT], ["$FDFORMAT"],
		   [Path to the fdformat command])
AC_DEFINE_UNQUOTED([PATH_MKFS], ["$MKFS"], [Path to the mkfs command])

AC_SYS_LARGEFILE

GETTEXT_PACKAGE=usermode
AC_SUBST([GETTEXT_PACKAGE])
AM_GLIB_GNU_GETTEXT
IT_PROG_INTLTOOL
AC_PATH_XTRA
PKG_CHECK_MODULES([GLIB], [glib-2.0])
PKG_CHECK_MODULES([GTK], [gtk+-2.0 >= 2.23])
PKG_CHECK_MODULES([LIBUSER], [libuser])
AC_CACHE_CHECK([for startup notification], [mitr_cv_lib_sn],
[mitr_cv_lib_sn=no
if pkg-config libstartup-notification-1.0 ; then
  mitr_cv_lib_sn=yes
fi])
if test $mitr_cv_lib_sn = yes; then
	PKG_CHECK_MODULES([SN], [libstartup-notification-1.0])
	AC_DEFINE([USE_STARTUP_NOTIFICATION], [1],
		  [Define if consolehelper should interact with startup notification.])
	AC_DEFINE([SN_API_NOT_YET_FROZEN], [1],
		  [Define if you want to use libsn, even though it is not yet API-stabilized, because we need to use it.])
fi
AC_CHECK_FUNC([pam_start], ,
              [AC_CHECK_LIB([pam], [pam_start], [PAM_LIBS="-lpam"])])
AC_CHECK_FUNC([misc_conv], ,
	      [AC_CHECK_LIB([pam_misc], [misc_conv],
			    [PAM_LIBS="-lpam_misc $PAM_LIBS"])])
AC_SUBST([PAM_LIBS])

AC_MSG_CHECKING([whether we should avoid deprecated functions])
AC_ARG_ENABLE([deprecation],
	      AS_HELP_STRING([--enable-deprecation],
	      		     [prohibit use of deprecated GTK+ features]),
	      [usedeprecation=$enableval], [usedeprecation=no])
if test "x$usedeprecation" = xyes ; then
	AC_DEFINE([G_DISABLE_DEPRECATED], ,
		  [Disable use of deprecated GLib APIs.])
	AC_DEFINE([GTK_DISABLE_DEPRECATED], ,
		  [Disable use of deprecated GTK+ APIs.])
fi
AC_MSG_RESULT([$usedeprecation])

AC_MSG_CHECKING([whether we should enable debugging messages])
AC_ARG_ENABLE([debug],
	      AS_HELP_STRING([--enable-debug], [Enable debugging messages]),
	      [debug=${enableval}], [debug=no])
if test "x$debug" != xno ; then
	AC_DEFINE([DEBUG_USERHELPER], [1], [Enable debugging messages])
fi
AC_MSG_RESULT([$debug])

AC_MSG_CHECKING([whether we should use fexecve])
AC_ARG_WITH([fexecve],
		AS_HELP_STRING([--with-fexecve], [use fexecve instead of execv]),
		[use_fexecve="$withval"], [use_fexecve=auto])
fexecve_found=no
if test "x$use_fexecve" = xno; then
	AC_MSG_RESULT([no])
else
	AC_MSG_RESULT([testing])
	AC_CHECK_FUNCS([fexecve], [fexecve_found=yes], [fexecve_found=no])
	if test x$fexecve_found = xno; then
		if test "x$use_fexecve" = xyes; then
			AC_MSG_ERROR([fexecve is required but not found])
		else
			AC_MSG_WARN([fexecve is not found - execv will be used instead])
		fi
	fi
fi

AC_MSG_CHECKING([whether we should use ElectricFence])
AC_ARG_WITH([efence],
	    AS_HELP_STRING([--with-efence], [Enable use of ElectricFence]),
	    [efence=${withval}], [efence=no])
EFENCE_LIBS=
if test "x$efence" != xno ; then
	EFENCE_LIBS="-lefence"
fi
AC_SUBST([EFENCE_LIBS])
AC_MSG_RESULT([$efence])

AC_MSG_CHECKING([whether we should use SELinux])
AC_ARG_WITH([selinux],
	    AS_HELP_STRING([--with-selinux], [Use SELinux functionality]),
	    [selinux=${withval}], [selinux=no])
SELINUX_LIBS=
if test "x$selinux" != xno ; then
	AC_DEFINE([WITH_SELINUX], [1], [Use SELinux features])
	SELINUX_LIBS="-lselinux"
fi
AC_SUBST([SELINUX_LIBS])
AC_MSG_RESULT([$selinux])

if test x$GCC = xyes ; then
	AC_CACHE_CHECK([for available GCC warning flags],
		       [mitr_cv_prog_gcc_warnings],
	[mitr_cv_prog_gcc_warnings=""
	for i in -Wall -W -Wcast-align -Wmissing-noreturn -Wpointer-arith dnl
 -Wshadow -Wstrict-prototypes -Wwrite-strings; do
		oldcflags=$CFLAGS
		CFLAGS="$CFLAGS $i"
		AC_COMPILE_IFELSE([AC_LANG_PROGRAM([], [])],
		    [mitr_cv_prog_gcc_warnings="$mitr_cv_prog_gcc_warnings $i"])
		CFLAGS=$oldcflags
	done])
	CFLAGS="$CFLAGS $mitr_cv_prog_gcc_warnings"
	AC_MSG_CHECKING([whether we should use -Werror])
	AC_ARG_ENABLE([gccwerror],
		      AS_HELP_STRING([--enable-gccwerror],
				     [Enable -Werror with GCC]),
				     [gccwerror=${enableval}], [gccwerror=no])
	if test "x$gccwerror" != xno ; then
		CFLAGS="$CFLAGS -Werror"
	fi
	AC_MSG_RESULT([$gccwerror])
fi

AC_CONFIG_FILES([Makefile po/Makefile.in])
AC_OUTPUT
