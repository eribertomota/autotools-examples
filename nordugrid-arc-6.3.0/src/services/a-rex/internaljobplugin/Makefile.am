pkglib_LTLIBRARIES = libaccINTERNAL.la

libaccINTERNAL_la_SOURCES  = INTERNALClient.cpp INTERNALClient.h \
	JobStateINTERNAL.cpp JobStateINTERNAL.h \
	SubmitterPluginINTERNAL.cpp SubmitterPluginINTERNAL.h \
	JobControllerPluginINTERNAL.cpp JobControllerPluginINTERNAL.h \
	JobListRetrieverPluginINTERNAL.cpp JobListRetrieverPluginINTERNAL.h \
	TargetInformationRetrieverPluginINTERNAL.cpp TargetInformationRetrieverPluginINTERNAL.h \
	DescriptorsINTERNAL.cpp \
	../job.cpp ../tools.cpp
libaccINTERNAL_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)


libaccINTERNAL_la_LIBADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
	../grid-manager/conf/libconf.la \
	../grid-manager/jobs/libjobs.la \
	../grid-manager/files/libfiles.la \
	../grid-manager/log/liblog.la \
	../grid-manager/run/librun.la \
	../grid-manager/mail/libmail.la \
	../delegation/libdelegation.la


#	$(top_builddir)/src/hed/libs/delegation/libarcdelegation.la \
#	$(top_builddir)/src/hed/libs/delegation/libarcdelegation.la \
#	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
#	$(top_builddir)/src/hed/libs/communication/libarccommunication.la \
#	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
#	$(top_builddir)/src/libs/data-staging/libarcdatastaging.la \
#	$(top_builddir)/src/services/a-rex/grid-manager/libgridmanager.la \
#	$(top_builddir)/src/services/a-rex/delegation/libdelegation.la \
#	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(GLOBUS_JOBPLUGIN_LIBS)

libaccINTERNAL_la_LDFLAGS = -no-undefined -avoid-version -module

