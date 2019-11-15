# gnubiff -- a mail notification program
# Copyright (C) 2000-2012 Nicolas Rougier, 2004-2016 Robert Sowada
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.
#
# Process this file with autoconf to produce a configure script.

######################################################################
#                           Initialization                           #
######################################################################

# gnubiff version numbering scheme:
#  gnubiff uses the  "major level", "minor level" & "patch level"
#  version numbering scheme
#
# - First number is the major number and it signifies major changes or
#   rewrites. 
# - The second number is the minor number and it represents added or
#    tweaked functionality on top of a largely coherent structure. 
# - The third number is the patch number and it usually will only
#    refer to releases fixing bugs
#
# Current version is 2.2.17

AC_PREREQ(2.59)
AC_INIT([gnubiff],[2.2.17],[gnubiff-bugs@lists.sourceforge.net])
AC_CONFIG_AUX_DIR(config)
AC_CONFIG_HEADERS([config/config.h])
AC_CONFIG_SRCDIR([src/gnubiff.cc])
AM_INIT_AUTOMAKE
AM_MAINTAINER_MODE

######################################################################
#                           Configure Options                        #
######################################################################
dnl syntaxt: AC_ARG_WITH (package, help-string, [action-if-given], [action-if-not-given])
dnl If the user gave configure the option `--with-package' or
dnl `--without-package', run shell commands action-if-given. If neither
dnl option was given, run shell commands action-if-not-given. The name
dnl package indicates another software package that this program should
dnl work with. It should consist only of alphanumeric characters and
dnl dashes.
AC_ARG_ENABLE(fam,
              [  --disable-fam           disable the use of FAM (autodetect)],
              OPT_USEFAM="$enableval", OPT_USEFAM="yes")
AC_ARG_ENABLE(gnome,
              [  --disable-gnome         disable the use of gnome (default: enable)],
              OPT_USEGNOME="$enableval", OPT_USEGNOME="yes")



######################################################################
#                         Checks for programs                        #
######################################################################
AC_PROG_CXX
AC_PROG_CC
AC_PROG_CPP
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET

######################################################################
#                         Checks for libraries                       #
######################################################################
dnl LIBPOPT (for parsing options)
AC_CHECK_LIB([popt],[main], ,
	AC_MSG_ERROR([
	Cannot find popt library
	Please consider installing it before installing gnubiff
	])
)

dnl From pkg.m4:
dnl # Note that if there is a possibility the first call to
dnl # PKG_CHECK_MODULES might not happen, you should be sure to
dnl # include an explicit call to PKG_PROG_PKG_CONFIG in your
dnl # configure.ac
PKG_PROG_PKG_CONFIG

dnl LIBFAM, LIBGAMIN (for monitoring files)
if test "x$OPT_USEFAM" = "xyes"; then
	AC_CHECK_LIB([fam], [main],
                 [FAM_LIBS="-lfam"
	              AC_DEFINE([HAVE_LIBFAM], [1], [libfam]) ])
	if test -z "$FAM_LIBS" ; then
		PKG_CHECK_MODULES(FAM, gamin >= 0.1.0)
	fi
	if test -z "$FAM_LIBS" ; then
		AC_MSG_ERROR([Cannot find FAM library])
	fi
fi
AC_SUBST(FAM_CFLAGS)
AC_SUBST(FAM_LIBS)

dnl LIBSSL (for network security)
AC_CHECK_LIB([ssl],[main])

dnl LIBCRYPTO, LIBSSL (for MD5 hash algorithm)
AC_CHECK_LIB(crypto, MD5_Init, [
	AC_DEFINE(HAVE_CRYPTO, 1, Define to 1 if you have crypto base functions)
	LIBS="$LIBS -lcrypto"], [
	AC_CHECK_LIB(ssl, MD5_init, AC_DEFINE(HAVE_CRYPTO, 1, Define to 1 if you have crypto base functions))])

dnl LIBSSL (for AES encryption/decryption)
AC_CHECK_LIB(ssl, AES_encrypt, AC_DEFINE_UNQUOTED(HAVE_AES, 1, 
			 Define to 1 if AES encryption is available), [
	AC_CHECK_LIB(crypto, AES_encrypt, AC_DEFINE_UNQUOTED(HAVE_AES, 1))])

dnl GLIB, GTK, ...
GTK_REQUIRED="gtk+-3.0 >= 3.0.0"
GMODULE_REQUIRED="gmodule-export-2.0 >= 2.4"
X11="xproto x11"
PKG_CHECK_MODULES(GNUBIFF_DEP, 
[
	$GTK_REQUIRED
	$GMODULE_REQUIRED
    $X11
])
AC_SUBST(GNUBIFF_DEP_CFLAGS)
AC_SUBST(GNUBIFF_DEP_LIBS)

######################################################################
#                     Checks for header files                        #
######################################################################
AC_HEADER_STDC
AC_HEADER_DIRENT
AC_CHECK_HEADERS([arpa/inet.h fcntl.h libintl.h netdb.h netinet/in.h stdlib.h string.h sys/socket.h unistd.h utime.h regex.h])
if test "x$OPT_USEFAM" = "xyes"; then
	AC_CHECK_HEADERS([fam.h], [],
		[AC_MSG_ERROR([Cannot find fam (File Alteration Monitor) library header file fam.h])])
fi


######################################################################
#   Checks for typedefs, structures, and compiler characteristics    #
######################################################################
AC_C_CONST



