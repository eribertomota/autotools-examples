dnl Autoconf configuration for pam-afs-session.
dnl
dnl Written by Russ Allbery <eagle@eyrie.org>
dnl Copyright 2015 Russ Allbery <eagle@eyrie.org>
dnl Copyright 2006, 2007, 2008, 2010, 2013
dnl     The Board of Trustees of the Leland Stanford Junior University
dnl
dnl This file is free software; the authors give unlimited permission to copy
dnl and/or distribute it, with or without modifications, as long as this
dnl notice is preserved.

AC_PREREQ([2.64])
AC_INIT([pam-afs-session], [2.6], [eagle@eyrie.org])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_LIBOBJ_DIR([portable])
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE([1.11 check-news foreign silent-rules subdir-objects
    -Wall -Werror])
AM_MAINTAINER_MODE

dnl Detect unexpanded macros.
m4_pattern_forbid([^_?RRA_])

AC_PROG_CC
AC_USE_SYSTEM_EXTENSIONS
RRA_PROG_CC_CLANG
AC_SYS_LARGEFILE
AM_PROG_CC_C_O
AM_PROG_AR
AC_PROG_INSTALL
LT_INIT([disable-static])
AC_CANONICAL_HOST
RRA_LD_VERSION_SCRIPT

dnl Probe for the functionality of the PAM libraries and their include file
dnl naming.  Mac OS X puts them in pam/* instead of security/*.
AC_SEARCH_LIBS([pam_set_data], [pam])
AC_CHECK_FUNCS([pam_getenv pam_getenvlist pam_modutil_getpwnam])
AC_REPLACE_FUNCS([pam_syslog pam_vsyslog])
AC_CHECK_HEADERS([security/pam_modutil.h], [],
    [AC_CHECK_HEADERS([pam/pam_modutil.h])])
AC_CHECK_HEADERS([security/pam_appl.h], [],
    [AC_CHECK_HEADERS([pam/pam_appl.h], [],
        [AC_MSG_ERROR([No PAM header files found])])])
AC_CHECK_HEADERS([security/pam_ext.h], [],
    [AC_CHECK_HEADERS([pam/pam_ext.h])])
RRA_HEADER_PAM_CONST
RRA_HEADER_PAM_STRERROR_CONST

dnl Needed for the pam_vsyslog replacement function.
AC_DEFINE([MODULE_NAME], ["pam_afs_session"],
    [The name of the PAM module, used by the pam_vsyslog replacement.])

dnl Determine the path to aklog.  If we can't figure it out, the user will
dnl have to set program in the PAM options.
AC_ARG_WITH([aklog],
    AC_HELP_STRING([--with-aklog=PATH],
        [Path to aklog or other Kerberos v5 AFS token program]),
    [AS_IF([test x"$withval" != xno], [PATH_AKLOG="$withval"])],
    [AC_PATH_PROGS([PATH_AKLOG], [aklog])])
AS_IF([test -n "$PATH_AKLOG"],
    [AC_DEFINE_UNQUOTED([PATH_AKLOG], ["$PATH_AKLOG"],
        [Full path to aklog binary.])])

dnl Crank up the warnings if we're using GCC.
AS_IF([test "$GCC" = "yes"], [CFLAGS="-Wall $CFLAGS"])

dnl We can optionally build with Kerberos libraries so that we can use
dnl Kerberos calls to get configuration information.  Check this before
dnl checking for libkafs.
RRA_LIB_KRB5_OPTIONAL
AS_IF([test x"$rra_use_kerberos" != xfalse],
    [RRA_LIB_KRB5_SWITCH
     AC_CHECK_TYPES([krb5_realm], [], [], [RRA_INCLUDES_KRB5])
     AC_CHECK_FUNCS([krb5_free_default_realm \
         krb5_init_secure_context])
     AC_CHECK_FUNCS([krb5_appdefault_string], [],
        [AC_CHECK_FUNCS([krb5_get_profile])
         AC_CHECK_HEADERS([k5profile.h profile.h])
         AC_LIBOBJ([krb5-profile])])
     AC_LIBOBJ([krb5-extra])
     RRA_LIB_KRB5_RESTORE])
RRA_LIB_KAFS
RRA_LIB_KAFS_SWITCH
AC_CHECK_FUNCS([krb5_afslog])
RRA_LIB_KAFS_RESTORE
AM_CONDITIONAL([NEED_KAFS], [test x"$rra_build_kafs" = xtrue])

dnl Other portability checks.
AC_HEADER_STDBOOL
AC_CHECK_HEADERS([strings.h sys/bittypes.h])
AC_CHECK_DECLS([snprintf, strlcat, strlcpy, vsnprintf])
AC_TYPE_LONG_LONG_INT
AC_TYPE_UINT32_T
AC_CHECK_TYPES([sig_atomic_t], [], [],
    [#include <sys/types.h>
     #include <signal.h>])
AC_CHECK_TYPES([ssize_t], [], [],
    [#include <sys/types.h>])
RRA_FUNC_SNPRINTF
AC_REPLACE_FUNCS([asprintf issetugid reallocarray strlcat strlcpy strndup])

dnl Needed for correct handling of errno with threaded applications on
dnl Solaris.
AC_DEFINE([_REENTRANT], [1],
    [Define to 1 on Solaris for correct errno handling with threads.])

dnl Try to specify the binding so that any references within the PAM module
dnl are resolved to the functions in that module in preference to any external
dnl function.
dnl
dnl Also, if and only if we're on Linux, make sure that all the symbols in the
dnl module are resolved, try to adjust for the 32-bit vs. 64-bit library
dnl paths, and install into /lib or /lib64 instead of /usr/lib or /usr/lib64
dnl if the prefix is /usr.
dnl
dnl Mac OS X systems don't support PAGs, so set a preprocessor define on that
dnl platform so that we can default "nopag" to true.
dnl
dnl More platforms could be handled here.  Contributions welcome.
AS_CASE([$host],
    [*-darwin*],
    [AC_DEFINE([NO_PAG_SUPPORT], [1],
        [Define to 1 if the operating system has no PAG support.])],

    [*-hpux*],
    [AS_IF([test x"$GCC" = x"yes"],
        [AM_LDFLAGS="-Wl,-Bsymbolic $AM_LDFLAGS"],
        [AM_LDFLAGS="-Wl,+vshlibunsats $AM_LDFLAGS"])],

    [*-linux*],
    [AM_LDFLAGS="-Wl,-z,defs -Wl,-Bsymbolic $AM_LDFLAGS"
     AS_IF([test x"${prefix}" = x"/usr"],
        [AS_IF([test x"${libdir}" = x'${exec_prefix}/lib'],
            [RRA_SET_LIBDIR])])],

    [*-solaris2*],
    [AS_IF([test x"$GCC" = x"yes"],
        [AM_LDFLAGS="-Wl,-Bsymbolic $AM_LDFLAGS"],
        [AM_LDFLAGS="-Wl,-xldscope=symbolic $AM_LDFLAGS"])])

dnl Enable appropriate warnings.
AM_CONDITIONAL([WARNINGS_GCC], [test x"$GCC" = xyes && test x"$CLANG" != xyes])
AM_CONDITIONAL([WARNINGS_CLANG], [test x"$CLANG" = xyes])

AC_CONFIG_HEADER([config.h])
AC_CONFIG_FILES([Makefile])
AC_OUTPUT
