bin_PROGRAMS = gniall

INCLUDES =					\
	$(GNOME2_CFLAGS)

gniall_SOURCES = 				\
	gnome.c					\
	niall.c					\
	niall.h

gniall_LDADD =					\
	$(GNOME2_LIBS)

$(bin_PROGRAMS): gnome.o niall.o
gnome.o: niall.h
niall.o: niall.h

dist-hook:
	mkdir $(distdir)/otherStuff
	cp -p otherStuff/* $(distdir)/otherStuff