######################################################################
#                  Checks for library functions                      #
######################################################################
AC_FUNC_CLOSEDIR_VOID
AC_FUNC_MALLOC
AC_FUNC_STAT
AC_FUNC_UTIME_NULL
AC_CHECK_FUNCS([gethostbyname memset socket strchr strerror strrchr strstr utime bind_textdomain_codeset])



######################################################################
#                       Internationalization                         #
######################################################################
GETTEXT_PACKAGE=gnubiff
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE, "$GETTEXT_PACKAGE",
	               [The prefix for our gettext translation domains.])
AC_PROG_INTLTOOL
#AM_GLIB_GNU_GETTEXT
AM_GNU_GETTEXT([external])



######################################################################
#                           GNOME support                            #
######################################################################
if test "$OPT_USEGNOME" = "yes"; then
	PKG_CHECK_MODULES(GNOME_DEP, [
	    libpanel-applet
    	], [
		AC_SUBST(GNOME_DEP_CFLAGS)
		AC_SUBST(GNOME_DEP_LIBS)
		AH_TEMPLATE([USE_GNOME])
		AC_DEFINE(USE_GNOME)
		AC_PATH_PROG(GCONFTOOL, gconftool-2, no)
		])
	if test "x$GCONFTOOL" = "xno"; then
	   AC_MSG_ERROR([gconftool-2 executable not found in your path - should be installed with GConf])
	fi
fi
AM_CONDITIONAL(USE_GNOME, test $OPT_USEGNOME = yes, Define to 1 if you want to have GNOME support)


######################################################################
#                        Save password option                        #
######################################################################
AC_ARG_WITH(password,
[  --with-password         Save password within configuration file (UNSECURE)],
        password=$withval, password=no)
if test "$password" = yes; then
	AH_TEMPLATE([USE_PASSWORD])
	AC_DEFINE(USE_PASSWORD)

    AC_ARG_WITH(password-string,
    [  --with-password-string  String to use to encrypt password (HIGHLY RECOMMENDED)],
        pstring=$withval, pstring="")
	AH_TEMPLATE([PASSWORD_STRING])
    if test "x$pstring" = "x"; then
		AC_DEFINE_UNQUOTED(PASSWORD_STRING, "FEDCBA9876543210")
    else
		AC_DEFINE_UNQUOTED(PASSWORD_STRING, "$withval")
    fi

fi
AM_CONDITIONAL(USE_PASSWORD, test "$password" = yes)
AM_CONDITIONAL(PASSWORD_STRING, test "$password" = yes)



######################################################################
#                           expert tab default                       #
######################################################################
AC_ARG_ENABLE(expert,
[  --disable-expert        disable showing expert tab as default, [default=yes]],
	AC_DEFINE(EXPERT_SHOW_NO_TAB, 1, [Define to 1 to disable showing expert tab as default.])
	expert="$enableval", expert="yes")



######################################################################
#                           debug support                            #
######################################################################
AC_ARG_ENABLE(debug,
		[  --enable-debug          turn on debugging [default=no]],
AC_DEFINE(DEBUG, 1, [Define to 1 to enable debugging code.]),)

AC_CHECK_FILE("CVS",
			  [AC_DEFINE(IS_CVS_VERSION, 1, [Is a CVS version being used?])],
			  [AC_DEFINE(IS_CVS_VERSION, 0, [Is a CVS version being used?])])



##################
# configure output
##################
AC_CONFIG_FILES([
Makefile
src/Makefile
po/Makefile.in
ui/Makefile
art/Makefile
sound/Makefile
doc/Makefile
man1/Makefile
config/gnubiff.spec
])
AC_OUTPUT
dnl file permissions in config subdirectory
chmod +x config/mkinstalldirs config/ltmain.sh config/depcomp config/missing config/config.guess config/config.sub config/install-sh config/mdate-sh


echo "--------------------------------------------------------------------------------"

if test "$password" = yes; then
	echo " Password saving : yes"
	echo " Password string : $pstring"
	if test "x$pstring" = "x"; then
		echo "  WARNING: You've not defined a string to encrypt passwords (this can be done"
		echo "           (with the option --with-password-string). The default string will"
		echo "           be used but it is less secure than using your own."
	fi
fi

if test "$password" = no; then
echo " Password saving : no"
echo "  If you want gnubiff to save password within configuration file, use"
echo "  ./configure --with-password [--with-password-string=\"any string you like...]\"."
echo "  But be careful, it is highly unsecure, you've been warned!"
fi

echo " FAM support     : $OPT_USEFAM"

echo " Gnome support   : $OPT_USEGNOME"
#if test "$OPT_USEGNOME" = "yes"; then
#  if test "$prefix" != "`$PKG_CONFIG --variable=libpanel_applet_dir libpanelapplet-4.0`"; then
#    echo "  NOTE: The installation directory for gnubiff is currently set to"
#    echo "        \"$prefix\","
#    echo "        the default installation directory for gnome panel applications is"
#    echo "        \""`pkg-config libpanelapplet-2.0 --variable=prefix`"\"."
#    echo "        It may be necessary to add the path"
#    echo "        \"$prefix/lib/bonobo/servers/\""
#    echo "        to the file \"/etc/bonobo-activation/bonobo-activation-config.xml\""
#    echo "        (root privileges needed) or to execute"
#    echo "        \"activation-client --add-path=$prefix/lib/bonobo/servers/\""
#    echo "        (no root privileges needed) before gnubiff can be added to the panel."
#  fi
#fi

echo " Expert tab      : $expert"

echo ""
echo " Just type 'make' and then 'make install' to install gnubiff"
echo "--------------------------------------------------------------------------------"
echo ""
