if DBJSTORE_ENABLED
CXXFLAGS_WITH_DBJSTORE = $(DBCXX_CPPFLAGS)
LIBADD_WITH_DBJSTORE   = $(DBCXX_LIBS)
else
CXXFLAGS_WITH_DBJSTORE =
LIBADD_WITH_DBJSTORE   =
endif

TESTS = SoftwareTest JobTest JobInformationStorageTest JobStateTest \
	BrokerTest JobDescriptionTest JobControllerPluginTest \
	JobDescriptionParserPluginTest SubmitterTest SubmitterPluginTest \
	JobSupervisorTest TargetInformationRetrieverTest \
	ServiceEndpointRetrieverTest JobListRetrieverTest ExecutionTargetTest \
	ComputingServiceUniqTest SubmissionStatusTest

check_PROGRAMS = $(TESTS)

TESTS_ENVIRONMENT = env ARC_PLUGIN_PATH=$(top_builddir)/src/hed/acc/TEST/.libs

SoftwareTest_SOURCES = $(top_srcdir)/src/Test.cpp SoftwareTest.cpp
SoftwareTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
SoftwareTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

JobTest_SOURCES = $(top_srcdir)/src/Test.cpp JobTest.cpp
JobTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) \
	$(CXXFLAGS_WITH_DBJSTORE) $(AM_CXXFLAGS)
JobTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(LIBADD_WITH_DBJSTORE)

JobInformationStorageTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	JobInformationStorageTest.cpp
JobInformationStorageTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
JobInformationStorageTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(DBCXX_LIBS)

JobDescriptionTest_SOURCES = $(top_srcdir)/src/Test.cpp JobDescriptionTest.cpp
JobDescriptionTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
JobDescriptionTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

JobStateTest_SOURCES = $(top_srcdir)/src/Test.cpp JobStateTest.cpp
JobStateTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
JobStateTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

BrokerTest_SOURCES = $(top_srcdir)/src/Test.cpp BrokerTest.cpp
BrokerTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
BrokerTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

JobControllerPluginTest_SOURCES = $(top_srcdir)/src/Test.cpp JobControllerPluginTest.cpp
JobControllerPluginTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
JobControllerPluginTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

JobSupervisorTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	JobSupervisorTest.cpp
JobSupervisorTest_CXXFLAGS = -I$(top_srcdir)/include\
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
JobSupervisorTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

JobDescriptionParserPluginTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	JobDescriptionParserPluginTest.cpp
JobDescriptionParserPluginTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
JobDescriptionParserPluginTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

SubmitterTest_SOURCES = $(top_srcdir)/src/Test.cpp SubmitterTest.cpp
SubmitterTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
SubmitterTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)


SubmitterPluginTest_SOURCES = $(top_srcdir)/src/Test.cpp SubmitterPluginTest.cpp
SubmitterPluginTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
SubmitterPluginTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

ServiceEndpointRetrieverTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	ServiceEndpointRetrieverTest.cpp
ServiceEndpointRetrieverTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
ServiceEndpointRetrieverTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

TargetInformationRetrieverTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	TargetInformationRetrieverTest.cpp
TargetInformationRetrieverTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
TargetInformationRetrieverTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

JobListRetrieverTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	JobListRetrieverTest.cpp
JobListRetrieverTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
JobListRetrieverTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

ExecutionTargetTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	ExecutionTargetTest.cpp
ExecutionTargetTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
ExecutionTargetTest_LDADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

ComputingServiceUniqTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	ComputingServiceUniqTest.cpp
ComputingServiceUniqTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
ComputingServiceUniqTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

SubmissionStatusTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	SubmissionStatusTest.cpp
SubmissionStatusTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
SubmissionStatusTest_LDADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

#~ EndpointTest_SOURCES = $(top_srcdir)/src/Test.cpp \
	#~ EndpointTest.cpp
#~ EndpointTest_CXXFLAGS = -I$(top_srcdir)/include \
	#~ $(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
#~ EndpointTest_LDADD = \
	#~ $(top_builddir)/src/hed/libs/compute/libarcclient.la \
	#~ $(top_builddir)/src/hed/libs/common/libarccommon.la \
	#~ $(top_builddir)/src/hed/libs/loader/libarcloader.la \
	#~ $(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)
