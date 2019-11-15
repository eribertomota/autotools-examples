AM_CFLAGS = -W -Wall -Wshadow -W -Wpointer-arith \
	-Wcast-qual -Wcast-align -Wwrite-strings \
	-Wconversion -Wstrict-prototypes -Wmissing-prototypes \
	-Wmissing-declarations -Wredundant-decls \
	-Wnested-externs -Winline -Wundef -Wbad-function-cast \
	-Waggregate-return \
	-std=c99 \
	-D_POSIX_SOURCE -D_GNU_SOURCE \
	-I${top_builddir}

sbin_PROGRAMS = cpufreqd

cpufreqd_SOURCES = \
		main.c \
		config_parser.c \
		cpufreqd_log.c \
		daemon_utils.c \
		plugin_utils.c \
		sock_utils.c \
		cpufreq_utils.c \
		list.c

cpufreqd_LDFLAGS = -export-dynamic @CPUFREQD_LDFLAGS@

BUILD_PLUGINS = \
		cpufreqd_programs.la \
		cpufreqd_cpu.la

if ACPI_PLUGIN
#BUILD_PLUGINS += cpufreqd_acpi_battery.la \
#		 cpufreqd_acpi_temperature.la \
#		 cpufreqd_acpi_event.la \
#		 cpufreqd_acpi_ac.la
BUILD_PLUGINS += cpufreqd_acpi.la
endif
if NFORCE2_PLUGIN
BUILD_PLUGINS += cpufreqd_nforce2.la
endif
if NVCLOCK_PLUGIN
BUILD_PLUGINS += cpufreqd_nvclock.la
endif
if APM_PLUGIN
BUILD_PLUGINS += cpufreqd_apm.la
endif
if PMU_PLUGIN
BUILD_PLUGINS += cpufreqd_pmu.la
endif
if SENSORS_PLUGIN
BUILD_PLUGINS += cpufreqd_sensors.la
endif
if EXEC_PLUGIN
BUILD_PLUGINS += cpufreqd_exec.la
endif
if GOVERNOR_PARAMETERS_PLUGIN
BUILD_PLUGINS += cpufreqd_governor_parameters.la
endif
if TAU_PLUGIN
BUILD_PLUGINS += cpufreqd_tau.la
endif

lib_LTLIBRARIES = $(BUILD_PLUGINS)

if NFORCE2_PLUGIN
cpufreqd_nforce2_la_SOURCES = \
		cpufreqd_nforce2.c

cpufreqd_nforce2_la_LDFLAGS = \
		-module -avoid-version
endif

if NVCLOCK_PLUGIN
cpufreqd_nvclock_la_SOURCES = \
		cpufreqd_nvclock.c

cpufreqd_nvclock_la_CFLAGS = \
		$(AM_CFLAGS) -I/@NVCLOCK_SRCDIR@/src/backend

cpufreqd_nvclock_la_LDFLAGS = \
		-module -avoid-version -L/@NVCLOCK_SRCDIR@/src/backend -lbackend
endif

if PMU_PLUGIN
cpufreqd_pmu_la_SOURCES = \
		cpufreqd_pmu.c

cpufreqd_pmu_la_LDFLAGS = \
		-module -avoid-version
endif

if APM_PLUGIN
cpufreqd_apm_la_SOURCES = \
		cpufreqd_apm.c

cpufreqd_apm_la_LDFLAGS = \
		-module -avoid-version
endif

if ACPI_PLUGIN
cpufreqd_acpi_la_SOURCES = \
		cpufreqd_acpi.c \
		cpufreqd_acpi_ac.c \
		cpufreqd_acpi_battery.c \
		cpufreqd_acpi_event.c \
		cpufreqd_acpi_temperature.c

cpufreqd_acpi_la_CFLAGS = \
		$(AM_CFLAGS) -I/@PTHREAD_SRCDIR@/include -I/usr/include/sysfs

cpufreqd_acpi_la_LDFLAGS = \
		-module -avoid-version -L/@PTHREAD_SRCDIR@/lib -lpthread -lsysfs

#cpufreqd_acpi_ac_la_SOURCES = \
#		cpufreqd_acpi_ac.c
#
#cpufreqd_acpi_ac_la_LDFLAGS = \
#		-module -avoid-version
#
#cpufreqd_acpi_temperature_la_SOURCES = \
#		cpufreqd_acpi_temperature.c
#
#cpufreqd_acpi_temperature_la_LDFLAGS = \
#		-module -avoid-version
#
#cpufreqd_acpi_event_la_SOURCES = \
#		cpufreqd_acpi_event.c
#
#cpufreqd_acpi_event_la_CFLAGS = \
#		$(AM_CFLAGS) -I/@PTHREAD_SRCDIR@/include
#
#cpufreqd_acpi_event_la_LDFLAGS = \
#		-module -avoid-version -L/@PTHREAD_SRCDIR@/lib -lpthread
#
#cpufreqd_acpi_battery_la_SOURCES = \
#		cpufreqd_acpi_battery.c
#
#cpufreqd_acpi_battery_la_LDFLAGS = \
#		-module -avoid-version
endif

cpufreqd_cpu_la_SOURCES = \
		cpufreqd_cpu.c

cpufreqd_cpu_la_LDFLAGS = \
		-module -avoid-version

cpufreqd_programs_la_SOURCES = \
		cpufreqd_programs.c

cpufreqd_programs_la_LDFLAGS = \
		-module -avoid-version

if EXEC_PLUGIN
cpufreqd_exec_la_SOURCES = \
		cpufreqd_exec.c

cpufreqd_exec_la_CFLAGS = \
		$(AM_CFLAGS) -I/@PTHREAD_SRCDIR@/include

cpufreqd_exec_la_LDFLAGS = \
		-module -avoid-version -L/@PTHREAD_SRCDIR@/lib -lpthread
endif

if SENSORS_PLUGIN
cpufreqd_sensors_la_SOURCES = \
		cpufreqd_sensors.c

cpufreqd_sensors_la_CFLAGS = \
		$(AM_CFLAGS) -I/@SENSORS_SRCDIR@/include

cpufreqd_sensors_la_LDFLAGS = \
		-module -avoid-version -L/@SENSORS_SRCDIR@/lib -lsensors
endif

if GOVERNOR_PARAMETERS_PLUGIN
cpufreqd_governor_parameters_la_SOURCES = \
		cpufreqd_governor_parameters.c

cpufreqd_governor_parameters_la_CFLAGS = \
		$(AM_CFLAGS) -I/usr/include/sysfs

cpufreqd_governor_parameters_la_LDFLAGS = \
		-module -avoid-version -lsysfs
endif

if TAU_PLUGIN
cpufreqd_tau_la_SOURCES = \
		cpufreqd_tau.c

cpufreqd_tau_la_LDFLAGS = \
		-module -avoid-version
endif

noinst_HEADERS = \
		cpufreqd.h \
		cpufreqd_plugin.h \
		cpufreqd_log.h \
		cpufreqd_acpi.h \
		cpufreqd_acpi_ac.h \
		cpufreqd_acpi_battery.h \
		cpufreqd_acpi_event.h \
		cpufreqd_acpi_temperature.h \
		cpufreq_utils.h \
		daemon_utils.h \
		plugin_utils.h \
		cpufreqd_remote.h \
		sock_utils.h \
		config_parser.h \
		list.h

