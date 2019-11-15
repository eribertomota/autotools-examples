#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT(mod_musicindex, 1.4.1, musicindex@slashdirt.org)
AC_CONFIG_SRCDIR([src/mod_musicindex.c])
AC_CONFIG_HEADER([mod_musicindex_config.h])
AC_CONFIG_MACRO_DIR([m4])

AC_CANONICAL_HOST

AM_INIT_AUTOMAKE()
# Checks for programs.
AC_PROG_CC
AM_PROG_CC_STDC
AC_PROG_CC_C99
AC_HEADER_STDC
AC_PROG_INSTALL
AC_CHECK_TOOL([STRIP],[strip])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_C_RESTRICT
AC_C_INLINE
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T
AC_STRUCT_TM

#Check if the compiler support attributes
AH_TEMPLATE([C_HAS_ATTRIBUTE],[Determines if the compilers supports attributes for structures.])
AC_MSG_CHECKING(whether the C compiler allows __attribute__)
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([[
typedef struct { } __attribute__((packed)) junk;]],
[[ ]])],[ AC_MSG_RESULT(yes);AC_DEFINE(C_HAS_ATTRIBUTE)],AC_MSG_RESULT(no))

#Check if the compiler supports __builtin_expect
AH_TEMPLATE([C_HAS_BUILTIN_EXPECT],[Determines if the compilers supports __builtin_expect for branch prediction.])
AC_MSG_CHECKING(whether the C compiler allows __builtin_expect)
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([[]],[[
int x=10;if( __builtin_expect ((x==1),0) ) ;
]])], [ AC_MSG_RESULT(yes);AC_DEFINE(C_HAS_BUILTIN_EXPECT)],AC_MSG_RESULT(no))

# Checks for library functions.
AC_CHECK_HEADERS([sys/time.h])
AC_FUNC_CLOSEDIR_VOID
AC_FUNC_MALLOC
AC_CHECK_FUNCS([setlocale strcasecmp strchr strncasecmp strrchr strstr gettimeofday timersub])

AM_GNU_GETTEXT([external])
#AM_GNU_GETTEXT_VERSION(0.14.5)

AC_DISABLE_STATIC
AC_PROG_LIBTOOL

#check if the user has a prefered apxs tool. by default, use apxs
AC_ARG_WITH([apxs],
       AC_HELP_STRING([--with-apxs=ARG], [apxs executable]),
       [APXS="${withval}"],
       [APXS="apxs"])

#check if the apxs tool actually exists
if test x$APXS != xnone; then
    AC_PATH_PROG([APXS], [$APXS], [], [$PATH:/usr/sbin:/usr/local/sbin])
fi

#last chance, some systems rename apxs to apxs2 for Apache 2
if test x$APXS = x; then
       AC_PATH_PROG([APXS], [apxs2], [], [$PATH:/usr/sbin:/usr/local/sbin])
fi

if test x$APXS = x; then
       AC_MSG_ERROR([cannot find a working apxs tool])
fi

if test x$APXS != xnone; then
    APXS_CFLAGS="`$APXS -q CFLAGS`"
    APXS_CFLAGS="$APXS_CFLAGS `$APXS -q CFLAGS_SHLIB`"
    APXS_LIBS="`$APXS -q LDFLAGS_SHLIB`"
    APXS_INCLUDE="-I`$APXS -q INCLUDEDIR`"
    libdir="`$APXS -q LIBEXECDIR`"
fi

AC_SUBST(APXS_CFLAGS)
AC_SUBST(APXS_LIBS)
AC_SUBST(APXS_INCLUDE)

AC_MSG_CHECKING([for which version of Apache we should build])

################################
ac_save_CFLAGS="$CFLAGS"
CFLAGS="$CFLAGS $APXS_INCLUDE"
cat >conftest.$ac_ext <<_ACEOF
#include <stdio.h>
#include <ap_mmn.h>

