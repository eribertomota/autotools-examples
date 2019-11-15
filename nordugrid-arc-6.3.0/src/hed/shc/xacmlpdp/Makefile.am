SUBDIRS = schema

noinst_LTLIBRARIES = libxacmlpdp.la

libxacmlpdp_la_SOURCES = XACMLEvaluationCtx.cpp XACMLEvaluationCtx.h \
	XACMLEvaluator.cpp XACMLEvaluator.h XACMLRequest.cpp XACMLRequest.h \
	XACMLPolicy.cpp XACMLPolicy.h XACMLRule.cpp XACMLRule.h \
	XACMLTarget.cpp XACMLTarget.h AttributeDesignator.cpp \
	AttributeDesignator.h AttributeSelector.cpp AttributeSelector.h \
	XACMLApply.cpp XACMLApply.h XACMLCondition.cpp XACMLCondition.h \
	XACMLAttributeProxy.h XACMLAttributeFactory.cpp \
	XACMLAttributeFactory.h XACMLFnFactory.cpp XACMLFnFactory.h \
	XACMLAlgFactory.cpp XACMLAlgFactory.h XACMLPDP.cpp XACMLPDP.h 
libxacmlpdp_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libxacmlpdp_la_LIBADD = \
	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la
