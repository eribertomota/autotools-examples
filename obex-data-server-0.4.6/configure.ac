AC_PREREQ(2.60)
AC_INIT(obex-data-server, 0.4.6)

AM_INIT_AUTOMAKE([foreign subdir-objects])
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])
AM_CONFIG_HEADER(config.h)

AM_MAINTAINER_MODE

AC_PREFIX_DEFAULT(/usr/local)

if test "$sysconfdir" = "\${prefix}/etc" \
    && { test "$prefix" = "NONE" || test "$prefix" = "/usr" \
      || test "$prefix" = "/usr/" ; } ; then
    if test "$( (uname -s) )" = "Linux" ; then
      sysconfdir=/etc
    fi
    (
    prefix=$ac_default_prefix
    sysconfdir=`eval echo "$sysconfdir"`
    AC_MSG_NOTICE([configuration directory is "$sysconfdir".])
    AC_MSG_NOTICE([use --sysconfdir to override.])
    )
fi
AC_DEFINE_UNQUOTED(CONFIGDIR, "$sysconfdir",
                   [Directory for the configuration files])

if test "${CFLAGS}" = ""; then
        CFLAGS="-Wall -O2 -D_FORTIFY_SOURCE=2"
fi

AC_LANG_C
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_SED
PKG_PROG_PKG_CONFIG

AC_PATH_PROG(GLIB_GENMARSHAL, glib-genmarshal)
AC_PATH_PROG([DBUS_BINDING_TOOL],[dbus-binding-tool])


GLIB_REQUIRED=2.10.0
DBUS_REQUIRED=0.70
BLUEZ_REQUIRED=3.34
OPENOBEX_REQUIRED=1.3
IMAGEMAGICK_REQUIRED=6.0.0


bip_found=no
bip_type=disabled

AC_ARG_ENABLE(bip,
				AC_HELP_STRING([--enable-bip=[gdk-pixbuf|magick|auto|no]],
				[Enable BIP support (disabling it will break some BIP functions)]),
				[bip_enable=${enableval}], [bip_enable=auto])

if test "$bip_enable" = "auto" || test "$bip_enable" = "magick"; then
	PKG_CHECK_MODULES(BIP, gthread-2.0 Wand >= $IMAGEMAGICK_REQUIRED,
			  [bip_found=yes], [bip_found=no])
	if test "$bip_found" = "yes" ; then
		AC_DEFINE(USE_IMAGEMAGICK, [], [We have ImageMagick support])
		bip_type="ImageMagick"
	else
		if test "$bip_enable" = "magick"; then
			AC_MSG_ERROR([you requested BIP support using ImageMagick, but it is not available])
		fi
	fi
fi

if test "$bip_enable" = "auto" -a "$bip_found" = "no" || test "$bip_enable" = "gdk-pixbuf" ; then
	PKG_CHECK_MODULES(BIP, gthread-2.0 gdk-pixbuf-2.0,
			  [bip_found=yes], [bip_found=no])
	if test "$bip_found" = "yes" ; then
		AC_DEFINE(USE_GDKPIXBUF, [], [We have ImageMagick support])
		bip_type="gdk-pixbuf"
	else
		if test "$bip_enable" = "gdk-pixbuf"; then
			AC_MSG_ERROR([you requested BIP support using gdk-pixbuf, but it is not available])
		fi
	fi
fi


AC_ARG_ENABLE(usb,
				AC_HELP_STRING([--disable-usb],
				[Disable USB support (breaks USB interface discovery functions)]),[usb_enable=no],
				[usb_enable=yes])
if test "${usb_enable}" = "yes"; then
	PKG_CHECK_MODULES(USB, libusb)
	AC_SUBST(USB_CFLAGS)
	AC_SUBST(USB_LIBS)
	AC_DEFINE(USE_USB, [], [We have USB support])
fi


AC_ARG_ENABLE(system-config,
				AC_HELP_STRING([--enable-system-config],
				[install D-Bus system config file]), [
	system_config_enable=${enableval}
])
AM_CONDITIONAL(SYSTEMCONFIG, test "${system_config_enable}" = "yes")


AC_ARG_ENABLE([debug],
	AC_HELP_STRING([--enable-debug], [turn on debugging]),
set_debug="$enableval",[
if test -d $srcdir/.svn; then
        set_debug=yes
else
        set_debug=no
fi
])
if test "$set_debug" != "no"; then
	CFLAGS="$CFLAGS -g -pg"
	LDFLAGS="$LDFLAGS -pg"
fi

AC_ARG_ENABLE(more-warnings,
  AC_HELP_STRING([--enable-more-warnings], [Maximum compiler warnings]),
set_more_warnings="$enableval",[
if test -d $srcdir/.svn; then
        set_more_warnings=yes
else
        set_more_warnings=no
fi
])
AC_MSG_CHECKING(for more warnings)
if test "$GCC" = "yes" -a "$set_more_warnings" != "no"; then
        AC_MSG_RESULT(yes)
        CFLAGS+=" -Werror -Wextra -Wcast-align"
        CFLAGS+=" -Wnested-externs -Wpointer-arith"
        CFLAGS+=" -Wno-unused-parameter -Wno-missing-field-initializers"
        CFLAGS+=" -Wredundant-decls"
        CFLAGS+=" -Wsign-compare -fno-strict-aliasing"
else
        AC_MSG_RESULT(no)
fi


PKG_CHECK_MODULES(GLIB, glib-2.0 >= $GLIB_REQUIRED gobject-2.0)
AC_SUBST(GLIB_CFLAGS)
AC_SUBST(GLIB_LIBS)

PKG_CHECK_MODULES(DBUS, dbus-glib-1 >= $DBUS_REQUIRED dbus-1 >= $DBUS_REQUIRED)
AC_SUBST(DBUS_CFLAGS)
AC_SUBST(DBUS_LIBS)

PKG_CHECK_MODULES(BLUEZ, bluez >= $BLUEZ_REQUIRED)
AC_SUBST(BLUEZ_CFLAGS)
AC_SUBST(BLUEZ_LIBS)
AC_CHECK_LIB(bluetooth, sdp_extract_seqtype_safe, AC_DEFINE(USE_BLUEZ3FUNCS, [], [We are using Bluez 3.x]))

PKG_CHECK_MODULES(OPENOBEX, openobex >= $OPENOBEX_REQUIRED)
AC_SUBST(OPENOBEX_CFLAGS)
AC_SUBST(OPENOBEX_LIBS)

AC_OUTPUT([Makefile])

dnl ==========================================================================
echo "
                    obex-data-server $VERSION
                  =============================

        prefix:                    ${prefix}
        compiler:                  ${CC}
        cflags:                    ${CFLAGS}
        BIP imaging support:       $bip_type
        USB support:               $usb_enable
"

