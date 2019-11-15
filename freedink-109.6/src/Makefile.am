AM_CXXFLAGS = -std=c++11 -Wno-write-strings -Wall
# Cf. (autoconf.info)Installation Directory Variables:
# Don't use DATADIR, it conflicts with something in MinGW
AM_CPPFLAGS = -DBUILD_DATA_DIR=\"$(datadir)\"

# Gnulib:
# includes generated files from top_builddir (not only top_srcdir)
AM_CPPFLAGS += -I$(top_srcdir)/gnulib/lib -I$(top_builddir)/gnulib/lib
LDADD = $(top_builddir)/gnulib/lib/libgnu.a

# gettext:
# Relative locale dir for woe/android
if WOE
AM_CPPFLAGS += -DLOCALEDIR=\"freedink/locale\"
else
if ANDROID
AM_CPPFLAGS += -DLOCALEDIR=\"freedink/locale\"
else
AM_CPPFLAGS += -DLOCALEDIR=\"$(localedir)\"
endif
endif
LDADD += @LIBINTL@
AM_CPPFLAGS += -I$(top_srcdir)/intl -I$(top_builddir)/intl

LIBS += -lm

COMMON_OBJS = app.cpp app.h bgm.cpp bgm.h BgTilesetsManager.cpp		\
	BgTilesetsManager.h dinkini.cpp dinkini.h DMod.cpp DMod.h	\
	fastfile.cpp fastfile.h str_util.cpp str_util.h io_util.cpp	\
	io_util.h EditorMap.cpp EditorMap.h editor_screen.cpp		\
	editor_screen.h gfx.cpp gfx.h gfx_tiles.cpp gfx_tiles.h		\
	gfx_palette.cpp gfx_palette.h gfx_fonts.cpp gfx_fonts.h		\
	hardness_tiles.cpp hardness_tiles.h ImageLoader.cpp		\
	ImageLoader.h IOGfxDisplay.cpp IOGfxDisplay.h			\
	IOGfxDisplayGL2.cpp IOGfxDisplayGL2.h IOGfxGLFuncs.cpp		\
	IOGfxGLFuncs.h IOGfxDisplaySW.cpp IOGfxDisplaySW.h		\
	IOGfxSurface.cpp IOGfxSurface.h IOGfxSurfaceGL2.cpp		\
	IOGfxSurfaceGL2.h IOGfxSurfaceSW.cpp IOGfxSurfaceSW.h		\
	IOGfxPrimitivesSW.cpp IOGfxPrimitives.h live_screen.cpp		\
	live_screen.h live_sprite.cpp live_sprite.h			\
	live_sprites_manager.cpp live_sprites_manager.h rect.cpp	\
	rect.h resources.cpp resources.h input.cpp input.h		\
	freedink_xpm.cpp freedink_xpm.h paths.cpp paths.h log.cpp	\
	log.h gfx_sprites.cpp gfx_sprites.h vgasys_fon.cpp		\
	vgasys_fon.h SDL_android_main.c sfx.cpp sfx.h
if ANDROID
  # Build .so JNI libs rather than executables
  # Define here rather than configure.ac, otherwise config.h gets confused
  AM_CFLAGS = -fPIC
  freedink_LDFLAGS = -shared
  LIBS += -llog
endif

bin_PROGRAMS = freedink freedinkedit
freedink_SOURCES = $(COMMON_OBJS) AppFreeDink.cpp AppFreeDink.h		\
	IOTouchDragAnywhere.cpp IOTouchDragAnywhere.h freedink.cpp	\
	freedink.h freedink_main.cpp update_frame.cpp update_frame.h	\
	brains.h brain.cpp brain.h brain_bounce.cpp brain_button.cpp	\
	brain_diagonal.cpp brain_duck.cpp brain_keyboard.cpp		\
	brain_lateral.cpp brain_missile.cpp brain_mouse.cpp		\
	brain_none.cpp brain_onetime.cpp brain_people.cpp		\
	brain_pig.cpp brain_repeat.cpp brain_scale.cpp			\
	brain_shadow.cpp brain_text.cpp dinkc_bindings.cpp		\
	dinkc_bindings.h dinkc.cpp dinkc.h dinkc_console.cpp		\
	dinkc_console.h dinkc_console_renderer.cpp			\
	dinkc_console_renderer.h debug.cpp debug.h debug_renderer.cpp	\
	debug_renderer.h game_choice.cpp game_choice.h			\
	game_choice_renderer.cpp game_choice_renderer.h			\
	game_engine.cpp game_engine.h game_state.cpp game_state.h	\
	i18n.cpp i18n.h inventory.cpp inventory.h meminfo.cpp		\
	meminfo.h savegame.cpp savegame.h status.cpp status.h		\
	text.cpp text.h
