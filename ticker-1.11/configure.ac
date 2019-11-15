dnl Written by Joey Hess <joey@kitenet.net> with some help from autoscan.
dnl Process this file with autoconf to generate the configure script.

AC_INIT(ticker.c)
AC_CONFIG_AUX_DIR(autoconf)
AC_CONFIG_HEADER(config.h)

dnl Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_LN_S

dnl If we are using gcc for a compiler, I'd like to add some cflags which
dnl are specified in the CFLAGS_FOR_GCC variable in the Makefile.
if test "$GCC" = yes ; then
	gcc_cflags='$(CFLAGS_FOR_GCC)'
fi
AC_SUBST(gcc_cflags)

dnl Let the user specify an alternate location for the libs.
dnl I have to add this to CFLAGS, instead of to LIBS, to placate
dnl some compiler that wanted -L before -l .
if test "$SLANG_LIB_LOC" != "" ; then
	CFLAGS="-L$SLANG_LIB_LOC $CFLAGS"
fi

dnl Checks for libraries.
dnl Replace `main' with a function in -lslang:
AC_CHECK_LIB(slang, SLsig_block_signals,,
	AC_MSG_ERROR(can't find required slang library or library is obsolete. Try setting the SLANG_LIB_LOC environment variable to point to the directory containing the slang library.))

dnl Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS(limits.h sys/time.h unistd.h getopt.h)

dnl The slang headers can be in several places.
AC_CHECK_HEADERS($SLANG_H_LOC, slang_h_ok=yes)
if test "$slang_h_ok" = yes ; then
	SLANG_H=$SLANG_H_LOC
else
	AC_CHECK_HEADERS(slang.h slang/slang.h, break)
	if test "$ac_cv_header_slang_h" = yes ; then
		SLANG_H=slang.h
	elif test "$ac_cv_header_slang_slang_h" = yes ; then
		SLANG_H=slang/slang.h
	else
		AC_MSG_ERROR(can't find required slang.h header file. Try setting the SLANG_H_LOC environment variable to point to it.)
	fi
fi
AC_SUBST(SLANG_H)

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_HEADER_TIME

dnl Checks for library functions.
AC_FUNC_VPRINTF
AC_CHECK_FUNCS(select)

AC_CHECK_FUNCS(getopt_long, , [
	AC_MSG_WARN(long command line switches are disabled.)
	AC_CHECK_FUNCS(getopt, ,
		AC_MSG_WARN(all command line switches are disabled!)
		)
	])

AC_OUTPUT(
	makeinfo:autoconf/makeinfo.in
	slang.h:autoconf/slang.h.in
)
