#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.56)
AC_INIT([nordugrid-arc],m4_normalize(m4_include(VERSION)),[http://bugzilla.nordugrid.org/])

dnl serial-tests is not recognized before 1.12, and required after 1.13
m4_define([serial_tests], [
    m4_esyscmd([case `${AUTOMAKE:-automake} --version | head -n 1` in
      *1.11.*|*1.10.*|*1.9.*);;
      *) echo serial-tests;;
      esac])
])

AM_INIT_AUTOMAKE([foreign 1.9 tar-pax] serial_tests)
AC_CONFIG_SRCDIR([Makefile.am])
AC_CONFIG_HEADERS([config.h])

baseversion=`echo $VERSION | sed 's/[[^0-9.]].*//'`
preversion=`echo $VERSION | sed 's/^[[0-9.]]*//'`

if test "x$baseversion" = "x" ; then
   baseversion=$VERSION
   preversion=""
fi

if test "x$preversion" = "x" ; then
   fedorarelease="1"
   fedorasetupopts="-q"
   debianversion="$baseversion"
else
   fedorarelease="0.$preversion"
   fedorasetupopts="-q -n %{name}-%{version}$preversion"
   debianversion="$baseversion~$preversion"
fi

# numeric ARC_VERSION_* used for API fall back to current release seriese (e.g. when 'master' is specified in VESRION file, the "6.0.0" will be used)
ARC_VERSION_MAJOR=`echo $VERSION | awk -F. '{print match($1, /^[[0-9]]+$/) ? $1 : "6"}'`
ARC_VERSION_MINOR=`echo $VERSION | awk -F. '{print match($2, /[[^ ]]/) ? $2 : "0"}'`
ARC_VERSION_PATCH=`echo $VERSION | awk -F. '{print match($3, /[[^ ]]/) ? $3 : "0"}'`
ARC_VERSION_NUM=`printf "0x%02x%02x%02x" $ARC_VERSION_MAJOR $ARC_VERSION_MINOR $ARC_VERSION_PATCH`
ARC_VERSION=`echo $ARC_VERSION_MAJOR.$ARC_VERSION_MINOR.$ARC_VERSION_PATCH`

AC_SUBST(baseversion)
AC_SUBST(preversion)
AC_SUBST(fedorarelease)
AC_SUBST(fedorasetupopts)
AC_SUBST(debianversion)
AC_SUBST(ARC_VERSION_MAJOR)
AC_SUBST(ARC_VERSION_MINOR)
AC_SUBST(ARC_VERSION_PATCH)
AC_SUBST(ARC_VERSION_NUM)
AC_SUBST(ARC_VERSION)

# This macro was introduced in autoconf 2.57g? but we currently only require 2.56
m4_ifdef([AC_CONFIG_MACRO_DIR], [AC_CONFIG_MACRO_DIR([m4])])

m4_pattern_allow([AC_PATH_PROG])
m4_pattern_allow([AC_MSG_WARN])

AC_PROG_CXX
AC_PROG_CC_STDC
AC_PROG_CPP
AC_GNU_SOURCE
AC_PROG_AWK
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_DISABLE_STATIC
AM_PROG_LIBTOOL

AC_PATH_PROG(PERL, perl, /usr/bin/perl, :)

# EL-5 compatibility.  $(mkdir_p) is now obsolete.
test -n "$MKDIR_P" || MKDIR_P="$mkdir_p"
AC_SUBST([MKDIR_P])

# Use arc for "pkgdir" instead of nordugrid-arc (@PACKAGE@)
pkgdatadir='${datadir}/arc'
pkgincludedir='${includedir}/arc'
pkglibdir='${libdir}/arc'
extpkglibdir='${libdir}/arc/external'
pkglibexecdir='${libexecdir}/arc'

AC_SUBST(pkgdatadir)
AC_SUBST(pkgincludedir)
AC_SUBST(pkglibdir)
AC_SUBST(extpkglibdir)
AC_SUBST(pkglibexecdir)

ARC_API
ARC_RELATIVE_PATHS

AC_ARG_WITH(systemd-units-location,
  AC_HELP_STRING([--with-systemd-units-location=<PATH>], [Location of the systemd unit files. [[None]]]),
  [ unitsdir="$withval" ],
  [ unitsdir= ]
)
AC_MSG_RESULT($unitsdir)
AC_SUBST(unitsdir)

AM_CONDITIONAL([SYSTEMD_UNITS_ENABLED],[test "x$unitsdir" != "x"])

AC_ARG_WITH(sysv-scripts-location,
  AC_HELP_STRING([--with-sysv-scripts-location=<PATH>], [Location of the SYSV init scripts. [[autodetect]]]),
  [
    initddirauto="no"
    initddir="$withval"
  ],
  [
    initddirauto="yes"
    initddir=
    case "${host}" in
      *linux* | *kfreebsd* | *gnu* )
        for i in init.d rc.d/init.d rc.d; do
          if test -d "/etc/$i" -a ! -h "/etc/$i" ; then
            initddir="$sysconfdir/$i"
            break
          fi
        done

        if test -z "$initddir"; then
          AC_MSG_WARN(could not find a suitable location for the SYSV init scripts - not installing)
        fi
        ;;
    esac
  ]
)
AC_MSG_RESULT($initddir)
AC_SUBST(initddir)

AM_CONDITIONAL([SYSV_SCRIPTS_ENABLED],[ ( test "x$initddirauto" == "xno" || test "x$unitsdir" = "x" ) && test "x$initddir" != "x"])

AC_ARG_WITH(cron-scripts-prefix,
  AC_HELP_STRING([--with-cron-scripts-prefix=<PATH>], [Specify the location of the cron directory. [[SYSCONFDIR/cron.d]]]),
  [ cronddir="$withval" ],
  [ cronddir="$sysconfdir/cron.d" ]
)
AC_SUBST(cronddir)

# gettext
AM_GNU_GETTEXT([external])
AM_GNU_GETTEXT_VERSION([0.17])
[[ -r $srcdir/po/POTFILES.in ]] || touch $srcdir/po/POTFILES.in

# Portable 64bit file offsets
AC_SYS_LARGEFILE

# pkg-config needed for many checks
AC_PATH_TOOL(PKG_CONFIG, pkg-config, no)
if test "x$PKG_CONFIG" = "xno"; then
        AC_MSG_ERROR([ *** pkg-config not found])
else
        pkgconfigdir=${libdir}/pkgconfig
        AC_SUBST(pkgconfigdir)
fi

# Default enable/disable switches
#  Features
enables_ldap=yes
enables_mysql=no
enables_systemd=no
enables_swig_python=yes
# Features directly related to components
enables_cppunit=yes
enables_python=yes
enables_altpython=yes
enables_pylint=yes
enables_mock_dmc=no
enables_gfal=no
enables_s3=no
enables_xrootd=yes
enables_argus=no
enables_xmlsec1=yes
enables_dbjstore=yes
enables_sqlitejstore=yes
enables_ldns=yes
#  Libraries and plugins
# Currently no fine-grained choice is supported.
# Also this variable is used to check if source
# build is needed at all because no component can
# be built without HED.
enables_hed=yes
#  Services
enables_a_rex_service=yes
enables_internal=no
enables_gridftpd_service=yes
enables_ldap_service=yes
enables_candypond=yes
enables_datadelivery_service=yes
enables_monitor=yes
#  Clients
enables_compute_client=yes
enables_credentials_client=yes
enables_data_client=yes
enables_jura_client=yes
enables_emies_client=yes
enables_arcrest_client=yes
#  Documentation
enables_doc=yes
# ACIX cache index
enables_acix=yes

# Handle group enable/disable switches
AC_ARG_ENABLE(all, AC_HELP_STRING([--disable-all], [disables all buildable components. Can be overwritten with --enable-* for group or specific component. It is also possible to use --enable-all to overwrite defaults for most of components.]),
[
enables_a_rex_service=$enableval
enables_internal=$enableval
enables_gridftpd_service=$enableval
enables_ldap_service=$enableval
enables_monitor=$enableval
enables_candypond=$enableval
enables_datadelivery_service=$enableval
enables_compute_client=$enableval
enables_credentials_client=$enableval
enables_echo_client=$enableval
enables_data_client=$enableval
enables_jura_client=$enableval
enables_emies_client=$enableval
enables_arcrest_client=$enableval
enables_hed=$enableval
enables_python=$enableval
enables_altpython=$enableval
enables_pylint=$enableval
enables_mock_dmc=$enableval
enables_gfal=$enableval
enables_s3=$enableval
enables_xrootd=$enableval
enables_xmlsec1=$enableval
enables_argus=$enableval
enables_cppunit=$enableval
enables_doc=$enableval
enables_acix=$enableval
enables_dbjstore=$enableval
enables_ldns=$enableval
enables_sqlitejstore=$enableval
],
[])

AC_ARG_ENABLE(all-clients, AC_HELP_STRING([--disable-all-clients], [disables all buildable client components. Can be overwritten with --enable-* for specific component. It is also possible to use --enable-all-clients to overwrite defaults and --enable-all.]),
[
enables_compute_client=$enableval
enables_credentials_client=$enableval
enables_echo_client=$enableval
enables_data_client=$enableval
enables_jura_client=$enableval
enables_emies_client=$enableval
enables_arcrest_client=$enableval
enables_doc=$enableval
],
[])

AC_ARG_ENABLE(all-data-clients, AC_HELP_STRING([--disable-all-data-clients], [disables all buildable client components providing data handling abilities. Can be overwritten with --enable-* for specific component. It is also possible to use --enable-all-data-clients to overwrite defaults, --enable-all and --enable-all-clients.]),
[
enables_data_client=$enableval
],
[])

AC_ARG_ENABLE(all-services, AC_HELP_STRING([--disable-all-services], [disables all buildable service componets. Can be overwritten with --enable-* for specific component. It is also possible to use --enable-all-services to overwrite defaults and --enable-all.]),
[
enables_a_rex_service=$enableval
enables_gridftpd_service=$enableval
enables_ldap_service=$enableval
enables_monitor=$enableval
enables_candypond=$enableval
enables_datadelivery_service=$enableval
enables_acix=$enableval
],
[])


# Be pedantic about compiler warnings.
AC_ARG_ENABLE(pedantic-compile, AC_HELP_STRING([--enable-pedantic-compile], [add pedantic compiler flags]),
[enables_pedantic_compile="yes"], [enables_pedantic_compile="no"])
if test "x$enables_pedantic_compile" = "xyes"; then
  # This check need to be enhanced. It won't work in case of cross-compilation
  # and if path to compiler is explicitly specified.
  if test x"$CXX" = x"g++"; then
    # GNU C/C++ flags
    AM_CXXFLAGS="-Wall -Wextra -Werror -Wno-sign-compare -Wno-unused"
    SAVE_CPPFLAGS=$CPPFLAGS
    AC_LANG_SAVE
    AC_LANG_CPLUSPLUS
    CPPFLAGS="$CPPFLAGS -Wno-unused-result"
    AC_TRY_COMPILE([],[], [
        AM_CXXFLAGS="$AM_CXXFLAGS -Wno-unused-result"
      ], [
        AC_MSG_NOTICE([compilation flag -Wno-unused-result is not supported])
      ]
    )
    AC_LANG_RESTORE
    CPPFLAGS=$SAVE_CPPFLAGS
  else
    # TODO: set generic flags for generic compiler
    AM_CXXFLAGS=""
  fi
  AC_SUBST(AM_CXXFLAGS)
fi
AM_CONDITIONAL([PEDANTIC_COMPILE], [test "x$enables_pedantic_compile" = "xyes"])


# Enable/disable switches for third-party.

#  Swig
AC_ARG_ENABLE(swig-python, AC_HELP_STRING([--disable-swig-python], [disable SWIG python bindings]),
[enables_swig_python=$enableval],[])
AC_ARG_ENABLE(swig, AC_HELP_STRING([--disable-swig], [disable all bindings through SWIG]),
[enables_swig_python=$enableval],[])
if test "$enables_swig_python" = "yes"; then
  AC_PATH_PROGS(SWIG, swig)
  if test "x$SWIG" = "x"; then
    enables_swig="no"
  else
    swigver=`$SWIG -version 2>&1 | grep Version | sed 's/.* //'`
    swigver1=`echo $swigver | cut -d. -f1`
    swigver2=`echo $swigver | cut -d. -f2`
    swigver3=`echo $swigver | cut -d. -f3`
    if test $swigver1 -lt 1 || ( test $swigver1 -eq 1 && ( \
       test $swigver2 -lt 3 || ( test $swigver2 -eq 3 && ( \
       test $swigver3 -lt 25 ) ) ) ) ; then
      AC_MSG_NOTICE([swig is too old (< 1.3.25)])
      SWIG=""
      enables_swig="no"
    elif test $swigver1 -eq 1 && test $swigver2 -eq 3 && test $swigver3 -eq 38 ; then
      AC_MSG_NOTICE([swig version 1.3.38 has bug which prevents it from being used for this software. Please upgrade or downgrade.])
      SWIG=""
      enables_swig="no"
    else
      SWIG2="no"
      if test $swigver1 -ge 2
      then
        SWIG2="yes"
      fi
      AC_SUBST(SWIG2)
      SWIG_PYTHON_NAMING="SwigPy"
      # In SWIG version 1.3.37 naming was changed from "PySwig" to "SwigPy".
      if test $swigver1 -lt 1 || ( test $swigver1 -eq 1 && ( \
         test $swigver2 -lt 3 || ( test $swigver2 -eq 3 && ( \
         test $swigver3 -lt 37 ) ) ) ) ; then
        SWIG_PYTHON_NAMING="PySwig"
      fi
      AC_SUBST(SWIG_PYTHON_NAMING)
    fi
  fi
else
  SWIG=""
fi
AM_CONDITIONAL([SWIG_ENABLED],[test "x$enables_swig" = "xyes"])

AC_ARG_ENABLE(hed, AC_HELP_STRING([--disable-hed], [disable building HED libraries and plugins. Do not do that unless You do not want to build anything. Even in that case better use --disable-all.]),
[enables_hed=$enableval],[])

# Python
if test "$enables_hed" = "yes"; then
AC_ARG_ENABLE(python,
  AC_HELP_STRING([--disable-python], [disable Python components]),
  [enables_python=$enableval
   enables_swig_python=$enableval], [])

