if MYSQL_LIBRARY_ENABLED
MYSQL_WRAPPER_TEST = MysqlWrapperTest
else
MYSQL_WRAPPER_TEST =
endif

TESTS = URLTest LoggerTest RunTest XMLNodeTest FileAccessTest FileUtilsTest \
        ProfileTest ArcRegexTest FileLockTest EnvTest UserConfigTest \
        StringConvTest CheckSumTest WatchdogTest UserTest $(MYSQL_WRAPPER_TEST) \
        Base64Test

check_PROGRAMS = $(TESTS) ThreadTest

TESTS_ENVIRONMENT = srcdir=$(srcdir)

URLTest_SOURCES = $(top_srcdir)/src/Test.cpp URLTest.cpp
URLTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
URLTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

LoggerTest_SOURCES = $(top_srcdir)/src/Test.cpp LoggerTest.cpp
LoggerTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
LoggerTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

RunTest_SOURCES = $(top_srcdir)/src/Test.cpp RunTest.cpp
RunTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
RunTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

ProfileTest_SOURCES = $(top_srcdir)/src/Test.cpp ProfileTest.cpp
ProfileTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
ProfileTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

ThreadTest_SOURCES = $(top_srcdir)/src/Test.cpp ThreadTest.cpp
ThreadTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
ThreadTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

XMLNodeTest_SOURCES = $(top_srcdir)/src/Test.cpp XMLNodeTest.cpp
XMLNodeTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
XMLNodeTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

FileAccessTest_SOURCES = $(top_srcdir)/src/Test.cpp FileAccessTest.cpp
FileAccessTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
FileAccessTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

FileUtilsTest_SOURCES = $(top_srcdir)/src/Test.cpp FileUtilsTest.cpp
FileUtilsTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
FileUtilsTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

ArcRegexTest_SOURCES = $(top_srcdir)/src/Test.cpp ArcRegexTest.cpp
ArcRegexTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
ArcRegexTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

FileLockTest_SOURCES = $(top_srcdir)/src/Test.cpp FileLockTest.cpp
FileLockTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
FileLockTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

EnvTest_SOURCES = $(top_srcdir)/src/Test.cpp EnvTest.cpp
EnvTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
EnvTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

UserConfigTest_SOURCES = $(top_srcdir)/src/Test.cpp UserConfigTest.cpp
UserConfigTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
UserConfigTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

StringConvTest_SOURCES = $(top_srcdir)/src/Test.cpp StringConvTest.cpp
StringConvTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
StringConvTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

CheckSumTest_SOURCES = $(top_srcdir)/src/Test.cpp CheckSumTest.cpp
CheckSumTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
CheckSumTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

WatchdogTest_SOURCES = $(top_srcdir)/src/Test.cpp WatchdogTest.cpp
WatchdogTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
WatchdogTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

UserTest_SOURCES = $(top_srcdir)/src/Test.cpp UserTest.cpp
UserTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
UserTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS)

if MYSQL_LIBRARY_ENABLED
MysqlWrapperTest_SOURCES = $(top_srcdir)/src/Test.cpp MysqlWrapperTest.cpp
MysqlWrapperTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(MYSQL_CFLAGS) $(AM_CXXFLAGS)
MysqlWrapperTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(MYSQL_LIBS)
endif

Base64Test_SOURCES = $(top_srcdir)/src/Test.cpp Base64Test.cpp
Base64Test_CXXFLAGS = -I$(top_srcdir)/include \
        $(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
Base64Test_LDADD = \
        $(top_builddir)/src/hed/libs/common/libarccommon.la \
        $(CPPUNIT_LIBS) $(GLIBMM_LIBS)

EXTRA_DIST = rcode
