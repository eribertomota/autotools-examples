lib_LTLIBRARIES = \
  libogmjob.la

BUILT_SOURCES = \
  ogmjob-marshal.c \
  ogmjob-marshal.h

libogmjob_la_SOURCES = \
  ogmjob-bin.c       \
  ogmjob-container.c \
  ogmjob-exec.c      \
  ogmjob-list.c      \
  ogmjob-log.c       \
  ogmjob-marshal.c   \
  ogmjob-pipeline.c  \
  ogmjob-queue.c     \
  ogmjob-spawn.c

libogmjob_ladir = \
  $(includedir)/ogmjob

libogmjob_la_HEADERS =  \
  ogmjob-bin.h         \
  ogmjob-container.h   \
  ogmjob-exec.h        \
  ogmjob-list.h        \
  ogmjob-log.h         \
  ogmjob-marshal.h     \
  ogmjob-pipeline.h    \
  ogmjob-queue.h       \
  ogmjob-spawn.h       \
  ogmjob.h

libogmjob_la_LDFLAGS = \
  -version-info $(OGMJOB_LT_VERSION)

libogmjob_la_LIBADD =\
  $(OGMRIP_LIBS)

ogmjob-marshal.h: ogmjob-marshal.list $(GLIB_GENMARSHAL)
	$(GLIB_GENMARSHAL) $< --header --prefix=ogmjob_cclosure_marshal > $@

ogmjob-marshal.c: ogmjob-marshal.list $(GLIB_GENMARSHAL)
	echo "#include \"ogmjob-marshal.h\"" > $@ && \
	$(GLIB_GENMARSHAL) $< --body --prefix=ogmjob_cclosure_marshal >> $@

if MAINTAINER_MODE
DEBUG_CFLAGS = \
  -DG_ENABLE_DEBUG
endif

INCLUDES = \
  $(OGMRIP_CFLAGS) \
  $(DEBUG_CFLAGS)

EXTRA_DIST = \
  ogmjob-marshal.list

CLEANFILES = \
  $(BUILT_SOURCES)

