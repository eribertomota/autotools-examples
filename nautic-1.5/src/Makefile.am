# what flags you want to pass to the C compiler & linker
AM_CPPFLAGS = -I$(top_srcdir)/gnulib/lib -I$(top_builddir)/gnulib/lib
CFLAGS = --pedantic -Wall -std=c99 -O2 -ansi
AM_LDFLAGS =

# this lists the binaries to produce, the (non-PHONY, binary) targets in
# the previous manual Makefile
bin_PROGRAMS = nautic
nautic_SOURCES = main.cpp main.h aberration.cpp about.cpp delta_t.cpp fund_arg.cpp\
          gui.cpp  h_correction.cpp ge2000a_data.cpp Info_Dlg.cpp \
          julian_date.cpp  nutation.cpp orbital_elements.cpp plot_dialog.cpp Pos_dialog.cpp\
          precession.cpp sofa.cpp spa.cpp starpos.cpp stars.cpp Sun.cpp un_known_star.cpp\
          aberration.h about.h addings.h coordinate.h delta_t.h fund_args.h gui.h\
          h_correction.h Info_Dlg.h julian_date.h kepler.h moon.h nutation.h\
           orbital_elements.h plant.h plot_dialog.h Pos_dialog.h precession.h sofa.h\
          sofam.h spa.h starpos.h stars.h sun.h un_known_star.h sext.ico star.cat\
          stnam.cat pos.cat

