DIST_SUBDIRS = test
SUBDIRS = $(TEST_DIR)

if MYSQL_LIBRARY_ENABLED
MYSQL_WRAPPER_HEADER = MysqlWrapper.h
MYSQL_WRAPPER_CPP = MysqlWrapper.cpp   
else
MYSQL_WRAPPER_HEADER =
MYSQL_WRAPPER_CPP =
endif

lib_LTLIBRARIES = libarccommon.la

pgmpkglibdir = $(pkglibdir)
pgmpkglib_PROGRAMS = arc-file-access arc-hostname-resolver

libarccommon_ladir = $(pkgincludedir)
nodist_libarccommon_la_HEADERS = ArcVersion.h
libarccommon_la_HEADERS = ArcConfig.h ArcLocation.h \
	ArcRegex.h ArcConfigIni.h ArcConfigFile.h \
	Base64.h CheckSum.h DBInterface.h DateTime.h \
	FileLock.h FileUtils.h FileAccess.h GUID.h IString.h \
	Logger.h OptionParser.h StringConv.h Thread.h URL.h \
	User.h UserConfig.h Utils.h XMLNode.h HostnameResolver.h \
	Counter.h IntraProcessCounter.h IniConfig.h Profile.h \
	Run.h Watchdog.h JobPerfLog.h $(MYSQL_WRAPPER_HEADER)

PLATFORM_SPECIFIC = Run_unix.cpp

libarccommon_la_SOURCES = ArcVersion.cpp ArcConfig.cpp ArcLocation.cpp \
	ArcRegex.cpp ArcConfigIni.cpp ArcConfigFile.cpp \
	Base64.cpp CheckSum.cpp DateTime.cpp \
	FileLock.cpp FileUtils.cpp FileAccess.cpp GUID.cpp IString.cpp \
	Logger.cpp OptionParser.cpp StringConv.cpp Thread.cpp URL.cpp \
	User.cpp UserConfig.cpp Utils.cpp XMLNode.cpp HostnameResolver.cpp \
	Counter.cpp IntraProcessCounter.cpp IniConfig.cpp Profile.cpp JobPerfLog.cpp \
	$(PLATFORM_SPECIFIC) $(MYSQL_WRAPPER_CPP)
libarccommon_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(GTHREAD_CFLAGS) $(ZLIB_CFLAGS) \
	$(MYSQL_CFLAGS) $(AM_CXXFLAGS)
libarccommon_la_LIBADD = $(LIBXML2_LIBS) $(GLIBMM_LIBS) $(GTHREAD_LIBS) $(ZLIB_LIBS) \
	$(UUID_LIBS) $(MYSQL_LIBS) $(LIBINTL) -lpthread
libarccommon_la_LDFLAGS = -version-info 3:0:0

arc_file_access_SOURCES  = file_access.cpp file_access.h
arc_file_access_CXXFLAGS = -I$(top_srcdir)/include $(AM_CXXFLAGS)
arc_file_access_LDADD    =

arc_hostname_resolver_SOURCES  = hostname_resolver.cpp hostname_resolver.h
arc_hostname_resolver_CXXFLAGS = -I$(top_srcdir)/include $(AM_CXXFLAGS)
arc_hostname_resolver_LDADD    =
