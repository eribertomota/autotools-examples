lib_LTLIBRARIES = libarccompute.la
noinst_PROGRAMS = test_jobdescription test_JobInformationStorage

if DBJSTORE_ENABLED
HEADER_WITH_DBJSTORE   = JobInformationStorageBDB.h
SOURCE_WITH_DBJSTORE   = JobInformationStorageBDB.cpp
CXXFLAGS_WITH_DBJSTORE = $(DBCXX_CPPFLAGS)
LIBADD_WITH_DBJSTORE   = $(DBCXX_LIBS)
else
HEADER_WITH_DBJSTORE   =
SOURCE_WITH_DBJSTORE   =
CXXFLAGS_WITH_DBJSTORE =
LIBADD_WITH_DBJSTORE   =
endif

if SQLITEJSTORE_ENABLED
HEADER_WITH_SQLITEJSTORE   = JobInformationStorageSQLite.h
SOURCE_WITH_SQLITEJSTORE   = JobInformationStorageSQLite.cpp
CXXFLAGS_WITH_SQLITEJSTORE = $(SQLITE_CFLAGS)
LIBADD_WITH_SQLITEJSTORE   = $(SQLITE_LIBS)
else
HEADER_WITH_SQLITEJSTORE   =
SOURCE_WITH_SQLITEJSTORE   =
CXXFLAGS_WITH_SQLITEJSTORE =
LIBADD_WITH_SQLITEJSTORE   =
endif

libarccompute_ladir = $(pkgincludedir)/compute
libarccompute_la_HEADERS = Broker.h BrokerPlugin.h ExecutionTarget.h \
	Submitter.h SubmitterPlugin.h GLUE2Entity.h SubmissionStatus.h \
	JobState.h Job.h JobControllerPlugin.h JobSupervisor.h \
	JobDescription.h JobDescriptionParserPlugin.h Software.h \
	GLUE2.h EndpointQueryingStatus.h TestACCControl.h \
	EntityRetriever.h EntityRetrieverPlugin.h Endpoint.h WSCommonPlugin.h \
	ComputingServiceRetriever.h JobInformationStorage.h \
	JobInformationStorageXML.h $(HEADER_WITH_DBJSTORE) $(HEADER_WITH_SQLITEJSTORE)
libarccompute_la_SOURCES = Broker.cpp BrokerPlugin.cpp ExecutionTarget.cpp \
	Submitter.cpp SubmitterPlugin.cpp \
	JobState.cpp Job.cpp JobControllerPlugin.cpp JobSupervisor.cpp \
	JobDescription.cpp JobDescriptionParserPlugin.cpp Software.cpp \
	GLUE2.cpp EndpointQueryingStatus.cpp TestACCControl.cpp \
	EntityRetriever.cpp EntityRetrieverPlugin.cpp Endpoint.cpp \
	ComputingServiceRetriever.cpp \
	JobInformationStorageDescriptor.cpp \
	JobInformationStorageXML.cpp $(SOURCE_WITH_DBJSTORE) $(SOURCE_WITH_SQLITEJSTORE)
libarccompute_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(OPENSSL_CFLAGS) \
	$(CXXFLAGS_WITH_DBJSTORE) $(CXXFLAGS_WITH_SQLITEJSTORE) $(AM_CXXFLAGS)
libarccompute_la_LIBADD = \
	$(top_builddir)/src/hed/libs/delegation/libarcdelegation.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(LIBADD_WITH_DBJSTORE) $(LIBADD_WITH_SQLITEJSTORE)
libarccompute_la_LDFLAGS = -version-info 3:0:0

test_jobdescription_SOURCES = test_jobdescription.cpp
test_jobdescription_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
test_jobdescription_LDADD = libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(DBCXX_LIBS)

test_JobInformationStorage_SOURCES = test_JobInformationStorage.cpp
test_JobInformationStorage_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
test_JobInformationStorage_LDADD = libarccompute.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS)

testjobdir = $(pkgdatadir)/test-jobs
testjob_DATA = test-job-1 test-job-2 test-job-3
EXTRA_DIST = $(testjob_DATA)

DIST_SUBDIRS = test examples
SUBDIRS = . $(TEST_DIR) examples
