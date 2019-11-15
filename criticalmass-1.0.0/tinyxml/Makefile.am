noinst_LIBRARIES = libtinyxml.a

libtinyxmlincludedir = $(includedir)/SDL

libtinyxml_a_SOURCES = \
         tinyxml.cpp \
         tinyxmlerror.cpp \
         tinyxmlparser.cpp

depend:
	makedepend -I/usr/include/g++-3 $(DEFS) $(INCLUDES) $(AM_CPPFLAGS) $(CPPFLAGS) $(AM_CXXFLAGS) $(CXXFLAGS) $(libtinyxml_a_SOURCES)

MAINTAINERCLEANFILES = Makefile.bak Makefile.in