if test "$enables_python" = "yes"; then
  AC_ARG_WITH(python, AC_HELP_STRING([--with-python=(PYTHON)],
    [specify python program from PATH]))

  # We do not look for python binary when cross-compiling
  # but we need to make the variable non-empty
  if test "${build}" = "${host}"; then
    AC_PATH_PROGS(PYTHON, $with_python python)
  else
    PYTHON=/usr/bin/python
  fi

  if test "X$PYTHON" != "X"; then
    PYNAME=`basename $PYTHON`
    PKG_CHECK_MODULES(PYTHON, $PYNAME-embed, [
    PYTHON_VERSION=`$PKG_CONFIG --modversion $PYNAME-embed`
    PYTHON_MAJOR=`echo $PYTHON_VERSION|cut -f1 -d.`
    ],[
    PKG_CHECK_MODULES(PYTHON, $PYNAME, [
    PYTHON_VERSION=`$PKG_CONFIG --modversion $PYNAME`
    PYTHON_MAJOR=`echo $PYTHON_VERSION|cut -f1 -d.`
    ],[
    PYNAME=python-`$PYTHON -c 'import sys; print(sys.version[[:3]])'`
    PKG_CHECK_MODULES(PYTHON, $PYNAME-embed, [
    PYTHON_VERSION=`$PKG_CONFIG --modversion $PYNAME-embed`
    PYTHON_MAJOR=`echo $PYTHON_VERSION|cut -f1 -d.`
    ],[
    PKG_CHECK_MODULES(PYTHON, $PYNAME, [
    PYTHON_VERSION=`$PKG_CONFIG --modversion $PYNAME`
    PYTHON_MAJOR=`echo $PYTHON_VERSION|cut -f1 -d.`
    ],[
    PYTHON_VERSION=`$PYTHON -c 'import sys; print(sys.version[[:3]])'`
    PYTHON_MAJOR=`$PYTHON -c 'import sys; print(sys.version_info[[0]])'`
    PYTHON_CFLAGS=-I`$PYTHON -c 'from distutils import sysconfig; print(sysconfig.get_python_inc())'`
    PY_LIBS=`$PYTHON -c "from distutils import sysconfig; print(sysconfig.get_config_vars().get('LIBS'))" | sed s/None//`
    PY_SYSLIBS=`$PYTHON -c "from distutils import sysconfig; print(sysconfig.get_config_vars().get('SYSLIBS'))" | sed s/None//`
    PY_LIBDEST=`$PYTHON -c "from distutils import sysconfig; print(sysconfig.get_config_vars().get('LIBDEST'))" | sed s/None//`
    PYTHON_LIBS="$PY_LIBS $PY_SYSLIBS"
    SAVE_LDFLAGS=$LDFLAGS
    LDFLAGS="$PYTHON_LIBS $LDFLAGS"
    AC_CHECK_LIB([python$PYTHON_VERSION], [Py_Initialize],[
        AC_MSG_NOTICE([No additional path to python library needed])
        PYTHON_LIBS="-lpython$PYTHON_VERSION $PYTHON_LIBS"],[
        LDFLAGS="-L$PY_LIBDEST/config $LDFLAGS"
        # check a different symbol or else configure will used cached value
        AC_CHECK_LIB([python$PYTHON_VERSION], [Py_Finalize],[
            AC_MSG_NOTICE([Adding path to python library])
            PYTHON_LIBS="-L$PY_LIBDEST/config -lpython$PYTHON_VERSION $PYTHON_LIBS"],[
            PYTHON_LIBS=""])])
    LDFLAGS=$SAVE_LDFLAGS
    ])])])])
    AC_SUBST(PYTHON_VERSION)
    AC_SUBST(PYTHON_CFLAGS)
    AC_SUBST(PYTHON_LIBS)

    if test "${build}" = "${host}"; then
        PYTHON_SOABI=`$PYTHON -c "from distutils import sysconfig; print(sysconfig.get_config_vars().get('SOABI'))" | sed s/None//`
    else
        PYTHON_SOABI=""
    fi
    AC_SUBST(PYTHON_SOABI)

    AC_ARG_WITH(python-site-arch, AC_HELP_STRING([--with-python-site-arch=directory], [Direcory where Python modules will be installed - defaults is to query the Python binary]))
    if test "X$PYTHON_SITE_ARCH" = "X"; then
      if test "${build}" = "${host}"; then
        PYTHON_SITE_ARCH=`$PYTHON -c 'from distutils import sysconfig; print(sysconfig.get_python_lib(1,0,"${prefix}"))'`
      else
        PYTHON_SITE_ARCH="${libdir}/python${PYTHON_VERSION}/site-packages"
      fi
    fi
    AC_SUBST(PYTHON_SITE_ARCH)

    AC_ARG_WITH(python-site-lib, AC_HELP_STRING([--with-python-site-lib=directory], [Direcory where Python modules will be installed - defaults is to query the Python binary]))
    if test "X$PYTHON_SITE_LIB" = "X"; then
      if test "${build}" = "${host}"; then
        PYTHON_SITE_LIB=`$PYTHON -c 'from distutils import sysconfig; print(sysconfig.get_python_lib(0,0,"${prefix}"))'`
      else
        PYTHON_SITE_LIB="${libdir}/python${PYTHON_VERSION}/site-packages"
      fi
    fi
    AC_SUBST(PYTHON_SITE_LIB)

    SAVE_LDFLAGS=$LDFLAGS
    SAVE_CPPFLAGS=$CPPFLAGS
    LDFLAGS="$LDFLAGS $PYTHON_LIBS"
    CPPFLAGS="$CPPFLAGS $PYTHON_CFLAGS"

    AC_CHECK_HEADER(Python.h, [pythonh="yes"], [pythonh="no"])

    AC_TRY_COMPILE([#include <Python.h>], [Py_InitializeEx(0)],[
        AC_MSG_NOTICE([Python includes functionality of skipping initialization registration of signal handlers])
        AC_DEFINE(HAVE_PYTHON_INITIALIZE_EX, 1,
          [Define if you have Py_InitializeEx function])
        enables_python_service="yes"
    ],[
        AC_MSG_NOTICE([Python does not include functionality of skipping initialization registration of signal handlers, since its version is below 2.4])
        enables_python_service="no"
    ])

    LDFLAGS=$SAVE_LDFLAGS
    CPPFLAGS=$SAVE_CPPFLAGS
  fi

  if test "X$PYTHON" = "X"; then
    AC_MSG_NOTICE([Missing Python - skipping Python components])
    enables_python=no
  elif test "X$PYTHON_SITE_ARCH" = "X" || test "X$PYTHON_SITE_LIB" = "X"; then
    AC_MSG_NOTICE([Missing python site packages location - skipping Python components])
    enables_python=no
  else
    AC_MSG_NOTICE([Python available: $PYTHON_VERSION])
  fi

  if test "x$enables_python" != "xyes"; then
    AC_MSG_NOTICE([Missing Python - skipping Python bindings])
    enables_swig_python=no
  elif test "X$PYTHON_LIBS" = "X"; then
    AC_MSG_NOTICE([Missing Python library - skipping Python bindings])
    enables_swig_python=no
  elif test "X$pythonh" != "Xyes"; then
    AC_MSG_NOTICE([Missing Python header - skipping Python bindings])
    enables_swig_python=no
  elif ! test -f python/arc_wrap.cpp && test "x$enables_swig_python" != "xyes"; then
    AC_MSG_NOTICE([Missing pre-compiled Python wrapper and SWIG - skipping Python bindings])
    enables_swig_python=no
  fi

fi
fi

AC_MSG_NOTICE([Python enabled: $enables_python])
AC_MSG_NOTICE([Python SWIG bindings enabled: $enables_swig_python])

AM_CONDITIONAL([PYTHON_ENABLED],[test "x$enables_python" = "xyes"])
AM_CONDITIONAL([PYTHON3], [test "x$enables_python" = "xyes" && test "x$PYTHON_MAJOR" = "x3"])
AM_CONDITIONAL([PYTHON_SWIG_ENABLED],[test "x$enables_swig_python" = "xyes"])
AM_CONDITIONAL([PYTHON_SERVICE],[test "x$enables_swig_python" = "xyes" &&
                                 test "x$enables_python_service" = "xyes"])

# Alternative Python
if test "$enables_hed" = "yes"; then
AC_ARG_ENABLE(altpython,
  AC_HELP_STRING([--disable-altpython], [enable alternative Python binding]),
  [enables_altpython=$enableval], [])

if test "$enables_altpython" = "yes"; then
  AC_ARG_WITH(altpython, AC_HELP_STRING([--with-altpython=(PYTHON)],
    [specify alternative python program from PATH]))

  AC_PATH_PROGS(ALTPYTHON, $with_altpython)

  if test "X$ALTPYTHON" != "X"; then
    ALTPYNAME=`basename $ALTPYTHON`
    PKG_CHECK_MODULES(ALTPYTHON, $ALTPYNAME-embed, [
    ALTPYTHON_VERSION=`$PKG_CONFIG --modversion $ALTPYNAME-embed`
    ALTPYTHON_MAJOR=`echo $ALTPYTHON_VERSION|cut -f1 -d.`
    ],[
    PKG_CHECK_MODULES(ALTPYTHON, $ALTPYNAME, [
    ALTPYTHON_VERSION=`$PKG_CONFIG --modversion $ALTPYNAME`
    ALTPYTHON_MAJOR=`echo $ALTPYTHON_VERSION|cut -f1 -d.`
    ],[
    ALTPYNAME=python-`$ALTPYTHON -c 'import sys; print(sys.version[[:3]])'`
    PKG_CHECK_MODULES(ALTPYTHON, $ALTPYNAME-embed, [
    ALTPYTHON_VERSION=`$PKG_CONFIG --modversion $ALTPYNAME-embed`
    ALTPYTHON_MAJOR=`echo $ALTPYTHON_VERSION|cut -f1 -d.`
    ],[
    PKG_CHECK_MODULES(ALTPYTHON, $ALTPYNAME, [
    ALTPYTHON_VERSION=`$PKG_CONFIG --modversion $ALTPYNAME`
    ALTPYTHON_MAJOR=`echo $ALTPYTHON_VERSION|cut -f1 -d.`
    ],[
    ALTPYTHON_VERSION=`$ALTPYTHON -c 'import sys; print(sys.version[[:3]])'`
    ALTPYTHON_MAJOR=`$ALTPYTHON -c 'import sys; print(sys.version_info[[0]])'`
    ALTPYTHON_CFLAGS=-I`$ALTPYTHON -c 'from distutils import sysconfig; print(sysconfig.get_python_inc())'`
    ALTPY_LIBS=`$ALTPYTHON -c "from distutils import sysconfig; print(sysconfig.get_config_vars().get('LIBS'))" | sed s/None//`
    ALTPY_SYSLIBS=`$ALTPYTHON -c "from distutils import sysconfig; print(sysconfig.get_config_vars().get('SYSLIBS'))" | sed s/None//`
    ALTPY_LIBDEST=`$ALTPYTHON -c "from distutils import sysconfig; print(sysconfig.get_config_vars().get('LIBDEST'))" | sed s/None//`
    ALTPYTHON_LIBS="$ALTPY_LIBS $ALTPY_SYSLIBS"
    SAVE_LDFLAGS=$LDFLAGS
    LDFLAGS="$ALTPYTHON_LIBS $LDFLAGS"
    AC_CHECK_LIB([python$ALTPYTHON_VERSION], [Py_Initialize],[
        AC_MSG_NOTICE([No additional path to python library needed])
        ALTPYTHON_LIBS="-lpython$ALTPYTHON_VERSION $ALTPYTHON_LIBS"],[
        LDFLAGS="-L$ALTPY_LIBDEST/config $LDFLAGS"
        # check a different symbol or else configure will used cached value
        AC_CHECK_LIB([python$ALTPYTHON_VERSION], [Py_Finalize],[
            AC_MSG_NOTICE([Adding path to python library])
            ALTPYTHON_LIBS="-L$ALTPY_LIBDEST/config -lpython$ALTPYTHON_VERSION $ALTPYTHON_LIBS"],[
            ALTPYTHON_LIBS=""])])
    LDFLAGS=$SAVE_LDFLAGS
    ])])])])
    AC_SUBST(ALTPYTHON_VERSION)
    AC_SUBST(ALTPYTHON_CFLAGS)
    AC_SUBST(ALTPYTHON_LIBS)

    ALTPYTHON_SOABI=`$ALTPYTHON -c "from distutils import sysconfig; print(sysconfig.get_config_vars().get('SOABI'))" | sed s/None//`
    AC_SUBST(ALTPYTHON_SOABI)

    AC_ARG_WITH(altpython-site-arch, AC_HELP_STRING([--with-altpython-site-arch=directory], [Direcory where Python modules will be installed - defaults is to query the Python binary]))
    if test "X$ALTPYTHON_SITE_ARCH" = "X"; then
      ALTPYTHON_SITE_ARCH=`$ALTPYTHON -c 'from distutils import sysconfig; print(sysconfig.get_python_lib(1,0,"${prefix}"))'`
    fi
    AC_SUBST(ALTPYTHON_SITE_ARCH)

    AC_ARG_WITH(altpython-site-lib, AC_HELP_STRING([--with-altpython-site-lib=directory], [Direcory where Python modules will be installed - defaults is to query the Python binary]))
    if test "X$ALTPYTHON_SITE_LIB" = "X"; then
      ALTPYTHON_SITE_LIB=`$ALTPYTHON -c 'from distutils import sysconfig; print(sysconfig.get_python_lib(0,0,"${prefix}"))'`
    fi
    AC_SUBST(ALTPYTHON_SITE_LIB)

    SAVE_LDFLAGS=$LDFLAGS
    SAVE_CPPFLAGS=$CPPFLAGS
    LDFLAGS="$LDFLAGS $ALTPYTHON_LIBS"
    CPPFLAGS="$CPPFLAGS $ALTPYTHON_CFLAGS"

    AC_CHECK_HEADER(Python.h, [altpythonh="yes"], [altpythonh="no"])

    LDFLAGS=$SAVE_LDFLAGS
    CPPFLAGS=$SAVE_CPPFLAGS
  fi

  if test "X$ALTPYTHON" = "X"; then
    AC_MSG_NOTICE([Missing alternative Python - skipping alternative Python])
    enables_altpython=no
  elif test "X$ALTPYTHON_LIBS" = "X"; then
    AC_MSG_NOTICE([Missing alternative Python library - skipping alternative Python bindings])
    enables_altpython=no
  elif test "X$altpythonh" != "Xyes"; then
    AC_MSG_NOTICE([Missing alternative Python header - skipping alternative Python bindings])
    enables_altpython=no

  elif test "X$ALTPYTHON_SITE_ARCH" = "X" || test "X$ALTPYTHON_SITE_LIB" = "X"; then
    AC_MSG_NOTICE([Missing python site packages location - skipping Python bindings])
    enables_altpython=no
  else
    AC_MSG_NOTICE([Alternative Python available: $ALTPYTHON_VERSION])
  fi

  if test "x$enables_altpython" != "xyes"; then
    AC_MSG_NOTICE([Missing alternative Python - skipping alternative Python bindings])
    enables_altpython=no
  elif ! test -f python/arc_wrap.cpp && test "x$enables_swig_python" != "xyes"; then
    AC_MSG_NOTICE([Missing pre-compiled Python wrapper and SWIG - skipping alternative Python bindings])
    enables_altpython=no
  fi

fi
fi

AC_MSG_NOTICE([Alternative Python enabled: $enables_altpython])

AM_CONDITIONAL([ALTPYTHON_ENABLED],[test "x$enables_altpython" = "xyes"])
AM_CONDITIONAL([ALTPYTHON3], [test "x$enables_altpython" = "xyes" && test "x$ALTPYTHON_MAJOR" = "x3"])


# check for pylint
dnl Check if pylint is explicitly disabled.
if test "$enables_hed" = "yes"; then
AC_ARG_ENABLE(pylint, AC_HELP_STRING([--disable-pylint], [disable python example checking using pylint]),
[enables_pylint=$enableval],[])
  AC_PATH_PROGS(PYLINT, pylint)
  if test "x$PYLINT" = "x"; then
    enables_pylint="no"
  else
    PYLINT_VERSION=`$PYLINT --version 2> /dev/null | sed -n 's/^pylint \([[0-9.]]*\).*/\1/p'`
    # Check if pylint supports the following arguments, otherwise disable pylint (python example checking).
    # Do not generate report
    # Disable convention and recommendation messages - we are only interested in fatals, errors and warnings.
    PYLINT_ARGS="--reports=no --disable=C,R"
    if $PYLINT $PYLINT_ARGS /dev/null > /dev/null 2>&1 ; then
       AC_MSG_NOTICE([pylint version $PYLINT_VERSION found - version ok])
       enables_pylint="yes"
    else
       AC_MSG_NOTICE([pylint version $PYLINT_VERSION found - bad version])
       enables_pylint="no"
       PYLINT_ARGS=""
    fi
    AC_SUBST(PYLINT_ARGS)
  fi

  # Check if the --disable=W0221 option is supported
  # W0221: Disable arguments differ messages since Swig uses tuple syntax (*args).
  if test "$enables_pylint" = "yes"; then
    PYLINT_ARGS_ARGUMENTS_DIFFER="--disable=W0221"
    if ! $PYLINT $PYLINT_ARGS $PYLINT_ARGS_ARGUMENTS_DIFFER /dev/null > /dev/null 2>&1 ; then
      PYLINT_ARGS_ARGUMENTS_DIFFER=""
    fi
    AC_SUBST(PYLINT_ARGS_ARGUMENTS_DIFFER)
  fi
