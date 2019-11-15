##############################################
#                                            #
# Nast - Network Analyzer Sniffer Tool       #
#	                                     #
# configure.ac - written by embyte@madlab.it # 
#                modified by Snifth@box.it   #
#                                            #
##############################################

AC_INIT(nast, 0.2.0, embyte@madlab.it)
AC_CONFIG_SRCDIR(main.c)
AC_CONFIG_HEADER(config.h)

# Print a banner
echo "
Please wait, I'm going to configure Nast 0.2.0
"

#########
# Subst #
#########

AC_SUBST(NCURSES)
AC_SUBST(GETOPT)


#################
# Checks for OS #
#################

AC_CANONICAL_TARGET
case "$target" in
*linux*)
	AC_MSG_NOTICE([Found Linux, happy day!])
        ;;    
*freebsd*)
    	AC_MSG_NOTICE([Found FreeBSD, are you a nerd?])
   	;;
*openbsd*)
	AC_MSG_WARN([
	OpenBSD port: we are working on...
	Nast could not run correctly
	])
  	;;
*netbsd*)
	AC_MSG_WARN([
	NetBSD port: we are working on...
	Nast could not run correctly
	])
	;;
*)
        AC_MSG_WARN([

        Your OS seems to be officially unsupported yet, please send an email authors

        ])
	;;
esac


################
# Setup prefix #
################

AC_PREFIX_DEFAULT(/usr/local)
if test "$prefix" = "NONE"; then
   prefix="/usr/local"
   fi
   

#######################
# Checks for compiler #
#######################

AC_PROG_CC


#########################
# Checks for libraries. #
#########################

#
# -- libnet --
#

AC_CHECK_LIB(net, libnet_name2addr4,, AC_MSG_ERROR([

Libnet-1.1.x Packet Shaping Library not found! It's required.
You can download it from official web site: http://www.packetfactory.net/libnet

]))

#
# -- libpcap --
#

AC_CHECK_LIB(pcap, pcap_dispatch,, AC_MSG_ERROR([

Libpcap-0.7.1 Packet Capture Library not found! It's required. 
You can download it from official web site: http://www.tcpdump.org/#current

]))

#
# -- libncurses support --
#

ENABLE_NCRS="no"
AC_CHECK_LIB(ncurses, initscr, ENABLE_NCRS="yes"; NCURSES=ncurses/n_nast.o; LIBS="-lncurses $LIBS"; AC_DEFINE(HAVE_LIBNCURSES), AC_MSG_RESULT([

Ncurses library (*) not found in your system.
You can download it from official web site: http://www.gnu.org/software/ncurses/ncurses.html
(*): CRT screen handling and optimization package

Building without ncurses menu support (-G flag will doesn't work)

]))
#fi

#
#  --lmenu support--
#

ENABLE_NCRS="no"
AC_CHECK_LIB(menu, menu_opts_off, ENABLE_NCRS="yes"; MENU=ncurses/n_menu.o; LIBS="-lmenu $LIBS"; AC_DEFINE(HAVE_LIBMENU), AC_MSG_RESULT([

Menu library (*) not found in your system.
You can download it from official web site: http://www.gnu.org/software/ncurses/ncurses.html
(*): CRT screen handling and optimization package

Building without ncurses menu support (-G flag will doesn't work)

]))






############################
# Checks for linux pthread #
############################

case "$target" in
*linux*)
	AC_CHECK_LIB(pthread, pthread_create, , AC_MSG_ERROR([

	Linux threads library not found in your linux-box! Strange..

	]))
	
	CFLAGS="-Wall -O2"
	;;
*bsd*)
	CFLAGS="-Wall -O2 -pthread"
	;;
esac	


##############################################
# Checks for headers and common libs/headers #
##############################################

AC_HEADER_STDC
AC_CHECK_HEADERS(errno.h sys/utsname.h,, AC_MSG_WARN(This headers are required!)) 

AH_TEMPLATE(HAVE_GETOPT, define if the getopt.h header is present, OpenBSD for ex. doesn't have one)
AC_CHECK_FUNC(getopt_long, AC_DEFINE(HAVE_GETOPT), GETOPT="getopt.o getopt1.o")
#AC_CHECK_HEADER(getopt.h, AC_DEFINE(HAVE_GETOPT), GETOPT="getopt.o getopt1.o")

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_HEADER_TIME
AC_STRUCT_TM

# Checks for library functions.
AC_FUNC_MALLOC
AC_TYPE_SIGNAL
AC_FUNC_VPRINTF


##################
# Write Makefile #
##################

AC_OUTPUT(Makefile)


#################
# Print results #
#################

echo "
Ok. I have done with all. 

Results are:

PLATFORM ...... : `uname -mp`
O.S. .......... : `uname -rs` (`uname -n`)
COMPILER ...... : ${CC}
CFLAGS ........ : ${CFLAGS}
CPPFLAGS ...... : ${CPPFLAGS}
LDFLAGS ....... : ${LDFLAGS}
LIBS .......... : ${LIBS}
PREFIX ........ : ${prefix}

NCURSES SUPPORT : ${ENABLE_NCRS}

Type 'make' to compile or 'make help' to show accepted options.
"

# ok we have done