int main(void)
{
#if (MODULE_MAGIC_COOKIE == 0x41503133UL)
	printf("AP13\n");
#elif (MODULE_MAGIC_COOKIE == 0x41503230UL)
	printf("AP20\n");
#elif (MODULE_MAGIC_COOKIE == 0x41503232UL)
	printf("AP22\n");
#elif (MODULE_MAGIC_COOKIE == 0x41503234UL)
	printf("AP24\n");
#endif
}
_ACEOF
rm -f conftest.$ac_objext conftest$ac_exeext
if { (eval echo "$as_me:$LINENO: \"$ac_link\"") >&5
  (eval $ac_link) 2>conftest.er1
  ac_status=$?
  grep -v '^ *+' conftest.er1 >conftest.err
  rm -f conftest.er1
  cat conftest.err >&5
  echo "$as_me:$LINENO: \$? = $ac_status" >&5
  (exit $ac_status); } &&
	 { ac_try='test -z "$ac_c_werror_flag"			 || test ! -s conftest.err'
  { (eval echo "$as_me:$LINENO: \"$ac_try\"") >&5
  (eval $ac_try) 2>&5
  ac_status=$?
  echo "$as_me:$LINENO: \$? = $ac_status" >&5
  (exit $ac_status); }; } &&
	 { ac_try='test -s conftest$ac_exeext'
  { (eval echo "$as_me:$LINENO: \"$ac_try\"") >&5
  (eval $ac_try) 2>&5
  ac_status=$?
  echo "$as_me:$LINENO: \$? = $ac_status" >&5
  (exit $ac_status); }; }; then
  apache_version=`./conftest$ac_exeext`
else
  echo "$as_me: failed program was:" >&5
sed 's/^/| /' conftest.$ac_ext >&5

ac_cv_lib_mad_mad_bit_init=no
fi
rm -f conftest.err conftest.$ac_objext \
      conftest$ac_exeext conftest.$ac_ext
CFLAGS=$ac_save_CFLAGS
################################

AC_MSG_RESULT([${apache_version}])

if test x$apache_version = xAP20; then
  AC_CHECK_PROG(APR_CONFIG, apr-config, apr-config, [], [], [exit1])
  AC_DEFINE([AP20], [], ["AP20"])
fi

if test x$apache_version = xAP22; then
  AC_CHECK_PROG(APR_CONFIG, apr-1-config, apr-1-config, [], [], [exit1])
  AC_DEFINE([AP22], [], ["AP22"])
fi

if test x$apache_version = xAP24; then
  AC_CHECK_PROG(APR_CONFIG, apr-1-config, apr-1-config, [], [], [exit1])
  AC_DEFINE([AP24], [], ["AP24"])
fi

if test "x$APR_CONFIG" != "x"; then

AC_DEFINE([BUILD_FOR_APACHE2], [], ["apache2"])
AM_CONDITIONAL(BUILD_FOR_APACHE2, true)

APR_INCLUDE="-I`$APR_CONFIG --includedir`"
AC_SUBST(APR_INCLUDE)
APR_LIBS="`$APR_CONFIG --link-ld`"
AC_SUBST(APR_LIBS)
APR_CFLAGS="`$APR_CONFIG --cflags`"
AC_SUBST(APR_CFLAGS)
APR_CPPFLAGS="`$APR_CONFIG --cppflags`"
AC_SUBST(APR_CPPFLAGS)

else
AM_CONDITIONAL(BUILD_FOR_APACHE2, false)
fi

# Checks for libraries.
##########################################################################

AC_ARG_ENABLE([vorbis],
	AC_HELP_STRING([--disable-vorbis], [Vorbis support]),
	[case "${enableval}" in
	  yes) vorbis=true ;;
	  no)  vorbis=false ;;
	  *) AC_MSG_ERROR(bad value ${enableval} for --enable-vorbis) ;;
	esac],[vorbis=true])

if test x$vorbis = xtrue; then
  XIPH_PATH_VORBIS( [], [echo "*****Coun't find Vorbis libraries, disabling Vorbis support"; vorbis=false])
fi

if test x$vorbis = xtrue; then
  AC_DEFINE([ENABLE_CODEC_VORBIS], [], [vorbis])
fi
AM_CONDITIONAL(ENABLE_CODEC_VORBIS, test x$vorbis = xtrue)

##########################################################################

