AC_PREREQ(2.52)
AC_INIT(pm-utils, 1.4.1)
AC_CONFIG_SRCDIR(src)
AM_INIT_AUTOMAKE(AC_PACKAGE_NAME, AC_PACKAGE_VERSION)
AM_CONFIG_HEADER(config.h)

AC_PROG_CC
AC_PROG_LN_S

dnl ---------------------------------------------------------------------------
dnl - Manual page build
dnl ---------------------------------------------------------------------------
AC_ARG_ENABLE([doc],
	AC_HELP_STRING([--disable-docs],
		[Disable manpage generating via xmlto [[default=auto]]]),
	[MAN="$enableval"],
	[MAN=auto])
	AC_PATH_PROG(XMLTO, xmlto, no)
	AS_IF([test "x$MAN" = "xyes"],
	[
		AS_IF([test "x$XMLTO" = "xno"],
			[AC_MSG_ERROR([Manpage generating requested but xmlto not found.])
		])
	],
	[test "x${MAN}" != "xno"],
	[
		AS_IF([test "x$XMLTO" != "xno"],
			[MAN="yes"],
			[MAN="no"])
	])
AM_CONDITIONAL(HAVE_XMLTO, [test "x$MAN" != xno])
AC_MSG_RESULT([checking whether to build manpages... $MAN])

dnl ---------------------------------------------------------------------------
dnl - Makefiles, etc.
dnl ---------------------------------------------------------------------------
AC_OUTPUT([
Makefile
pm-utils.pc
man/Makefile
src/Makefile
pm/Makefile
pm/sleep.d/Makefile
pm/power.d/Makefile
pm/module.d/Makefile
])

dnl ==========================================================================
echo "
                    pm-utils $VERSION
                  ==================

        prefix:                    ${prefix}
        compiler:                  ${CC}
        cflags:                    ${CFLAGS}
"
