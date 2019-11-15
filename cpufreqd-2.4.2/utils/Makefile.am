AM_CFLAGS = -W -Wall -Wshadow -W -Wpointer-arith \
	-Wcast-qual -Wcast-align -Wwrite-strings \
	-Wconversion -Wstrict-prototypes -Wmissing-prototypes \
	-Wmissing-declarations -Wredundant-decls \
	-Wnested-externs -Winline -Wundef -Wbad-function-cast \
	-Waggregate-return \
	-std=c99 -pedantic \
	-D_POSIX_SOURCE -D_GNU_SOURCE \
	-I${top_srcdir}/src

bin_PROGRAMS = cpufreqd-set cpufreqd-get

cpufreqd_set_SOURCES = setspeed.c

cpufreqd_get_SOURCES = getspeed.c