fi
AM_CONDITIONAL([PYLINT_ENABLED], [test "x$enables_pylint" = "xyes"])
AC_MSG_NOTICE([Python example checking with pylint enabled: $enables_pylint])

# check systemd daemon integration
AC_ARG_ENABLE(systemd, AC_HELP_STRING([--enable-systemd], [enable use of the systemd daemon integration features]),[enables_systemd="$enableval"],[])
if test "x$enables_systemd" = "xyes"; then
systemd_daemon_save_LIBS=$LIBS
LIBS=
AC_SEARCH_LIBS(sd_listen_fds,[systemd systemd-daemon],
  [have_sd_listen_fds=yes],[have_sd_listen_fds=no],$systemd_daemon_save_LIBS)
AC_SEARCH_LIBS(sd_notify,[systemd systemd-daemon],
  [have_sd_notify=yes],[have_sd_notify=no],$systemd_daemon_save_LIBS)
AC_CHECK_HEADERS(systemd/sd-daemon.h,
  [have_systemd_sd_daemon_h=yes],[have_systemd_sd_daemon_h=no])

if test x"$have_sd_listen_fds" = x"yes" && \
   test x"$have_sd_notify" = x"yes" && \
   test x"$have_systemd_sd_daemon_h" = x"yes"; then
  AC_DEFINE([HAVE_SYSTEMD_DAEMON],[1],[Define if you have systemd daemon])
  SYSTEMD_DAEMON_LIBS=$LIBS
else
  AC_MSG_FAILURE([--enable-systemd was given, but test for systemd libraries had failed])
fi
LIBS=$systemd_daemon_save_LIBS
fi
AC_SUBST(SYSTEMD_DAEMON_LIBS)

# check gthread
if test "$enables_hed" = "yes"; then
PKG_CHECK_MODULES(GTHREAD, [gthread-2.0 >= 2.4.7])
AC_SUBST(GTHREAD_CFLAGS)
AC_SUBST(GTHREAD_LIBS)
fi

# check glibmm
# check for giomm which became a part of glibmm as of version 2.16
if test "$enables_hed" = "yes"; then
"$PKG_CONFIG" giomm-2.4
if test "$?" = '1'; then
  PKG_CHECK_MODULES(GLIBMM, [glibmm-2.4 >= 2.4.7])
else
  PKG_CHECK_MODULES(GLIBMM, [giomm-2.4])
  AC_DEFINE(HAVE_GIOMM, 1, [define if giomm is supported in glibmm])
