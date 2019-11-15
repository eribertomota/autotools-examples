SUBDIRS = files

INCLUDES = \
	-I$(top_srcdir)					\
	-I$(top_srcdir)/tests				\
	$(PLANNER_CFLAGS) $(WARN_CFLAGS)		\
	-DG_LOG_DOMAIN=\"Planner\"			\
	-DEXAMPLESDIR=\"$(top_srcdir)/tests/files\"

LDADD =	\
	$(top_builddir)/src/libplannerapp.la \
	$(top_builddir)/libplanner/libplanner-1.la \
	$(PLANNER_LIBS)

check_LTLIBRARIES = libselfcheck.la

libselfcheck_la_SOURCES =                              \
       self-check.c                                    \
       self-check.h

check_PROGRAMS = $(TESTS)

scheduler_test_SOURCES = scheduler-test.c
scheduler_test_LDADD = $(LDADD) libselfcheck.la

time_test_SOURCES = time-test.c
time_test_LDADD = $(LDADD) libselfcheck.la

calendar_test_SOURCES = calendar-test.c
calendar_test_LDADD = $(LDADD) libselfcheck.la

task_test_SOURCES = task-test.c
task_test_LDADD = $(LDADD) libselfcheck.la

cmd_manager_test_SOURCES = cmd-manager-test.c
cmd_manager_test_LDADD = $(LDADD) libselfcheck.la

TESTS_ENVIRONMENT = \
	PLANNER_STORAGEMODULEDIR=$(top_builddir)/libplanner/.libs \
	PLANNER_FILEMODULESDIR=$(top_builddir)/libplanner/.libs \
	PLANNER_PLUGINDIR=$(top_builddir)/src/.libs \
	PLANNER_DATADIR=$(top_srcdir)/data

TESTS = \
	calendar-test \
	cmd-manager-test \
	scheduler-test \
	task-test \
	time-test

