## Process this file with automake to produce Makefile.in

INCLUDES =			\
    -I$(top_srcdir)         	\
    -I$(top_srcdir)/src/client	\
    -I$(top_srcdir)/src/shared  \
    -I/usr/include/slang

noinst_LIBRARIES = libfs.a
noinst_HEADERS = fs_base.h fs_ext2.h fs_fat.h fs_hpfs.h fs_jfs.h fs_ntfs.h \
                 fs_reiser.h fs_ufs.h fs_xfs.h fs_afs.h fs_hfs.h fs_be.h

libfs_a_SOURCES = \
	fs_base.cpp \
	fs_afs.cpp \
	fs_ext2.cpp \
	fs_fat.cpp \
	fs_hpfs.cpp \
	fs_jfs.cpp \
	fs_ntfs.cpp \
	fs_reiser.cpp \
	fs_hfs.cpp \
	fs_ufs.cpp \
	fs_xfs.cpp
	
DEFS=@DEFS@ -DLOCALEDIR=\"${localedir}\" -D_REENTRANT -D_FILE_OFFSET_BITS=64
CPPFLAGS=@CPPFLAGS@ -Wall

MAINTAINERCLEANFILES = Makefile.in
