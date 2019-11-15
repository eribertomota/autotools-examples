noinst_LIBRARIES = libutilsgl.a

libutilsglincludedir = $(includedir)/SDL

libutilsgl_a_SOURCES = \
	GLBitmapCollection.cpp \
	GLBitmapFont.cpp \
	GLExtension.cpp \
	GLMultiTexture.cpp \
	GLVertexArrayEXT.cpp \
	GLTexture.cpp \
	GLTextureCubeMap.cpp \
	Model.cpp \
	TextureManager.cpp \
	gl++.cpp

INCLUDES = -I../utils -I../utilssdl

depend:
	makedepend -I/usr/include/g++-3 $(DEFS) $(INCLUDES) $(AM_CPPFLAGS) $(CPPFLAGS) $(AM_CXXFLAGS) $(CXXFLAGS) $(libutilsgl_a_SOURCES)

MAINTAINERCLEANFILES = Makefile.bak Makefile.in
