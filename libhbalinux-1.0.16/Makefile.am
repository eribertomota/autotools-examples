AM_CFLAGS = $(HBAAPI_CFLAGS) $(PCIACCESS_CFLAGS)
AM_LDFLAGS= $(PCIACCESS_LIBS)

lib_LTLIBRARIES = libhbalinux.la
libhbalinux_la_SOURCES = adapt.c adapt_impl.h api_lib.h bind.c bind_impl.h \
fc_scsi.h fc_types.h lib.c lport.c net_types.h pci.c rport.c scsi.c sg.c \
utils.c utils.h
libhbalinux_la_LDFLAGS = -version-info 2:2:0
libhbalinux_la_LIBADD = $(PCIACCESS_LIBS)

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libhbalinux.pc

dist_noinst_DATA = README COPYING INSTALL libhbalinux.pc.in libhbalinux.spec

install-data-hook: libhbalinux.la
	. $${PWD}/$<; \
	ORG=org.open-fcoe.libhbalinux; \
	LIB=${libdir}/$${dlname}; \
	STR="$$ORG	$$LIB"; \
	CONF=${sysconfdir}/hba.conf; \
	if test -f $$CONF; then \
		grep -E -q ^[[:space:]]*$$ORG[[:space:]]+$$LIB $$CONF; \
		if test $$? -ne 0; then \
			echo $$STR >> $$CONF; \
		else \
			echo "** $$CONF already configured"; \
			echo "** system configuration not updated"; \
		fi; \
	else \
		echo "** WARNING: $$CONF does not exist"; \
		echo "** system configuration not updated"; \
	fi

