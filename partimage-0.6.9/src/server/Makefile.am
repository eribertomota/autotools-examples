## Process this file with automake to produce Makefile.in

INCLUDES =							\
	-I$(top_srcdir)					\
	-I$(top_srcdir)/src/shared		\
	-I$(top_srcdir)/src/client		\
	-I$(top_srcdir)/src/server              \
	-I/usr/include/slang

sbin_PROGRAMS = partimaged

partimaged_SOURCES = 			\
	netserver.cpp			\
	partimaged.cpp			\
	partimaged-client.cpp		\
	partimaged-gui_dummy.cpp	\
	partimaged-gui_newt.cpp		\
	partimaged-main.cpp		

noinst_HEADERS = netserver.h partimaged-client.h partimaged-gui.h \
                 partimaged-gui_dummy.h partimaged-gui_newt.h partimaged.h

#partimaged_LDADD = -L/usr/lib -lz -lbz2 -lnewt -lpthread -lcrypt -lslang -lcom_err -lext2fs ../shared/libshared.a
partimaged_LDADD = -lslang ../shared/libshared.a

partimaged_LDFLAGS = @PARTIMAGE_LDFLAGS@

DEFS=@DEFS@ -DLOCALEDIR=\"${localedir}\" -D_REENTRANT -D_FILE_OFFSET_BITS=64

CPPFLAGS=@CPPFLAGS@ -Wall

MAINTAINERCLEANFILES = Makefile.in
