INCLUDES =						\
	-I$(top_srcdir)					\
	-I$(top_builddir)				\
	$(EDS_BACKEND_CFLAGS)				

SUBDIRS = utils planner-source

extension_LTLIBRARIES = libecalbackendplanner.la

libecalbackendplanner_la_SOURCES =			\
	e-cal-backend-planner-factory.c     		\
	e-cal-backend-planner-factory.h			\
	e-cal-backend-planner.c				\
	e-cal-backend-planner.h

libecalbackendplanner_la_LIBADD =		 	\
	$(top_builddir)/libplanner/libplanner-1.la 	\
	$(EDS_BACKEND_LIBS)				
