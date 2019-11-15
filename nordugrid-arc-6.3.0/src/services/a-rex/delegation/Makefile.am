noinst_LTLIBRARIES = libdelegation.la

libdelegation_la_SOURCES = \
	uid.cpp FileRecord.cpp FileRecordBDB.cpp FileRecordSQLite.cpp DelegationStore.cpp DelegationStores.cpp \
	uid.h   FileRecord.h   FileRecordBDB.h   FileRecordSQLite.h   DelegationStore.h   DelegationStores.h
libdelegation_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(DBCXX_CPPFLAGS) $(SQLITE_CFLAGS) $(AM_CXXFLAGS)
libdelegation_la_LIBADD = $(top_builddir)/src/hed/libs/common/libarccommon.la $(DBCXX_LIBS) $(SQLITE_LIBS)

