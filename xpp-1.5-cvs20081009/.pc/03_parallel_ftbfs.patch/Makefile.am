bin_PROGRAMS = xpp

xpp_SOURCES = mainwindow.fl mainwindow.cxx mainwindow.h \
	passworddialog.cxx cupshelper.cxx \
	xpp.cxx xppmain.cxx inputslider.cxx passworddialog.h \
	xpp.h cupshelper.h inputslider.h
#FLTK tries too hard, place it last or it will break the build
xpp_CPPFLAGS = -D_IPP_PRIVATE_STRUCTURES
xpp_CXXFLAGS= $(CUPS_CFLAGS) $(X_CFLAGS) $(FLTK_CXXFLAGS) $(AM_CXXFLAGS)
xpp_LDADD = $(CUPS_LIBS) $(X_PRE_LIBS) $(X_LIBS) $(X_EXTRA_LIBS) $(FLTK_LDFLAGS) $(AM_LDADD)
#xpp_LDFLAGS = $(all_libraries)

# .fl must be added as suffix because otherwise .fl files are not 
# compiled by fluid.
SUFFIXES = .cxx .h .o .fl

mainwindow.cxx:	mainwindow.fl
	$(FLUID) -c $<

mainwindow.h: mainwindow.cxx
	@if test -f "$@"; then \
		touch "$@" ; \
	else \
		rm -f mainwindow.cxx ;\
		$(MAKE) $(AM_MAKEFLAGS) mainwindow.cxx ;\
	fi

# removing the fluid-generated source files
mostlyclean-local:
	rm -f mainwindow.cxx mainwindow.h
