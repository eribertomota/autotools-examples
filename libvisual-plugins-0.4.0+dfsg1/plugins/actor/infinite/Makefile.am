## Process this file with automake to generate a Makefile.in

actor_plugin_LTLIBRARIES = actor_infinite.la

AM_CFLAGS = $(LIBVISUAL_CFLAGS)

INCLUDES = $(all_includes) -I$(top_srcdir) 

actor_infinite_la_LDFLAGS = -module -avoid-version 
actor_infinite_la_LIBADD = $(LIBVISUAL_LIBS)

actor_infinite_la_SOURCES = compute.c compute.h \
			    display.c display.h \
			    renderer.c renderer.h \
			    file.c lv_infinite.c \
			    main.h

