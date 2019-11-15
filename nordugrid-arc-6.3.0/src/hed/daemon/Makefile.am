PLATFORM_DIR = unix

SUBDIRS = scripts $(PLATFORM_DIR) schema

sbin_PROGRAMS = arched
SRC = options.cpp options.h 
LIB = unix/libdaemon.la
SOURCES = $(SRC)
LDADD = $(LIB)

arched_SOURCES = $(SOURCES)
arched_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
arched_LDADD = $(LDADD) \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS)

man_MANS = arched.8