freedinkedit_SOURCES = $(COMMON_OBJS) AppFreeDinkedit.h	\
	freedinkedit.cpp
nodist_freedink_SOURCES = $(WOERES)
nodist_freedinkedit_SOURCES = $(WOERES)

EXTRA_DIST = media/freedink.ico media/system.sfd media/README

resdir=$(top_srcdir)/share/freedink
install-exec-hook:
if HAVE_UPX
# UPX compression
# Not using --best because it takes much more time and the result is
# only a little bit smaller
# Needs to be done before bundling resources
	-$(UPX) "$(DESTDIR)$(bindir)/freedink$(EXEEXT)"
	-$(UPX) "$(DESTDIR)$(bindir)/freedinkedit$(EXEEXT)"
endif
# Add 'dink' and 'dinkedit' aliases, to please 3rd-party tools
	$(LN_S) -f "freedink$(EXEEXT)" "$(DESTDIR)$(bindir)/dink$(EXEEXT)"
	$(LN_S) -f "freedinkedit$(EXEEXT)" "$(DESTDIR)$(bindir)/dinkedit$(EXEEXT)"

uninstall-hook:
	rm -f "$(DESTDIR)$(bindir)/dink$(EXEEXT)"
	rm -f "$(DESTDIR)$(bindir)/dinkedit$(EXEEXT)"


# help2man-generated manpages
# Inspiration from (automake-1.10.info.gz)distcleancheck
dist_man_MANS = freedink.6 freedinkedit.6 dink.6 dinkedit.6
freedink.6: app.cpp $(top_srcdir)/configure.ac Makefile.am
	$(MAKE) $(AM_MAKEFLAGS) freedink$(EXEEXT)
	-$(HELP2MAN) -s6 -n "adventure and role-playing game (engine)"	\
	  --no-info --output=freedink.6 ./freedink$(EXEEXT)
freedinkedit.6: app.cpp $(top_srcdir)/configure.ac Makefile.am
	$(MAKE) $(AM_MAKEFLAGS) freedinkedit$(EXEEXT)
	-$(HELP2MAN) -s6 -n "adventure and role-playing game (editor)"	\
	  --no-info --output=freedinkedit.6 ./freedinkedit$(EXEEXT)
distclean-local:
	rm -f freedink.6 freedinkedit.6


# Woe icon and app infos
# Also check http://fragglet.livejournal.com/4448.html
.rc.o:
	$(WINDRES) -i $< -o $@

# How do we handle resources embedded in the executable binary?
if HAVE_WINDRES
WOERES=woeres.rc
else
WOERES=
endif


if HAVE_TESTS
check_PROGRAMS = test_str_util test_io_util TestEditorMap		\
	test_editor_screen test_dinkini test_dinkc test_dinkc_console	\
	test_dinkc_bindings test_live_sprites_manager test_brain_text	\
	test_text test_gfx_fonts TestIOGfxDisplay			\
	TestIOTouchDragAnywhere test_integration
.cxx.cpp:
	$(CXXTESTGEN) --error-printer \
		--include test_android_workaround.h \
		--include config.h --include SDL.h \
		-o $@ $<
EXTRA_DIST += test_android_workaround.h \
	$(patsubst %$(EXEEXT),%.cxx,$(check_PROGRAMS))
