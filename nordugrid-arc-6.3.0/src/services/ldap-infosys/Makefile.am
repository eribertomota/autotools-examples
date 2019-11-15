if SYSV_SCRIPTS_ENABLED
GRID_INFOSYS_SCRIPT = arc-infosys-ldap
else
GRID_INFOSYS_SCRIPT = 
endif

initd_SCRIPTS = $(GRID_INFOSYS_SCRIPT)

if SYSTEMD_UNITS_ENABLED
GRID_INFOSYS_UNIT = arc-infosys-ldap.service arc-infosys-ldap-slapd.service
else
GRID_INFOSYS_UNIT =
endif

units_DATA = $(GRID_INFOSYS_UNIT)

pkgdata_SCRIPTS = create-bdii-config create-slapd-config
