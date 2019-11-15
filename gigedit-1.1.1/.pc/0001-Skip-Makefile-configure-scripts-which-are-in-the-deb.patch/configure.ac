dnl Process this file with autoconf to produce a configure script.

#------------------------------------------------------------------------------------
# The following is the current, official release version of gigedit:

m4_define(gigedit_ver_major, 1)
m4_define(gigedit_ver_minor, 1)
m4_define(gigedit_ver_release, 1)

AC_INIT([gigedit], [gigedit_ver_major.gigedit_ver_minor.gigedit_ver_release])
AC_CONFIG_SRCDIR([configure.ac])
AC_CONFIG_AUX_DIR([.])

#------------------------------------------------------------------------------------
# The following is the libtool / shared library version. This doesn't have to
# do anything with the release version. It MUST conform to the following rules:
#
#  1. Start with version information of `0:0:0' for each libtool library.
#  2. Update the version information only immediately before a public release of
#     your software. More frequent updates are unnecessary, and only guarantee
#     that the current interface number gets larger faster.
#  3. If the library source code has changed at all since the last update, then
#     increment revision (`c:r:a' becomes `c:r+1:a').
#  4. If any interfaces have been added, removed, or changed since the last update,
#     increment current, and set revision to 0.
#  5. If any interfaces have been added since the last public release, then increment
#     age.
#  6. If any interfaces have been removed since the last public release, then set age
#     to 0.

LIBGIGEDIT_LT_CURRENT=4
LIBGIGEDIT_LT_REVISION=0
LIBGIGEDIT_LT_AGE=0

SHARED_VERSION_INFO="$LIBGIGEDIT_LT_CURRENT:$LIBGIGEDIT_LT_REVISION:$LIBGIGEDIT_LT_AGE"
AC_LANG([C++])
AC_PROG_CXX
AC_LIBTOOL_WIN32_DLL
AC_PROG_LIBTOOL
AC_SUBST(SHLIB_VERSION_ARG)
AC_SUBST(SHARED_VERSION_INFO)
AC_SUBST(GIGEDIT_VER_MAJOR, gigedit_ver_major)
AC_SUBST(GIGEDIT_VER_MINOR, gigedit_ver_minor)
AC_SUBST(GIGEDIT_VER_RELEASE, gigedit_ver_release)

# configure checks for the following file's existence to make sure that
# the directory that it is told contains the source code in fact does.
# Occasionally people accidentally specify the wrong directory with
# `--srcdir'; this is a safety check.
AC_CONFIG_SRCDIR(src/gigedit/main.cpp)

GETTEXT_PACKAGE=gigedit
AC_SUBST([GETTEXT_PACKAGE])
AC_DEFINE_UNQUOTED([GETTEXT_PACKAGE],["$GETTEXT_PACKAGE"],[Gettext package])

# the libgig header files need this
AC_C_BIGENDIAN

AC_PROG_CXX

IT_PROG_INTLTOOL(0.35.0)
AM_GLIB_GNU_GETTEXT

windows=no
mac=no
case $host in
    *mingw*|*cygwin*) windows=yes ;;
    *-*-darwin*) mac=yes ;;
esac
AM_CONDITIONAL(WINDOWS, test "$windows" = "yes")
AM_CONDITIONAL(MAC, test "$mac" = "yes")

# Note: even though Objective-C sources are just compiled for Mac, the
# following AC macros though must not be embedded into a shell check
# (if test "$mac" = "yes" ...), because those AC macros themselves are
# expanded before any shell code is executed, the generated configure
# code though would then not be executed and would lead to interesting
# libtool errors on non-Mac systems due to this.
AC_PROG_OBJC
# The OBJCXX macro didn't exist before autoconf 2.65, so ifdef it to
# avoid warnings on old systems.
m4_ifdef([AC_PROG_OBJCXX], [AC_PROG_OBJCXX])

m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

PKG_CHECK_EXISTS(gtk+-3.0 >= 2.99,
        [PKG_CHECK_MODULES([GTK], [gtk+-3.0])],
        [PKG_CHECK_MODULES([GTK], [gtk+-2.0])])

PKG_PROG_PKG_CONFIG
have_gtk3=no
PKG_CHECK_EXISTS(gtkmm-3.0 >= 2.99,
        [PKG_CHECK_MODULES(GTKMM, gtkmm-3.0, have_gtk3=yes)],
        [PKG_CHECK_MODULES(GTKMM, gtkmm-2.4 >= 2.8 gthread-2.0 cairomm-1.0)])
AM_CONDITIONAL(HAVE_GTK3, [test "$have_gtk3" = "yes"])

# Check for cairommconfig.h, as it was moved in cairomm 1.8.4. We only
# need it for newer versions.
gigedit_save_CPPFLAGS=$CPPFLAGS
CPPFLAGS="$GTKMM_CFLAGS $CPPFLAGS"
AC_CHECK_HEADERS([cairommconfig.h])
CPPFLAGS=$gigedit_save_CPPFLAGS

PKG_CHECK_MODULES(SIGC, sigc++-2.0)
AC_SUBST(SIGC_CFLAGS)
AC_SUBST(SIGC_LIBS)

PKG_CHECK_MODULES(GIG, gig >= 4.2.0)
AC_SUBST(GIG_CFLAGS)
AC_SUBST(GIG_LIBS)

# check for presence of libsndfile
PKG_CHECK_MODULES(SNDFILE, sndfile >= 1.0.11)
AC_SUBST(SNDFILE_CFLAGS)
AC_SUBST(SNDFILE_LIBS)

