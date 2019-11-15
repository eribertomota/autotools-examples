dnl Process this file with autoconf to produce a configure script.

AC_INIT([awffull], [3.10.2], [spm@stedee.id.au])
AC_PREREQ([2.59])
AC_CONFIG_SRCDIR([src/awffull.c])
AC_CONFIG_AUX_DIR([config])
AC_CONFIG_HEADER(src/config.h:src/config-h.in)
AM_INIT_AUTOMAKE([-Wall -Werror foreign])

dnl Grab the current CFLAGS variable - gets set by other tests otherwise
OLD_CFLAGS=${CFLAGS}
if test "x$CFLAGS" = "x"; then
    CFLAGS="-O2"
fi

AM_GNU_GETTEXT_VERSION([0.15])
AM_GNU_GETTEXT([external])

AC_REVISION($Revision: 1.1 $)

dnl Checks for programs.
AC_PROG_CC

OPTS=${DEFS}
AC_SUBST(OPTS)


dnl ********************
dnl Set CFLAGS to use
dnl  Use extra optimisations if using gcc
if test "x$OLD_CFLAGS" = "x"; then
    if test "x$CC" = "xgcc"; then
        CFLAGS="-O3 -fexpensive-optimizations"
    else
        CFLAGS="-O2"
    fi
fi

dnl ********************
dnl Config Arg: --enable-debug
dnl  Enable the debug flag for compiling
dnl ********************
AC_ARG_ENABLE([debug],
              AS_HELP_STRING([--enable-debug],
                             [Turn on compiler debugging information (default=no)]),
                             [if eval "test x$enable_debug = xyes"; then
                              CFLAGS="${CFLAGS} -Wall -g"
                          fi])


dnl ********************
dnl Config Arg: --enable-developer
dnl  Enable maximum warnings. Base taken from Samba.
dnl ********************
AC_ARG_ENABLE([developer],
              AS_HELP_STRING([--enable-developer],
                             [Turn on developer warnings and debugging (default=no)]),
                             [if eval "test x$enable_developer = xyes"; then
                                  CFLAGS="${OLD_CFLAGS} -g -pg -Wall -Wshadow -Wstrict-prototypes -DDEVELOPER"
                              else
                                  if eval "test x$enable_developer != xno"; then
                                      CFLAGS="${OLD_CFLAGS} -g -pg -Wall $enable_developer -DDEVELOPER"
                                  fi
                          fi])


dnl ********************
dnl Config Arg: --enable-coverage
dnl  Enable the coverage testing
dnl ********************
AC_ARG_ENABLE([coverage],
              AS_HELP_STRING([--enable-coverage],
                             [Turn on compiler coverage testing: gcov (default=no)]),
                             [if eval "test x$enable_coverage = xyes"; then
                              CFLAGS="${OLD_CFLAGS} -Wall -fprofile-arcs -ftest-coverage"
                          fi])


dnl ********************
dnl Config Arg: --enable-static
dnl ********************
AC_ARG_ENABLE([static],
              AS_HELP_STRING([--enable-static],
                             [Build as static executable (default=no)]),
                             [if eval "test x$enable_static = xyes"; then
                              LDFLAGS="--static ${LDFLAGS}"
                          fi])

              
dnl ********************
dnl Config Arg: --enable-geoip
dnl ********************
ENABLE_GEOIP="yes"
AC_ARG_ENABLE([geoip],
              AS_HELP_STRING([--disable-geoip],
                             [Disable GeoIP (default=no)]),
                             [if eval "test x$enable_geoip = xno"; then
                              ENABLE_GEOIP="no"
                          fi])

              
dnl ********************
dnl Config Arg: --enable-ttf
dnl ********************
ENABLE_TTF="yes"
AC_ARG_ENABLE([ttf],
              AS_HELP_STRING([--disable-ttf],
                             [Disable TrueType Fonts (default=no)]),
                             [if eval "test x$enable_ttf = xno"; then
                              ENABLE_TTF="no"
                          fi])

              
dnl ********************
dnl Config Arg: --with-etcdir
dnl ********************
AC_ARG_WITH([etcdir],
            AS_HELP_STRING([--with-etcdir=DIR],
                           [Where to look for default config file (default=/etc)]),
                           [ETCDIR="${withval}"], 
                           [CACHE_ETC="yes"])


