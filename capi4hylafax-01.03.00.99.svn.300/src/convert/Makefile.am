## Process this file with automake to produce Makefile.in

AUTOMAKE_OPTIONS        = foreign
CLEANFILES              = *~ comperr
MAINTAINERCLEANFILES    = Makefile.in

INCLUDES                = -I$(srcdir)/../standard -I$(srcdir)/../linuxdep -I$(srcdir)/../capi -I$(srcdir)/..

noinst_HEADERS          = BasicFax.h ftif2huf.h huf2ftif.h huf2sff.h hufman.h osImport.h revbyte.h sff2huf.h
noinst_LIBRARIES        = libconvert.a

libconvert_a_SOURCES    = BasicFax.cpp ftif2huf.cpp huf2ftif.cpp huf2sff.cpp sff2huf.cpp

test: test.cpp libconvert.a
	$(CXX) $(CXXFLAGS) -O0 -I../standard -o test $< libconvert.a -ltiff    

