if ALTPYTHON_ENABLED
ALTPYTHON_DIR = altpython
else
ALTPYTHON_DIR =
endif

if PYTHON_SWIG_ENABLED
EXAMPLES_DIR = examples
else
EXAMPLES_DIR =
endif

DIST_SUBDIRS = python altpython test examples
SUBDIRS = python $(ALTPYTHON_DIR) $(TEST_DIR) $(EXAMPLES_DIR)

EXTRA_DIST = Doxyfile.api.in doxy2swig.py __init__.py common.mk \
             swigmodulesinit_wrap.cpp arc_init.cpp
