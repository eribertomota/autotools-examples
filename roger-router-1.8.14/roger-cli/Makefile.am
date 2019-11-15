bin_PROGRAMS = roger_cli

AM_CFLAGS = -I$(top_srcdir)

roger_cli_CFLAGS = $(EXTRA_CFLAGS) $(GMODULE_CFLAGS) -Wall -O2 -g -DAPP_PLUGINS=\"$(libdir)/roger_cli\" -DAPP_DATA=\"$(datadir)/roger_cli\" $(PEAS_GTK_CFLAGS) $(AM_CFLAGS)
roger_cli_LDFLAGS = $(EXTRA_LIBS) $(GMODULE_LIBS) -export-dynamic $(top_builddir)/libroutermanager/libroutermanager.la $(PEAS_GTK_LIBS)

roger_cli_SOURCES =\
	main_cli.c
