# Help DFArc look for either 'dink' or 'dink.exe':
AM_CPPFLAGS = -DEXEEXT=\"$(EXEEXT)\"
# Cf. (autoconf.info)Installation Directory Variables:
# Don't use DATADIR, it conflicts with something in MinGW
AM_CPPFLAGS += -DDEFAULT_DATA_DIR=\"$(datadir)\"

bin_PROGRAMS = dfarc
dfarc_SOURCES = BZip.cpp BZip.hpp ClientData.hpp Config.cpp Config.hpp	\
	DFArcApp.cpp DFArcFrame.cpp DFArcFrame.hpp DFile.cpp DFile.hpp	\
	DMod.cpp DMod.hpp icon_xpm.cpp icon_xpm.hpp IOUtils.cpp		\
	IOUtils.hpp InstallVerifyFrame.cpp InstallVerifyFrame.hpp	\
	Options.cpp Options.hpp Package.cpp Package.hpp			\
	RecursiveDelete.cpp RecursiveDelete.hpp Tar.cpp Tar.hpp		\
	DFArcFrame_Base.cpp DFArcFrame_Base.h Options_Base.cpp		\
	Options_Base.h Package_Base.cpp Package_Base.h			\
	InstallVerifyFrame_Base.cpp InstallVerifyFrame_Base.h

# DFArcFrame_Base.cpp/h will be automatically generated before the
# rest of the source code. In addition, they will be included in
# tarballs, so people won't need wxglade to compile DFArc :)
# Using $(srcdir) so that the .po build system will find them
BUILT_SOURCES = $(srcdir)/DFArcFrame_Base.cpp						\
	$(srcdir)/DFArcFrame_Base.h $(srcdir)/Options_Base.cpp				\
	$(srcdir)/Options_Base.h $(srcdir)/Package_Base.cpp $(srcdir)/Package_Base.h	\
	$(srcdir)/InstallVerifyFrame_Base.cpp $(srcdir)/InstallVerifyFrame_Base.h
CLEANFILES = $(BUILT_SOURCES)
EXTRA_DIST = DFArcFrame_Base.wxg Options_Base.wxg Package_Base.wxg	\
	InstallVerifyFrame_Base.wxg
# work-around for wxglade < 2.6.9
AM_CPPFLAGS += -DwxTHICK_FRAME=wxRESIZE_BORDER
# disable obnoxious wxWidgets3 assertions
AM_CPPFLAGS += -DNDEBUG


# How do we handle resources embedded in the executable binary?
if HAVE_WINDRES
nodist_dfarc_SOURCES = woeres.rc
endif

if HAVE_WXGLADE
# wxGlade (GUI builder) code generation
.wxg.cpp:
	$(AM_V_GEN)
	$(AM_V_at) $(WXGLADE) -g C++ -o $@ $<
else
.wxg.cpp:
	@echo
	@echo "  Please install 'wxglade' to rebuild the '.wxg' GUI files"
	@echo "  (and then run ./config.status --recheck)"
	@echo
	exit 1
endif
# Woe icon and app infos
# Also check http://fragglet.livejournal.com/4448.html
.rc.o:
	$(WINDRES) -i $< -o $@

install-exec-hook:
if HAVE_UPX
# UPX compression
# Needs to be done before bundling resources
# Not using --best because it takes much more time and the result is
# only a little bit smaller
	-$(UPX) "$(DESTDIR)$(bindir)/dfarc$(EXEEXT)"
endif
# Add 'freedink-dfarc' alias so that command-line FreeDink users see
# the front-end more easily (via tab completion)
	$(LN_S) -f "dfarc$(EXEEXT)" "$(DESTDIR)$(bindir)/freedink-dfarc$(EXEEXT)"

uninstall-hook:
	rm -f "$(DESTDIR)$(bindir)/freedink-dfarc$(EXEEXT)"


EXTRA_DIST += dink.ico


# For reference, wxGlade (GUI builder) alternate 2-steps code
# generation:
#.wxg.xrc:
#	$(WXGLADE) -g XRC -o $@ $<
#.xrc.cpp:
#	$(WXRC) -c -e -o $@ -n Init$* $<
##	Fix GCC-4.2 + wxrc-2.6 warning
#	sed -i -e 's/$*:://g' $*.h
