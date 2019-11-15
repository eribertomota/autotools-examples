if FLTK_OPT
  FLTK_OPT_DIR=GUI
endif 

bin_PROGRAMS = ed2k_hash

ed2k_hash_SOURCES = md4.c processfile.c linkedlist.c options.c cl_ui.c main.c 
ed2k_hash_LDADD   = 


SUBDIRS = docs $(FLTK_OPT_DIR)

EXTRA_DIST = cl_ui.h options.h linkedlist.h ui.h processfile.h md4.h global.h Makefile.mingw32 

