AC_INIT(weplab, 0.1.5, Topo[LB] - Jose Ignacio Sanchez <topolb@users.sourceforge.net>, main)
AM_INIT_AUTOMAKE(weplab, 0.1.5)
AC_PROG_CC
AC_PROG_INSTALL
#AC_CONFIG_FILES([Makefile])
AC_CHECK_HEADERS(pcap.h stdlib.h string.h unistd.h signal.h time.h netinet/in.h sys/types.h sys/wait.h)
AC_HEADER_STDC

if test "$CC" = "gcc" ; then
	CFLAGS="$CFLAGS -Wall -pipe"
fi

AC_CANONICAL_HOST
    case $host_os in
      *cygwin* ) CYGWIN=yes;;
             * ) CYGWIN=no;;
esac
 
if test "$CYGWIN" = "yes"; then
	AC_DEFINE(WIN32)
	AC_DEFINE(_BITTYPES_H)
	AC_DEFINE(_STDLIB_H_)
	AC_DEFINE( _NETINET_IN_H)
	AC_DEFINE( _SYS_UNISTD_H)
	AC_DEFINE(_ARPA_INET_H)	
	CFLAGS="$CFLAGS"
	LIBS="$LIBS -mms-bitfields  -lwpcap"
else  
	AC_CHECK_LIB(pcap, pcap_open_live, , [echo ERROR\: You need libpcap-dev\!; exit])
fi

#UNAMEP=`uname -p`
if test "x$UNAMEP" = "x"; then
	UNAMEP="unknown"
fi
if test "x$UNAMEP" = "xunknown"; then
	UNAMEP=`grep "model name" /proc/cpuinfo | cut -d: -f2`
fi

if $CC -dumpversion|egrep -q "^3\.0.*"; then
# gcc-3.0
	CFLAGS="-DG_DISABLE_ASSERT -O3 -fomit-frame-pointer -fno-exceptions -pipe -s -ffast-math -fexpensive-optimizations -falign-functions -falign-loops"
elif $CC -dumpversion|egrep -q "^3\..*"; then
# gcc-3.x
	if echo $UNAMEP|grep -q "Intel(R) Pentium(R) 4"; then
		MARCH="-march=pentium4 -mmmx -mfpmath=sse -msse"
	elif echo $UNAMEP|grep -q "Pentium III"; then
		MARCH="-march=pentium3 -mmmx -mfpmath=sse"
	elif echo $UNAMEP|grep -q "AMD-K6(tm) 3D"; then
		MARCH="-march=k6-2 -m3dnow"
	elif echo $UNAMEP|grep -q "Pentium 75 - 200"; then
		MARCH=-march=pentium
	elif echo $UNAMEP|grep -q "Pentium II"; then
		MARCH="-march=pentium2 -mmmx"
	elif echo $UNAMEP|grep -q -i "AMD Athlon(TM) XP"; then
		MARCH="-march=athlon-xp -mfpmath=sse -mmmx -msse -m3dnow"
	elif echo $UNAMEP|grep -q "Intel(R) Xeon(TM)"; then
		MARCH="-march=pentium4 -mmmx -mfpmath=sse -msse"
	else
		MARCH=""
	fi
	CFLAGS="-DG_DISABLE_ASSERT -O3 $MARCH -fomit-frame-pointer -fno-exceptions -pipe -s -ffast-math -fexpensive-optimizations -falign-functions -falign-loops -fstrict-aliasing"
elif $CC -dumpversion | egrep -q "^2\.9.*" ; then
# gcc-2.95
	if echo $UNAMEP|egrep -q "(Pentium III|Pentium II|Pentium\(R\) 4|Athlon)"; then
		MARCH=-march=pentiumpro
	elif echo $UNAMEP|grep -q "AMD-K6"; then
		MARCH=-march=k6
	elif echo $UNAMEP|grep -q "Pentium 75 - 200"; then
		MARCH=-march=pentium
	else 
		MARCH=""
	fi
	CFLAGS="-DG_DISABLE_ASSERT $MARCH -O3 -fomit-frame-pointer -fno-exceptions -pipe -s -ffast-math -fexpensive-optimizations"
else
	echo "warning: compiler is not known: not optimizing!"
fi
echo "using $CC $CFLAGS"



AC_OUTPUT(Makefile)
