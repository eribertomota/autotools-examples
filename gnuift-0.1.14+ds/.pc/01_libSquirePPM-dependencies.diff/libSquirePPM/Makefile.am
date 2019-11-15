noinst_LIBRARIES= libSquirePPM.a

noinst_HEADERS=normaliseContrast.h  ppm.h  ppm_noproto.h  typedefs.h

libSquirePPM_a_SOURCES= ppm_comment.c\
		ppm_error.c\
		ppm_io.c\
		ppm_memory.c\
		ppm_normalize.c\
		ppm_plane.c\
		ppm_subimage.c\
		normaliseContrast.c

noinst_PROGRAMS= ppm-new-executable

ppm_new_executable_LDADD= -L. -lSquirePPM -lm

ppm_new_executable_SOURCES= new_executable.c 


