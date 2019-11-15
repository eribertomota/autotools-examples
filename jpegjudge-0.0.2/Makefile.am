EXTRA_DIST = README-jpeg6a judge.1 judge.txt config.h.bot estim.h estim.c

AUTOMAKE_OPTIONS = foreign

man_MANS = judge.1
bin_PROGRAMS = judge
judge_SOURCES = judge.c

judge.txt: judge.1
	man -T ascii -l $< >$@

# everything below is maintainer-only!
# create manual page in -html format. Don't ask
copy-www: judge.txt all dist
