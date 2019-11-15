## Process this file with automake to produce Makefile.in


# Should be another room for .cpp files but I can't find it.
EXTRA_DIST = access.cpp common.cpp exceptions.cpp image_disk.cpp \
             messages.cpp net.cpp

# Pickup header files here so automake knows about them.
# useful at least for 'make dist'
noinst_HEADERS = access.h common.h errors.h exceptions.h image_disk.h \
                 messages.h net.h structures.h privs.h endianess.h pathnames.h
INCLUDES = 			\
    -I$(top_srcdir)         	\
    -I$(top_srcdir)/src/client	\
    -I$(top_srcdir)/src/shared  \
    -I/usr/include/slang

noinst_LIBRARIES = libshared.a

libshared_a_SOURCES =		\
	common.cpp		\
	access.cpp		\
	net.cpp			\
	exceptions.cpp		\
	messages.cpp		\
	privs.cpp		\
	image_disk.cpp		

DEFS=@DEFS@ -DLOCALEDIR=\"${localedir}\" -D_REENTRANT -D_FILE_OFFSET_BITS=64
CPPFLAGS=@CPPFLAGS@ -Wall

MAINTAINERCLEANFILES = Makefile.in
