if SYSV_SCRIPTS_ENABLED
HED_SCRIPT = arched
else
HED_SCRIPT =
endif
initd_SCRIPTS = $(HED_SCRIPT)

if SYSTEMD_UNITS_ENABLED
HED_UNIT = arched.service
else
HED_UNIT =
endif
units_DATA = $(HED_UNIT)

pkgdata_SCRIPTS = arched-start
