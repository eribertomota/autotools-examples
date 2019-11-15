if HED_ENABLED
if DOC_ENABLED
BUILD_SOURCES = external doc hed libs tests services clients utils wn doxygen
else
BUILD_SOURCES = external doc hed libs tests services clients utils wn
endif
else
BUILD_SOURCES =
endif

SUBDIRS = $(BUILD_SOURCES)
DIST_SUBDIRS = external doc hed libs tests services clients utils doxygen wn

# This won't work in case of cross-compilation. Please
# some autotools experts fix it.
if HED_ENABLED
install-exec-hook:
	if test "x$(build_triplet)" = "x$(host_triplet)"; then env LD_LIBRARY_PATH=$(DESTDIR)$(libdir):$(LD_LIBRARY_PATH) $(top_builddir)/src/utils/hed/arcplugin$(EXEEXT) -c $(DESTDIR)$(pkglibdir) -c $(DESTDIR)$(pkglibdir)/test -c $(DESTDIR)$(pkglibdir)/external; else echo "No .apd files since we are cross-compiling"; fi

uninstall-local:
	test "x$(build_triplet)" = "x$(host_triplet)" && rm -f $(DESTDIR)$(pkglibdir)/*.apd $(DESTDIR)$(pkglibdir)/test/*.apd $(DESTDIR)$(pkglibdir)/external/*.apd
endif
