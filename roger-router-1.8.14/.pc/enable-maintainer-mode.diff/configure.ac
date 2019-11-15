dnl Process this file with autoconf to produce configure.

m4_define([roger_major], [1])
m4_define([roger_minor], [8])
m4_define([roger_micro], [14])

m4_define([roger_version],[roger_major.roger_minor.roger_micro])

AC_INIT([Roger Router],[roger_version],[http://www.tabos.org/roger])
m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])])

AC_PREFIX_DEFAULT(/usr)
AM_INIT_AUTOMAKE([1.11 no-dist-gzip dist-xz foreign subdir-objects])
AC_CONFIG_HEADERS(config.h)

AC_CONFIG_MACRO_DIR(m4)

# Check for compilers.
AC_PROG_CC
AC_PROG_CXX
AC_CHECK_PROG(found_cc, "$CC", yes, no)
AM_PROG_CC_C_O

# Check for libtool
LT_INIT(win32-dll)

AC_CANONICAL_HOST

GLIB_GSETTINGS

ROGER_VERSION_MAJOR=roger_major()
AC_SUBST(ROGER_VERSION_MAJOR)
ROGER_VERSION_MINOR=roger_minor()
AC_SUBST(ROGER_VERSION_MINOR)
ROGER_VERSION_MICRO=roger_micro()
AC_SUBST(ROGER_VERSION_MICRO)

AC_CHECK_LIB(m, pow)
AC_CHECK_LIB(gthread-2.0, g_thread_init)
AC_PATH_PROG(INTLTOOL_MSGMERGE, msgmerge, msgmerge)
AC_PATH_PROG(INTLTOOL_XGETTEXT, xgettext, xgettext)

dnl Add the languages which your application supports to po/LINGUAS
GETTEXT_PACKAGE=roger
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE, ["$GETTEXT_PACKAGE"], [Define to the Gettext package name])
AC_SUBST(GETTEXT_PACKAGE)
IT_PROG_INTLTOOL([0.40.0])

ALL_LINGUAS=""
AM_GLIB_GNU_GETTEXT

AC_MSG_CHECKING([if cross-building for win32])
case "$host" in
	*-*-*mingw*)
		WIN32=yes
		macos=no
		OS_CFLAGS="-D_WIN32_WINNT=0x0501 -DROUTERMANAGER_PLUGINS='\"lib/routermanager/\"' -DAPP_PLUGINS='\"lib/roger/\"' -DAPP_DATA='\"share/roger/\"' -DAPP_LOCALE='\"share/locale\"'"
		OS_LIBS="-mwindows -mms-bitfields -Wl,-subsystem,windows -lws2_32"
		AC_CHECK_TOOL(WINDRES, windres)
	;;
	*darwin*)
		WIN32=no
		macos=yes
		OS_CFLAGS="-DROUTERMANAGER_PLUGINS='\"lib/routermanager/\"' -DAPP_PLUGINS='\"lib/roger/\"' -DAPP_DATA='\"share/roger/\"' -DAPP_LOCALE='\"share/locale\"'"
		OS_LIBS="-rdynamic"
	;;
	*freebsd*)
		WIN32=no
		macos=no
		AC_PREFIX_DEFAULT(/usr/local)
		OS_CFLAGS=""
		OS_LIBS="-rdynamic"
	;;
	*)
		WIN32=no
		macos=no
		OS_CFLAGS="-DROUTERMANAGER_PLUGINS='\"\$(libdir)/routermanager/\"' -DAPP_PLUGINS='\"\$(libdir)/roger/\"' -DAPP_DATA='\"\$(datadir)/roger/\"' -DAPP_LOCALE='\"\$(localedir)\"' -Wall"
		OS_LIBS="-rdynamic"
	;;
esac
AC_SUBST(OS_CFLAGS)
AC_SUBST(OS_LIBS)
AC_MSG_RESULT([$WIN32])
AM_CONDITIONAL(WIN32, test "x$WIN32" != "xno")
AM_CONDITIONAL(MACOSX, test "x$macos" != "xno")

