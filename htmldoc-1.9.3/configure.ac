#
# Configuration script for HTMLDOC, an HTML document processing program.
#
# Copyright © 2011-2018 by Michael R Sweet.
# Copyright © 1997-2010 by Easy Software Products.
#
# This program is free software.  Distribution and use rights are outlined in
# the file "COPYING".
#

AC_INIT([HTMLDOC], [1.9.3], [https://github.com/michaelrsweet/htmldoc/issues], [htmldoc],  [https://michaelrsweet.github.io/htmldoc])
AC_CONFIG_HEADER(config.h)

dnl Define the version number...
SVERSION="AC_PACKAGE_VERSION"
AC_SUBST(SVERSION)
AC_DEFINE_UNQUOTED([SVERSION], ["$SVERSION"], [version number])

dnl Get the operating system and version number...
uname=`uname`
uversion=`uname -r | sed -e '1,$s/[[^0-9]]//g'`

if test "$uname" = "IRIX64"; then
    uname="IRIX"
fi

dnl Clear the debugging options unless the user asks for them...
INSTALL_STRIP="-s"
AC_SUBST(INSTALL_STRIP)
OPTIM="${OPTIM:=}"
AC_SUBST(OPTIM)
CFLAGS="${CFLAGS:=}"
CXXFLAGS="${CXXFLAGS:=}"
LDFLAGS="${LDFLAGS:=}"

AC_ARG_ENABLE(debug, [  --enable-debug          turn on debugging, default=no],
    [if eval "test x$enable_debug = xyes"; then
	INSTALL_STRIP=""
	OPTIM="-g "
    fi])

AC_ARG_WITH(gui, [  --without-gui           do not compile the GUI version of HTMLDOC, default=yes])

dnl Checks for programs...
AC_PROG_AWK
AC_PROG_CC(clang cc gcc)
AC_PROG_CXX(clang++ c++ g++)
AC_PROG_CPP
AC_PROG_RANLIB
AC_PATH_PROG(AR,ar)
AC_PATH_PROG(CHMOD,chmod)
AC_PATH_PROG(CP,cp)
AC_PATH_PROG(FLTKCONFIG,fltk-config)
AC_MSG_CHECKING(for install-sh script)
INSTALL="`pwd`/install-sh"
AC_SUBST(INSTALL)
AC_MSG_RESULT(using $INSTALL)
AC_PATH_PROG(MV,mv)
AC_PATH_PROG(MKDIR,mkdir)
AC_PATH_PROG(RM,rm)
AC_PATH_TOOL(PKGCONFIG, pkg-config)

dnl See if we need a .exe extension on executables...
AC_EXEEXT

dnl Figure out the correct "ar" command flags...
if test "$ac_cv_prog_ranlib" = ":"; then
    ARFLAGS="crs"
else
    ARFLAGS="cr"
fi

AC_SUBST(ARFLAGS)

dnl Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADER(strings.h, AC_DEFINE([HAVE_STRINGS_H], [], [strings.h support]))
AC_CHECK_HEADER(locale.h, AC_DEFINE([HAVE_LOCALE_H], [], [locale.h support]))

dnl Checks for string functions.
AC_CHECK_FUNCS(strdup strcasecmp strncasecmp strlcat strlcpy)
if test "$uname" = "HP-UX" -a "$uversion" = "1020"; then
    AC_MSG_WARN(Forcing snprintf emulation for HP-UX...)
else
    AC_CHECK_FUNCS(snprintf vsnprintf)
fi

dnl Check for random number functions...
AC_CHECK_FUNC(arc4random, AC_DEFINE([HTMLDOC_RAND()], [arc4random()], [use arc4random]) AC_DEFINE([HTMLDOC_SRAND(v)], [srand for arc4random]),
  AC_CHECK_FUNC(random, AC_DEFINE([HTMLDOC_RAND()], [random()], [use random]) AC_DEFINE([HTMLDOC_SRAND(v)], [srandom(v)], [srand for random]),
    AC_CHECK_FUNC(lrand48, AC_DEFINE([HTMLDOC_RAND()], [lrand48()], [use lrand48]) AC_DEFINE([HTMLDOC_SRAND(v)], [srand48(v)], [srand for lrand48]),
      AC_DEFINE([HTMLDOC_RAND()], [rand()], [fallback to rand]) AC_DEFINE([HTMLDOC_SRAND(v)], [srand(v)], [fallback to srand]))))

dnl See if the tm structure has the tm_gmtoff member...
AC_MSG_CHECKING(for tm_gmtoff member in tm structure)
AC_TRY_COMPILE([#include <time.h>],[struct tm t;
    int o = t.tm_gmtoff;],
    AC_MSG_RESULT(yes)
    AC_DEFINE([HAVE_TM_GMTOFF], [], [tm_gmtoff support]),
    AC_MSG_RESULT(no))

dnl Check for libraries...
LDFLAGS="${LDFLAGS:=}"
AC_SUBST(LDFLAGS)

AC_CHECK_LIB(m,pow)
AC_CHECK_FUNC(poll, AC_DEFINE([HAVE_POLL], [], [poll support]))
AC_SEARCH_LIBS(socket, socket)
AC_SEARCH_LIBS(gethostbyaddr, nsl)
AC_SEARCH_LIBS(getaddrinfo, nsl, AC_DEFINE([HAVE_GETADDRINFO], [], [getaddrinfo support]))
AC_SEARCH_LIBS(getnameinfo, nsl, AC_DEFINE([HAVE_GETNAMEINFO], [], [getnameinfo support]))
AC_SEARCH_LIBS(hstrerror, nsl socket resolv, AC_DEFINE([HAVE_HSTRERROR], [], [hstrerror support]))
AC_SEARCH_LIBS(__res_init, resolv bind, AC_DEFINE([HAVE_RES_INIT], [], [__res_init support]),
	AC_SEARCH_LIBS(res_9_init, resolv bind, AC_DEFINE(HAVE_RES_INIT),
	AC_SEARCH_LIBS(res_init, resolv bind, AC_DEFINE(HAVE_RES_INIT))))
AC_CHECK_HEADER(resolv.h, AC_DEFINE([HAVE_RESOLV_H], [], [resolv.h support]))

dnl Check for largefile support...
AC_SYS_LARGEFILE

dnl Define largefile options as needed...
LARGEFILE=""
if test x$enable_largefile != xno; then
    LARGEFILE="-D_LARGEFILE_SOURCE -D_LARGEFILE64_SOURCE"

    if test x$ac_cv_sys_large_files = x1; then
	LARGEFILE="$LARGEFILE -D_LARGE_FILES"
    fi

    if test x$ac_cv_sys_file_offset_bits = x64; then
	LARGEFILE="$LARGEFILE -D_FILE_OFFSET_BITS=64"
    fi
fi
AC_SUBST(LARGEFILE)

dnl Check for "long long" support...
AC_CACHE_CHECK(for long long int, ac_cv_c_long_long,
    [if test "$GCC" = yes; then
	ac_cv_c_long_long=yes
    else
	AC_TRY_COMPILE(,[long long int i;],
		       ac_cv_c_long_long=yes,
		       ac_cv_c_long_long=no)
    fi])

if test $ac_cv_c_long_long = yes; then
    AC_DEFINE([HAVE_LONG_LONG], [], [long long support])
	AC_DEFINE([HTMLDOC_LLFMT], ["%lld"], [long long format])
	AC_DEFINE([HTMLDOC_LLCAST], [(long long)], [long long cast])
else
	AC_DEFINE([HTMLDOC_LLFMT], ["%ld"], [long long format])
	AC_DEFINE([HTMLDOC_LLCAST], [(long)], [long long cast])
fi

AC_CHECK_FUNC(strtoll, AC_DEFINE([HAVE_STRTOLL], [], [strtoll support]))

dnl Check for TLS/SSL libraries...
AC_ARG_ENABLE(ssl, [  --enable-ssl            turn on SSL/TLS support, default=yes])
AC_ARG_ENABLE(gnutls, [  --enable-gnutls         use GNU TLS for SSL/TLS support, default=yes])
AC_ARG_ENABLE(cdsassl, [  --enable-cdsassl        use CDSA for SSL/TLS support, default=yes])

SSLFLAGS=""
SSLLIBS=""
have_ssl=0

if test x$enable_ssl != xno; then
    dnl Look for CDSA...
    if test $have_ssl = 0 -a "x$enable_cdsassl" != "xno"; then
	if test $uname = Darwin; then
	    AC_CHECK_HEADER(Security/SecureTransport.h, [
	    	have_ssl=1
		AC_DEFINE([HAVE_SSL], [], [ssl support])
		AC_DEFINE([HAVE_CDSASSL], [], [cdsassl support])
		SSLLIBS="-framework Security -framework CoreFoundation"

		AC_CHECK_HEADER(Security/SecureTransportPriv.h,
		    AC_DEFINE([HAVE_SECURETRANSPORTPRIV_H], [], [SecureTransportPriv.h support]))
		AC_CHECK_HEADER(Security/SecCertificate.h,
		    AC_DEFINE([HAVE_SECCERTIFICATE_H], [], [SecCertificate.h support]))
		AC_CHECK_HEADER(Security/SecItem.h,
		    AC_DEFINE([HAVE_SECITEM_H], [], [SecItem.h support]))
		AC_CHECK_HEADER(Security/SecItemPriv.h,
		    AC_DEFINE([HAVE_SECITEMPRIV_H], [], [SecItemPriv.h support]))
		AC_CHECK_HEADER(Security/SecPolicy.h,
		    AC_DEFINE([HAVE_SECPOLICY_H], [], [SecPolicy.h support]))
		AC_CHECK_HEADER(Security/SecPolicyPriv.h,
		    AC_DEFINE([HAVE_SECPOLICYPRIV_H], [], [SecPolicyPriv.h support]))
		AC_CHECK_HEADER(Security/SecBasePriv.h,
		    AC_DEFINE([HAVE_SECBASEPRIV_H], [], [SecBasePriv.h support]))
		AC_CHECK_HEADER(Security/SecIdentitySearchPriv.h,
		    AC_DEFINE([HAVE_SECIDENTITYSEARCHPRIV_H], [], [SecIdentitySearchPriv.h support]))

		AC_DEFINE([HAVE_CSSMERRORSTRING], [], [cssmerrorstring support])
		AC_DEFINE([HAVE_SECKEYCHAINOPEN], [], [seckeychainopen support])])

		if test $uversion -ge 150; then
			AC_DEFINE([HAVE_SSLSETENABLEDCIPHERS], [], [ssl setenabledciphers support])
		fi
	fi
    fi

    dnl Then look for GNU TLS...
    if test $have_ssl = 0 -a "x$enable_gnutls" != "xno" -a "x$PKGCONFIG" != x; then
    	AC_PATH_TOOL(LIBGNUTLSCONFIG,libgnutls-config)
    	AC_PATH_TOOL(LIBGCRYPTCONFIG,libgcrypt-config)
	if $PKGCONFIG --exists gnutls; then
	    have_ssl=1
	    SSLLIBS=`$PKGCONFIG --libs gnutls`
	    SSLFLAGS=`$PKGCONFIG --cflags gnutls`
	    AC_DEFINE(HAVE_SSL)
	    AC_DEFINE([HAVE_GNUTLS], [], [gnutls support])
	elif test "x$LIBGNUTLSCONFIG" != x; then
	    have_ssl=1
	    SSLLIBS=`$LIBGNUTLSCONFIG --libs`
	    SSLFLAGS=`$LIBGNUTLSCONFIG --cflags`
	    AC_DEFINE(HAVE_SSL)
	    AC_DEFINE(HAVE_GNUTLS)
	fi

	if test $have_ssl = 1; then
	    SAVELIBS="$LIBS"
	    LIBS="$LIBS $SSLLIBS"
	    AC_CHECK_FUNC(gnutls_transport_set_pull_timeout_function, AC_DEFINE([HAVE_GNUTLS_TRANSPORT_SET_PULL_TIMEOUT_FUNCTION], [], [gnutls transport_set_pull_timeout_function support]))
	    AC_CHECK_FUNC(gnutls_priority_set_direct, AC_DEFINE([HAVE_GNUTLS_PRIORITY_SET_DIRECT], [], [gnutls priority_set_direct support]))
	    LIBS="$SAVELIBS"
	fi
    fi
fi

AC_MSG_NOTICE([Using SSLFLAGS="$SSLFLAGS", SSLLIBS="$SSLLIBS"])

AC_SUBST(SSLFLAGS)
AC_SUBST(SSLLIBS)

dnl Check for GUI libraries...
POST=:
if test "x$with_gui" != xno; then
    if test "x$FLTKCONFIG" != x; then
	LIBS="$LIBS `$FLTKCONFIG --use-images --ldflags`"
	AC_DEFINE([HAVE_LIBFLTK], [], [libfltk support])
	POST="$FLTKCONFIG --post"

	AC_CHECK_LIB(Xpm,XpmCreatePixmapFromData)
	AC_CHECK_LIB(X11,XCreateBitmapFromData)
    else
        AC_MSG_WARN(FLTK not available so no GUI will be built.)
    fi
fi

AC_SUBST(POST)

dnl Check for image libraries...
NEWLIBS=""

AC_ARG_ENABLE(localjpeg, [  --enable-localjpeg      use local JPEG library, default=auto])
if test x$enable_localjpeg = xyes; then
    AC_MSG_CHECKING([for library containing jpeg_CreateCompress])
    AC_MSG_RESULT([local libjpeg])
    JPEGINC="-I../jpeg"
    JPEG="jpeg"
    NEWLIBS="../jpeg/libjpeg.a $NEWLIBS"
else
    AC_SEARCH_LIBS(jpeg_CreateCompress,turbojpeg jpeg,
	JPEGINC=""
	JPEG="",
	JPEGINC="-I../jpeg"
	JPEG="jpeg"
	NEWLIBS="../jpeg/libjpeg.a $NEWLIBS")
fi

AC_ARG_ENABLE(localzlib, [  --enable-localzlib      use local ZLIB library, default=auto])
if test x$enable_localzlib = xyes; then
    AC_MSG_CHECKING([for library containing gzgets])
    AC_MSG_RESULT([local libz])
    ZLIBINC="-I../zlib"
    ZLIB="zlib"
    NEWLIBS="../zlib/libz.a $NEWLIBS"
else
    AC_SEARCH_LIBS(gzgets,z,
	ZLIBINC=""
	ZLIB="",
	ZLIBINC="-I../zlib"
	ZLIB="zlib"
	NEWLIBS="../zlib/libz.a $NEWLIBS")
fi

AC_ARG_ENABLE(localpng, [  --enable-localpng       use local PNG library, default=auto])
if test x$enable_localpng = xyes; then
    AC_MSG_CHECKING([for library containing png_set_tRNS_to_alpha])
    AC_MSG_RESULT([local libpng])
    PNGINC="-I../png"
    PNG="png"
    NEWLIBS="../png/libpng.a $NEWLIBS"
else
    AC_SEARCH_LIBS(png_set_tRNS_to_alpha,png,
	PNGINC=""
	PNG="",
	PNGINC="-I../png"
	PNG="png"
	NEWLIBS="../png/libpng.a $NEWLIBS")
fi

AC_SUBST(JPEG)
AC_SUBST(JPEGINC)
AC_SUBST(PNG)
AC_SUBST(PNGINC)
AC_SUBST(ZLIB)
AC_SUBST(ZLIBINC)

AC_DEFINE([HAVE_LIBJPEG], [], [libjpeg support])
AC_DEFINE([HAVE_LIBPNG], [], [libpng support])

LIBS="$NEWLIBS $LIBS"

dnl Directories for config.h...
if test "$prefix" = "NONE"; then
    prefix="/usr/local"
fi

if test "$exec_prefix" = "NONE"; then
    exec_prefix="$prefix"
fi

if test "$bindir" = "\${exec_prefix}/bin"; then
    bindir="$exec_prefix/bin"
fi

dnl Fix "datarootdir" variable if it hasn't been specified...
if test "$datarootdir" = "\${prefix}/share"; then
    if test "$prefix" = "/"; then
	datarootdir="/usr/share"
    else
	datarootdir="$prefix/share"
    fi
fi

dnl Fix "datadir" variable if it hasn't been specified...
if test "$datadir" = "\${prefix}/share"; then
    if test "$prefix" = "/"; then
	datadir="/usr/share"
    else
	datadir="$prefix/share"
    fi
elif test "$datadir" = "\${datarootdir}"; then
    datadir="$datarootdir"
fi

AC_DEFINE([MAX_CHAPTERS], [1000], [max number of chapters or files])
AC_DEFINE([MAX_COLUMNS], [200], [max number of columns in a table])
AC_DEFINE([MAX_HF_IMAGES], [10], [max number of header/footer images])

AC_DEFINE([ALLOC_FILES], [10], [temporary/image files])
AC_DEFINE([ALLOC_HEADINGS], [50], [headings])
AC_DEFINE([ALLOC_LINKS], [100], [web links])
AC_DEFINE([ALLOC_OBJECTS], [100], [pdf objects])
AC_DEFINE([ALLOC_PAGES], [10], [ps/pdf pages])
AC_DEFINE([ALLOC_ROWS], [20], [table rows])

AC_DEFINE_UNQUOTED([DOCUMENTATION], ["$datadir/doc/htmldoc"], [documentation directory])
AC_DEFINE_UNQUOTED([HTML_DATA], ["$datadir/htmldoc"], [data directory])

dnl Update compiler options...
if test -n "$GXX"; then
    dnl Set optimization flags...
    if test -z "$OPTIM"; then
        OPTIM="-Os -g"
    fi

    dnl Show all standard warnings + unused variables when compiling...
    OPTIM="-Wall -Wunused -Wno-char-subscripts -Wno-format-y2k $OPTIM"

    dnl See if GCC supports -fno-rtti...
    AC_MSG_CHECKING(if GCC supports -fno-rtti)
    OLDCFLAGS="$CFLAGS"
    CFLAGS="$CFLAGS -fno-rtti"
    AC_TRY_COMPILE(,,
	CXXFLAGS="$CXXFLAGS -fno-rtti"
	AC_MSG_RESULT(yes),
	AC_MSG_RESULT(no))
    CFLAGS="$OLDCFLAGS"

    dnl See if GCC supports -fno-exceptions...
    AC_MSG_CHECKING(if GCC supports -fno-exceptions)
    OLDCFLAGS="$CFLAGS"
    CFLAGS="$CFLAGS -fno-exceptions"
    AC_TRY_COMPILE(,,
	CXXFLAGS="$CXXFLAGS -fno-exceptions"
	AC_MSG_RESULT(yes),
	AC_MSG_RESULT(no))
    CFLAGS="$OLDCFLAGS"

    dnl See if we are running Solaris; if so, try the -fpermissive option...
    if test "$uname" = SunOS; then
	AC_MSG_CHECKING(if GCC supports -fpermissive)

	OLDCFLAGS="$CFLAGS"
	CFLAGS="$CFLAGS -fpermissive"
	AC_TRY_COMPILE(,,
	    CXXFLAGS="$CXXFLAGS -fpermissive"
	    AC_MSG_RESULT(yes),
	    AC_MSG_RESULT(no))
	CFLAGS="$OLDCFLAGS"
    fi
fi

if test "x$with_gui" != xno; then
    if test "x$FLTKCONFIG" != x; then
	    OPTIM="`$FLTKCONFIG --cflags` $OPTIM"
    fi
fi

dnl Generate the top-level Makefile and Makedefs file...
AC_OUTPUT(Makedefs Makefile desktop/htmldoc.plist)