dnl ********************
dnl Config Arg: --with-gd
dnl ********************
AC_ARG_WITH([gd],
            AS_HELP_STRING([--with-gd=DIR],
                           [Where to additionally look for gd header files]),
                           [CFLAGS="-I${withval} ${CFLAGS}"])


dnl ********************
dnl Config Arg: --with-gdlib
dnl ********************
AC_ARG_WITH([gdlib],
            AS_HELP_STRING([--with-gdlib=DIR],
                           [Alternate location for libgd library]),
                           [LDFLAGS="-L${withval} ${LDFLAGS}"])


dnl ********************
dnl Config Arg: --with-z
dnl ********************
AC_ARG_WITH([z],
            AS_HELP_STRING([--with-z=DIR],
                           [Alternate location for libz header files]),
                           [CFLAGS="-I${withval} ${CFLAGS}"])


dnl ********************
dnl Config Arg: --with-zlib
dnl ********************
AC_ARG_WITH([zlib],
            AS_HELP_STRING([--with-zlib=DIR],
                           [Alternate location for libz library]),
                           [LDFLAGS="-L${withval} ${LDFLAGS}"])


dnl ********************
dnl Config Arg: --with-png
dnl ********************
AC_ARG_WITH([png],
            AS_HELP_STRING([--with-png=DIR],
                           [Alternate location of png header files]),
                           [CFLAGS="-I${withval} ${CFLAGS}"])


dnl ********************
dnl Config Arg: --with-pnglib
dnl ********************
AC_ARG_WITH([pnglib],
            AS_HELP_STRING([--with-pnglib=DIR],
                           [Alternate location for libpng library]),
                           [LDFLAGS="-L${withval} ${LDFLAGS}"])


dnl ********************
dnl Config Arg: --with-pcre
dnl ********************
AC_ARG_WITH([pcre],
            AS_HELP_STRING([--with-pcre=DIR],
                           [Alternate location of pcre header files]),
                           [CFLAGS="-I${withval} ${CFLAGS}"])


dnl ********************
dnl Config Arg: --with-pcrelib
dnl ********************
AC_ARG_WITH([pcrelib],
            AS_HELP_STRING([--with-pcrelib=DIR],
                           [Alternate location for libpcre library]),
                           [LDFLAGS="-L${withval} ${LDFLAGS}"])


dnl ********************
dnl Config Arg: --with-geoip
dnl ********************
AC_ARG_WITH([geoip],
            AS_HELP_STRING([--with-geoip=DIR],
                           [Alternate location of geoip header files]),
                           [CFLAGS="-I${withval} ${CFLAGS}"])


dnl ********************
dnl Config Arg: --with-geoiplib
dnl ********************
AC_ARG_WITH([geoiplib],
            AS_HELP_STRING([--with-geoiplib=DIR],
                           [Alternate location for libGeoIP library]),
                           [LDFLAGS="-L${withval} ${LDFLAGS}"])


dnl ********************
dnl Config Arg: --with-font-default
dnl ********************
AH_TEMPLATE([FONTDEFAULT],
            [Define if need to override the Default TrueType Font location.])

AC_ARG_WITH([font-default],
            AS_HELP_STRING([--with-font-default=FILE],
                           [Where to look for the Default TrueType Font]),
                           AC_DEFINE_UNQUOTED([FONTDEFAULT], ["${withval}"]))

dnl ********************
dnl Config Arg: --with-font-label
dnl ********************
AH_TEMPLATE([FONTLABEL],
            [Define if need to override the Default Label TrueType Font location.])

AC_ARG_WITH([font-label],
            AS_HELP_STRING([--with-font-label=FILE],
                           [Where to look for the Default Label TrueType Font]),
                           AC_DEFINE_UNQUOTED([FONTLABEL], ["${withval}"]))

dnl ********************
dnl Config Arg: --with-generated-by
dnl ********************
AH_TEMPLATE([GENERATEDBY],
            [Define if choose to override the Generated By footer.])

