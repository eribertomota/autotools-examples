if BUILD_SSG

lib_LTLIBRARIES = libplibssg.la

include_HEADERS = ssg.h ssgconf.h ssgMSFSPalette.h ssgKeyFlier.h pcx.h

libplibssg_la_SOURCES = ssg.cxx ssgAnimation.cxx ssgBase.cxx \
	ssgBaseTransform.cxx ssgBranch.cxx ssgContext.cxx ssgCutout.cxx \
	ssgDList.cxx ssgEntity.cxx ssgIsect.cxx ssgLeaf.cxx ssgList.cxx \
	ssgLoadDOF.cxx ssgLoadAC.cxx \
        ssgLocal.h ssgOptimiser.cxx ssgRoot.cxx ssgSaveAC.cxx \
	ssgSelector.cxx ssgSimpleState.cxx ssgState.cxx ssgStateTables.cxx \
	ssgStats.cxx  ssgTween.cxx ssgTweenController.cxx \
	ssgTexTrans.cxx ssgTexture.cxx ssgTransform.cxx \
	ssgStateSelector.cxx ssgRangeSelector.cxx ssgLoadTexture.cxx \
	ssgLoadBMP.cxx ssgLoadSGI.cxx ssgLoadPNG.cxx ssgLoadTGA.cxx \
	ssgLoadPCX.cxx ssgInvisible.cxx ssgLoadSSG.cxx ssgVTable.cxx \
	ssgSimpleList.cxx ssgVtxTable.cxx ssgIO.cxx ssgLoad3ds.cxx \
	ssgSaveASE.cxx ssgLoadASE.cxx ssgParser.cxx ssgParser.h \
	ssgLoadDXF.cxx ssgSaveDXF.cxx ssgLoadTRI.cxx ssgSaveTRI.cxx \
	ssgLoadOBJ.cxx ssgSaveOBJ.cxx ssgVtxArray.cxx ssgLoadMD2.cxx \
	ssgLoadMDL.cxx ssgLoadX.cxx ssgSaveX.cxx ssgLoaderWriterStuff.cxx \
	ssgLoadFLT.cxx ssgLoadM.cxx ssgSaveM.cxx ssgLoadStrip.cxx \
	ssgLoadOFF.cxx ssgSaveOFF.cxx ssgSaveQHI.cxx ssgLoadVRML1.cxx \
	ssgSaveVRML1.cxx ssgLoaderWriterStuff.h ssgMSFSPalette.h ssg3ds.h \
	ssgLoadMDL.h ssgSave3ds.cxx ssgAxisTransform.cxx ssgLoadATG.cxx \
	ssgSaveFLT.cxx ssgSaveATG.cxx ssgLoadIV.cxx ssgLoad.cxx ssgLoadVRML.h \
	ssgLoadMDL_BGLTexture.cxx ssgLoadXPlaneObj.cxx ssgLoadASC.cxx ssgSaveASC.cxx \
	ssgSaveIV.cxx ssgAnimTransform.cxx\
	ssgVertSplitter.h ssgVertSplitter.cxx ssgStatistics.cxx
libplibssg_la_LIBADD = ../util/libplibul.la ../sg/libplibsg.la
libplibssg_la_LDFLAGS = -version-info 9:5:8

INCLUDES = -I$(top_srcdir)/src/sg -I$(top_srcdir)/src/util

endif

EXTRA_DIST = ssg.dsp

