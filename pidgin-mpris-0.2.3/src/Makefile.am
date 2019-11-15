AM_CFLAGS = 			-g -g3 -O2 -Wall -DVERSION=\"$(VERSION)\"

pidgindir =			$(PIDGIN_INSTALL)

pidgin_LTLIBRARIES =		pidgin-mpris.la

pidgin_mpris_la_SOURCES =	pidgin-mpris.c

pidgin_mpris_la_CFLAGS =	$(pidgin_CFLAGS)	\
				$(gtk2_CFLAGS)		\
				$(dbus_CFLAGS)		\
				$(dbus_glib_CFLAGS)

pidgin_mpris_la_LDFLAGS =	-module			\
				-avoid-version		\
				-L$(PIDGIN_INSTALL)	\
				$(pidgin_LIBS)		\
				$(gtk2_LIBS)		\
				$(dbus_LIBS)		\
				$(dbus_glib_LIBS)