# check for (optional) presence of liblinuxsampler
liblinuxsampler_version="2.1.1"
PKG_CHECK_MODULES(
    LINUXSAMPLER, linuxsampler >= $liblinuxsampler_version,
    have_linuxsampler=1, have_linuxsampler=0
)
LINUXSAMPLER_PLUGIN_DIR=
if test "$have_linuxsampler" = "0"; then
    echo "Required liblinuxsampler version not found!"
    echo "You need to have liblinuxsampler version ${liblinuxsampler_version}"
    echo "installed. Support for on-the-fly editing with LinuxSampler will"
    echo "be disabled."
else
    echo "Found linuxsampler $liblinuxsampler_version"
    echo -n "Retrieving LinuxSampler's plugin dir... "
    LINUXSAMPLER_PLUGIN_DIR=`$PKG_CONFIG --variable plugindir linuxsampler`
    if test "$LINUXSAMPLER_PLUGIN_DIR" = ""; then
        have_linuxsampler=0
        echo "Error"
        echo "Could not retrieve LinuxSampler's plugin directory. Support"
        echo "for on-the-fly editing with LinuxSampler will be disabled."
    else
        echo "${LINUXSAMPLER_PLUGIN_DIR} "
        # convert absolute LS plugin dir into relative dir
        # (see ch 27.10 of the automake manual,
        #  "Installing to Hard-Coded Locations")
        # this one is extended to work with digit postfixed lib directories
        # (e.g. "/usr/lib64/linuxsampler") as well
        LINUXSAMPLER_PLUGIN_DIR=`echo "${LINUXSAMPLER_PLUGIN_DIR}" | sed 's/^.*\/lib[[0-9]]*\//\${libdir}\//g'`
        if echo "${LINUXSAMPLER_PLUGIN_DIR}" | grep "\${libdir}" > /dev/null; then
            echo "Relative plugin dir: ${LINUXSAMPLER_PLUGIN_DIR}"
        else
            echo "*********************************************************"
            echo "* ! WARNING ! : Could not resolve LinuxSampler's plugin"
            echo "* directory as relative path. This is probably not an"
            echo "* issue if you're just going to install gigedit by"
            echo "* 'make install', but it IS a problem if you're"
            echo "* installing to a certain destination directory and/or"
            echo "* compile in sandbox (e.g. Debian package or Gentoo emerge)"
            echo "*********************************************************"
        fi
    fi
fi
AC_SUBST(LINUXSAMPLER_CFLAGS)
AC_SUBST(LINUXSAMPLER_LIBS)
AC_SUBST(LINUXSAMPLER_PLUGIN_DIR)
AM_CONDITIONAL(HAVE_LINUXSAMPLER, test $have_linuxsampler = "1")
AC_DEFINE_UNQUOTED(
    HAVE_LINUXSAMPLER, $have_linuxsampler,
    [Define to 1 if you have LinuxSampler installed.]
)

have_ls_vmidi=0
if test $have_linuxsampler = "1"; then
    AC_MSG_CHECKING([whether LinuxSampler supports virtual MIDI devices])
    AC_LANG_PUSH([C++])
    LIBS="$LINUXSAMPLER_LIBS $LIBS"
    CFLAGS="$CFLAGS $LINUXSAMPLER_CFLAGS"
    CXXFLAGS="$CXXFLAGS $CFLAGS"
    AC_COMPILE_IFELSE([AC_LANG_PROGRAM([[
            #include <linuxsampler/drivers/midi/VirtualMidiDevice.h>
            using namespace LinuxSampler;
        ]], [[
            bool (VirtualMidiDevice::*ptr1)(uint8_t, uint8_t) = 0;
            bool (VirtualMidiDevice::*ptr2)() = 0;
            bool (VirtualMidiDevice::*ptr3)(uint8_t) = 0;
            uint8_t (VirtualMidiDevice::*ptr4)(uint8_t) = 0;
            ptr1 = &VirtualMidiDevice::SendNoteOnToSampler;
            ptr2 = &VirtualMidiDevice::NotesChanged;
            ptr3 = &VirtualMidiDevice::NoteChanged;
            ptr4 = &VirtualMidiDevice::NoteOffVelocity;
        ]])],[
            AC_MSG_RESULT(yes)
            have_ls_vmidi=1
        ],[
            AC_MSG_RESULT(no)
            echo "!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!"
            echo "! Support for the virtual MIDI keyboard in gigedit will"
            echo "! be disabled. You'll see the keyboard in gigedit, but"
            echo "! you won't be able to trigger notes with it nor see"
            echo "! active notes caused by external MIDI sources of LS."
            echo "! Update LinuxSampler and recompile gigedit if you want"
            echo "! this feature."
            echo "!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!"
    ])
    AC_LANG_POP([C++])
fi
AC_DEFINE_UNQUOTED(
    HAVE_LINUXSAMPLER_VIRTUAL_MIDI_DEVICE, $have_ls_vmidi,
    [Define to 1 if LinuxSampler supports virtual MIDI devices.]
)

AC_CONFIG_HEADERS(config.h)
AM_INIT_AUTOMAKE

AC_CONFIG_FILES([
	Makefile
	src/Makefile
	src/gigedit/Makefile
    src/gigedit/gfx/Makefile
	src/plugin/Makefile
	gfx/Makefile
	po/Makefile.in
	debian/Makefile
	doc/Makefile
	doc/quickstart/Makefile
	win32/libgigedit.dev
	win32/gigedit.dev
	win32/gigedit.nsi
	win32/Makefile
	gigedit.spec
])
AC_OUTPUT
