if A_REX_SERVICE_ENABLED
AREX_SERVICE = a-rex
else
AREX_SERVICE =
endif

if GRIDFTPD_SERVICE_ENABLED
GRIDFTPD_SERVICE = gridftpd
else
GRIDFTPD_SERVICE =
endif

if LDAP_SERVICE_ENABLED
LDAP_SERVICE = ldap-infosys
else
LDAP_SERVICE =
endif

if MONITOR_ENABLED
MONITOR = monitor
else
MONITOR =
endif

if CANDYPOND_ENABLED
CANDYPOND_SERVICE = candypond
else
CANDYPOND_SERVICE =
endif

if DATADELIVERY_SERVICE_ENABLED
DATADELIVERY_SERVICE = data-staging
else
DATADELIVERY_SERVICE =
endif

if ACIX_ENABLED
ACIX = acix
else
ACIX =
endif

SUBDIRS = $(GRIDFTPD_SERVICE) $(AREX_SERVICE) $(LDAP_SERVICE) \
	$(MONITOR) \
	$(CANDYPOND_SERVICE) \
	$(DATADELIVERY_SERVICE) \
	$(ACIX) \
	wrappers examples
DIST_SUBDIRS = gridftpd a-rex ldap-infosys \
	monitor \
	candypond \
	data-staging wrappers examples acix

