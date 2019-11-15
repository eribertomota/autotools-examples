
if BUILD_PSL

lib_LTLIBRARIES = libplibpsl.la

include_HEADERS = psl.h

libplibpsl_la_SOURCES = psl.cxx pslCodeGen.cxx pslContext.cxx \
                       pslCompiler.cxx pslSymbols.cxx pslToken.cxx \
                       pslExpression.cxx pslProgram.cxx pslDump.cxx \
                       pslError.cxx pslFileIO.cxx pslCompiler.h \
                       pslContext.h pslFileIO.h pslLocal.h \
                       pslOpcodes.h pslSymbol.h
libplibpsl_la_LIBADD = ../util/libplibul.la
libplibpsl_la_LDFLAGS = -version-info 9:5:8

INCLUDES = -I$(top_srcdir)/src/util

endif

EXTRA_DIST = psl.dsp

