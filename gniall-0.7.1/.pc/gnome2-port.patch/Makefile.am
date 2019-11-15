bin_PROGRAMS = gniall

INCLUDES =					\
	$(GNOME_INCLUDEDIR)

gniall_SOURCES = 				\
	gnome.c					\
	niall.c					\
	niall.h

gniall_LDADD =					\
	$(GNOME_LIBDIR)                		\
	$(GNOMEUI_LIBS)

$(bin_PROGRAMS): gnome.o niall.o
gnome.o: niall.h
niall.o: niall.h

dist-hook:
	mkdir $(distdir)/otherStuff
	cp -p otherStuff/* $(distdir)/otherStuff
