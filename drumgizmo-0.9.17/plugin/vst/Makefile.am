if ENABLE_VST
noinst_LTLIBRARIES = libvstsdk.la
endif

# We know there are warnings in the VSTSDK code, so don't consider them errors.
CXXFLAGS:=$(filter-out -Werror -Wall ,$(CXXFLAGS))

# Targets to copy vst source files
pluginterfaces/vst2.x:
	$(MKDIR_P) pluginterfaces/vst2.x

pluginterfaces/vst2.x/aeffect.h: pluginterfaces/vst2.x @VST_SOURCE_PATH@/pluginterfaces/vst2.x/aeffect.h
	cp @VST_SOURCE_PATH@/pluginterfaces/vst2.x/aeffect.h $@

pluginterfaces/vst2.x/aeffectx.h: pluginterfaces/vst2.x @VST_SOURCE_PATH@/pluginterfaces/vst2.x/aeffectx.h
	cp @VST_SOURCE_PATH@/pluginterfaces/vst2.x/aeffectx.h $@

#pluginterfaces/vst2.x/vstfxstore.h: pluginterfaces/vst2.x @VST_SOURCE_PATH@/pluginterfaces/vst2.x/vstfxstore.h
#	cp @VST_SOURCE_PATH@/pluginterfaces/vst2.x/vstfxstore.h $@

public.sdk/source/vst2.x:
	$(MKDIR_P) public.sdk/source/vst2.x

public.sdk/source/vst2.x/audioeffectx.h: public.sdk/source/vst2.x public.sdk/source/vst2.x/audioeffect.h pluginterfaces/vst2.x/aeffect.h @VST_SOURCE_PATH@/public.sdk/source/vst2.x/audioeffectx.h
	cp @VST_SOURCE_PATH@/public.sdk/source/vst2.x/audioeffectx.h $@

public.sdk/source/vst2.x/audioeffectx.cpp: public.sdk/source/vst2.x public.sdk/source/vst2.x/aeffeditor.h pluginterfaces/vst2.x/aeffectx.h public.sdk/source/vst2.x/audioeffectx.h @VST_SOURCE_PATH@/public.sdk/source/vst2.x/audioeffectx.cpp
	cp @VST_SOURCE_PATH@/public.sdk/source/vst2.x/audioeffectx.cpp $@

public.sdk/source/vst2.x/audioeffect.h: public.sdk/source/vst2.x @VST_SOURCE_PATH@/public.sdk/source/vst2.x/audioeffect.h
	cp @VST_SOURCE_PATH@/public.sdk/source/vst2.x/audioeffect.h $@

public.sdk/source/vst2.x/audioeffect.cpp: public.sdk/source/vst2.x public.sdk/source/vst2.x/audioeffect.h @VST_SOURCE_PATH@/public.sdk/source/vst2.x/audioeffect.cpp
	cp @VST_SOURCE_PATH@/public.sdk/source/vst2.x/audioeffect.cpp $@

public.sdk/source/vst2.x/aeffeditor.h: public.sdk/source/vst2.x @VST_SOURCE_PATH@/public.sdk/source/vst2.x/aeffeditor.h
	cp @VST_SOURCE_PATH@/public.sdk/source/vst2.x/aeffeditor.h $@

public.sdk/source/vst2.x/vstplugmain.cpp: public.sdk/source/vst2.x @VST_SOURCE_PATH@/public.sdk/source/vst2.x/vstplugmain.cpp
	cp @VST_SOURCE_PATH@/public.sdk/source/vst2.x/vstplugmain.cpp $@

# Hack to compile vst sources without -Wall -Werror
libvstsdk_la_CXXFLAGS = -w $(VST_CPPFLAGS) -Ipublic.sdk/source/vst2.x -I.

nodist_libvstsdk_la_SOURCES = \
	public.sdk/source/vst2.x/audioeffectx.cpp \
	public.sdk/source/vst2.x/audioeffect.cpp \
	public.sdk/source/vst2.x/vstplugmain.cpp

CLEANFILES = \
	pluginterfaces/vst2.x/aeffect.h \
	pluginterfaces/vst2.x/aeffectx.h \
	public.sdk/source/vst2.x/audioeffectx.h \
	public.sdk/source/vst2.x/audioeffectx.cpp \
	public.sdk/source/vst2.x/audioeffect.h \
	public.sdk/source/vst2.x/audioeffect.cpp \
	public.sdk/source/vst2.x/aeffeditor.h \
	public.sdk/source/vst2.x/vstplugmain.cpp

clean-local:
	-rm -rf public.sdk pluginterfaces

#pluginterfaces/vst2.x/vstfxstore.h