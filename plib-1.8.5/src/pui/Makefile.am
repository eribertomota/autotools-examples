if BUILD_PUI

lib_LTLIBRARIES = libplibpu.la

include_HEADERS = pu.h puGLUT.h puFLTK.h puSDL.h puNative.h puPW.h

libplibpu_la_SOURCES = \
        pu.cxx            puBox.cxx       puButton.cxx puButtonBox.cxx    \
        puArrowButton.cxx puDialogBox.cxx puFrame.cxx  puGroup.cxx        \
        puInput.cxx       puInterface.cxx puLocal.h    puMenuBar.cxx      \
        puObject.cxx      puOneShot.cxx   puPopup.cxx  puPopupMenu.cxx    \
        puListBox.cxx   puSlider.cxx puText.cxx         \
        puValue.cxx       puFont.cxx      \
        puDial.cxx        \
        puRange.cxx	  \
        puInputBase.cxx
libplibpu_la_LIBADD = ../util/libplibul.la ../fnt/libplibfnt.la
libplibpu_la_LDFLAGS = -version-info 9:5:8

AM_CPPFLAGS = -I$(top_srcdir)/src/sg -I$(top_srcdir)/src/fnt
AM_CPPFLAGS += -I$(top_srcdir)/src/util

endif

EXTRA_DIST = pui.dsp