AC_ARG_ENABLE([flac],
	AC_HELP_STRING([--disable-flac], [FLAC support]),
	[case "${enableval}" in
	  yes) flac=true ;;
	  no)  flac=false ;;
	  *) AC_MSG_ERROR(bad value ${enableval} for --disable-flac) ;;
	esac],[flac=true])

if test x$flac = xtrue; then
 AM_PATH_LIBFLAC( [], [echo "*****Coun't find FLAC library, disabling FLAC support"; flac=false])
fi

if test x$flac = xtrue; then
 AC_DEFINE([ENABLE_CODEC_FLAC], [], [flac])
fi
AM_CONDITIONAL(ENABLE_CODEC_FLAC, test x$flac = xtrue)

##########################################################################

AC_ARG_ENABLE([mp3],
	AC_HELP_STRING([--disable-mp3], [MP3 support]),
	[case "${enableval}" in
	  yes) mp3=true ;;
	  no)  mp3=false ;;
	  *) AC_MSG_ERROR(bad value ${enableval} for --disable-mp3) ;;
	esac],[mp3=true])

if test x$mp3 = xtrue; then
  AC_CHECK_LIB(mad, mad_bit_init, [MAD_LIBS="-lmad"], [echo "*****Coun't find libMAD, disabling MP3 support"; mp3=false])
  AC_CHECK_LIB(id3tag, id3_file_open, [ID3TAG_LIBS="-lid3tag"], [MAD_LIBS=""; echo "*****Coun't find libid3tag, disabling MP3 support"; mp3=false])
fi
AC_SUBST(MAD_LIBS)
AC_SUBST(ID3TAG_LIBS)

if test x$mp3 = xtrue; then
  AC_DEFINE([ENABLE_CODEC_MP3], [], ["mp3"])
fi
AM_CONDITIONAL(ENABLE_CODEC_MP3, test x$mp3 = xtrue)

##########################################################################

AC_ARG_ENABLE([mp4],
	AC_HELP_STRING([--disable-mp4], [MP4 support]),
	[case "${enableval}" in
	  yes) mp4=true ;;
	  no)  mp4=false ;;
	  *) AC_MSG_ERROR(bad value ${enableval} for --disable-mp4) ;;
	esac],[mp4=true])

if test x$mp4 = xtrue; then
  AC_CHECK_LIB(mp4v2, MP4GetNumberOfTracks, [], [echo "*****Coun't find libMP4, disabling MP4 support"; mp4=false])
fi

if test x$mp4 = xtrue; then
  AC_DEFINE([ENABLE_CODEC_MP4], [], ["mp4"])
fi
AM_CONDITIONAL(ENABLE_CODEC_MP4, test x$mp4 = xtrue)

##########################################################################

AC_ARG_ENABLE([archive],
	AC_HELP_STRING([--disable-archive], [archive support]),
	[case "${enableval}" in
	  yes) archive=true ;;
	  no)  archive=false ;;
	  *) AC_MSG_ERROR(bad value ${enableval} for --disable-archive) ;;
	esac],[archive=true])

if test x$archive = xtrue; then
  AC_CHECK_LIB(archive, archive_write_new, [], [echo "*****Coun't find libarchive, disabling archive support"; archive=false])
fi

if test x$archive = xtrue; then
  AC_DEFINE([ENABLE_OUTPUT_ARCHIVE], [], ["archive"])
fi
AM_CONDITIONAL(ENABLE_OUTPUT_ARCHIVE, test x$archive = xtrue)

##########################################################################

AC_ARG_ENABLE([filecache],
	AC_HELP_STRING([--disable-filecache], [File cache support]),
	[case "${enableval}" in
	  yes) filecache=true ;;
	  no)  filecache=false ;;
	  *) AC_MSG_ERROR(bad value ${enableval} for --disable-filecache) ;;
	esac],[filecache=true])

case $host_os in
	solaris*)
		echo "*****Flat file cache system is not supported on this system, disabling it"
		filecache=false
		;;
esac

