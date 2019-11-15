## Process this file with automake to produce Makefile.in

## Created by Anjuta

INCLUDES = \
	-DPACKAGE_SRC_DIR=\""$(srcdir)"\" \
	-DPACKAGE_DATA_DIR=\""$(datadir)"\"

AM_CFLAGS =\
	 -Wall\
	 -g

bin_PROGRAMS = open-invaders

open_invaders_SOURCES = \
	main.cc        \
	collision.cc        \
	ending.cc        \
	graphics.cc        \
	init.cc        \
	input.cc        \
	interrupt.cc        \
	intro.cc        \
	logic.cc        \
	pmask.c        \
	sound.cc        \
	unlock.cc        \
	../headers/collision.h        \
	../headers/declare.h        \
	../headers/ending.h        \
	../headers/graphics.h        \
	../headers/init.h        \
	../headers/input.h        \
	../headers/interrupt.h        \
	../headers/intro.h        \
	../headers/logic.h        \
	../headers/main.h        \
	../headers/pmask.h        \
	../headers/sound.h        \
	../headers/unlock.h        

open_invaders_LDFLAGS =  \
	-laldmd  \
	-ldumbd  \
	`allegro-config  \
	--libs`

open_invaders_LDADD = 

