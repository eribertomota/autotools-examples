#     GIFT, a flexible content based image retrieval system.
#     Copyright (C) 1998, 1999, 2000, 2001, 2002, CUI University of Geneva

#     This program is free software; you can redistribute it and/or modify
#     it under the terms of the GNU General Public License as published by
#     the Free Software Foundation; either version 2 of the License, or
#     (at your option) any later version.

#     This program is distributed in the hope that it will be useful,
#     but WITHOUT ANY WARRANTY; without even the implied warranty of
#     MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#     GNU General Public License for more details.

#     You should have received a copy of the GNU General Public License
#     along with this program; if not, write to the Free Software
#     Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA

#
# we configure the add collection program to work even if gift is not in the path
# this is also necessary for installing several versions of GIFT at the same time
#

EXTRA_DIST=  CTripleTransfer.pre-pl\
 CGLDAudreyMTam.pre-pl\
 CGLStructuredAnnotation.pre-pm\
  CGIFTLink.pre-pm\
 CGLDistanceMatrix.pre-pm\
  CGIFTLinkDemo.pre-pl\
  CXMLTreeBuilder.pre-pm\
  CXMLTreeWriter.pre-pm\
  CXMLTreeVisitor.pre-pm\
  CXTVWriter.pre-pm\
  CXTVTripletList.pre-pm\
 gift-dtd-to-keywords.pre-pl\
 gift-add-collection.pre-pl\
 gift-remove-collection.pre-pl\
 gift-browser-benchmark.pre-pl\
 gift-ranking-comparison.pre-pl\
 gift-mrml-client.pre-pl\
 gift-url-to-fts.pre-pl\
 CQueryParadigmMatcher.pre-pm\
 CFeedbackClient.pre-pm\
 CGraphCollection.pre-pm\
 CFCMovingTarget.pre-pm\
 CFCRankingComparison.pre-pm\
 gift-diagnose-print-all-ADI.pre-pl\
 gift-perl-example-server.pre-pl\
 gift-dtd-to-tex.pre-pl\
 gift-extract-text-features.pre-pl\
 gift-annotation-to-html.pre-pl\
 gift-old-to-new-url2fts.pre-pl\
 gift-start.pre-pl


PERLCONFIG=sed -e "s:__EXECBINDIR__:@DEBEXECBINDIR@:g;s:__PERL_LOCATION__:@PERL@:g;s:__BINDIR__:@DEBPERLLIBDIR@:g;s:__DATADIR__:@DEBDATADIR@:g;s:__LIBDIR__:@DEBSHAREDIR@:g;s:__HOME__:${HOME}:g;s:__WEB_PUBLISHING_DIRECTORY__:@WEB_PUBLISHING_DIRECTORY@:g;s§__WEB_PUBLISHING_LOCATION__§@WEB_PUBLISHING_LOCATION@§g;" < $< > $@


CTripleTransfer.pl: CTripleTransfer.pre-pl
	$(PERLCONFIG)

CGLDAudreyMTam.pl: CGLDAudreyMTam.pre-pl
	$(PERLCONFIG)

CGLStructuredAnnotation.pm: CGLStructuredAnnotation.pre-pm
	$(PERLCONFIG)

CGIFTLink.pm:  CGIFTLink.pre-pm
	$(PERLCONFIG)

CGLDistanceMatrix.pm: CGLDistanceMatrix.pre-pm
	$(PERLCONFIG)

CGIFTLinkDemo.pl:  CGIFTLinkDemo.pre-pl
	$(PERLCONFIG)

CXMLTreeBuilder.pm:  CXMLTreeBuilder.pre-pm
	$(PERLCONFIG)

CXMLTreeWriter.pm:  CXMLTreeWriter.pre-pm
	$(PERLCONFIG)

CXMLTreeVisitor.pm:  CXMLTreeVisitor.pre-pm
	$(PERLCONFIG)

CXTVWriter.pm:  CXTVWriter.pre-pm
	$(PERLCONFIG)

CXTVTripletList.pm:  CXTVTripletList.pre-pm
	$(PERLCONFIG)

gift-dtd-to-keywords.pl: gift-dtd-to-keywords.pre-pl
	$(PERLCONFIG)

gift-add-collection.pl: gift-add-collection.pre-pl
	$(PERLCONFIG)

gift-remove-collection.pl: gift-remove-collection.pre-pl
	$(PERLCONFIG)

gift-browser-benchmark.pl: gift-browser-benchmark.pre-pl
	$(PERLCONFIG)

gift-ranking-comparison.pl: gift-ranking-comparison.pre-pl
	$(PERLCONFIG)

gift-mrml-client.pl: gift-mrml-client.pre-pl
	$(PERLCONFIG)

gift-url-to-fts.pl: gift-url-to-fts.pre-pl
	$(PERLCONFIG)

CQueryParadigmMatcher.pm: CQueryParadigmMatcher.pre-pm
	$(PERLCONFIG)

CFeedbackClient.pm: CFeedbackClient.pre-pm
	$(PERLCONFIG)

CGraphCollection.pm: CGraphCollection.pre-pm
	$(PERLCONFIG)

CFCMovingTarget.pm: CFCMovingTarget.pre-pm
	$(PERLCONFIG)

CFCRankingComparison.pm: CFCRankingComparison.pre-pm
	$(PERLCONFIG)

gift-diagnose-print-all-ADI.pl: gift-diagnose-print-all-ADI.pre-pl
	$(PERLCONFIG)

gift-perl-example-server.pl: gift-perl-example-server.pre-pl
	$(PERLCONFIG)

gift-dtd-to-tex.pl: gift-dtd-to-tex.pre-pl
	$(PERLCONFIG)

gift-extract-text-features.pl: gift-extract-text-features.pre-pl
	$(PERLCONFIG)

gift-annotation-to-html.pl: gift-annotation-to-html.pre-pl
	$(PERLCONFIG)

gift-old-to-new-url2fts.pl: gift-old-to-new-url2fts.pre-pl
	$(PERLCONFIG)

gift-start.pl: gift-start.pre-pl
	$(PERLCONFIG)


bin_SCRIPTS= @GIFT_INTERNAL_PERLS@ gift-url-to-fts.pl gift-diagnose-print-all-ADI.pl gift-mrml-client.pl CFeedbackClient.pm CFCMovingTarget.pm gift-perl-example-server.pl gift-add-collection.pl gift-remove-collection.pl gift-dtd-to-tex.pl gift-dtd-to-keywords.pl CQueryParadigmMatcher.pm CTripleTransfer.pl CGLDAudreyMTam.pl CGLStructuredAnnotation.pm CGIFTLink.pm CGLDistanceMatrix.pm CGIFTLinkDemo.pl CXMLTreeBuilder.pm CXMLTreeWriter.pm CXMLTreeVisitor.pm CXTVTripletList.pm CXTVWriter.pm CGraphCollection.pm gift-old-to-new-url2fts.pl gift-start.pl gift-diagnose-print-all-ADI.pl

EXTRA_SCRIPTS=gift-browser-benchmark.pl gift-extract-text-features.pl gift-annotation-to-html.pl gift-ranking-comparison.pl CFCRankingComparison.pm CGraphCollection.pm

clean: 
	-rm *.pl *.pm

distclean: 
	-rm *.pl *.pm
