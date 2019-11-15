## Process this file with automake to produce Makefile.in

SUBDIRS = fs

INCLUDES =					\
	-I$(top_srcdir)				\
	-I$(top_srcdir)/src/shared		\
	-I$(top_srcdir)/src/client		\
	-I$(top_srcdir)/src/client/fs           \
	-I/usr/include/slang

sbin_PROGRAMS = partimage


noinst_HEADERS =  buffer.h cbitmap.h gui_text.h image_base.h image_net.h \
                  imagefile.h imginfo.h interface.h interface_newt.h \
		  interface_none.h \
                  mbr_backup.h misc.h netclient.h partimage.h

partimage_SOURCES =         \
    netclient.cpp	\
    imagefile.cpp	    \
    misc.cpp		    \
    image_net.cpp           \
    buffer.cpp              \
    gui_text.cpp            \
    main.cpp                \
    imginfo.cpp             \
    cbitmap.cpp             \
    interface_base.cpp      \
    interface_newt.cpp      \
    interface_none.cpp      \
    mbr_backup.cpp

# all libs are added in LIBS, we needn't add them to partimage_LDADD 
partimage_LDADD = -lslang fs/libfs.a ../shared/libshared.a
partimage_LDFLAGS = @PARTIMAGE_LDFLAGS@

DEFS=@DEFS@ -DLOCALEDIR=\"${localedir}\" -D_REENTRANT -D_FILE_OFFSET_BITS=64

CPPFLAGS=@CPPFLAGS@ -Wall 

MAINTAINERCLEANFILES = Makefile.in
