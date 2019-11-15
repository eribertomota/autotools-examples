dnl initialize
AC_INIT(main.c)

dnl preserve initial CFLAGS - must come after AC_INIT or it isn't run!
CFLAGS_OLD="$CFLAGS"

VER=`head -1 $srcdir/README |sed 's/ *netrik \([[^ ]]*\).*/\1/'`
AM_INIT_AUTOMAKE(netrik, $VER)

dnl initialize config header
AM_CONFIG_HEADER(config.h)

dnl check for some essential programs
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_MAKE_SET

dnl check for standard headers
AC_HEADER_STDC

dnl check for ncurses
AC_CHECK_LIB(ncursesw,
	     tparm,
	     [NCURSES="yes"],
	     AC_MSG_ERROR([ncursesw is absolutely required!]))

LIBS="-lncursesw $LIBS"

dnl check for readline
AC_CHECK_LIB(readline,
	    readline,
	    [READLINE="yes"])
AC_CHECK_LIB(history,
	    add_history,
	    [HISTORY="yes"])

if test x"$READLINE" = "xyes" -a x"$HISTORY" = "xyes"; then
  AC_DEFINE(READLINE, 1, [Define if GNU Readline is present.])
  LIBS="-lreadline -lhistory $LIBS"
else
  AC_MSG_WARN([Having GNU Readline is recommended.])
fi

dnl check for getopt_long
AC_CHECK_FUNC([getopt_long],
	      [GETOPT="y"],
	      [AC_MSG_ERROR(netrik requires getopt_long()!)])

dnl some options
AC_ARG_WITH(wget-call,
	    [AC_HELP_STRING([--with-wget-call="wget ..."],
			    [specify the command to call wget])],
	    [AC_DEFINE_UNQUOTED(WGET_CMD, ["$withval"], [Your command to call wget])],
	    [AC_DEFINE(WGET_CMD, ["wget -nv -O- '%s'"], [Default command to call wget])])

AC_ARG_ENABLE(debug,
	      [AC_HELP_STRING([--disable-debug],
			      [do not include debug options and sanity checks])])

AC_ARG_ENABLE(optimization,
	      [AC_HELP_STRING([[--enable-optimization[[[=LEVEL]]]]],
			      [use compiler optimization with -OLEVEL (default: -O2 if CFLAGS not set)])])

dnl process results
dnl define
if test x"$enable_debug" != "xno"; then
  AC_DEFINE(DEBUG, 1,
	    [Define if debug options and sanity checks are desired.])
fi

dnl restore CFLAGS
CFLAGS="$CFLAGS_OLD"

dnl set default CFLAGS
if test -z "$CFLAGS_OLD" ; then
  CFLAGS="$CFLAGS -g"

  dnl set warning options for GCC
  if test x"$GCC" = "xyes"; then
    CFLAGS="$CFLAGS -W -Wall -Wstrict-prototypes -Wmissing-prototypes"
  fi
fi

dnl adjust optimization options
case x"$enable_optimization" in
  dnl option given but no argument specified
  xyes)
    CFLAGS="$CFLAGS -O2"
    ;;

  dnl chosen not to optimize
  xno)
    dnl use -O0 to make sure no optimization is performed
    CFLAGS="$CFLAGS -O0"
    ;;

  dnl option not given
  x)
    dnl optimize if CFLAGS not specified
    if test -z "$CFLAGS_OLD"; then
      CFLAGS="$CFLAGS -O2"
    fi
    ;;

  dnl argument given
  *)
    dnl use argument to optimize
    CFLAGS="$CFLAGS -O${enable_optimization}"
    ;;
esac

dnl generate Makefiles
AC_OUTPUT(Makefile doc/Makefile)
