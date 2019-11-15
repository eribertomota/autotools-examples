bin_PROGRAMS = tabble

INCLUDES = $(GTK_CFLAGS)
AM_CFLAGS = -O2 `pkg-config --cflags gtk+-2.0`
LIBS = `pkg-config --libs gtk+-2.0`

tabble_SOURCES = add_stuff.c choices.c edits.c icon.c options.c read_line.c \
  tabble.c load_lists.c save_lists.c signals.c icons.c

noinst_HEADERS = add_stuff.h choices.h edits.h icon.h options.h read_line.h \
  world.h load_lists.h save_lists.h signals.h icons.h