test_str_util_SOURCES = str_util.cpp test_str_util.cpp
test_io_util_SOURCES = io_util.cpp test_io_util.cpp
TestEditorMap_SOURCES = $(COMMON_OBJS) brain.cpp brain.h		\
	brain_bounce.cpp brain_button.cpp brain_diagonal.cpp		\
	brain_duck.cpp brain_keyboard.cpp brain_lateral.cpp		\
	brain_missile.cpp brain_mouse.cpp brain_none.cpp		\
	brain_onetime.cpp brain_people.cpp brain_pig.cpp		\
	brain_repeat.cpp brain_scale.cpp brain_shadow.cpp		\
	brain_text.cpp dinkc_bindings.cpp dinkc_bindings.h dinkc.cpp	\
	dinkc.h dinkc_console.cpp dinkc_console.h freedink.cpp		\
	game_engine.cpp game_engine.h game_choice.cpp game_choice.h	\
	game_state.cpp game_state.h i18n.cpp i18n.h inventory.cpp	\
	inventory.h meminfo.cpp meminfo.h savegame.cpp savegame.h	\
	status.cpp status.h text.cpp text.h TestEditorMap.cpp
test_dinkini_SOURCES = dinkini.cpp rect.cpp gfx_sprites.cpp	\
	ImageLoader.cpp fastfile.cpp str_util.cpp io_util.cpp	\
	paths.cpp log.cpp test_dinkini.cpp
test_dinkc_SOURCES = dinkc.cpp str_util.cpp paths.cpp io_util.cpp	\
	i18n.cpp test_dinkc.cpp
test_dinkc_console_SOURCES = test_dinkc_console.cpp dinkc_console.cpp	\
	str_util.cpp
test_editor_screen_SOURCES = $(COMMON_OBJS) brain.cpp brain.h		\
	brain_bounce.cpp brain_button.cpp brain_diagonal.cpp		\
	brain_duck.cpp brain_keyboard.cpp brain_lateral.cpp		\
	brain_missile.cpp brain_mouse.cpp brain_none.cpp		\
	brain_onetime.cpp brain_people.cpp brain_pig.cpp		\
	brain_repeat.cpp brain_scale.cpp brain_shadow.cpp		\
	brain_text.cpp dinkc_bindings.cpp dinkc_bindings.h dinkc.cpp	\
	dinkc.h dinkc_console.cpp dinkc_console.h freedink.cpp		\
	game_engine.cpp game_engine.h game_choice.cpp game_choice.h	\
	game_state.cpp game_state.h i18n.cpp i18n.h inventory.cpp	\
	inventory.h meminfo.cpp meminfo.h savegame.cpp savegame.h	\
	status.cpp status.h text.cpp text.h test_editor_screen.cpp
test_dinkc_bindings_SOURCES = $(COMMON_OBJS) brain.cpp brain.h		\
	brain_bounce.cpp brain_button.cpp brain_diagonal.cpp		\
	brain_duck.cpp brain_keyboard.cpp brain_lateral.cpp		\
	brain_missile.cpp brain_mouse.cpp brain_none.cpp		\
	brain_onetime.cpp brain_people.cpp brain_pig.cpp		\
	brain_repeat.cpp brain_scale.cpp brain_shadow.cpp		\
	brain_text.cpp dinkc_bindings.cpp dinkc_bindings.h dinkc.cpp	\
	dinkc.h dinkc_console.cpp dinkc_console.h freedink.cpp		\
	game_choice.cpp game_choice.h game_engine.cpp game_engine.h	\
	game_state.cpp game_state.h i18n.cpp i18n.h inventory.cpp	\
	inventory.h meminfo.cpp meminfo.h savegame.cpp savegame.h	\
	status.cpp status.h text.cpp text.h test_dinkc_bindings.cpp
test_live_sprites_manager_SOURCES = live_sprites_manager.cpp rect.cpp	\
	test_live_sprites_manager.cpp
