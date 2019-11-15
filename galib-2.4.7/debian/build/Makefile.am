topdir=../../ga

INCLUDES = -I$(topdir)/../

ga_includedir = $(includedir)/ga/
ga_include_HEADERS = $(topdir)/ga.h $(topdir)/gaconfig.h \
	$(topdir)/gatypes.h $(topdir)/gaid.h $(topdir)/garandom.h \
	$(topdir)/gaerror.h $(topdir)/std_stream.h $(topdir)/GAEvalData.h \
	$(topdir)/GAParameter.h $(topdir)/GAStatistics.h $(topdir)/GABaseGA.h \
	$(topdir)/GASStateGA.h $(topdir)/GASimpleGA.h $(topdir)/GAIncGA.h \
	$(topdir)/GADemeGA.h $(topdir)/GADCrowdingGA.h $(topdir)/GASelector.h \
	$(topdir)/GAScaling.h $(topdir)/GAPopulation.h $(topdir)/GAGenome.h \
	$(topdir)/GAMask.h $(topdir)/GABinStr.h $(topdir)/gabincvt.h \
	$(topdir)/GAAllele.h $(topdir)/GAArray.h $(topdir)/GANode.h \
	$(topdir)/GA1DBinStrGenome.h $(topdir)/GA2DBinStrGenome.h \
	$(topdir)/GA3DBinStrGenome.h $(topdir)/GABin2DecGenome.h \
	$(topdir)/GA1DArrayGenome.h $(topdir)/GA2DArrayGenome.h \
	$(topdir)/GA3DArrayGenome.h $(topdir)/GAStringGenome.h \
	$(topdir)/GARealGenome.h $(topdir)/GATreeBASE.h $(topdir)/GATree.h \
	$(topdir)/GATreeGenome.h $(topdir)/GAListBASE.h $(topdir)/GAList.h \
	$(topdir)/GAListGenome.h $(topdir)/GAAllele.C \
	$(topdir)/GA1DArrayGenome.C $(topdir)/GA2DArrayGenome.C \
	$(topdir)/GA3DArrayGenome.C $(topdir)/GATree.C \
	$(topdir)/GATreeGenome.C $(topdir)/GAList.C $(topdir)/GAListGenome.C \
	$(topdir)/GAStringGenome.C $(topdir)/GARealGenome.C

lib_LTLIBRARIES = libga.la

libga_la_SOURCES = $(topdir)/garandom.C $(topdir)/gaerror.C \
	$(topdir)/GAParameter.C $(topdir)/GAStatistics.C $(topdir)/GABaseGA.C \
	$(topdir)/GASStateGA.C $(topdir)/GASimpleGA.C $(topdir)/GAIncGA.C \
	$(topdir)/GADemeGA.C $(topdir)/GADCrowdingGA.C $(topdir)/GASelector.C \
	$(topdir)/GAScaling.C $(topdir)/GAPopulation.C $(topdir)/GAGenome.C \
	$(topdir)/GABinStr.C $(topdir)/gabincvt.C $(topdir)/GAAllele.C \
	$(topdir)/GAStringGenome.C $(topdir)/GARealGenome.C \
	$(topdir)/GA1DBinStrGenome.C $(topdir)/GA2DBinStrGenome.C \
	$(topdir)/GA3DBinStrGenome.C $(topdir)/GABin2DecGenome.C \
	$(topdir)/GA1DArrayGenome.C $(topdir)/GA2DArrayGenome.C \
	$(topdir)/GA3DArrayGenome.C $(topdir)/GATreeBASE.C $(topdir)/GATree.C \
	$(topdir)/GATreeGenome.C $(topdir)/GAListBASE.C $(topdir)/GAList.C \
	$(topdir)/GAListGenome.C

libga_la_LDFLAGS = -version-info 6:7:4
libga_la_LIBADD =