AC_ARG_WITH([generated-by],
            AS_HELP_STRING([--with-generated-by=HTML],
                           [Override HTML for the "Generated By" footer.]),
                           AC_DEFINE_UNQUOTED([GENERATEDBY], ["${withval}"]))

dnl ********************
dnl   LIBRARY CHECKING
dnl ********************
AC_PROG_RANLIB
AC_FUNC_MKTIME
AC_CHECK_LIB([m], [main],[], [echo "Missing Math Library" ; exit])
AC_CHECK_LIB([z], [main],[], [echo "Missing Z Compression Library" ; exit])
AC_CHECK_LIB([png], [main],[], [echo "Missing PNG Library" ; exit])
AC_CHECK_LIB([gd], [gdImagePng],[], [echo "Missing GD Library" ; exit])

if test "$ENABLE_TTF" = "yes"; then
    dnl #define HAVE_GDIMAGESTRINGFT in config.h if we can do GD TrueType Text
    AC_CHECK_LIB([gd], [gdImageStringFT],
                 [AC_DEFINE([HAVE_GDIMAGESTRINGFT], [1], [Define if gdImageStringFT Exists])],
                 [echo "Missing GD TrueType Font Capability"])

    dnl #define HAVE_GDFTUSEFONTCONFIG in config.h if we can do GD TrueType Font Config
    AC_CHECK_LIB([gd], [gdFTUseFontConfig],
                 [AC_DEFINE([HAVE_GDFTUSEFONTCONFIG], [1], [Define if gdFTUseFontConfig Exists])],
                 [echo "Missing GD TrueType Font Config Capability"])
fi

AC_CHECK_LIB([pcre], [main],[], [echo "Missing Perl Reg. Ex. Library" ; exit])
if test "$ENABLE_GEOIP" = "yes"; then
    AC_CHECK_LIB([GeoIP], [main],[], [echo "Missing GeoIP Library" ; ENABLE_GEOIP="no"])
fi

dnl Checks for library functions.
dnl - messes up Solaris - AC_FUNC_MALLOC
AC_CHECK_FUNC([getopt_long], [], [echo "Missing getopt_long Function" ; exit])
AC_CHECK_FUNCS([floor memset strlcpy])

dnl ********************
dnl   HEADER CHECKING
dnl ********************
dnl Checks for header files.
AC_HEADER_STDC
AC_HEADER_STDBOOL
AC_HEADER_TIME
AC_CHECK_HEADERS([getopt.h], [], [echo "Missing getopt.h" ; exit])
AC_CHECK_HEADERS([math.h], [], [echo "Missing math.h" ; exit])
AC_CHECK_HEADERS([zlib.h], [], [echo "Missing zlib.h" ; exit])
AC_CHECK_HEADERS([pcre.h], [],
                 [ AC_CHECK_HEADERS([pcre/pcre.h], [], [ echo "Missing pcre.h" ; exit ] ])
         )
AC_CHECK_HEADERS([ctype.h], [], [echo "Missing ctype.h" ; exit])
AC_CHECK_HEADERS([sys/utsname.h], [], [echo "Missing sys/utsname.h" ; exit])
AC_CHECK_HEADERS([sys/times.h], [], [echo "Missing sys/times.h" ; exit])
AC_CHECK_HEADERS([unistd.h], [], [echo "Missing unistd.h" ; exit])
if test "$ENABLE_GEOIP" = "yes"; then
    AC_CHECK_HEADERS([GeoIP.h], [], [echo "Missing GeoIP.h"])
fi


dnl ********************
dnl Checks for typedefs, structures, and compiler characteristics.
dnl ********************
AC_C_CONST
AC_STRUCT_TM
AC_TYPE_SIZE_T

AC_MSG_CHECKING(default config dir)
if test "$CACHE_ETC" = "yes"; then
 AC_CACHE_VAL(ac_cv_etcdir, ac_cv_etcdir=/etc)
 ETCDIR=$ac_cv_etcdir
fi
ac_cv_etcdir=$ETCDIR
AC_MSG_RESULT($ETCDIR)
AC_SUBST(ETCDIR)

AC_CONFIG_FILES([Makefile src/Makefile doc/Makefile flags/Makefile po/Makefile.in contrib/Makefile])
AC_OUTPUT

