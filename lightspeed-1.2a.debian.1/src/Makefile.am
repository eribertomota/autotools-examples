## src/Makefile.am

localedir = $(datadir)/locale

#this is mandated by GNU standards
#   ( see 'info autoconf' at section 'Installation Directory Variables' )
lightspeed_CPPFLAGS=$(CPPFLAGS) -DLOCALEDIR=\"$(localedir)\" -DDATADIR=\"$(datadir)\"

lightspeed_CFLAGS=$(GTK_CFLAGS) $(GL_CFLAGS)  $(GTKGL_CFLAGS)
lightspeed_CXXFLAGS=$(GTK_CFLAGS) $(GL_CFLAGS) $(GTKGL_CFLAGS) $(FTGL_CFLAGS) $(FC_CFLAGS)
lightspeed_LDADD=$(GTKGL_LIBS) $(GTK_LIBS) $(GL_LIBS) $(FTGL_LIBS)  $(FC_LIBS) $(IMG_LIBS)

bin_PROGRAMS = lightspeed

if COND_FTGL
o=ogl-ftgl.cc
else
if COND_GTK1
o=ogl-gtk1.c
else
o=ogl-gtk2.c
endif
endif

lightspeed_SOURCES = \
        compat.h \
        lightspeed.h \
        lstrings.h \
        read3ds.h \
        readlwo.h \
        settings.h \
        trackmem.h \
        animation.c \
        auxobjects.c \
        camera.c \
        command.c \
        geometry.c \
        globals.c \
        gtkwidgets.c \
        importobjs.c \
        infodisp.c \
        lattice.c \
        lightspeed.c \
        lstrings.c \
        mainwindow.c \
        menu_cbs.c \
        misc.c \
        ogl.c $(o) \
        read3ds.c \
        readlwo.c \
        snapshot.c \
        trackmem.c \
        warp.c

EXTRA_DIST = gtkglext-workaround.c \
	icon.xpm \
	title.xpm

## end src/Makefile.am
