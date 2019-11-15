CPPFLAGS =	@CPPFLAGS@ \
		-DDEFAULT_CONF=\"$(sysconfdir)/bbtools/bbtime.conf\" \
		-DDEFAULT_NOBB=\"$(sysconfdir)/bbtools/bbtime.nobb\"


SUBDIRS = data
bin_PROGRAMS = bbtime
bbtime_SOURCES = bbtime.cc Image.cc LinkedList.cc \
		 bbtime.hh Image.hh LinkedList.hh \
		 resource.cc resource.hh \
		 Baseresource.cc Baseresource.hh \
		 Basewindow.cc Basewindow.hh \
		 Basemenu.cc Basemenu.hh \
		 timemenu.cc timemenu.hh \
		 blackboxstyle.hh
EXTRA_DIST = BUGS TODO
bbtime_LDADD = @X_LIBS@