if test x$filecache = xtrue; then
#need to tweak cache-file.c to use these, and eventually disable cache if
#some return bogus values
AC_HEADER_DIRENT
AC_HEADER_STAT
AC_FUNC_STAT
AC_CHECK_FUNCS([fchdir mkdir rmdir strcspn], [], [filecache=false])
fi

if test x$filecache = xtrue; then
  AC_DEFINE([ENABLE_CACHE_FILE], [], ["cache"])
fi
AM_CONDITIONAL(ENABLE_CACHE_FILE, test x$filecache = xtrue)

##########################################################################

#check if the user has a prefered mysql_config tool. by default, use mysql_config
AC_ARG_WITH([mysql_config],
	AC_HELP_STRING([--with-mysql_config=ARG], [mysql_config executable]),
	[MYSQL_CONFIG="${withval}"],
	[MYSQL_CONFIG="mysql_config"])

#check if the mysql_config tool actually exists
if test x$MYSQL_CONFIG != xnone; then
	AC_PATH_PROG([MYSQL_CONFIG], [$MYSQL_CONFIG], [], [$PATH:/usr/sbin:/usr/local/bin])
fi

AC_ARG_ENABLE([mysqlcache],
	AC_HELP_STRING([--disable-mysqlcache], [MySQL cache support]),
	[case "${enableval}" in
	  yes) mysqlcache=true ;;
	  no)  mysqlcache=false ;;
	  *) AC_MSG_ERROR(bad value ${enableval} for --disable-mysqlcache) ;;
	esac],[mysqlcache=true])

if test x$MYSQL_CONFIG = x; then
	echo "*****Cannot find mysql_config, mysql cache support disabled"
	mysqlcache=false
fi

if test x$mysqlcache = xtrue; then
	MYSQL_CFLAGS="`$MYSQL_CONFIG --cflags`"
	MYSQL_LIBS="`$MYSQL_CONFIG --libs`"
	MYSQL_INCLUDE="`$MYSQL_CONFIG --include`"
fi

AC_SUBST(MYSQL_CFLAGS)
AC_SUBST(MYSQL_LIBS)
AC_SUBST(MYSQL_INCLUDE)

if test x$mysqlcache = xtrue; then
#need to tweak cache-file.c to use these, and eventually disable cache if
#some return bogus values
AC_CHECK_HEADERS([libgen.h])
AC_CHECK_FUNCS([basename dirname], [], [mysqlcache=false])
fi

if test x$mysqlcache = xtrue; then
  AC_DEFINE([ENABLE_CACHE_MYSQL], [], ["mysql"])
fi
AM_CONDITIONAL(ENABLE_CACHE_MYSQL, test x$mysqlcache = xtrue)

##########################################################################

#AC_CONFIG_FILES([Makefile])
AC_OUTPUT([
Makefile
data/Makefile
po/Makefile.in
src/Makefile
])

echo "-------------------------------------------------------------------"
echo "Conditionally built codecs suports:"
echo "-------------------------------------------------------------------"
if test x$vorbis = xtrue; then
        echo "Building Vorbis codec support: ....................YES"
else
        echo "Building Vorbis codec support: ....................NO"
fi

if test x$flac = xtrue; then
        echo "Building FLAC codec support: ......................YES"
else
        echo "Building FLAC codec support: ......................NO"
fi

if test x$mp3 = xtrue; then
        echo "Building MP3 codec support: .......................YES"
else
        echo "Building MP3 codec support: .......................NO"
fi

if test x$mp4 = xtrue; then
        echo "Building MP4 codec support: .......................YES"
else
        echo "Building MP4 codec support: .......................NO"
fi
echo "-------------------------------------------------------------------"
echo "Conditionally built cache backends:"
echo "-------------------------------------------------------------------"
if test x$filecache = xtrue; then
        echo "Building flat file backend: .......................YES"
else
        echo "Building flat file backend: .......................NO"
fi

if test x$mysqlcache = xtrue; then
        echo "Building mysql backend: ...........................YES"
else
        echo "Building mysql backend: ...........................NO"
fi

echo "-------------------------------------------------------------------"

if test x$archive = xtrue; then
        echo "Building archive output support: ..................YES"
else
        echo "Building archive output support: ..................NO"
fi
