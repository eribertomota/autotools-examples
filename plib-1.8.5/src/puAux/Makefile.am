if BUILD_PUAUX

lib_LTLIBRARIES = libplibpuaux.la

include_HEADERS = puAux.h puAuxLocal.h

libplibpuaux_la_SOURCES = puAux.cxx                  \
                         puAuxBiSlider.cxx          \
                         puAuxBiSliderWithEnds.cxx  \
                         puAuxComboBox.cxx          \
                         puAuxCompass.cxx           \
                         puAuxFileSelector.cxx      \
                         puAuxLargeInput.cxx        \
                         puAuxList.cxx              \
                         puAuxScrollBar.cxx         \
                         puAuxSelectBox.cxx         \
                         puAuxSliderWithInput.cxx   \
                         puAuxSpinBox.cxx           \
                         puAuxTriSlider.cxx         \
                         puAuxVerticalMenu.cxx      \
                         puAuxChooser.cxx
libplibpuaux_la_LIBADD = ../util/libplibul.la ../pui/libplibpu.la \
	../fnt/libplibfnt.la ../sg/libplibsg.la
libplibpuaux_la_LDFLAGS = -version-info 9:5:8

INCLUDES = -I$(top_srcdir)/src/sg  \
           -I$(top_srcdir)/src/pui \
           -I$(top_srcdir)/src/fnt \
           -I$(top_srcdir)/src/util

endif

EXTRA_DIST = puAux.dsp


