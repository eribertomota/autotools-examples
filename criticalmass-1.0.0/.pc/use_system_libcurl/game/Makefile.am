bin_PROGRAMS = critter

critter_SOURCES = \
        ActionCallbacks.cpp \
        Audio.cpp \
	BitmapManager.cpp \
        Callback.cpp \
        CallbackManager.cpp \
        Camera.cpp \
        EnemyFactory.cpp \
        FontManager.cpp \
        Game.cpp \
        GameState.cpp \
        Hero.cpp \
        Input.cpp \
        Keys.cpp \
        LPathManager.cpp \
        MenuManager.cpp \
        ModelManager.cpp \
	OnlineUpdate.cpp \
        OnlineUpdateDisplay.cpp \
        ParticleGroup.cpp \
        ParticleGroupManager.cpp \
        ParticleType.cpp \
        Particles.cpp \
        SampleManager.cpp \
	ScoreKeeper.cpp \
	Selectable.cpp \
	SelectableFactory.cpp \
        BaseEnemy.cpp \
        SimpleEnemy.cpp \
        Boss1Enemy.cpp \
        Skill.cpp \
        StageManager.cpp \
        Starfield.cpp \
	TextInput.cpp \
        Video.cpp \
        Weapon.cpp \
        WeaponDepot.cpp \
        XMLHelper.cpp \
        main.cpp

LDADD = \
	../curl/lib/libcurl.a \
	../utils/libutils.a \
	../utilssdl/libutilssdl.a \
	../utilsgl/libutilsgl.a \
	../tinyxml/libtinyxml.a

if WIN32
INCLUDES = -I../curl/include -I../tinyxml -I../utils -I../utilssdl -I../utilsgl -DDATA_DIR=\"./\"
LDADD += critter.res
else

if APPLE
INCLUDES = -I../curl/include -I../tinyxml -I../utils -I../utilssdl -I../utilsgl -DDATA_DIR=\"/Contents/Resources/\"
else
INCLUDES = -I../curl/include -I../tinyxml -I../utils -I../utilssdl -I../utilsgl -DDATA_DIR=\"$(pkgdatadir)/\"
endif

endif

depend:
	makedepend -I. -I/usr/include/g++-3 $(DEFS) $(INCLUDES) $(AM_CPPFLAGS) $(AM_CXXFLAGS) $(critter_SOURCES)

if WIN32
else
pkgdata_DATA = resource.dat

resource.dat:
	../tools/Packer ../data/description_file resource.dat

DISTCLEANFILES = resource.dat critter-static
endif

small:
	strip $(bin_PROGRAMS)
	upx -9 $(bin_PROGRAMS)

critter-static: $(critter_OBJECTS) $(critter_DEPENDENCIES)
	@ln -sf `g++ -print-file-name=libstdc++.a`
	@rm -f critter-static
	$(CXXLINK) -static-libgcc -L. $(critter_LDFLAGS) $(critter_OBJECTS) $(critter_LDADD) $(LIBS)
	@rm -f libstdc++.a
	strip critter-static
	upx -9 critter-static


MAINTAINERCLEANFILES = Makefile.bak Makefile.in
