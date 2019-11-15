if DATA_CLIENT_ENABLED
DATA_CLIENT = data
else
DATA_CLIENT =
endif

if CREDENTIALS_CLIENT_ENABLED
CREDENTIALS_CLIENT = credentials
else
CREDENTIALS_CLIENT =
endif

if COMPUTE_CLIENT_ENABLED
COMPUTE_CLIENT = compute
else
COMPUTE_CLIENT =
endif

SUBDIRS = $(DATA_CLIENT) $(CREDENTIALS_CLIENT) $(COMPUTE_CLIENT) 
DIST_SUBDIRS = data credentials compute

arcsysconfdir = $(sysconfdir)/arc
arcsysconf_DATA = client.conf
exampledir = $(pkgdatadir)/examples
example_DATA = client.conf
EXTRA_DIST = $(example_DATA) $(arcsysconf_DATA)

