AM_CPPFLAGS		= -DSYSCONFDIR="\"$(sysconfdir)\""

bin_PROGRAMS		= gscanbus
#bin_PROGRAMS		= gscanbus @GSCANBUS-MPATROL@ @GSCANBUS-EFENCE@
#EXTRA_PROGRAMS		= gscanbus-mpatrol gscanbus-efence

#gscanbus-mpatrol_LDADD	= mpatrol.so elf.so bfd.so iberty.so
#gscanbus-efence_LDADD	= efence.so

gscanbus_SOURCES	= fatal.c debug.c raw1394util.c simpleavc.c decodeselfid.c topologyTree.c rominfo.c topologyMap.c menues.c icons.c gscanbus.c
#gscanbus_LDADD = @LIBOBJS@
EXTRA_DIST		= debug.h decodeselfid.h fatal.h menues.h raw1394support.h raw1394util.h rominfo.h simpleavc.h topologyMap.h topologyTree.h icons.h gnome-qeye.xpm gnome-question.xpm gnome-term.xpm apple-green.xpm gnome-term-linux.xpm gtcd.xpm gnome-term-apple.xpm gnome-term-windows.xpm guid-resolv.conf oui-resolv.conf TODO

INCLUDES		= @GTK_CFLAGS@
LDADD			= @GTK_LIBS@

sysconf_DATA = guid-resolv.conf oui-resolv.conf