fi
AC_SUBST(GLIBMM_CFLAGS)
AC_SUBST(GLIBMM_LIBS)
SAVE_CPPFLAGS=$CPPFLAGS
AC_LANG_SAVE
AC_LANG_CPLUSPLUS
CPPFLAGS="$CPPFLAGS $GLIBMM_CFLAGS"
AC_CHECK_HEADER([glibmm/optioncontext.h], [
  AC_TRY_COMPILE([#include <glibmm/optioncontext.h>],
    [Glib::OptionContext ctx; ctx.set_summary("summary")], [
      AC_DEFINE(HAVE_GLIBMM_OPTIONCONTEXT_SET_SUMMARY, 1,
        [define if glibmm has Glib::OptionContext::set_summary()])
      AC_MSG_NOTICE([using glibmm command line parsing])
    ], [
      AC_MSG_NOTICE([using getopt_long command line parsing])
    ]
  )
  AC_TRY_COMPILE([#include <glibmm/optioncontext.h>],
    [Glib::OptionContext ctx; ctx.get_help();],[
      AC_DEFINE(HAVE_GLIBMM_OPTIONCONTEXT_GET_HELP, 1,
        [define if glibmm has Glib::OptionContext::get_help()])
    ], [
    ]
  )
])
AC_TRY_COMPILE([#include <glibmm.h>],[Glib::SignalChildWatch watch = Glib::signal_child_watch();],[glibmm_childwatch=yes],[glibmm_childwatch=no])
if test "$glibmm_childwatch" = yes; then
  AC_DEFINE(HAVE_GLIBMM_CHILDWATCH, 1,
    [define if glibmm have support for controling state of children processes])
else
  AC_MSG_NOTICE([WARNING: glibmm has no API for controlling children processes - result of external processes may be inconsistent])
fi
AC_TRY_COMPILE([#include <glibmm.h>],[Glib::ModuleFlags flags = Glib::MODULE_BIND_LOCAL;],[glibmm_bind_local=yes],[glibmm_bind_local=no])
if test "$glibmm_bind_local" = yes; then
  AC_DEFINE(HAVE_GLIBMM_BIND_LOCAL, 1,
    [define if glibmm have support local symbol resolution in shared libraries])
else
  AC_MSG_NOTICE([WARNING: glibmm has no way to limit scope of symbols of shared libraries. Make sure external libraries used by plugins have no conflicting symbols. HINT: use Globus compiled against system OpenSSL library.])
fi
AC_TRY_COMPILE([#include <glibmm/miscutils.h>],[Glib::getenv("");],[glibmm_getenv=yes],[glibmm_getenv=no])
if test "$glibmm_getenv" = yes; then
  AC_DEFINE(HAVE_GLIBMM_GETENV, 1, [define if glibmm have getenv operations])
else
  AC_MSG_NOTICE([WARNING: glibmm has no support for getenv. Usage of libc getenv is unsafe in multi-threaded applications.])
fi
AC_TRY_COMPILE([#include <glibmm/miscutils.h>],[Glib::setenv("", "");],[glibmm_setenv=yes],[glibmm_setenv=no])
if test "$glibmm_setenv" = yes; then
  AC_DEFINE(HAVE_GLIBMM_SETENV, 1, [define if glibmm have setenv operations])
else
  AC_MSG_NOTICE([WARNING: glibmm has no support for setenv. Usage of libc setenv may be unsafe in multi-threaded applications.])
fi
AC_TRY_COMPILE([#include <glibmm/miscutils.h>],[Glib::unsetenv("");],[glibmm_unsetenv=yes],[glibmm_unsetenv=no])
if test "$glibmm_unsetenv" = yes; then
  AC_DEFINE(HAVE_GLIBMM_UNSETENV, 1, [define if glibmm have unsetenv operations])
else
  AC_MSG_NOTICE([WARNING: glibmm has no support for unsetenv. Usage of libc unsetenv may be unsafe in multi-threaded applications.])
fi
AC_TRY_COMPILE([#include <glibmm/miscutils.h>],[Glib::listenv();],[glibmm_listenv=yes],[glibmm_listenv=no])
if test "$glibmm_listenv" = yes; then
  AC_DEFINE(HAVE_GLIBMM_LISTENV, 1, [define if glibmm have listenv operations])
else
  AC_MSG_NOTICE([WARNING: glibmm has no support for listenv. Usage of libc environ is unsafe in multi-threaded applications.])
fi
AC_LANG_RESTORE
CPPFLAGS=$SAVE_CPPFLAGS
fi

# check libxml
if test "$enables_hed" = "yes"; then
PKG_CHECK_MODULES(LIBXML2, [libxml-2.0 >= 2.4.0])
AC_SUBST(LIBXML2_CFLAGS)
AC_SUBST(LIBXML2_LIBS)
fi

# check openssl
if test "$enables_hed" = "yes"; then
PKG_CHECK_MODULES(OPENSSL, [openssl >= 1.0.0])
PKG_CHECK_MODULES(OPENSSL_1_1, [openssl >= 1.1.0], [
  OPENSSL_CFLAGS="$OPENSSL_CFLAGS -DOPENSSL_API_COMPAT=0x10100000L"
  AC_MSG_NOTICE([Forcing off deprecated functions for OpenSSL >= 1.1])
], [
  AC_MSG_NOTICE([OpenSSL is pre-1.1])
])
AC_SUBST(OPENSSL_CFLAGS)
AC_SUBST(OPENSSL_LIBS)
fi

# Check for available *_method functions in OpenSSL
SAVE_CPPFLAGS=$CPPFLAGS
SAVE_LIBS=$LIBS
CPPFLAGS="$CPPFLAGS $OPENSSL_CFLAGS"
LIBS="$LIBS $OPENSSL_LIBS"
AC_LANG_PUSH([C++])

AC_COMPILE_IFELSE(
  [AC_LANG_PROGRAM([[
#include <openssl/ssl.h>
void _test(void) { (void)SSLv3_method(); }
  ]])],
  [AC_DEFINE(HAVE_SSLV3_METHOD,1,[define if SSLv3_method is available])],
  [AC_MSG_NOTICE([No SSLv3_method function avialable])])

AC_COMPILE_IFELSE(
  [AC_LANG_PROGRAM([[
#include <openssl/ssl.h>
void _test(void) { (void)TLSv1_method(); }
  ]])],
  [AC_DEFINE(HAVE_TLSV1_METHOD,1,[define if TLSv1_method is available])],
  [AC_MSG_NOTICE([No TLSv1_method function avialable])])

AC_COMPILE_IFELSE(
  [AC_LANG_PROGRAM([[
#include <openssl/ssl.h>
void _test(void) { (void)TLSv1_1_method(); }
  ]])],
  [AC_DEFINE(HAVE_TLSV1_1_METHOD,1,[define if TLSv1_1_method is available])],
  [AC_MSG_NOTICE([No TLSv1_1_method function avialable])])

AC_COMPILE_IFELSE(
  [AC_LANG_PROGRAM([[
#include <openssl/ssl.h>
void _test(void) { (void)TLSv1_2_method(); }
  ]])],
  [AC_DEFINE(HAVE_TLSV1_2_METHOD,1,[define if TLSv1_2_method is available])],
  [AC_MSG_NOTICE([No TLSv1_2_method function avialable])])

AC_COMPILE_IFELSE(
  [AC_LANG_PROGRAM([[
#include <openssl/ssl.h>
void _test(void) { (void)TLS_method(); }
  ]])],
  [AC_DEFINE(HAVE_TLS_METHOD,1,[define if TLS_method is available])],
  [AC_MSG_NOTICE([No TLS_method function avialable])])

AC_COMPILE_IFELSE(
  [AC_LANG_PROGRAM([[
#include <openssl/ssl.h>
void _test(void) { (void)DTLSv1_method(); }
  ]])],
  [AC_DEFINE(HAVE_DTLSV1_METHOD,1,[define if DTLSv1_method is available])],
  [AC_MSG_NOTICE([No DTLSv1_method function avialable])])

AC_COMPILE_IFELSE(
  [AC_LANG_PROGRAM([[
#include <openssl/ssl.h>
void _test(void) { (void)DTLSv1_2_method(); }
  ]])],
  [AC_DEFINE(HAVE_DTLSV1_2_METHOD,1,[define if DTLSv1_2_method is available])],
  [AC_MSG_NOTICE([No DTLSv1_2_method function avialable])])

AC_COMPILE_IFELSE(
  [AC_LANG_PROGRAM([[
#include <openssl/ssl.h>
void _test(void) { (void)DTLS_method(); }
  ]])],
  [AC_DEFINE(HAVE_DTLS_METHOD,1,[define if DTLS_method is available])],
  [AC_MSG_NOTICE([No DTLS_method function avialable])])

AC_LANG_POP([C++])
CPPFLAGS=$SAVE_CPPFLAGS
LIBS=$SAVE_LIBS

#check mozilla nss
enables_nss=yes
NSS_INSTALLED=no
dnl Check if nss lib is explicitly enabled, default is disable.
AC_ARG_ENABLE(nss, AC_HELP_STRING([--disable-nss], [disable use of the mozilla nss library]),[enables_nss="$enableval"],[])
if test "$enables_nss" = "yes"; then
  PKG_CHECK_MODULES(NSS, [nss >= 3.10], [NSS_INSTALLED=yes] , [
    AC_MSG_WARN([Cannot locate nss lib])
    NSS_INSTALLED=no
    enables_nss=no
  ])
  if test "x$NSS_INSTALLED" = "xyes" ; then
    AC_DEFINE(HAVE_NSS, 1, [define if NSS is enabled and available])
  fi
fi
AC_SUBST(NSS_CFLAGS)
AC_SUBST(NSS_LIBS)
AM_CONDITIONAL([NSS_ENABLED], test x$NSS_INSTALLED = xyes)

#check SQLite
SQLITE_INSTALLED=no
PKG_CHECK_MODULES(SQLITE, [sqlite3 >= 3.6], [SQLITE_INSTALLED=yes] , [
  AC_MSG_WARN([Cannot locate SQLite newer than 3.6])
  SQLITE_INSTALLED=no
  enables_sqlite=no
])
if test "x$SQLITE_INSTALLED" = "xyes" ; then
  AC_DEFINE(HAVE_SQLITE, 1, [define if SQLite is available])
  # Check for function available since 3.8
  SAVE_CFLAGS=$CFLAGS
  SAVE_LIBS=$LIBS
  CFLAGS="$CFLAGS $SQLITE_CFLAGS"
  LIBS="$LIBS $SQLITE_LIBS"
  AC_CHECK_FUNCS(sqlite3_errstr)
  CFLAGS=$SAVE_CFLAGS
  LIBS=$SAVE_LIBS
fi
AC_SUBST(SQLITE_CFLAGS)
AC_SUBST(SQLITE_LIBS)
AM_CONDITIONAL([SQLITE_ENABLED], test x$SQLITE_INSTALLED = xyes)

# check cppunit
if test "$enables_hed" = "yes"; then
AC_ARG_ENABLE(cppunit, AC_HELP_STRING([--disable-cppunit], [disable cppunit-based UNIT testing of code]),[enables_cppunit=$enableval],[])
if test "$enables_cppunit" = "yes"; then
  PKG_CHECK_MODULES(CPPUNIT, [cppunit],[],
    [AC_PATH_PROG(CPPUNIT_CONFIG, cppunit-config, no)
    if test "x$CPPUNIT_CONFIG" = "xno"; then
        AC_MSG_WARN([cppunit-config not found - no UNIT testing will be performed])
        CPPUNIT_CFLAGS=
        CPPUNIT_LIBS=
        enables_cppunit="no"
    else
        CPPUNIT_CFLAGS="`$CPPUNIT_CONFIG --cflags`"
        CPPUNIT_LIBS="`$CPPUNIT_CONFIG --libs`"
    fi])
  if test "x$CPPUNIT_CONFIG" != "xno" || test "x$CPPUNIT_PKG_ERRORS" != "x"
  then
    TEST_DIR=test
  else
    enables_cppunit=no
    TEST_DIR=
  fi
fi
AC_SUBST(CPPUNIT_CFLAGS)
AC_SUBST(CPPUNIT_LIBS)
AC_SUBST(TEST_DIR)
else
  enables_cppunit="no"
fi

# check ldns library
if test "$enables_compute_client" = "yes"; then
  AC_ARG_ENABLE(ldns, AC_HELP_STRING([--disable-ldns], [disable ldns library usage (makes ARCHERY client unavailable) ]),[enables_ldns=$enableval],[])
  if test "$enables_ldns" = "yes"; then
    PKG_CHECK_MODULES(LDNS, [ldns],[],
      [AC_PATH_PROG(LDNS_CONFIG, ldns-config, no)
      if test "x$LDNS_CONFIG" = "xno"; then
        AC_CHECK_HEADER([ldns/ldns.h],
          [AC_CHECK_LIB([ldns], [ldns_dname_new_frm_str],
            [
              LDNS_CFLAGS="$LDNS_CFLAGS"
              LDNS_LIBS="$LDNS_LIBS -lldns"
            ],
          [enables_ldns="no"])
        ],[enables_ldns="no"])
      else
        LDNS_CFLAGS="`$LDNS_CONFIG --cflags`"
        LDNS_LIBS="`$LDNS_CONFIG --libs`"
      fi
    ])
    if test "$enables_ldns" = "no"; then
      AC_MSG_WARN([ldns library was not found. Compute clients will be built without ARCHERY support.])
    fi
  fi
else
  enables_ldns="no"
fi
if test "x$enables_ldns" = "xyes" ; then
  AC_DEFINE(HAVE_LDNS, 1, [define if LDNS is enabled and available])
else
  LDNS_CFLAGS=
  LDNS_LIBS=
fi
AC_SUBST(LDNS_CFLAGS)
AC_SUBST(LDNS_LIBS)
AM_CONDITIONAL(LDNS_ENABLED, test "x$enables_ldns" = "xyes")

##############################
#
# Check xmlsec1
#
#############################
MACOSX=""
case "${host}" in
  *darwin*)
    MACOSX="yes"
    ;;
esac

if test "x$MACOSX" = "xyes"; then
  AC_DEFINE(_MACOSX, 1, [Define if compiling for MacOSX])
fi
AM_CONDITIONAL([MACOSX], [ test "x$MACOSX" = "xyes"])

if test "$enables_hed" = "yes"; then
XMLSEC_MIN_VERSION="1.2.4"
XMLSEC_OPENSSL_MIN_VERSION="1.2.4"
XMLSEC_CONFIG="${XMLSEC1_CONFIG:-xmlsec1-config}"
XMLSEC_CFLAGS=""
XMLSEC_LIBS=""
XMLSEC_INSTALLED=no
dnl Check if xmlsec1 is explicitly disabled, default is enable.
AC_ARG_ENABLE(xmlsec1, AC_HELP_STRING([--disable-xmlsec1], [disable features which need xmlsec1 library]),[enables_xmlsec1=$enableval],[])
if test "x$enables_xmlsec1" = "xyes"; then
  AC_ARG_WITH(xmlsec1, [  --with-xmlsec1=(PATH)  xmlsec1 location])
  if test "x$with_xmlsec1" = "x" ; then
    PKG_CHECK_MODULES(XMLSEC, [xmlsec1 >= $XMLSEC_MIN_VERSION],
        [XMLSEC_INSTALLED=yes], [XMLSEC_INSTALLED=no])
    if test "x$XMLSEC_INSTALLED" = "xyes" ; then
      PKG_CHECK_MODULES(XMLSEC_OPENSSL, [xmlsec1-openssl >= $XMLSEC_OPENSSL_MIN_VERSION],
          [XMLSEC_INSTALLED=yes],[XMLSEC_INSTALLED=no])
    fi

    # Find number of backslashes in XMLSEC_CFLAGS
    n=$(echo $XMLSEC_CFLAGS|sed 's/.*-DXMLSEC_CRYPTO=\([[^ ]]*\).*/\1/'|tr -d '[[A-Za-z0-1\n"]]'| wc -c)

    # Fixes due to bugs in pkg-config and/or xmlsec1 
    #
    # 0: Indicates a bug in pkg-config which removes the escaping of the quotes
    # 2: Correct value with escaped quotes
    # 6: Old xmlsec1 version which used 3 back-slashes to escape quotes
    #    See eg. https://bugzilla.redhat.com/show_bug.cgi?id=675334

    # Make sure that the quotes are escaped with single backslash
    if test $n = 0 -o $n = 6; then 
      AC_MSG_NOTICE([Working around bad combination of pkgconfig and xmlsec1 with $n back-slashes])
      XMLSEC_CFLAGS=$(echo $XMLSEC_CFLAGS|sed 's/\(.*-DXMLSEC_CRYPTO=\)\\*"\([[^ \\"]]*\)\\*" \(.*\)/\1\\"\2\\" \3/')
      XMLSEC_OPENSSL_CFLAGS=$(echo $XMLSEC_OPENSSL_CFLAGS|sed 's/\(.*-DXMLSEC_CRYPTO=\)\\*"\([[^ \\"]]*\)\\*" \(.*\)/\1\\"\2\\" \3/')
    fi

  fi

  if test "x$XMLSEC_INSTALLED" = "xno" -a "x$MACOSX" != "xyes"; then
      AC_MSG_CHECKING(for xmlsec1 libraries >= $XMLSEC_MIN_VERSION)
      if test "x$with_xmlsec1" != "x" ; then
        XMLSEC_CONFIG=$with_xmlsec1/bin/$XMLSEC_CONFIG
      fi
      "$XMLSEC_CONFIG" --version 2>/dev/null 1>/dev/null
      if test "$?" != '0' ; then
        AC_MSG_WARN(Could not find xmlsec1 anywhere; The xml security related functionality will not be compiled)
      else
        vers=`$XMLSEC_CONFIG --version 2>/dev/null | awk -F. '{ printf "%d", ($1 * 1000 + $2) * 1000 + $3;}'`
        minvers=`echo $XMLSEC_MIN_VERSION | awk -F. '{ printf "%d", ($1 * 1000 + $2) * 1000 + $3;}'`
        if test "$vers" -ge "$minvers" ; then
          XMLSEC_LIBS="`$XMLSEC_CONFIG --libs`"
          XMLSEC_CFLAGS="`$XMLSEC_CONFIG --cflags`"
          #check the xmlsec1-openssl here
          if test "x$PKG_CONFIG_PATH" != "x"; then
            PKG_CONFIG_PATH="$with_xmlsec1/lib/pkgconfig:$PKG_CONFIG_PATH"
          else
            PKG_CONFIG_PATH="$with_xmlsec1/lib/pkgconfig"
          fi
          PKG_CHECK_MODULES(XMLSEC_OPENSSL, [xmlsec1-openssl >= $XMLSEC_OPENSSL_MIN_VERSION],
              [XMLSEC_INSTALLED=yes],[XMLSEC_INSTALLED=no])
        else
          AC_MSG_WARN(You need at least xmlsec1 $XMLSEC_MIN_VERSION for this version of arc)
        fi
      fi
  elif test "x$XMLSEC_INSTALLED" = "xno" -a "x$MACOSX" = "xyes"; then
    #MACOSX has no "ldd" which is needed by xmlsec1-config, so here simply we use PKG_CHECK_MODULES
    if test "x$PKG_CONFIG_PATH" != "x"; then
      PKG_CONFIG_PATH="$with_xmlsec1/lib/pkgconfig:$PKG_CONFIG_PATH"
    else
      PKG_CONFIG_PATH="$with_xmlsec1/lib/pkgconfig"
    fi
    PKG_CHECK_MODULES(XMLSEC, [xmlsec1 >= $XMLSEC_MIN_VERSION],
        [XMLSEC_INSTALLED=yes], [XMLSEC_INSTALLED=no])
    if test "x$XMLSEC_INSTALLED" = "xyes" ; then
      PKG_CHECK_MODULES(XMLSEC_OPENSSL, [xmlsec1-openssl >= $XMLSEC_OPENSSL_MIN_VERSION],
          [XMLSEC_INSTALLED=yes],[XMLSEC_INSTALLED=no])
    fi
  fi

  AC_SUBST(XMLSEC_CFLAGS)
  AC_SUBST(XMLSEC_LIBS)
  AC_SUBST(XMLSEC_OPENSSL_CFLAGS)
  AC_SUBST(XMLSEC_OPENSSL_LIBS)

  #AC_SUBST(XMLSEC_CONFIG)
  #AC_SUBST(XMLSEC_MIN_VERSION)
  enables_xmlsec1="$XMLSEC_INSTALLED"
fi
else
  enables_xmlsec1="no"
fi

#########################
#
# Check libmysqlclient
#
#########################
MYSQL_INSTALLED=no
if test "$enables_hed" = "yes"; then
MYSQL_CONFIG="mysql_config"
MYSQL_CFLAGS=""
MYSQL_LIBS=""
dnl Check if libmysqlclient is explicitly enabled, default is disable.
AC_ARG_ENABLE(mysql, AC_HELP_STRING([--enable-mysql], [enable use of the MySQL client library]),[enables_mysql="$enableval"],[])
# Ask user for path to libmysqlclient
if test "x$enables_mysql" = "xyes"; then
  AC_ARG_WITH(mysql, [  --with-mysql=(PATH) prefix of MySQL installation. e.g. /usr/local or /usr])
  AC_MSG_CHECKING(for mysql client library)
  if test "x$with_mysql" != "x" ; then
      MYSQL_CONFIG=$with_mysql/bin/$MYSQL_CONFIG
  fi
  if ! $MYSQL_CONFIG --version > /dev/null 2>&1 ; then
      AC_MSG_ERROR(Could not find mysql C library anywhere (see config.log for details).)
  fi
  MYSQL_LIBS="`$MYSQL_CONFIG --libs`"
  MYSQL_CFLAGS="`$MYSQL_CONFIG --cflags`"
  MYSQL_INSTALLED="yes"

  AC_SUBST(MYSQL_LIBS)
  AC_SUBST(MYSQL_CFLAGS)
  enables_mysql=$MYSQL_INSTALLED
fi
AC_MSG_NOTICE([MySQL client library enabled: $MYSQL_INSTALLED])
fi
AM_CONDITIONAL([MYSQL_LIBRARY_ENABLED],[test "x$MYSQL_INSTALLED" = "xyes"])

# Check monitor
AC_ARG_ENABLE(monitor, AC_HELP_STRING([--enable-monitor], [enable use of the monitor]),[enables_monitor="$enableval"],[])
if test "x$enables_monitor" = "xyes"; then
  AC_ARG_WITH(monitor, [  --with-monitor=(PATH) where to install the monitor, eg /var/www/monitor or /usr/share/arc/monitor])
  AC_MSG_CHECKING(for monitor installation path)
  if test "x$with_monitor" != "x" ; then
      monitor_prefix=$with_monitor
  else
      monitor_prefix=${datadir}/arc/monitor
  fi
  AC_MSG_RESULT([$monitor_prefix])
  AC_SUBST(monitor_prefix)
fi

# check zlib
ZLIB_CFLAGS=
ZLIB_LDFLAGS=
ZLIB_LIBS=
if test "$enables_hed" = "yes"; then
SAVE_CPPFLAGS=$CPPFLAGS
SAVE_LDFLAGS=$LDFLAGS
AC_ARG_WITH(zlib,
  AC_HELP_STRING([--with-zlib=PATH], [where zlib is installed]),
    [ if test -d "$withval"; then
        ZLIB_CFLAGS="${CPPFLAGS} -I$withval/include"
        ZLIB_LDFLAGS="${LDFLAGS} -L$withval/lib"
      fi
    ]
)
CPPFLAGS="$CPPFLAGS $ZLIB_CFLAGS"
LDFLAGS="$LDFLAGS $ZLIB_LDFLAGS"
AC_CHECK_HEADER([zlib.h],[ZLIB_CFLAGS="$ZLIB_CFLAGS"],AC_MSG_ERROR([unable to find zlib header files]))
AC_CHECK_LIB([z],[deflateInit2_],[ZLIB_LIBS="$ZLIB_LDFLAGS -lz"],AC_MSG_ERROR([unable to link with zlib library]))
CPPFLAGS=$SAVE_CPPFLAGS
LDFLAGS=$SAVE_LDFLAGS
fi
AC_SUBST(ZLIB_CFLAGS)
AC_SUBST(ZLIB_LIBS)

# check ARGUS
ARGUS_CFLAGS=
ARGUS_LIBS=
AC_ARG_ENABLE(argus, AC_HELP_STRING([--enable-argus], [enable use of Argus PEP V2 libraries]),[enables_argus="$enableval"],[])
if test "x$enables_argus" = "xyes"; then
  AC_ARG_WITH(argus,
    AC_HELP_STRING([--with-argus=PATH], [ARGUS PEP installation path]),
    [
      if test "x$PKG_CONFIG_PATH" != "x"; then
        PKG_CONFIG_PATH="$withval/lib/pkgconfig:$PKG_CONFIG_PATH"
      else
        PKG_CONFIG_PATH="$withval/lib/pkgconfig"
      fi
    ]
  )
  PKG_CHECK_MODULES(ARGUS, [libargus-pep >= 2.0.0], [], [
    AC_MSG_NOTICE([Failed to find Argus PEP libraries with version >= 2])
    enables_argus=no
  ])
fi
AC_SUBST(ARGUS_CFLAGS)
AC_SUBST(ARGUS_LIBS)
AM_CONDITIONAL(ARGUS_ENABLED, test "x$enables_argus" = "xyes")

###############################################
#
# Check for Berkeley DB C++
#
###############################################
DBCXX_LIBS=""
DBCXX_CPPFLAGS=

if test "$enables_hed" = "yes"; then

#
# Allow the user to specify db_cxx.h location (we will still check though)
#

dbcxx_include_paths=
AC_ARG_WITH(dbcxx-include,
   [  --with-dbcxx-include=PATH   Specify path to db_cxx.h],
   [
  if test "x$withval" = "xyes" ; then
    AC_MSG_ERROR([--with-dbcxx-include requires PATH argument])
  fi
  if test "x$withval" != "xno" ; then
    dbcxx_include_paths=$withval
  fi
   ]
)

#
# Allow the user to specify DB4 library location (we will still check though)
#

db4_library_path=
AC_ARG_WITH(db4-library-path,
   [  --with-db4-library-path=PATH   Specify path to DB4 library],
   [
  if test "x$withval" = "xyes" ; then
    AC_MSG_ERROR([--with-db4-library-path requires PATH argument])
  fi
  if test "x$withval" != "xno" ; then
    db4_library_path=$withval
  fi
   ]
)

AC_LANG_SAVE
AC_LANG_CPLUSPLUS

#
# If user did not specify location we start by searching at the standard locations
#

if test "x$dbcxx_include_paths" = "x"
then
  AC_MSG_NOTICE([Looking for db_cxx.h in standard locations])
  AC_CHECK_HEADERS(db_cxx.h,HAVE_DBCXX=yes,HAVE_DBCXX=no)
  # If the user did not provide a location we have some good suggestions
  dbcxx_include_paths="/usr/include/db4 /usr/include/db44 /usr/include/db43"
else
  HAVE_DBCXX=no
fi

#
# Now Look for db_cxx.h in non-standard locations
#

if test "$HAVE_DBCXX" = no
then
  for dbcxx_dir in $dbcxx_include_paths
  do
    SAVE_CPPFLAGS=$CPPFLAGS
    DBCXX_CPPFLAGS=-I$dbcxx_dir
    CPPFLAGS="$CPPFLAGS $DBCXX_CPPFLAGS"
    # Disable Autoconf caching
    unset ac_cv_header_db_cxx_h
    AC_MSG_NOTICE([Looking for db_cxx.h in $dbcxx_dir])
    AC_CHECK_HEADERS(db_cxx.h,HAVE_DBCXX=yes,HAVE_DBCXX=no)
    CPPFLAGS=$SAVE_CPPFLAGS
    # If a db_cxx.h was found we break and keep the current value of DBCXX_CPPFLAGS
    if test "$HAVE_DBCXX" = yes
    then
      break
    fi
    DBCXX_CPPFLAGS=
  done
fi
AC_SUBST(DBCXX_CPPFLAGS)

if test "x$db4_library_path" != "x"
then
  db4_library_path="-L$db4_library_path"
fi

if test "$HAVE_DBCXX" = no
then
  DBCXX_LIBS=""
else
  SAVE_LDFLAGS=$LDFLAGS
  SAVE_CXXFLAGS=$CXXFLAGS

  # pthread needed for RH9
  LDFLAGS="$LDFLAGS -lpthread"

  LDFLAGS="$LDFLAGS $db4_library_path"

  for db_ver in "" -4.7 -4.3 -4.2
  do
    AC_CHECK_LIB(db_cxx$db_ver,main,DBCXX_LIBS="$db4_library_path -ldb_cxx$db_ver",DBCXX_LIBS="")

    if test "$DBCXX_LIBS" = ""
    then
      AC_MSG_WARN([BerkeleyDB library libdb_cxx$db_ver was not found!])
    else
      break
    fi
  done

  if test "$DBCXX_LIBS" = ""
  then
    AC_MSG_WARN([No BerkeleyDB library found!])
  fi

  LDFLAGS=$SAVE_LDFLAGS
  CXXFLAGS=$SAVE_CXXFLAGS
fi

AC_SUBST(DBCXX_LIBS)
if test ! "x$DBCXX_LIBS" = "x"
then
  AC_DEFINE(HAVE_DBCXX, 1, [define if Berkeley DB C++ binding is available])
  SAVE_CXXFLAGS=$CXXFLAGS
  CXXFLAGS="$CXXFLAGS $DBCXX_CPPFLAGS"
  AC_DBCXX_HAVE_DBDEADLOCKEXCEPTION
  CXXFLAGS=$SAVE_CXXFLAGS
fi
AC_LANG_RESTORE

fi

# DBJSTORE (storing jobs information in BDB)
AC_ARG_ENABLE(dbjstore, AC_HELP_STRING([--disable-dbjstore], [disable storing local jobs information in BDB]),
  [enables_dbjstore=$enableval],[])
if test "$enables_dbjstore" = "yes"; then
  if test "x$DBCXX_LIBS" = "x" ; then
    AC_MSG_NOTICE([For storing jobs in BDB C++ API is needed (dbcxx) - disabling])
    enables_dbjstore="no"
  fi
fi
AC_MSG_NOTICE([Storing jobs in BDB enabled: $enables_dbjstore])
AM_CONDITIONAL([DBJSTORE_ENABLED],[test "x$enables_dbjstore" = "xyes"])
if test "x$enables_dbjstore" = "xyes"; then
  AC_DEFINE(DBJSTORE_ENABLED, 1,
    [define if to build job information in BDB storage])
fi

# SQLITEJSTORE (storing jobs information in SQLite)
AC_ARG_ENABLE(sqlitejstore, AC_HELP_STRING([--disable-sqlitejstore], [disable storing local jobs information in SQLite]),
  [enables_sqlitejstore=$enableval],[])
if test "$enables_sqlitejstore" = "yes"; then
  if test "x$SQLITE_INSTALLED" != "xyes" ; then
    AC_MSG_NOTICE([For storing jobs in SQLite install SQLite 3.6 or newer - disabling])
    enables_dbjstore="no"
  fi
fi
AC_MSG_NOTICE([Storing jobs in SQLite enabled: $enables_sqlitejstore])
AM_CONDITIONAL([SQLITEJSTORE_ENABLED],[test "x$enables_sqlitejstore" = "xyes"])
if test "x$enables_sqlitejstore" = "xyes"; then
  AC_DEFINE(SQLITEJSTORE_ENABLED, 1,
    [define if to build job information in SQLite storage])
fi

# globus/gpt packages
# globus/gpt packages
if test "$enables_hed" = "yes"; then
PKG_CHECK_MODULES(GLOBUS_COMMON, [globus-common], [
GLOBUS_COMMON_VERSION=`$PKG_CONFIG --modversion globus-common`], [
GPT_PKG(globus_common)
])
AC_SUBST(GLOBUS_COMMON_CFLAGS)
AC_SUBST(GLOBUS_COMMON_LIBS)

PKG_CHECK_MODULES(GLOBUS_GSSAPI_GSI, [globus-gssapi-gsi], [
GLOBUS_GSSAPI_GSI_VERSION=`$PKG_CONFIG --modversion globus-gssapi-gsi`], [
GPT_PKG(globus_gssapi_gsi)
])
AC_SUBST(GLOBUS_GSSAPI_GSI_CFLAGS)
AC_SUBST(GLOBUS_GSSAPI_GSI_LIBS)

PKG_CHECK_MODULES(GLOBUS_GSS_ASSIST, [globus-gss-assist], [
GLOBUS_GSS_ASSIST_VERSION=`$PKG_CONFIG --modversion globus-gss-assist`], [
GPT_PKG(globus_gss_assist)
])
AC_SUBST(GLOBUS_GSS_ASSIST_CFLAGS)
AC_SUBST(GLOBUS_GSS_ASSIST_LIBS)

PKG_CHECK_MODULES(GLOBUS_GSI_CALLBACK, [globus-gsi-callback], [
GLOBUS_GSI_CALLBACK_VERSION=`$PKG_CONFIG --modversion globus-gsi-callback`], [
GPT_PKG(globus_gsi_callback)
])
AC_SUBST(GLOBUS_GSI_CALLBACK_CFLAGS)
AC_SUBST(GLOBUS_GSI_CALLBACK_LIBS)

PKG_CHECK_MODULES(GLOBUS_FTP_CLIENT, [globus-ftp-client], [
GLOBUS_FTP_CLIENT_VERSION=`$PKG_CONFIG --modversion globus-ftp-client`], [
GPT_PKG(globus_ftp_client)
])
AC_SUBST(GLOBUS_FTP_CLIENT_CFLAGS)
AC_SUBST(GLOBUS_FTP_CLIENT_LIBS)

PKG_CHECK_MODULES(GLOBUS_FTP_CONTROL, [globus-ftp-control], [
GLOBUS_FTP_CONTROL_VERSION=`$PKG_CONFIG --modversion globus-ftp-control`], [
GPT_PKG(globus_ftp_control)
])
AC_SUBST(GLOBUS_FTP_CONTROL_CFLAGS)
AC_SUBST(GLOBUS_FTP_CONTROL_LIBS)

PKG_CHECK_MODULES(GLOBUS_IO, [globus-io], [
GLOBUS_IO_VERSION=`$PKG_CONFIG --modversion globus-io`], [
GPT_PKG(globus_io)
])
AC_SUBST(GLOBUS_IO_CFLAGS)
AC_SUBST(GLOBUS_IO_LIBS)

PKG_CHECK_MODULES(GLOBUS_GSI_CERT_UTILS, [globus-gsi-cert-utils], [
GLOBUS_GSI_CERT_UTILS_VERSION=`$PKG_CONFIG --modversion globus-gsi-cert-utils`], [
GPT_PKG(globus_gsi_cert_utils)
])
AC_SUBST(GLOBUS_GSI_CERT_UTILS_CFLAGS)
AC_SUBST(GLOBUS_GSI_CERT_UTILS_LIBS)

PKG_CHECK_MODULES(GLOBUS_GSI_CREDENTIAL, [globus-gsi-credential], [
GLOBUS_GSI_CREDENTIAL_VERSION=`$PKG_CONFIG --modversion globus-gsi-credential`], [
GPT_PKG(globus_gsi_credential)
])
AC_SUBST(GLOBUS_GSI_CREDENTIAL_CFLAGS)
AC_SUBST(GLOBUS_GSI_CREDENTIAL_LIBS)

PKG_CHECK_MODULES(GLOBUS_OPENSSL_MODULE, [globus-openssl-module], [
GLOBUS_OPENSSL_MODULE_VERSION=`$PKG_CONFIG --modversion globus-openssl-module`], [
GPT_PKG(globus_openssl_module)
])
AC_SUBST(GLOBUS_OPENSSL_MODULE_CFLAGS)
AC_SUBST(GLOBUS_OPENSSL_MODULE_LIBS)

# Check for new globus thread model selection
SAVE_CFLAGS=$CFLAGS
SAVE_LIBS=$LIBS
CFLAGS="$CFLAGS $GLOBUS_COMMON_CFLAGS"
LIBS="$LIBS $GLOBUS_COMMON_LIBS"
AC_CHECK_FUNCS(globus_thread_set_model)
CFLAGS=$SAVE_CFLAGS
LIBS=$SAVE_LIBS

# Check for gridftp-v2
SAVE_CFLAGS=$CFLAGS
SAVE_LIBS=$LIBS
CFLAGS="$CFLAGS $GLOBUS_FTP_CLIENT_CFLAGS"
LIBS="$LIBS $GLOBUS_FTP_CLIENT_LIBS"
AC_CHECK_FUNCS(globus_ftp_client_handleattr_set_gridftp2)
CFLAGS=$SAVE_CFLAGS
LIBS=$SAVE_LIBS

globus_openssl_detected=
PKG_CHECK_MODULES(GLOBUS_OPENSSL, [globus-openssl], [
GLOBUS_OPENSSL_VERSION=`$PKG_CONFIG --modversion globus-openssl`], [
GPT_PKG(globus_openssl)
])
if test ! "x$GLOBUS_OPENSSL_LIBS" = "x" ; then
  globus_openssl_detected=`echo "$GLOBUS_OPENSSL_LIBS" | grep "lssl_$GPT_FLAVOR"`
  if test ! "x$globus_openssl_detected" = "x" ; then
    globus_openssl_detected="yes"
  fi
fi
if test "x$globus_openssl_detected" = "xyes" ; then
AC_MSG_RESULT([
Globus own OpenSSL library detected.
In order to avoid runtime conflicts following components will be disabled:
GridFTP DMC,
SRM DMC,
GSI MCC.
To enable these components use Globus compiled for system OpenSSL.
])
GLOBUS_FTP_CLIENT_VERSION=
GLOBUS_FTP_CONTROL_VERSION=
GLOBUS_IO_VERSION=
GLOBUS_GSSAPI_GSI_VERSION=
fi

if test "x$GLOBUS_IO_VERSION" = "x"; then
  IO_VERSION_MAJOR=0
else
  IO_VERSION_MAJOR=`echo "$GLOBUS_IO_VERSION" | sed 's/^\([[^.]]*\).*/\1/'`;
fi
AC_DEFINE_UNQUOTED(GLOBUS_IO_VERSION,$IO_VERSION_MAJOR,[Globus IO version])

if test "x$GLOBUS_GSSAPI_GSI_VERSION" = "x"; then
  GLOBUS_GSSAPI_GSI_VERSION_MAJOR=0
  GLOBUS_GSSAPI_GSI_VERSION_MINOR=0
else
  GLOBUS_GSSAPI_GSI_VERSION_MAJOR=`echo "$GLOBUS_GSSAPI_GSI_VERSION" | sed 's/^\([[^.]]*\).*/\1/'`;
  GLOBUS_GSSAPI_GSI_VERSION_MINOR=`echo "$GLOBUS_GSSAPI_GSI_VERSION" | sed 's/^[[^.]]*\.\([[^.]]*\).*/\1/'`;
fi
if test "$GLOBUS_GSSAPI_GSI_VERSION_MAJOR" -lt "12"; then
  GLOBUS_GSSAPI_GSI_OLD_OPENSSL=1
elif test "$GLOBUS_GSSAPI_GSI_VERSION_MAJOR" -eq "12"; then
  if test "$GLOBUS_GSSAPI_GSI_VERSION_MINOR" -lt "2"; then
    GLOBUS_GSSAPI_GSI_OLD_OPENSSL=1
  else
    GLOBUS_GSSAPI_GSI_OLD_OPENSSL=0
  fi
else
  GLOBUS_GSSAPI_GSI_OLD_OPENSSL=0
fi

AC_DEFINE_UNQUOTED(GLOBUS_GSSAPI_GSI_VERSION,$GSSAPI_GSI_VERSION_MAJOR,[Globus GSSAPI GSI version])
AC_DEFINE_UNQUOTED(GLOBUS_GSSAPI_GSI_OLD_OPENSSL,$GLOBUS_GSSAPI_GSI_OLD_OPENSSL,[Globus GSSAPI GSI is for OpenSSL post-1.1])

dnl
dnl DEFAULT_GLOBUS_LOCATION
dnl
AC_MSG_CHECKING(for DEFAULT_GLOBUS_LOCATION)
# GLOBUS_LOCATION is set by GPT macros
DEFAULT_GLOBUS_LOCATION="$GLOBUS_LOCATION"
AC_MSG_RESULT($DEFAULT_GLOBUS_LOCATION)
AC_SUBST(DEFAULT_GLOBUS_LOCATION)

#check lcas
DEFAULT_LCAS_LOCATION=/opt/glite
LCAS_LOCATION=
LCAS_CFLAGS=
LCAS_LIBS=
AC_ARG_WITH(lcas-location,
  [  --with-lcas-location=<PATH>        Specify the LCAS installation path. [[/opt/glite]]],
  [
    LCAS_LOCATION=$with_lcas_location
    if test ! -d $LCAS_LOCATION; then
      AC_MSG_WARN([LCAS_LOCATION ($LCAS_LOCATION) does not exist])
      LCAS_LOCATION=
    fi
  ],[
    if test "x$LCAS_LOCATION" = "x"; then
      LCAS_LOCATION=$DEFAULT_LCAS_LOCATION
    fi
    if test ! -d $LCAS_LOCATION; then
      LCAS_LOCATION=
    fi
  ]
)
if test "x$LCAS_LOCATION" != "x"; then
  LCAS_CFLAGS=$LCAS_LOCATION/include/glite/security/lcas
  if test ! -d $LCAS_CFLAGS; then
    LCAS_CFLAGS=$LCAS_LOCATION/include/lcas
    if test ! -d $LCAS_CFLAGS; then
      LCAS_CFLAGS=$LCAS_LOCATION/include
    fi
  fi
  LCAS_CFLAGS=-I$LCAS_CFLAGS
  SAVE_CPPFLAGS=$CPPFLAGS
  CPPFLAGS="$LCAS_CFLAGS $GLOBUS_GSSAPI_GSI_CFLAGS"
  AC_CHECK_HEADERS([lcas.h],
    LCAS_LDFLAGS=
    if test -d $LCAS_LOCATION/lib64; then
      LCAS_LDFLAGS="-L$LCAS_LOCATION/lib64 $GLOBUS_GSSAPI_GSI_LIBS"
    else
      LCAS_LDFLAGS="-L$LCAS_LOCATION/lib $GLOBUS_GSSAPI_GSI_LIBS"
    fi
    SAVE_LDFLAGS=$LDFLAGS
    LDFLAGS="$LDFLAGS $LCAS_LDFLAGS"
    AC_CHECK_LIB(lcas,lcas_init, LCAS_LIBS="$LCAS_LDFLAGS -llcas",LCAS_LOCATION="",)
    LDFLAGS=$SAVE_LDFLAGS
    ,
    LCAS_LOCATION=""
  )
  CPPFLAGS=$SAVE_CPPFLAGS
fi
if test "x$LCAS_LOCATION" != "x"; then
  AC_DEFINE(HAVE_LCAS, 1, [define if lcas is available])
  AC_SUBST(LCAS_LOCATION)
  AC_SUBST(LCAS_CFLAGS)
  AC_SUBST(LCAS_LIBS)
fi

#check lcmaps
DEFAULT_LCMAPS_LOCATION=/opt/glite
LCMAPS_LOCATION=
LCMAPS_CFLAGS=
LCMAPS_LIBS=
AC_ARG_WITH(lcmaps-location,
  [  --with-lcmaps-location=<PATH>        Specify the LCMAPS installation path. [[/opt/glite]]],
  [
    LCMAPS_LOCATION=$with_lcmaps_location
    if test ! -d $LCMAPS_LOCATION; then
      AC_MSG_WARN([LCMAPS_LOCATION ($LCMAPS_LOCATION) does not exist])
      LCMAPS_LOCATION=
    fi
  ],[
    if test "x$LCMAPS_LOCATION" = "x"; then
      LCMAPS_LOCATION=$DEFAULT_LCMAPS_LOCATION
    fi
    if test ! -d $LCMAPS_LOCATION; then
      LCMAPS_LOCATION=
    fi
  ]
)
if test "x$LCMAPS_LOCATION" != "x"; then
  LCMAPS_CFLAGS=$LCMAPS_LOCATION/include/glite/security/lcmaps
  if test ! -d $LCMAPS_CFLAGS; then
    LCMAPS_CFLAGS=$LCMAPS_LOCATION/include/lcmaps
    if test ! -d $LCMAPS_CFLAGS; then
      LCMAPS_CFLAGS=$LCMAPS_LOCATION/include
    fi
  fi
  LCMAPS_CFLAGS=-I$LCMAPS_CFLAGS
  SAVE_CPPFLAGS=$CPPFLAGS
  CPPFLAGS="$LCMAPS_CFLAGS $GLOBUS_GSSAPI_GSI_CFLAGS"
  AC_CHECK_HEADERS([lcmaps.h],
    LCMAPS_LDFLAGS=
    if test -d $LCMAPS_LOCATION/lib64; then
      LCMAPS_LDFLAGS="-L$LCMAPS_LOCATION/lib64 $GLOBUS_GSSAPI_GSI_LIBS"
    else
      LCMAPS_LDFLAGS="-L$LCMAPS_LOCATION/lib $GLOBUS_GSSAPI_GSI_LIBS"
    fi
    SAVE_LDFLAGS=$LDFLAGS
    LDFLAGS="$LDFLAGS $LCMAPS_LDFLAGS"
    AC_CHECK_LIB(lcmaps,lcmaps_init, LCMAPS_LIBS="$LCMAPS_LDFLAGS -llcmaps",LCMAPS_LOCATION="",)
    LDFLAGS=$SAVE_LDFLAGS
    ,
    LCMAPS_LOCATION=""
  )
  CPPFLAGS=$SAVE_CPPFLAGS
fi
if test "x$LCMAPS_LOCATION" != "x"; then
  AC_DEFINE(HAVE_LCMAPS, 1, [define if lcmaps is available])
  AC_SUBST(LCMAPS_LOCATION)
  AC_SUBST(LCMAPS_CFLAGS)
  AC_SUBST(LCMAPS_LIBS)
fi

# Check if mock DMC is enabled
AC_ARG_ENABLE(mock-dmc, AC_HELP_STRING([--enable-mock-dmc], [enable mock DMC, default is disable]),[enables_mock_dmc="$enableval"],[])

# Check for GFAL2
AC_ARG_ENABLE(gfal, AC_HELP_STRING([--enable-gfal], [enable the GFAL support, default is disable]),[enables_gfal="$enableval"],[])
if test "x$enables_gfal" = "xyes"; then
  PKG_CHECK_MODULES(GFAL2, gfal_transfer, [], [enables_gfal="no"])
  AC_SUBST(GFAL2_CFLAGS)
  AC_SUBST(GFAL2_LIBS)
fi

# Check for S3
AC_ARG_ENABLE(s3, AC_HELP_STRING([--enable-s3], [enable the S3 support, default is disable]),[enables_s3="$enableval"],[])
if test "x$enables_s3" = "xyes"; then
  AC_ARG_WITH(s3, [  --with-s3=(PATH)        libs3 location])
  if test ! "x$with_s3" = "x" ; then
    S3_LOCATION="$with_s3"
    S3_CPPFLAGS="-I$S3_LOCATION/include"
    if test -d $S3_LOCATION/lib64; then
      S3_LDFLAGS="-L$S3_LOCATION/lib64"
    else
      S3_LDFLAGS="-L$S3_LOCATION/lib"
    fi
  fi
  SAVE_CPPFLAGS=$CPPFLAGS
  CPPFLAGS="$CPPFLAGS $S3_CPPFLAGS"
  AC_CHECK_HEADER(libs3.h, [], [enables_s3="no"])
  CPPFLAGS=$SAVE_CPPFLAGS
  SAVE_LDFLAGS=$LDFLAGS
  LDFLAGS="$LDFLAGS $S3_LDFLAGS"
  AC_CHECK_LIB([s3], [S3_initialize],
               [S3_LIBS="$S3_LDFLAGS -ls3"], [enables_s3="no"])
  LDFLAGS=$SAVE_LDFLAGS
  AC_SUBST(S3_CPPFLAGS)
  AC_SUBST(S3_LIBS)
  if test x$enables_s3 = xyes
  then
    if s3 help 2>&1 | grep -q  -- '--timeout' ; then
      AC_DEFINE([HAVE_S3_TIMEOUT], 1, [Define if S3 API has timeouts])
    fi
  fi
fi


# Check for xrootd (c++)

AC_LANG_SAVE
AC_LANG_CPLUSPLUS

AC_ARG_ENABLE(xrootd, AC_HELP_STRING([--disable-xrootd], [disable the xrootd support, default is enable]),[enables_xrootd="$enableval"],[])
if test "x$enables_xrootd" = "xyes"; then
  XROOTD_CPPFLAGS="-I/usr/include/xrootd"
  AC_ARG_WITH(xrootd, [  --with-xrootd=(PATH)    Xrootd location])
  if test ! "x$with_xrootd" = "x" ; then
    XROOTD_LOCATION="$with_xrootd"
    XROOTD_CPPFLAGS="-I$XROOTD_LOCATION/include/xrootd"
    if test -d $XROOTD_LOCATION/lib64; then
      XROOTD_LDFLAGS="-L$XROOTD_LOCATION/lib64"
    else
      XROOTD_LDFLAGS="-L$XROOTD_LOCATION/lib"
    fi
  fi
  AC_MSG_CHECKING([for XROOTD headers])
  SAVE_CPPFLAGS=$CPPFLAGS
  CPPFLAGS="$CPPFLAGS $XROOTD_CPPFLAGS"
  AC_TRY_COMPILE([#include <XrdCl/XrdClBuffer.hh>], [], [
    AC_MSG_RESULT([$XROOTD_CPPFLAGS])
    ], [
    XROOTD_CPPFLAGS="-std=c++0x $XROOTD_CPPFLAGS"
    CPPFLAGS="$SAVE_CPPFLAGS $XROOTD_CPPFLAGS"
    AC_TRY_COMPILE([#include <XrdCl/XrdClBuffer.hh>], [], [
      AC_MSG_RESULT([$XROOTD_CPPFLAGS])
      ], [
      AC_MSG_RESULT([no])
      enables_xrootd="no"
    ])
  ])
  CPPFLAGS=$SAVE_CPPFLAGS
  SAVE_LDFLAGS=$LDFLAGS
  LDFLAGS="$LDFLAGS $XROOTD_LDFLAGS"
  AC_CHECK_LIB([XrdPosix], [_init],
               [XROOTD_LIBS="$XROOTD_LDFLAGS -lXrdPosix -lXrdCl"], [enables_xrootd="no"])
  LDFLAGS=$SAVE_LDFLAGS
fi
AC_SUBST(XROOTD_CPPFLAGS)
AC_SUBST(XROOTD_LIBS)
fi

AC_LANG_RESTORE

# Setup conditionals
AM_CONDITIONAL([GLOBUSUTILS_ENABLED], test -n "$GLOBUS_COMMON_VERSION")
AM_CONDITIONAL([GRIDFTP_ENABLED], test -n "$GLOBUS_FTP_CLIENT_VERSION")
AM_CONDITIONAL([MOCK_DMC_ENABLED], test x$enables_mock_dmc = xyes)
AM_CONDITIONAL([GFAL_ENABLED], test x$enables_gfal = xyes)
AM_CONDITIONAL([S3_DMC_ENABLED], test x$enables_s3 = xyes)
AM_CONDITIONAL([XROOTD_ENABLED], test x$enables_xrootd = xyes)
AM_CONDITIONAL([XMLSEC_ENABLED], test x$XMLSEC_INSTALLED = xyes)
AM_CONDITIONAL([CPPUNIT_ENABLED], test x$enables_cppunit = xyes)

enables_srm_dmc=no
if test "$enables_hed" = "yes"; then
  enables_srm_dmc=yes
fi

AM_CONDITIONAL([SRM_DMC_ENABLED],[test "x$enables_srm_dmc" = "xyes"])

# Setup defines
if test -n "$GLOBUS_COMMON_VERSION"; then
    AC_DEFINE(HAVE_GLOBUS, 1, [define if GLOBUS is available])
fi
if test x"$XMLSEC_INSTALLED" = xyes; then
    AC_DEFINE(HAVE_XMLSEC, 1, [define if XMLSEC package is available])
fi

# Setup messages for reporting
enables_gridftp=no
if test -n "$GLOBUS_FTP_CLIENT_VERSION" ; then enables_gridftp=yes; fi
enables_dbcxx=no
if test -n "$DBCXX_LIBS" ; then enables_dbcxx=yes; fi
enables_sqlite=no
if test "x$SQLITE_INSTALLED" = "xyes" ; then enables_sqlite=yes; fi

# Check for LDAP

if test "$enables_hed" = "yes"; then
LDAP=no
AC_ARG_ENABLE(ldap, AC_HELP_STRING([--disable-ldap], [disable the LDAP support - requires OpenLDAP]),[enables_ldap="$enableval"],[])
if test "x$enables_ldap" = "xyes"; then
  AC_CHECK_HEADER(ldap.h, [
    LDAP=yes

    SAVE_LDFLAGS=$LDFLAGS
    LDFLAGS=-lpthread

    AC_CHECK_LIB([ldap_r], [ldap_first_message], [
      AC_CHECK_LIB([ldap_r], [ldap_initialize], [
        AC_DEFINE(HAVE_LDAP_INITIALIZE,[],[Define if you have ldap_initialize function])
      ])
      LDAP_LIBS=-lldap_r ], [
      AC_CHECK_LIB([ldap], [ldap_first_message], [
        AC_CHECK_LIB([ldap], [ldap_initialize], [ AC_DEFINE(HAVE_LDAP_INITIALIZE,[],[Define if you have ldap_initialize function])
      ])
      LDAP_LIBS=-lldap ], [
      LDAP=no
    ])
  ])
  AC_CHECK_LIB([lber], [ber_init], [LDAP_LIBS="$LDAP_LIBS -llber"], [])
  AC_SUBST(LDAP_LIBS)
  LDFLAGS=$SAVE_LDFLAGS
  ],

  [
    LDAP=no
  ])

  enables_ldap="$LDAP"
fi
else
  enables_ldap="no"
fi
AM_CONDITIONAL([LDAP_ENABLED], test x$LDAP = xyes)
if test "x$LDAP" = "xyes"; then
  AC_DEFINE(HAVE_LDAP,[],[Define if OpenLDAP is available])
fi

# Check version of Test::More Perl module.
min_perl_test_more_version_required="0.88" # Stable version of Test::More containing done_testing sub.
PERL_TEST_DIR=
perl_test_more_version_found=$(perl -MTest::More -e "print \"\$Test::More::VERSION\"")
if test $(echo "$perl_test_more_version_found" | cut -d. -f1) -gt $(echo "$min_perl_test_more_version_required" | cut -d. -f1) || \
   test $(echo "$perl_test_more_version_found" | cut -d. -f1) -eq $(echo "$min_perl_test_more_version_required" | cut -d. -f1) && \
   test $(echo "$perl_test_more_version_found" | cut -d. -f2) -ge $(echo "$min_perl_test_more_version_required" | cut -d. -f2); then
  PERL_TEST_DIR="test"
fi
AC_SUBST(PERL_TEST_DIR)

# Check for the Perl module Inline::Python - temporary during rewrite.
PERL5LIB_INLINE_PYTHON=
INLINE_PYTHON_FOUND=no
AC_ARG_WITH(inline-python,
  AC_HELP_STRING([--with-inline-python=<PATH>], [Location of the Perl module Inline::Python.]),
  [if test "$with_inline_python" = "yes"
   then
     PERL5LIB_INLINE_PYTHON=
     if ${PERL} -e "use Inline::Python; exit;" > /dev/null 2>&1
     then
       INLINE_PYTHON_FOUND="yes"
       AC_MSG_NOTICE([Perl module Inline::Python found])
     else
       AC_MSG_ERROR([Perl module Inline::Python not found])
     fi
   elif test "$with_inline_python" = "no"
   then
     AC_MSG_NOTICE([Disabling PYTHON LRMS])
   else
     PERL5LIB_INLINE_PYTHON="$with_inline_python"
     if test -d $PERL5LIB_INLINE_PYTHON; then
       PERL5LIB_INLINE_PYTHON="-I${PERL5LIB_INLINE_PYTHON}"
       if `${PERL} ${PERL5LIB_INLINE_PYTHON} -e "use Inline::Python; exit;" > /dev/null 2>&1`
       then    
         INLINE_PYTHON_FOUND="yes"
         AC_MSG_NOTICE([Perl module Inline::Python found])
       else
         AC_MSG_ERROR([--with-inline-python given, but test failed: PERL5LIB_INLINE_PYTHON=${PERL5LIB_INLINE_PYTHON}])
       fi
     fi
   fi
   ],[
   if `${PERL} -e "use Inline::Python; exit;" > /dev/null 2>&1`
   then
     INLINE_PYTHON_FOUND="yes"
     AC_MSG_NOTICE([Perl module Inline::Python found])
   else
     AC_MSG_NOTICE([Perl module Inline::Python not found])
   fi]
)
AC_SUBST(PERL5LIB_INLINE_PYTHON)
AM_CONDITIONAL([PYTHON_LRMS_ENABLED],[test "x${INLINE_PYTHON_FOUND}" = "xyes"])


# Check for the uuid lib
UUID_LIBS=""
if test "$enables_hed" = "yes"; then
AC_CHECK_HEADER(uuid/uuid.h, [
  AC_CHECK_FUNC([uuid_generate], [UUID_LIBS=], [
    AC_CHECK_LIB([uuid], [uuid_generate], [UUID_LIBS=-luuid], [
      AC_MSG_NOTICE([Can't find library containing uuid implementation])
    ])
  ])
], [AC_MSG_NOTICE([Can't find uuid header])])
AC_SUBST(UUID_LIBS)
LIBS="$LIBS $UUID_LIBS"
fi

# Check for dlopen
DLOPEN_LIBS=""
if test "$enables_hed" = "yes"; then
AC_CHECK_FUNC([dlopen], [DLOPEN_LIBS=], [
  AC_CHECK_LIB([dl], [dlopen], [DLOPEN_LIBS=-ldl], [
    AC_MSG_NOTICE([Can't find library containing dlopen implementation])
  ])
])
AC_SUBST(DLOPEN_LIBS)
fi

# Check for clock_gettime
AC_SEARCH_LIBS([clock_gettime], [rt])

# check for fsusage
if test "$enables_hed" = "yes"; then
gl_FSUSAGE
fi


if test "$enables_hed" = "yes"; then

# Checks for header files.
AC_HEADER_DIRENT
AC_HEADER_STDC
AC_HEADER_SYS_WAIT
AC_CHECK_HEADERS([arpa/inet.h fcntl.h float.h limits.h netdb.h netinet/in.h sasl.h sasl/sasl.h stdint.h stdlib.h string.h sys/file.h sys/socket.h sys/vfs.h unistd.h uuid/uuid.h getopt.h])
AC_CXX_HAVE_SSTREAM

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_C_CONST
AC_TYPE_UID_T
AC_C_INLINE
AC_TYPE_MODE_T
AC_TYPE_OFF_T
AC_TYPE_PID_T
AC_TYPE_SIZE_T
AC_CHECK_MEMBERS([struct stat.st_blksize])
AC_HEADER_TIME
AC_STRUCT_TM
AC_CHECK_TYPES([ptrdiff_t])

# Checks for library functions.
AC_FUNC_CHOWN
AC_FUNC_CLOSEDIR_VOID
AC_FUNC_ERROR_AT_LINE
AC_FUNC_FORK
AC_FUNC_LSTAT
AC_FUNC_LSTAT_FOLLOWS_SLASHED_SYMLINK
AC_FUNC_MEMCMP
AC_FUNC_MKTIME
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_FUNC_SELECT_ARGTYPES
AC_TYPE_SIGNAL
AC_FUNC_STRERROR_R
AC_FUNC_STAT
AC_CHECK_FUNCS([acl dup2 floor ftruncate gethostname getdomainname getpid gmtime_r lchown localtime_r memchr memmove memset mkdir mkfifo regcomp rmdir select setenv socket strcasecmp strchr strcspn strdup strerror strncasecmp strstr strtol strtoul strtoull timegm tzset unsetenv getopt_long_only getgrouplist mkdtemp posix_fallocate readdir_r [mkstemp] mktemp])
AC_CHECK_LIB([resolv], [res_query], [LIBRESOLV=-lresolv], [LIBRESOLV=])
AC_CHECK_LIB([resolv], [__dn_skipname], [LIBRESOLV=-lresolv], [LIBRESOLV=])
AC_CHECK_LIB([nsl], [gethostbyname], [LIBRESOLV="$LIBRESOLV -lnsl"], [])
AC_CHECK_LIB([nsl], [getdomainname])
AC_SUBST(LIBRESOLV)

fi

# check for platfom specific flags
case " $LDFLAGS " in
     " -Wl,--no-undefined ") ;;
     " -Wl,-no-undefined ") ;;
     " -Wl,-z -Wl,defs ") ;;
     " -Wl,-z,defs ") ;;
     *)
        case "${host}" in
            *darwin*);;
            *) LDFLAGS="$LDFLAGS -Wl,--no-undefined" ;;
        esac
        ;;
esac

AC_PATH_PROGS(PDFLATEX, pdflatex)
AC_PATH_PROGS(DOXYGEN, doxygen)
AC_PATH_PROGS(DOT, dot)

# Check if user asks to skip documentation build
AC_ARG_ENABLE(doc, AC_HELP_STRING([--disable-doc], [disable building documentation (requires doxygen and pdflatex)]),[enables_doc=$enableval],[])
#if test "x$enables_doc" = "xyes"; then
#  There is no point disabling docs due to missing tools since the pdf
#  files are both in svn and in the dist tarball
#  if test "x$PDFLATEX" = "x"; then
#    enables_doc="no"
#    AC_MSG_NOTICE([WARNING: Missing pdflatex - documentation won't be built])
#  elif test "x$DOXYGEN" = "x"; then
#    enables_doc="no"
#    AC_MSG_NOTICE([WARNING: Missing doxygen - documentation won't be built])
#  elif test "x$DOT" = "x"; then
#    enables_doc="no"
#    AC_MSG_NOTICE([WARNING: Missing dot - documentation won't be built])
#  fi
#fi
AC_MSG_NOTICE([Documentation enabled: $enables_doc])
AM_CONDITIONAL([DOC_ENABLED],[test "x$enables_doc" = "xyes"])

AM_CONDITIONAL([PYDOXYGEN],[test -f python/python/arc/index.xml -o "x$DOXYGEN" != "x"])
AM_CONDITIONAL([ALTPYDOXYGEN],[test -f python/altpython/arc/index.xml -o "x$DOXYGEN" != "x"])

# Check for explicitly and implicitely disabled services
# A-Rex
AC_ARG_ENABLE(a_rex_service, AC_HELP_STRING([--disable-a-rex-service], [disable building A-Rex service]),
  [enables_a_rex_service=$enableval],[])
if test "$enables_a_rex_service" = "yes"; then
  if test "x$SQLITE_INSTALLED" != "xyes" ; then
    AC_MSG_NOTICE([A-Rex can't be built without SQLite - disabling])
    enables_a_rex_service="no"
  elif test "x$DBCXX_LIBS" = "x" ; then
    AC_MSG_NOTICE([A-Rex can't be built without C++ API for DB4.x - disabling])
    enables_a_rex_service="no"
  fi
fi
AC_MSG_NOTICE([A-Rex service enabled: $enables_a_rex_service])
AM_CONDITIONAL([A_REX_SERVICE_ENABLED],[test "x$enables_a_rex_service" = "xyes"])

# Internal job plugin
AC_ARG_ENABLE(internal, AC_HELP_STRING([--enable-internal], [enable building the internal job plugin]),
  [enables_internal=$enableval],[])
if test "$enables_internal" = "yes"; then
  if test "x$enables_a_rex_service" != "xyes" ; then
    AC_MSG_NOTICE([Internal job plugin can't be built without A-Rex - disabling])
    enables_internal="no"
  fi
fi
AC_MSG_NOTICE([Internal plugin enabled: $enables_internal])
AM_CONDITIONAL([INTERNAL_ENABLED],[test "x$enables_internal" = "xyes"])

# Gridftpd
AC_ARG_ENABLE(gridftpd_service, AC_HELP_STRING([--disable-gridftpd-service], [disable building Gridftpd service]),
  [enables_gridftpd_service=$enableval],[])
if test "$enables_gridftpd_service" = "yes"; then
  gridftpd_service_globus_pkgs="globus-common globus-io globus-gsi-credential globus-openssl-module globus-ftp-control"
  gridftpd_service_globus_pkgs_missing=""
  for pkg in $gridftpd_service_globus_pkgs
  do
      var=`echo '$'$pkg|tr '[\-a-z]' '[_A-Z]'|sed 's/$/_VERSION/'`
      if test -z "`eval echo $var`"
      then
        gridftpd_service_globus_pkgs_missing="$gridftpd_service_globus_pkgs_missing $pkg"
      fi
  done


  if test -n "$gridftpd_service_globus_pkgs_missing" ; then
    AC_MSG_NOTICE([GridFTP service can not be built (missing development packages for$gridftpd_service_globus_pkgs_missing) - disabling])
    enables_gridftpd_service="no"
  fi

  #check for struct statfs
  AC_CHECK_FUNCS([fstatfs])
  AC_CHECK_HEADERS([sys/param.h sys/statfs.h sys/mount.h sys/vfs.h])dnl
  AC_CHECK_MEMBERS([struct statfs.f_type],,,
    [$ac_includes_default
     #if HAVE_SYS_STATFS_H
     #include <sys/statfs.h>
     #endif
     #if HAVE_SYS_MOUNT_H
     #include <sys/mount.h>
     #endif
     #if HAVE_SYS_VFS_H
     #include <sys/vfs.h>
     #endif])
fi
AC_MSG_NOTICE([Gridftpd service enabled: $enables_gridftpd_service])
AM_CONDITIONAL([GRIDFTPD_SERVICE_ENABLED],[test "x$enables_gridftpd_service" = "xyes"])

# LDAP service
AC_ARG_ENABLE(ldap_service, AC_HELP_STRING([--disable-ldap-service], [disable building LDAP Infosystem Service]),
  [enables_ldap_service=$enableval],[])

AC_MSG_NOTICE([LDAP Infosystem service enabled: $enables_ldap_service])
AM_CONDITIONAL([LDAP_SERVICE_ENABLED],[test "x$enables_ldap_service" = "xyes"])

# LDAP monitor
AC_ARG_ENABLE(monitor, AC_HELP_STRING([--disable-monitor], [disable building LDAP Monitor]),
  [enables_monitor=$enableval],[])

AC_MSG_NOTICE([LDAP Monitor enabled: $enables_monitor])
AM_CONDITIONAL([MONITOR_ENABLED],[test "x$enables_monitor" = "xyes"])

# Cache service
AC_ARG_ENABLE(candypond, AC_HELP_STRING([--disable-candypond], [disable building candypond]),
  [enables_candypond=$enableval],[])
if test "$enables_candypond" = "yes"; then
  if test ! "x$enables_a_rex_service" = "xyes" ; then
    enables_candypond="no"
    AC_MSG_NOTICE([CandyPond can't be built without A-REX - disabling])
  fi
fi
AC_MSG_NOTICE([CandyPond enabled: $enables_candypond])
AM_CONDITIONAL([CANDYPOND_ENABLED],[test "x$enables_candypond" = "xyes"])

# DataDelivery service
AC_ARG_ENABLE(datadelivery_service, AC_HELP_STRING([--disable-datadelivery-service], [disable building DataDelivery service]),
  [enables_datadelivery_service=$enableval],[])
AC_MSG_NOTICE([DataDelivery service enabled: $enables_datadelivery_service])
AM_CONDITIONAL([DATADELIVERY_SERVICE_ENABLED],[test "x$enables_datadelivery_service" = "xyes"])

# ACIX service
AC_ARG_ENABLE(acix, AC_HELP_STRING([--disable-acix], [disable building ACIX service]),
  [enables_acix=$enableval],[])
AC_PATH_PROGS(TWISTD, twistd-${PYTHON_MAJOR} twistd${PYTHON_MAJOR} twistd)
if test "x$TWISTD" = "x"; then
  AC_MSG_NOTICE([twistd not found - ACIX service disabled])
  enables_acix="no"
fi
AC_MSG_NOTICE([ACIX enabled: $enables_acix])
AM_CONDITIONAL([ACIX_ENABLED],[test "x$enables_acix" = "xyes"])

# trial command (from python-twisted-core) is used for acix unittests
AC_PATH_PROGS(TRIAL, trial-${PYTHON_MAJOR} trial${PYTHON_MAJOR} trial)
if test "x$TRIAL" = "x"; then
  AC_MSG_NOTICE([trial not found - ACIX unit tests will be skipped])
fi
# unit tests also require python >=2.6
AM_CONDITIONAL([ACIX_TESTS_ENABLED], [test "x$TRIAL" != "x" && test "x$PYTHON_VERSION" != "x2.4" && test "x$PYTHON_VERSION" != "x2.5"])

# Check for explicitly and implicitely disabled clients
AC_ARG_ENABLE(compute_client, AC_HELP_STRING([--disable-compute-client], [disable building compute (job management) client tools]),
  [enables_compute_client=$enableval],[])
AC_MSG_NOTICE([Compute client tools enabled: $enables_compute_client])
AM_CONDITIONAL([COMPUTE_CLIENT_ENABLED],[test "x$enables_compute_client" = "xyes"])

AC_ARG_ENABLE(credentials_client, AC_HELP_STRING([--disable-credentials-client], [disable building client tools for handling X.509 credentials]),
  [enables_credentials_client=$enableval],[])
AC_MSG_NOTICE([Credentials client tools enabled: $enables_credentials_client])
AM_CONDITIONAL([CREDENTIALS_CLIENT_ENABLED],[test "x$enables_credentials_client" = "xyes"])

AC_ARG_ENABLE(data_client, AC_HELP_STRING([--disable-data-client], [disable building generic client tools for handling data]),
  [enables_data_client=$enableval],[])
AC_MSG_NOTICE([Data client tools enabled: $enables_data_client])
AM_CONDITIONAL([DATA_CLIENT_ENABLED],[test "x$enables_data_client" = "xyes"])

AC_ARG_ENABLE(jura_client, AC_HELP_STRING([--disable-jura-client], [disable building client tool for communicating JURA]),
  [enables_jura_client=$enableval],[])
AC_MSG_NOTICE([JURA client tool enabled: $enables_jura_client])
AM_CONDITIONAL([JURA_CLIENT_ENABLED],[test "x$enables_jura_client" = "xyes"])

AC_ARG_ENABLE(emies_client, AC_HELP_STRING([--disable-emies-client], [disables building EMI ES-related client plugins.]),
  [enables_emies_client=$enableval],[])
AC_MSG_NOTICE([EMI ES plugin(s) enabled: $enables_emies_client])
AM_CONDITIONAL([EMIES_ENABLED],[test "x$enables_emies_client" = "xyes"])

AC_ARG_ENABLE(arcrest_client, AC_HELP_STRING([--disable-arcrest-client], [disables building ARC REST interface client plugins.]),
  [enables_arcrest_client=$enableval],[])
AC_MSG_NOTICE([ARC REST plugin(s) enabled: $enables_arcrest_client])
AM_CONDITIONAL([ARCREST_ENABLED],[test "x$enables_arcrest_client" = "xyes"])

# Check for consistency among disabled components
if test "$enables_hed" = "no"; then
  if test "$enables_a_rex_service" = "yes" -o \
          "$enables_candypond" = "yes" -o \
          "$enables_datadelivery_service" = "yes" -o \
          "$enables_compute_client" = "yes" -o \
          "$enables_credentials_client" = "yes" -o \
          "$enables_data_client" = "yes" -o \
          "$enables_jura_client" = "yes" -o \
          ; then
    AC_MSG_ERROR(HED is needed for building any of the client or service tools. Please enable HED by using --enable-hed.)
  fi
fi
AM_CONDITIONAL([HED_ENABLED],[test "x$enables_hed" = "xyes"])

# A-Rex specific hack for backend scripts

tmp_dir=/tmp
gnu_time=/usr/bin/time

case "${host}" in
    *darwin*)
        # hostname -f does not work on OS X
        nodename="hostname" ;;
    *)
        nodename="/bin/hostname -f" ;;
esac

arc_location=$prefix

AC_SUBST(arc_location)
AC_SUBST(tmp_dir)
AC_SUBST(gnu_time)
AC_SUBST(nodename)

# Shell for the job control scripts
posix_shell='/bin/sh'
AC_SUBST(posix_shell)

DATE=`date +%Y-%m-%d ${SOURCE_DATE_EPOCH:+-u -d @$SOURCE_DATE_EPOCH}`
AC_SUBST(DATE)
#DATER=`date -R`
DATER=`date +'%a, %d %b %Y %H:%M:%S %z'`
AC_SUBST(DATER)
SPECDATE=`LANG=C date +"%a %b %d %Y"`
AC_SUBST(SPECDATE)

AC_CONFIG_FILES([Makefile
                 include/arc/ArcVersion.h
                 src/Makefile
                 src/external/Makefile
                 src/external/cJSON/Makefile
                 src/hed/Makefile
                 src/hed/libs/compute/Makefile
                 src/hed/libs/compute/test/Makefile
                 src/hed/libs/compute/examples/Makefile
                 src/hed/libs/common/ArcVersion.h
                 src/hed/libs/common/Makefile
                 src/hed/libs/common/test/Makefile
                 src/hed/libs/communication/Makefile
                 src/hed/libs/credential/Makefile
                 src/hed/libs/credential/test/Makefile
                 src/hed/libs/credentialmod/Makefile
                 src/hed/libs/crypto/Makefile
                 src/hed/libs/cryptomod/Makefile
                 src/hed/libs/data/Makefile
                 src/hed/libs/data/cache-clean.1
                 src/hed/libs/data/cache-list.1
                 src/hed/libs/data/test/Makefile
                 src/hed/libs/data/examples/Makefile
                 src/hed/libs/Makefile
                 src/hed/libs/loader/Makefile
                 src/hed/libs/loader/schema/Makefile
                 src/hed/libs/loader/test/Makefile
                 src/hed/libs/message/Makefile
                 src/hed/libs/message/test/Makefile
                 src/hed/libs/security/Makefile
                 src/hed/libs/security/ArcPDP/Makefile
                 src/hed/libs/security/ArcPDP/attr/Makefile
                 src/hed/libs/security/ArcPDP/policy/Makefile
                 src/hed/libs/security/ArcPDP/alg/Makefile
                 src/hed/libs/security/ArcPDP/fn/Makefile
                 src/hed/libs/credentialstore/Makefile
                 src/hed/libs/ws-addressing/Makefile
                 src/hed/libs/ws-security/Makefile
                 src/hed/libs/ws-security/test/Makefile
                 src/hed/libs/infosys/Makefile
                 src/hed/libs/infosys/schema/Makefile
                 src/hed/libs/infosys/test/Makefile
                 src/hed/libs/delegation/Makefile
                 src/hed/libs/delegation/test/Makefile
                 src/hed/libs/xmlsec/Makefile
                 src/hed/libs/globusutils/Makefile
                 src/hed/libs/scitokens/Makefile
                 src/hed/daemon/Makefile
                 src/hed/daemon/scripts/Makefile
                 src/hed/daemon/schema/Makefile
                 src/hed/daemon/unix/Makefile
                 src/hed/mcc/Makefile
                 src/hed/mcc/soap/Makefile
                 src/hed/mcc/tcp/Makefile
                 src/hed/mcc/tcp/schema/Makefile
                 src/hed/mcc/http/Makefile
                 src/hed/mcc/http/schema/Makefile
                 src/hed/mcc/tls/Makefile
                 src/hed/mcc/tls/schema/Makefile
                 src/hed/mcc/msgvalidator/Makefile
                 src/hed/mcc/msgvalidator/schema/Makefile
                 src/hed/acc/Makefile
                 src/hed/acc/GRIDFTPJOB/Makefile
                 src/hed/acc/ARCREST/Makefile
                 src/hed/acc/EMIES/Makefile
                 src/hed/acc/EMIES/arcemiestest.1
                 src/hed/acc/EMIES/schema/Makefile
                 src/hed/acc/Broker/Makefile
                 src/hed/acc/Broker/test/Makefile
                 src/hed/acc/PythonBroker/Makefile
                 src/hed/acc/JobDescriptionParser/Makefile
                 src/hed/acc/JobDescriptionParser/test/Makefile
                 src/hed/acc/ARCHERY/Makefile
                 src/hed/acc/LDAP/Makefile
                 src/hed/acc/TEST/Makefile
                 src/hed/dmc/Makefile
                 src/hed/dmc/file/Makefile
                 src/hed/dmc/gridftp/Makefile
                 src/hed/dmc/http/Makefile
                 src/hed/dmc/ldap/Makefile
                 src/hed/dmc/srm/Makefile
                 src/hed/dmc/srm/srmclient/Makefile
                 src/hed/dmc/gfal/Makefile
                 src/hed/dmc/xrootd/Makefile
                 src/hed/dmc/mock/Makefile
                 src/hed/dmc/acix/Makefile
                 src/hed/dmc/rucio/Makefile
                 src/hed/dmc/s3/Makefile
                 src/hed/profiles/general/general.xml
                 src/hed/shc/Makefile
                 src/hed/shc/arcpdp/Makefile
                 src/hed/shc/arcpdp/schema/Makefile
                 src/hed/shc/xacmlpdp/Makefile
                 src/hed/shc/xacmlpdp/schema/Makefile
                 src/hed/shc/delegationpdp/Makefile
                 src/hed/shc/delegationpdp/schema/Makefile
                 src/hed/shc/gaclpdp/Makefile
                 src/hed/shc/pdpserviceinvoker/Makefile
                 src/hed/shc/pdpserviceinvoker/schema/Makefile
                 src/hed/shc/allowpdp/Makefile
                 src/hed/shc/denypdp/Makefile
                 src/hed/shc/simplelistpdp/Makefile
                 src/hed/shc/simplelistpdp/schema/Makefile
                 src/hed/shc/arcauthzsh/Makefile
                 src/hed/shc/arcauthzsh/schema/Makefile
                 src/hed/shc/usernametokensh/Makefile
                 src/hed/shc/usernametokensh/schema/Makefile
                 src/hed/shc/x509tokensh/Makefile
                 src/hed/shc/x509tokensh/schema/Makefile
                 src/hed/shc/samltokensh/Makefile
                 src/hed/shc/samltokensh/schema/Makefile
                 src/hed/shc/saml2sso_assertionconsumersh/Makefile
                 src/hed/shc/delegationsh/Makefile
                 src/hed/shc/delegationsh/schema/Makefile
                 src/hed/shc/legacy/Makefile
                 src/hed/shc/legacy/schema/Makefile
                 src/hed/identitymap/Makefile
                 src/hed/identitymap/schema/Makefile
                 src/libs/Makefile
                 src/libs/data-staging/Makefile
                 src/libs/data-staging/test/Makefile
                 src/libs/data-staging/examples/Makefile
                 src/services/Makefile
                 src/services/a-rex/Makefile
                 src/services/a-rex/arc-arex
                 src/services/a-rex/arc-arex.service
                 src/services/a-rex/arc-arex-start
                 src/services/a-rex/a-rex-backtrace-collect
                 src/services/a-rex/a-rex-backtrace-collect.8
                 src/services/a-rex/perferator
                 src/services/a-rex/grid-manager/arc-blahp-logger.8
                 src/services/a-rex/grid-manager/gm-jobs.8
                 src/services/a-rex/grid-manager/gm-delegations-converter.8
                 src/services/a-rex/delegation/Makefile
                 src/services/a-rex/grid-manager/Makefile
                 src/services/a-rex/grid-manager/conf/Makefile
                 src/services/a-rex/grid-manager/files/Makefile
                 src/services/a-rex/grid-manager/jobs/Makefile
                 src/services/a-rex/grid-manager/jobplugin/Makefile
                 src/services/a-rex/grid-manager/log/Makefile
                 src/services/a-rex/grid-manager/mail/Makefile
                 src/services/a-rex/grid-manager/misc/Makefile
                 src/services/a-rex/grid-manager/run/Makefile
                 src/services/a-rex/internaljobplugin/Makefile
                 src/services/a-rex/grid-manager/arc-config-check.1
                 src/services/a-rex/infoproviders/Makefile
                 src/services/a-rex/infoproviders/CEinfo.pl
                 src/services/a-rex/infoproviders/ConfigCentral.pm
                 src/services/a-rex/infoproviders/PerfData.pl
                 src/services/a-rex/infoproviders/test/Makefile
                 src/services/a-rex/jura/Makefile
                 src/services/a-rex/jura/jura.1
                 src/services/a-rex/jura/ssm/Makefile
                 src/services/a-rex/jura/ssm/ssmsend
                 src/services/a-rex/lrms/Makefile
                 src/services/a-rex/lrms/test/Makefile
                 src/services/a-rex/lrms/arc/Makefile
                 src/services/a-rex/lrms/arc/lrms/Makefile
                 src/services/a-rex/lrms/arc/lrms/common/Makefile
                 src/services/a-rex/lrms/lrms_common.sh
                 src/services/a-rex/lrms/condor/Makefile
                 src/services/a-rex/lrms/condor/scan-condor-job
                 src/services/a-rex/lrms/condor/cancel-condor-job
                 src/services/a-rex/lrms/condor/submit-condor-job
                 src/services/a-rex/lrms/fork/Makefile
                 src/services/a-rex/lrms/fork/scan-fork-job
                 src/services/a-rex/lrms/fork/submit-fork-job
                 src/services/a-rex/lrms/fork/cancel-fork-job
                 src/services/a-rex/lrms/ll/Makefile
                 src/services/a-rex/lrms/ll/submit-ll-job
                 src/services/a-rex/lrms/ll/cancel-ll-job
                 src/services/a-rex/lrms/ll/scan-ll-job
                 src/services/a-rex/lrms/lsf/Makefile
                 src/services/a-rex/lrms/lsf/submit-lsf-job
                 src/services/a-rex/lrms/lsf/cancel-lsf-job
                 src/services/a-rex/lrms/lsf/scan-lsf-job
                 src/services/a-rex/lrms/pbs/Makefile
                 src/services/a-rex/lrms/pbs/submit-pbs-job
                 src/services/a-rex/lrms/pbs/cancel-pbs-job
                 src/services/a-rex/lrms/pbs/scan-pbs-job
                 src/services/a-rex/lrms/pbspro/Makefile
                 src/services/a-rex/lrms/pbspro/submit-pbspro-job
                 src/services/a-rex/lrms/pbspro/cancel-pbspro-job
                 src/services/a-rex/lrms/pbspro/scan-pbspro-job
                 src/services/a-rex/lrms/sge/Makefile
                 src/services/a-rex/lrms/sge/submit-sge-job
                 src/services/a-rex/lrms/sge/scan-sge-job
                 src/services/a-rex/lrms/sge/cancel-sge-job
                 src/services/a-rex/lrms/slurm/Makefile
                 src/services/a-rex/lrms/slurm/submit-SLURM-job
                 src/services/a-rex/lrms/slurm/scan-SLURM-job
                 src/services/a-rex/lrms/slurm/cancel-SLURM-job
                 src/services/a-rex/lrms/slurm/test/Makefile
                 src/services/a-rex/lrms/slurm/test/scan/Makefile
                 src/services/a-rex/lrms/slurm/test/submit/Makefile
                 src/services/a-rex/lrms/boinc/Makefile
                 src/services/a-rex/lrms/boinc/submit-boinc-job
                 src/services/a-rex/lrms/boinc/scan-boinc-job
                 src/services/a-rex/lrms/boinc/cancel-boinc-job
                 src/services/a-rex/lrms/slurmpy/Makefile
                 src/services/a-rex/lrms/slurmpy/submit-SLURMPY-job
                 src/services/a-rex/lrms/slurmpy/scan-SLURMPY-job
                 src/services/a-rex/lrms/slurmpy/cancel-SLURMPY-job
                 src/services/a-rex/lrms/slurmpy/test/Makefile
                 src/services/a-rex/lrms/slurmpy/test/submit/Makefile
                 src/services/a-rex/lrms/slurmpy/test/scan/Makefile
                 src/services/a-rex/rte/Makefile
                 src/services/a-rex/rte/ENV/PROXY
                 src/services/a-rex/rte/ENV/CANDYPOND
                 src/services/a-rex/schema/Makefile
                 src/services/acix/Makefile
                 src/services/acix/scanner/Makefile
                 src/services/acix/scanner/arc-acix-scanner
                 src/services/acix/scanner/arc-acix-scanner-start
                 src/services/acix/scanner/arc-acix-scanner.service
                 src/services/acix/scanner/test/Makefile
                 src/services/acix/core/Makefile
                 src/services/acix/core/test/Makefile
                 src/services/acix/indexserver/Makefile
                 src/services/acix/indexserver/arc-acix-index
                 src/services/acix/indexserver/arc-acix-index-start
                 src/services/acix/indexserver/arc-acix-index.service
                 src/services/acix/indexserver/test/Makefile
                 src/services/candypond/Makefile
                 src/services/data-staging/Makefile
                 src/services/data-staging/arc-datadelivery-service
                 src/services/data-staging/arc-datadelivery-service.service
                 src/services/data-staging/arc-datadelivery-service-start
                 src/services/gridftpd/Makefile
                 src/services/gridftpd/arc-gridftpd
                 src/services/gridftpd/arc-gridftpd.service
                 src/services/gridftpd/arc-gridftpd-start
                 src/services/gridftpd/gridftpd.8
                 src/services/gridftpd/auth/Makefile
                 src/services/gridftpd/conf/Makefile
                 src/services/gridftpd/misc/Makefile
                 src/services/gridftpd/run/Makefile
                 src/services/gridftpd/fileplugin/Makefile
                 src/services/ldap-infosys/Makefile
                 src/services/ldap-infosys/create-bdii-config
                 src/services/ldap-infosys/create-slapd-config
                 src/services/ldap-infosys/arc-infosys-ldap
                 src/services/ldap-infosys/arc-infosys-ldap.service
                 src/services/ldap-infosys/arc-infosys-ldap-slapd.service
                 src/services/monitor/Makefile
                 src/services/monitor/monitor
                 src/services/monitor/README
                 src/services/monitor/man/Makefile
                 src/services/monitor/man/monitor.7
                 src/services/monitor/includes/Makefile
                 src/services/monitor/mon-icons/Makefile
                 src/services/monitor/lang/Makefile
                 src/services/examples/Makefile
                 src/services/examples/echo_python/Makefile
                 src/services/wrappers/Makefile
                 src/services/wrappers/python/Makefile
                 src/services/wrappers/python/schema/Makefile
                 src/clients/Makefile
                 src/clients/data/Makefile
                 src/clients/data/arccp.1
                 src/clients/data/arcls.1
                 src/clients/data/arcrm.1
                 src/clients/data/arcmkdir.1
                 src/clients/data/arcrename.1
                 src/clients/credentials/Makefile
                 src/clients/credentials/arcproxy.1
                 src/clients/compute/Makefile
                 src/clients/compute/arcstat.1
                 src/clients/compute/arcinfo.1
                 src/clients/compute/arcsub.1
                 src/clients/compute/arcclean.1
                 src/clients/compute/arckill.1
                 src/clients/compute/arcget.1
                 src/clients/compute/arccat.1
                 src/clients/compute/arcresub.1
                 src/clients/compute/arcsync.1
                 src/clients/compute/arcrenew.1
                 src/clients/compute/arcresume.1
                 src/clients/compute/arctest.1
                 src/tests/Makefile
                 src/tests/echo/Makefile
                 src/tests/echo/perftest.1
                 src/tests/echo/echo_service.xml.example
                 src/tests/echo/schema/Makefile
                 src/tests/policy-delegation/Makefile
                 src/tests/delegation/Makefile
                 src/tests/translator/Makefile
                 src/tests/xpath/Makefile
                 src/tests/arcpolicy/Makefile
                 src/tests/perf/Makefile
                 src/tests/perf/arcperftest.1
                 src/tests/client/Makefile
                 src/tests/lrms/Makefile
                 src/utils/archery/Makefile
                 src/utils/archery/archery-manage
                 src/utils/python/Makefile
                 src/utils/python/arccandypond
                 src/utils/python/arcctl
                 src/utils/python/arcctl.1
                 src/utils/python/jura-archive-manager
                 src/utils/python/arc/Makefile
                 src/utils/python/arc/gen_paths_dist.sh
                 src/utils/python/arc/utils/Makefile
                 src/utils/python/arc/control/Makefile
                 src/utils/hed/wsdl2hed.1
                 src/utils/hed/arcplugin.1
                 src/utils/hed/Makefile
                 src/utils/gridmap/nordugridmap.cron
                 src/utils/gridmap/nordugridmap.8
                 src/utils/gridmap/Makefile
                 src/utils/Makefile
                 src/wn/Makefile
                 src/doc/Makefile
                 src/doc/arc.conf.5
                 swig/Makefile
                 python/Makefile
                 python/Doxyfile.api
                 python/python/Makefile
                 python/python/arc/Makefile
                 python/altpython/Makefile
                 python/altpython/arc/Makefile
                 python/test/Makefile
                 python/test/python/Makefile
                 python/test/altpython/Makefile
                 python/examples/Makefile
                 po/Makefile.in
                 include/Makefile
                 debian/Makefile
                 debian/changelog.deb
                 nordugrid-arc.spec
                 src/hed/daemon/arched.8
                 src/hed/daemon/scripts/arched
                 src/hed/daemon/scripts/arched.service
                 src/hed/daemon/scripts/arched-start
                 src/doxygen/Makefile
])
AC_CONFIG_FILES([src/utils/python/arcconfig-parser],
       [chmod +x src/utils/python/arcconfig-parser])
AC_OUTPUT

AC_MSG_RESULT([
Unit testing:       ${enables_cppunit}
Python binding:     ${enables_swig_python} ($PYTHON_VERSION)
Alt.Python binding: ${enables_altpython} ($ALTPYTHON_VERSION)

Available third-party features:

GridFTP:            ${enables_gridftp}
GFAL:               ${enables_gfal}
S3:                 ${enables_s3}
Xrootd:             ${enables_xrootd}
MYSQL CLIENT LIB:   ${enables_mysql}
LDAP:               ${enables_ldap}
xmlsec1:            ${enables_xmlsec1}
ARGUS:              ${enables_argus}
NSS:                ${enables_nss}
BDB C++:            ${enables_dbcxx}
SQLite:             ${enables_sqlite}
LDNS:               ${enables_ldns}

Enabled features:

Local jobs info in BDB:    ${enables_dbjstore}
Local jobs info in SQLite: ${enables_sqlitejstore}
Systemd Integration:       ${enables_systemd}

Python LRMS back-end dependency:
Inline::Python Perl module: ${INLINE_PYTHON_FOUND}

Included components:
HED:                ${enables_hed}

A-REX service:      ${enables_a_rex_service}
Internal plugin:    ${enables_internal}
GRIDFTPD service:   ${enables_gridftpd_service}
LDAP Info service:  ${enables_ldap_service}
CANDYPOND service:  ${enables_candypond}
DATADELIVERY service: ${enables_datadelivery_service}
ACIX service:       ${enables_acix}

COMPUTE clients:    ${enables_compute_client}
DATA clients:       ${enables_data_client}
CREDENTIAL clients: ${enables_credentials_client}
JURA client:        ${enables_jura_client}

EMI ES client (ACC): ${enables_emies_client}
ARC REST client (ACC): ${enables_arcrest_client}
SRM client (DMC):   ${enables_srm_dmc}

Documentation:      ${enables_doc}

Monitoring:
LDAP Monitor        ${enables_monitor}
])