test_brain_text_SOURCES = $(COMMON_OBJS) brain.cpp brain.h		\
	brain_bounce.cpp brain_button.cpp brain_diagonal.cpp		\
	brain_duck.cpp brain_keyboard.cpp brain_lateral.cpp		\
	brain_missile.cpp brain_mouse.cpp brain_none.cpp		\
	brain_onetime.cpp brain_people.cpp brain_pig.cpp		\
	brain_repeat.cpp brain_scale.cpp brain_shadow.cpp		\
	brain_text.cpp dinkc_bindings.cpp dinkc_bindings.h dinkc.cpp	\
	dinkc.h dinkc_console.cpp freedink.cpp game_choice.cpp		\
	game_choice.h game_engine.cpp game_engine.h game_state.cpp	\
	game_state.h i18n.cpp i18n.h inventory.cpp inventory.h		\
	meminfo.cpp meminfo.h savegame.cpp savegame.h status.cpp	\
	status.h text.cpp text.h test_brain_text.cpp
test_text_SOURCES = test_text.cpp text.cpp live_sprites_manager.cpp	\
	dinkini.cpp live_sprite.cpp rect.cpp gfx_sprites.cpp		\
	ImageLoader.cpp str_util.cpp io_util.cpp fastfile.cpp		\
	paths.cpp
test_gfx_fonts_SOURCES = test_gfx_fonts.cpp test_gfx_fonts_libe.h	\
	gfx_fonts.cpp rect.cpp ImageLoader.cpp str_util.cpp		\
	io_util.cpp paths.cpp resources.cpp gfx_palette.cpp		\
	FakeIOGfxDisplay.cpp FakeIOGfxDisplay.h IOGfxDisplay.cpp	\
	freedink_xpm.cpp
TestIOTouchDragAnywhere_SOURCES = TestIOTouchDragAnywhere.cpp	\
	IOTouchDragAnywhere.cpp
test_integration_SOURCES = $(COMMON_OBJS) brain.cpp brain.h		\
	brain_bounce.cpp brain_button.cpp brain_diagonal.cpp		\
	brain_duck.cpp brain_keyboard.cpp brain_lateral.cpp		\
	brain_missile.cpp brain_mouse.cpp brain_none.cpp		\
	brain_onetime.cpp brain_people.cpp brain_pig.cpp		\
	brain_repeat.cpp brain_scale.cpp brain_shadow.cpp		\
	brain_text.cpp dinkc_bindings.cpp dinkc_bindings.h dinkc.cpp	\
	dinkc.h dinkc_console.cpp dinkc_console.h freedink.cpp		\
	game_engine.cpp game_engine.h game_choice.cpp game_choice.h	\
	game_state.cpp game_state.h i18n.cpp i18n.h inventory.cpp	\
	inventory.h meminfo.cpp meminfo.h savegame.cpp savegame.h	\
	status.cpp status.h text.cpp text.h test_integration.cpp
TestIOGfxDisplay_SOURCES = TestIOGfxDisplay.cpp IOGfxDisplayGL2.cpp	\
	IOGfxDisplaySW.cpp IOGfxDisplay.cpp IOGfxSurfaceGL2.cpp		\
	IOGfxSurfaceSW.cpp IOGfxSurface.cpp IOGfxGLFuncs.cpp		\
	ImageLoader.cpp gfx_palette.cpp paths.cpp io_util.cpp		\
	str_util.cpp log.cpp freedink_xpm.cpp SDL_android_main.c
# Tests to run
TESTS = $(check_PROGRAMS)

clean-local:
	rm -f $(patsubst %$(EXEEXT),%.cpp,$(check_PROGRAMS))
	rm -rf tmp_ts/

if ANDROID
# Use ugly work-around
LOG_DRIVER = $(SHELL) $(top_srcdir)/android/remote-test-driver
# Needs graphics, will be marked as SKIP (driver detects 'shared')
# Can be tested manually by replacing libmain.so with it
TestIOGfxDisplay_LDFLAGS = -shared
else
# need to redefine it explicitely because we modified it for ANDROID :/
LOG_DRIVER = $(SHELL) $(top_srcdir)/autotools/test-driver
endif

if WOE
# Outside of wine stdout/stderr is not working unless explicitely redirected with > and 2>
TestIOGfxDisplay_LDFLAGS = -mconsole
endif

endif
