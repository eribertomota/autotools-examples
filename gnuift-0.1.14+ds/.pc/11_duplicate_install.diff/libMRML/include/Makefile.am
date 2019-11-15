
directory.h:
	echo "Making directory.h"
	@rm -f directory.h; \
	echo '#define __LIBDIR__ "@DEBSHAREDIR@"' > directory.h;\
	echo '#define __PERL_LOCATION__ "@PERL@"' >> directory.h;\
	echo '#define __BINDIR__ "@DEBPERLLIBDIR@"' >> directory.h;\
	echo '#define __EXECBINDIR__ "@DEBEXECBINDIR@"' >> directory.h;\
	echo '#define __DATADIR__ "@DEBDATADIR@"' >> directory.h

all: directory.h

dist-hook: 
	rm $(distdir)/directory.h

#install-data-local:
#		echo "ca marche"

#install-data-hook:
#		echo "pas"

libMRMLdir=$(includedir)/libMRML/include

libMRML_HEADERS= directory.h \
	CAFPlugin.h		     CMRMLStringConstants.h   CTimeStampGenerator.h \
	CAccessor.h		     CMagic.h		      CXEVCommunication.h \
	CAccessorAdmin.h	     CMutex.h		      CXEVTripletList.h \
	CAccessorAdminCollection.h   CNoDelete.h	      CXMLElement.h \
	CAccessorElement.h	     CPropertySheetList.h     CXMLElementBuilder.h \
	CAccessorFactory.h	     CQMultiple.h	      CXMLElementVisitor.h \
	CAccessorFactoryContainer.h  CQParallel.h	      CXMLHelper.h \
	CAccessorImplementation.h    CQuery.h		      GIFTExceptions.h \
	CAlgorithm.h		     CQueryParadigmMatcher.h  TID.h \
	CAlgorithmCollection.h	     CQueryPlugin.h	      directory.h \
	CArraySelfDestroyPointer.h   CQueryTreeBuilder.h      mrml_const.h \
	CAttributeList.h	     CQueryTreeNode.h	      myNew.h \
	CCommunicationHandler.h      CRelevanceLevel.h	      my_assert.h \
	CDebuggingMemoryManager.h    CRelevanceLevelList.h    my_diagnose.h \
	CDynamicQueryFactory.h	     CSelfDestroyPointer.h    my_throw.h \
	CIDRelevanceLevelPair.h      CSessionManager.h \
	CIDRelevanceLevelPairList.h  CStaticQueryFactory.h uses-declarations.h \
 CRPipe.h CReaper.h CReaperDistributor.h safePopen.h\
	createErrorMessage.h 	CI18nTranslator.h 	CXEVI18nTranslator.h gift-config.h

#install-data-hook:
#	$(INSTALL_DATA) $(srcdir)/gift-config.h $(includedir)/libMRML/include/gift-config.h


CLEANFILES= directory.h 
