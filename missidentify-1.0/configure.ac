
AC_INIT([MISSIDENTIFY],[1.0],[research@jessekornblum.com])
AM_INIT_AUTOMAKE

AC_CONFIG_FILES([Makefile])
AM_CONFIG_HEADER([config.h])

AC_CANONICAL_HOST

case $host in
  *-*-*linux*-*) AC_DEFINE([__LINUX__],1,[Linux operating system functions]) ;;
  *-*-mingw32)   LIBS="-liberty $LIBS" && CPPFLAGS="-DUNICODE -D_UNICODE $CPPFLAGS"
esac


# Bring additional directories where things might be found into our
# search path. I don't know why autoconf doesn't do this by default
for spfx in /usr/local /opt/local /sw ; do
    echo checking ${spfx}/include
    if test -d ${spfx}/include; then
        CPPFLAGS="-I${spfx}/include $CPPFLAGS"
        LDFLAGS="-L${spfx}/lib $LDFLAGS"
    fi
done

AC_GNU_SOURCE
AC_PROG_CC
AC_PROG_INSTALL

AC_C_BIGENDIAN

AC_CHECK_HEADERS([libgen.h])
AC_CHECK_HEADERS([dirent.h])
AC_CHECK_HEADERS([inttypes.h])

AC_OUTPUT