PKG_CHECK_MODULES([EXTRA], [glib-2.0 >= 2.40 gio-2.0 >= 2.40 speex >= 1.0 speexdsp >= 1.0 sndfile >= 1.0.0 libxml-2.0 gupnp-1.0 gssdp-1.0])

# Check for GTK >= 3.14
PKG_CHECK_MODULES([GTK], [gtk+-3.0 >= 3.10])

PKG_CHECK_MODULES([GMODULE], [gmodule-2.0])

PKG_CHECK_MODULES([SOUP], [libsoup-2.4])

PKG_CHECK_MODULES([PEAS], [libpeas-1.0])
PKG_CHECK_MODULES([PEAS_GTK], [libpeas-gtk-1.0])

AC_CHECK_HEADERS([tiffio.h])
AC_CHECK_LIB([tiff], [TIFFOpen], , AC_MSG_ERROR("Can't build without libtiff (does your system require a libtiff-devel package?)"), -lm)

dnl *******************************************************************
dnl Decide which fax spooler solution to use
dnl *******************************************************************
# determine prefered default type
case "$host" in
	*-*-*mingw*)
		fax_printer=socket-server
	;;
	*darwin* | *freebsd*)
		PKG_CHECK_MODULES(FAX_SPOOLER, 
			[gio-2.0 >= 2.36], 
			[fax_printer=spoolerdir],
			[fax_printer=socket-server]
		)
	;;
	
	*)
		fax_printer=spoolerdir
	;;
esac

AC_ARG_WITH([fax_spooler-type],
	[AS_HELP_STRING([--with-fax-spooler-type=@<:@ARG@:>@],
		[type of fax printer spooler to be supported (possible values: spoolerdir, socket-server or auto) @<:@default=auto@:>@])],
	[if test x$with_fax_spooler_type = xauto; then 
		with_fax_spooler_type=$fax_printer
	 fi],
	[with_fax_spooler_type=$fax_printer])

AC_MSG_CHECKING(for fax spooler type)
case "$with_fax_spooler_type" in
	spoolerdir)
		AC_DEFINE(USE_PRINTER_SPOOLER, 1, [Expect files in spooler directory /var/spool/roger])
		AC_MSG_RESULT([Outgoing faxes are expected in spooler directory /var/spool/roger])
	;;
	socket-server)
		AC_DEFINE(USE_PRINTER_SERVER, 1, [Use printer server on port 9100])
		AC_MSG_RESULT([Outgoing faxes are received by fax printer server on port 9100])
	;;
	*)
		AC_MSG_ERROR([Invalid option $with_fax_spooler_type])
	;;
esac

dnl *******************************************************************
dnl Check if we can support gtkstatusicon plugin
dnl *******************************************************************
AC_MSG_CHECKING(for statusicon support)
AS_IF($PKG_CONFIG --atleast-version=3.16 gtk+-3.0, [with_statusicon=no], [with_statusicon=yes])
AC_MSG_RESULT($with_statusicon)
AM_CONDITIONAL(WITH_STATUSICON, test "x$with_statusicon" != "xno")

# Check for unistd.h
AC_CHECK_HEADERS([unistd.h])

#  Check for sigaction and sigset
AC_CHECK_FUNCS(sigaction, [ have_sigaction="1" ], [ have_sigaction="0" ])

AC_CACHE_CHECK([for sigset()],[ac_cv_sigset],[
	AC_TRY_COMPILE([#include <signal.h>],[sigset(SIGTERM,SIG_IGN);],
	[ac_cv_sigset=yes], [ac_cv_sigset=no])
])
if test x"ac_cv_sigset" = xyes; then
	AC_DEFINE([HAVE_SIGSET],1,[Define to 1 if you have the `sigset' function.])
fi

dnl ********************************************************************
dnl libnotify is optional
dnl ********************************************************************
AC_ARG_WITH([libnotify],
        [AS_HELP_STRING([--with-libnotify=@<:@ARG@:>@],
        [Use libnotify (possible values: no, yes, check, or the path to libnotify) @<:@default=check@:>@])],
        [],
        [with_libnotify=check])

AC_MSG_CHECKING(for libnotify)
AS_IF([test "x$with_libnotify" != xsuper],
        [if test "x$with_libnotify" = xcheck; then
                $PKG_CONFIG --exists libnotify && with_libnotify=yes
        elif test "x$with_libnotify" = xyes; then
                ( $PKG_CONFIG --exists libnotify ) || AC_MSG_FAILURE(
                        [--with-libnotify=yes was given, but test for libnotify failed])
        fi
        if test "x$with_libnotify" = xyes; then
                AC_SUBST([LIBNOTIFY_CFLAGS], ["`$PKG_CONFIG --cflags libnotify`"])
                AC_SUBST([LIBNOTIFY_LIBS], ["`$PKG_CONFIG --libs libnotify`"])
                AC_DEFINE([HAVE_LIBNOTIFY], 1, [Have libnotify])
                ROGER_FEATURES_YES="\tlibnotify\n$ROGER_FEATURES_YES"
        else
                with_libnotify=no
                ROGER_FEATURES_NO="\tlibnotify\n$ROGER_FEATURES_NO"
        fi
])

AC_MSG_RESULT($with_libnotify)

AM_CONDITIONAL(WITH_LIBNOTIFY, test "x$with_libnotify" != "xno")

dnl ********************************************************************
dnl secret is optional
dnl ********************************************************************
AC_ARG_WITH([secret],
	[AS_HELP_STRING([--with-secret=@<:@ARG@:>@],
	[Use secret (possible values: no, yes, check, or the path to secret) @<:@default=check@:>@])],
	[],
	[with_secret=check])

AC_MSG_CHECKING(for libsecret-1 >= 0.11)
AS_IF([test "x$with_secret" != xno],
	[if test "x$with_secret" = xcheck; then
		$PKG_CONFIG --atleast-version=0.11 libsecret-1 && with_secret=yes
	elif test "x$with_secret" = xyes; then
		$PKG_CONFIG --atleast-version=0.11 libsecret-1 || AC_MSG_FAILURE(
		[--with-secret=yes was given, but test for secret failed])
	fi
	if test "x$with_secret" = xyes; then
		AC_SUBST([SECRET_CFLAGS], ["`$PKG_CONFIG --cflags libsecret-1`"])
		AC_SUBST([SECRET_LIBS], ["`$PKG_CONFIG --libs libsecret-1`"])

		ROGER_FEATURES_YES="\tsecret\n$ROGER_FEATURES_YES"
	else
		with_secret=no
		ROGER_FEATURES_NO="\tsecret\n$ROGER_FEATURES_NO"
	fi
])
AC_MSG_RESULT($with_secret)
AM_CONDITIONAL(WITH_SECRET, test "x$with_secret" != "xno")
AM_CONDITIONAL(HAVE_SECRET_SOURCE_REGISTRY, test "x$with_secret_registry" = "xyes")

dnl ********************************************************************
dnl MacOS keyChain is optional
dnl ********************************************************************
AC_ARG_WITH([macos-keychain],
	[AS_HELP_STRING([--with-macos-keychain=@<:@ARG@:>@], 
	[Use macos-keychain (possible values: no, yes, check) @<:@default=check@:>@])],
	[],
	[with_macos_keychain=check])

AC_MSG_CHECKING(for MacOS-keyring)

if test "$with_macos_keychain" = "check"; then
AC_CACHE_CHECK([for SecKeychainGetVersion], 
    ac_cv_func_SecKeychainGetVersion, 
    [ac_save_LIBS="$LIBS" 
    LIBS="$LIBS -Wl,-framework -Wl,Security" 
    AC_TRY_LINK([#include <Security/Security.h>], 
        [SecKeychainGetVersion(NULL);], 
        [ac_cv_func_SecKeychainGetVersion=yes], 
        [ac_cv_func_SecKeychainGetVersion=no]) 
    LIBS="$ac_save_LIBS"]) 
if test $ac_cv_func_SecKeychainGetVersion = yes; then 
    with_macos_keychain=yes
    OS_LIBS="$OS_LIBS -Wl,-framework -Wl,Security"
else
    with_macos_keychain=no 
fi 
fi

if test "x$with_macos_keychain" != "xno"; then
	ROGER_FEATURES_YES="\tmacos-keyring\n$ROGER_FEATURES_YES"
	with_macos_keychain=yes
else
	ROGER_FEATURES_NO="\tmacos-keyring\n$ROGER_FEATURES_NO"
fi

AC_MSG_RESULT($with_macos_keychain)

AM_CONDITIONAL(WITH_MACOS_KEYCHAIN, test "x$with_macos_keychain" != "xno")

AM_CONDITIONAL(WITH_OSX_AB, test "x$with_macos_keychain" != "xno")

dnl ********************************************************************
dnl kwallet is optional
dnl ********************************************************************
AC_ARG_WITH([kwallet],
	[AS_HELP_STRING([--with-kwallet=@<:@ARG@:>@],
	[Use kwallet (possible values: no, yes or the path to kwallet) @<:@default=no@:>@])],
	[],
	[with_kwallet=no])

AC_MSG_CHECKING(for kwallet)
AS_IF([test "x$with_kwallet" != xno],
	[AC_SUBST([KWALLET_CFLAGS], ["`pkg-config --cflags-only-I QtCore QtDBus QtGui` -I`kde4-config --path include`"])
	AC_SUBST([KWALLET_LIBS], ["-lQtCore -lQtDBus -lQtGui -lkdecore -lkdeui -L`kde4-config --path lib` -L/usr/lib/kde4/devel -L/usr/lib64/kde4/devel"])
	AC_DEFINE([HAVE_KWALLET], 1, [Have kwallet])
	ROGER_FEATURES_YES="\tkwallet\n$ROGER_FEATURES_YES"
])
AC_MSG_RESULT($with_kwallet)

AM_CONDITIONAL(WITH_KWALLET, test "x$with_kwallet" != "xno")


dnl ********************************************************************
dnl gdata is optional
dnl ********************************************************************
AC_ARG_WITH([gdata],
	[AS_HELP_STRING([--with-gdata=@<:@ARG@:>@],
	[Use gdata (possible values: no, yes, check, or the path to secret) @<:@default=check@:>@])],
	[],
	[with_gdata=check])

AC_MSG_CHECKING(for libgdata)
AS_IF([test "x$with_gdata" != xno],
	[if test "x$with_gdata" = xcheck; then
		$PKG_CONFIG libgdata && with_gdata=yes
	elif test "x$with_gdata" = xyes; then
		$PKG_CONFIG libgdata || AC_MSG_FAILURE(
		[--with-gdata=yes was given, but test for gdata failed])
	fi
	if test "x$with_gdata" = xyes; then
		AC_SUBST([GDATA_CFLAGS], ["`$PKG_CONFIG --cflags libgdata`"])
		AC_SUBST([GDATA_LIBS], ["`$PKG_CONFIG --libs libgdata`"])

		ROGER_FEATURES_YES="\tgdata\n$ROGER_FEATURES_YES"
	else
		with_gdata=no
		ROGER_FEATURES_NO="\tgdata\n$ROGER_FEATURES_NO"
	fi
])
AC_MSG_RESULT($with_gdata)
AM_CONDITIONAL(WITH_GDATA, test "x$with_gdata" != "xno")

dnl ********************************************************************
dnl ebook is optional
dnl ********************************************************************
AC_ARG_WITH([ebook],
	[AS_HELP_STRING([--with-ebook=@<:@ARG@:>@],
	[Use ebook (possible values: no, yes, check, or the path to ebook) @<:@default=check@:>@])],
	[],
	[with_ebook=check])

AC_MSG_CHECKING(for libebook-1.2 >= 3.10.0)
AS_IF([test "x$with_ebook" != xno],
	[if test "x$with_ebook" = xcheck; then
		$PKG_CONFIG --atleast-version=3.10.0 libebook-1.2 && with_ebook=yes
	elif test "x$with_ebook" = xyes; then
		$PKG_CONFIG --atleast-version=3.10.0 libebook-1.2 || AC_MSG_FAILURE(
		[--with-ebook=yes was given, but test for ebook failed])
	fi
	if test "x$with_ebook" = xyes; then
		AC_SUBST([EBOOK_CFLAGS], ["`$PKG_CONFIG --cflags libebook-1.2`"])
		AC_SUBST([EBOOK_LIBS], ["`$PKG_CONFIG --libs libebook-1.2`"])

		ROGER_FEATURES_YES="\tebook\n$ROGER_FEATURES_YES"
	else
		with_ebook=no
		ROGER_FEATURES_NO="\tebook\n$ROGER_FEATURES_NO"
	fi
])
AC_MSG_RESULT($with_ebook)
AM_CONDITIONAL(WITH_EBOOK, test "x$with_ebook" != "xno")

dnl ********************************************************************
dnl gstreamer-1.4 is optional
dnl ********************************************************************
AC_ARG_WITH([gstreamer1],
	[AS_HELP_STRING([--with-gstreamer1=@<:@ARG@:>@],
	[Use gstreamer-1.0 (possible values: no, yes, check, or the path to gstreamer) @<:@default=check@:>@])],
	[],
	[with_gstreamer1=check])

AC_MSG_CHECKING(for gstreamer-1.4 and gstreamer-app-1.4)
AS_IF([test "x$with_gstreamer1" != xno],
	[if test "x$with_gstreamer1" = xcheck; then
		pkg-config --atleast-version=1.4.0 gstreamer-1.0 && pkg-config --exists gstreamer-app-1.0 && with_gstreamer1=yes
	elif test "x$with_gstreamer1" = xyes; then
		( pkg-config --atleast-version=1.4.0 gstreamer-1.0 && pkg-config --exists gstreamer-app-1.0) || AC_MSG_FAILURE(
			[--with-gstreamer-1.0=yes was given, but test for gstreamer-1.0 and gstreamer-app-1.0 failed])
	fi
	if test "x$with_gstreamer1" = xyes; then
		AC_SUBST([GSTREAMER1_CFLAGS], ["`pkg-config --cflags gstreamer-1.0 gstreamer-app-1.0`"])
		AC_SUBST([GSTREAMER1_LIBS], ["`pkg-config --libs gstreamer-1.0 gstreamer-app-1.0`"])
		AC_DEFINE([HAVE_GSTREAMER1], 1, [Have gstreamer 1.0])
		ROGER_FEATURES_YES="\tgstreamer 1.0\n$ROGER_FEATURES_YES"
	else
		with_gstreamer1=no
		ROGER_FEATURES_NO="\tgstreamer 1.0\n$ROGER_FEATURES_NO"
	fi
])

AC_MSG_RESULT($with_gstreamer1)

AM_CONDITIONAL(WITH_GSTREAMER1, test "x$with_gstreamer1" != "xno")

dnl ********************************************************************
dnl pulseaudio is optional
dnl ********************************************************************
AC_ARG_WITH([pulseaudio],
	[AS_HELP_STRING([--with-pulseaudio=@<:@ARG@:>@],
	[Use pulseaudio (possible values: no, yes, check, or the path to pulseaudio) @<:@default=no@:>@])],
	[],
	[with_pulseaudio=no])

AC_MSG_CHECKING(for libpulse-simple)
AS_IF([test "x$with_pulseaudio" != xsuper],
	[if test "x$with_pulseaudio" = xcheck; then
		$PKG_CONFIG --exists libpulse-simple && with_pulseaudio=yes
	elif test "x$with_pulseaudio" = xyes; then
		( $PKG_CONFIG --exists libpulse-simple ) || AC_MSG_FAILURE(
			[--with-pulseaudio=yes was given, but test for libpulse-simple failed])
	fi
	if test "x$with_pulseaudio" = xyes; then
		AC_SUBST([PULSEAUDIO_CFLAGS], ["`$PKG_CONFIG --cflags libpulse-simple`"])
		AC_SUBST([PULSEAUDIO_LIBS], ["`$PKG_CONFIG --libs libpulse-simple`"])
		AC_DEFINE([HAVE_PULSEAUDIO], 1, [Have pulseaudio])
		ROGER_FEATURES_YES="\tpulseaudio\n$ROGER_FEATURES_YES"
	else
		with_pulseaudio=no
		ROGER_FEATURES_NO="\tpulseaudio\n$ROGER_FEATURES_NO"
	fi
])

AC_MSG_RESULT($with_pulseaudio)

AM_CONDITIONAL(WITH_PULSEAUDIO, test "x$with_pulseaudio" != "xno")

dnl ********************************************************************
dnl portaudio is optional
dnl ********************************************************************
AC_ARG_WITH([portaudio],
	[AS_HELP_STRING([--with-portaudio=@<:@ARG@:>@],
	[Use portaudio (possible values: no, yes, check, or the path to portaudio) @<:@default=no@:>@])],
	[],
	[with_portaudio=no])

AC_MSG_CHECKING(for portaudio-2.0 version 19)
AS_IF([test "x$with_portaudio" != xsuper],
	[if test "x$with_portaudio" = xcheck; then
		$PKG_CONFIG --atleast-version=19 portaudio-2.0 && with_portaudio=yes
	elif test "x$with_portaudio" = xyes; then
		( $PKG_CONFIG --atleast-version=19 portaudio-2.0 ) || AC_MSG_FAILURE(
			[--with-portaudio=yes was given, but test for portaudio-2.0 failed])
	fi
	if test "x$with_portaudio" = xyes; then
		AC_SUBST([PORTAUDIO_CFLAGS], ["`$PKG_CONFIG --cflags portaudio-2.0`"])
		AC_SUBST([PORTAUDIO_LIBS], ["`$PKG_CONFIG --libs portaudio-2.0`"])
		AC_DEFINE([HAVE_PORTAUDIO], 1, [Have portaudio])
		ROGER_FEATURES_YES="\tportaudio\n$ROGER_FEATURES_YES"
	else
		with_portaudio=no
		ROGER_FEATURES_NO="\tportaudio\n$ROGER_FEATURES_NO"
	fi
])

AC_MSG_RESULT($with_portaudio)

AM_CONDITIONAL(WITH_PORTAUDIO, test "x$with_portaudio" != "xno")


dnl ********************************************************************
dnl faxophone
dnl ********************************************************************
AC_MSG_CHECKING(for faxophone)
AC_ARG_WITH([faxophone],
	[AS_HELP_STRING([--with-faxophone=@<:@ARG@:>@],
	[Use faxophone (possible values: yes or no) @<:@default=yes@:>@])],
	[],
	[with_faxophone=yes])
AC_MSG_RESULT($with_faxophone)

# Faxophone test
if test "x$with_faxophone" = xyes; then
	AC_DEFINE([HAVE_FAXOPHONE], 1, [Have faxophone])
	ROGER_FEATURES_YES="\tfaxophone\n$ROGER_FEATURES_YES"

	PKG_CHECK_MODULES([CAPI], [capi20 >= 3.6],
		[AC_DEFINE([HAVE_CAPI_36], 1, [Use new CAPI])],
		[PKG_CHECK_MODULES([CAPI], [capi20 >= 3.5])])

	dnl ********************************************************************
	dnl spandsp
	dnl ********************************************************************
	AC_ARG_WITH([spandsp],
		[AS_HELP_STRING([--with-spandsp=@<:@ARG@:>@],
		[Use spandsp (possible values: yes, check, or the path to spandsp) @<:@default=check@:>@])],
		[],
		[with_spandsp=check])

	AC_MSG_CHECKING(for spandsp)
	AS_IF([test "x$with_spandsp" != xsuper],
		[if test "x$with_spandsp" = xcheck; then
			$PKG_CONFIG --exists spandsp && with_spandsp=yes
		elif test "x$with_spandsp" = xyes; then
			( $PKG_CONFIG --exists spandsp ) || AC_MSG_FAILURE(
				[--with-spandsp=yes was given, but test for spandsp])
		fi
		if test "x$with_spandsp" = xyes; then
			AC_SUBST([SPANDSP_CFLAGS], ["`$PKG_CONFIG --cflags spandsp`"])
			AC_SUBST([SPANDSP_LIBS], ["`$PKG_CONFIG --libs spandsp`"])
			AC_MSG_RESULT($with_spandsp)
		else
			AC_MSG_RESULT($with_spandsp)
			AC_CHECK_LIB(spandsp, fax_init, [with_spandsp=yes], AC_MSG_ERROR([spandsp is required by this package]))
			AC_SUBST([SPANDSP_CFLAGS], [""])
			AC_SUBST([SPANDSP_LIBS], ["-lspandsp"])
		fi
	])
else
	ROGER_FEATURES_NO="\tfaxophone\n$ROGER_FEATURES_NO"
fi

AM_CONDITIONAL(WITH_FAXOPHONE, test "x$with_faxophone" != "xno")

dnl ********************************************************************
dnl appindicator is optional
dnl ********************************************************************
AC_ARG_WITH([appindicator3],
	[AS_HELP_STRING([--with-appindicator3=@<:@ARG@:>@],
	[Use appindicator3 (possible values: no, yes, check, or the path to appindicator3) @<:@default=check@:>@])],
	[],
	[with_appindicator3=check])

AC_MSG_CHECKING(for appindicator3-0.1)
AS_IF([test "x$with_appindicator3" != xno],
	[if test "x$with_appindicator3" = xcheck; then
		pkg-config --exists appindicator3-0.1 && with_appindicator3=yes
	elif test "x$with_appindicator3" = xyes; then
		pkg-config --exists appindicator3-0.1 || AC_MSG_FAILURE(
			[--with-appindicator3=yes was given, but test for appindicator3 failed])
	fi
	if test "x$with_appindicator3" = xyes; then
		AC_SUBST([APPINDICATOR_CFLAGS], ["`pkg-config --cflags appindicator3-0.1`"])
		AC_SUBST([APPINDICATOR_LIBS], ["`pkg-config --libs appindicator3-0.1`"])
		AC_DEFINE([HAVE_APPINDICATOR], 1, [Have appindicator])
		ROGER_FEATURES_YES="\tappindicator3\n$ROGER_FEATURES_YES"
	else
		with_appindicator3=no
		ROGER_FEATURES_NO="\tappindicator3\n$ROGER_FEATURES_NO"
	fi
])

AC_MSG_RESULT($with_appindicator3)

AM_CONDITIONAL(WITH_APPINDICATOR3, test "x$with_appindicator3" != "xno")

dnl ********************************************************************
dnl gnotification is optional
dnl ********************************************************************
AC_ARG_WITH([gnotification],
	[AS_HELP_STRING([--with-gnotifcation=@<:@ARG@:>@],
	[Use gnotification (possible values: no, yes, check, or the path to gnotification) @<:@default=check@:>@])],
	[],
	[with_gnotification=check])

AC_MSG_CHECKING(for gnotification)
AS_IF([test "x$with_gnotification" != xno],
	[if test "x$with_gnotification" = xcheck; then
		pkg-config --atleast-version=3.12.0 gtk+-3.0 && with_gnotification=yes
	elif test "x$with_gnotification" = xyes; then
		( pkg-config --atleast-version=3.12.0 gtk+-3.12.0) || AC_MSG_FAILURE(
			[--with-gnotificaion=yes was given, but test for gnotificaion failed])
	fi
	if test "x$with_gnotification" = xyes; then
		AC_DEFINE([HAVE_GNOTIFICATION], 1, [Have gnotification])
		ROGER_FEATURES_YES="\tgnotification\n$ROGER_FEATURES_YES"
	else
		with_gnotification=no
		ROGER_FEATURES_NO="\tgnotification\n$ROGER_FEATURES_NO"
	fi
])

AC_MSG_RESULT($with_gnotification)

AM_CONDITIONAL(WITH_GNOTIFICATION, test "x$with_gnotification" != "xno")

AC_ARG_ENABLE(werror,
	AS_HELP_STRING([--disable-werror], [don't use gcc's -Werror option when building]))

if test x"$enable_werror" != xno
then
	EXTRA_CFLAGS+="-Werror"
fi

dnl ********************************************************************
dnl Check for coverage tool gcov
dnl ********************************************************************
dnl AC_TDD_GCOV

AC_CONFIG_FILES([
    Makefile
    win32/roger.nsi
    doc/Makefile
    doc/roger.1
    doc/roger_cli.1
    po/Makefile.in
    libroutermanager/routermanager.pc
    libroutermanager/Makefile
    libroutermanager/data/Makefile
    libroutermanager/plugins/Makefile
    libroutermanager/plugins/fritzbox/Makefile
    libroutermanager/plugins/callmonitor/Makefile
    libroutermanager/plugins/areacodes_global/Makefile
    libroutermanager/plugins/pulseaudio/Makefile
    libroutermanager/plugins/reverselookup/Makefile
    libroutermanager/plugins/webjournal/Makefile
    libroutermanager/plugins/wincred/Makefile
    libroutermanager/plugins/portaudio/Makefile
    libroutermanager/plugins/gstreamer1/Makefile
    libroutermanager/plugins/secret/Makefile
    roger/Makefile
    roger/roger_winres.rc
    roger/data/Makefile
    roger-cli/Makefile
    roger/plugins/Makefile
    roger/plugins/statusicon/Makefile
    roger/plugins/statusicon/data/Makefile
    roger/plugins/fritzfon/Makefile
    roger/plugins/fritzfon/data/Makefile
    roger/plugins/evolution/Makefile
    roger/plugins/evolution/data/Makefile
    roger/plugins/gtknotify/Makefile
    roger/plugins/gtknotify/data/Makefile
    roger/plugins/indicator/Makefile
    roger/plugins/indicator/data/Makefile
    roger/plugins/vcard/Makefile
    roger/plugins/vcard/data/Makefile
    roger/plugins/google/Makefile
    roger/plugins/google/data/Makefile
    roger/plugins/thunderbird/Makefile
    roger/plugins/thunderbird/data/Makefile
    roger/plugins/kwallet/Makefile
    roger/plugins/keychain/Makefile
    roger/plugins/osxab/Makefile
    roger/plugins/notification/Makefile
    roger/plugins/notification/data/Makefile
    roger/plugins/gnotification/Makefile
    roger/plugins/gnotification/data/Makefile
    roger/images/Makefile
    roger/images/16x16/Makefile
    roger/images/22x22/Makefile
    roger/images/24x24/Makefile
    roger/images/32x32/Makefile
    roger/images/48x48/Makefile
    roger/images/scalable/Makefile
    macosx/roger.plist
    macosx/package
])
AC_OUTPUT


printf "\n"
printf "configure: *** Extra features that will be built:"
printf "$ROGER_FEATURES_YES\n" | sort
printf "\n"
printf "configure: *** Extra features that will NOT be built:"
printf "$ROGER_FEATURES_NO\n" | sort
printf "\n"
