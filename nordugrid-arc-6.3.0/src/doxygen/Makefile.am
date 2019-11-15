SWIG_DEPENDS = \
	$(top_srcdir)/swig/common.i \
	$(top_srcdir)/swig/credential.i \
	$(top_srcdir)/swig/data.i \
	$(top_srcdir)/swig/compute.i

INPUT = $(top_srcdir)/src/hed/libs/common \
	$(top_srcdir)/src/hed/libs/credential \
	$(top_srcdir)/src/hed/libs/data \
	$(top_srcdir)/src/libs/data-staging \
	$(top_srcdir)/src/hed/libs/compute

CPP_EXAMPLES = $(top_srcdir)/src/hed/libs/common/examples \
	$(top_srcdir)/src/hed/libs/credential/examples \
	$(top_srcdir)/src/hed/libs/data/examples \
	$(top_srcdir)/src/libs/data-staging/examples \
	$(top_srcdir)/src/hed/libs/compute/examples
PYTHON_EXAMPLES = $(top_srcdir)/python/examples

SPECIALISATION_MAPPINGS = JobState JobDescription
SPECIALISATION_MAPPINGS_JobState = \
	$(top_srcdir)/src/hed/acc/GRIDFTPJOB/JobStateGRIDFTPJOB.cpp \
	$(top_srcdir)/src/hed/acc/EMIES/JobStateEMIES.cpp
SPECIALISATION_MAPPINGS_JobDescription = \
	$(top_srcdir)/src/hed/acc/JobDescriptionParser/XRSLParser.cpp \
	$(top_srcdir)/src/hed/acc/JobDescriptionParser/ADLParser.cpp


.SECONDEXPANSION:

$(addsuffix _Mapping.dox, $(SPECIALISATION_MAPPINGS)): %_Mapping.dox: $(srcdir)/create-mapping-documentation.py $(top_srcdir)/src/hed/libs/compute/%.h $$(SPECIALISATION_MAPPINGS_%)
	$(PYTHON) $^ $*_Mapping.dox

Doxyfile.SDK.build: $(top_srcdir)/src/doxygen/Doxyfile.SDK
	cp $(srcdir)/Doxyfile.SDK Doxyfile.SDK.build
	sed "s/@TOP_SRCDIR@/$(subst /,\/,$(top_srcdir))/g" Doxyfile.SDK.build > Doxyfile.SDK.build.tmp
	mv Doxyfile.SDK.build.tmp Doxyfile.SDK.build
	sed "s/@INPUT@/$(subst /,\/,$(INPUT) $(addsuffix _Mapping.dox, $(SPECIALISATION_MAPPINGS)))/g" Doxyfile.SDK.build > Doxyfile.SDK.build.tmp
	mv Doxyfile.SDK.build.tmp Doxyfile.SDK.build
	sed "s/@EXAMPLES@/$(subst /,\/,$(CPP_EXAMPLES) $(PYTHON_EXAMPLES))/g" Doxyfile.SDK.build > Doxyfile.SDK.build.tmp
	mv Doxyfile.SDK.build.tmp Doxyfile.SDK.build
	sed "s/Doxyfile.SDK.layout.xml/Doxyfile.SDK.build.layout.xml/g" Doxyfile.SDK.build > Doxyfile.SDK.build.tmp
	mv Doxyfile.SDK.build.tmp Doxyfile.SDK.build
	for mapping in $(SPECIALISATION_MAPPINGS); do \
		sed "s/^FILTER_PATTERNS[[:space:]]*=/& *\/$${mapping}.h=$(subst /,\/,$(srcdir))\/adapt-and-filter-mapping-attributes.sed/g" Doxyfile.SDK.build > Doxyfile.SDK.build.tmp;\
		mv Doxyfile.SDK.build.tmp Doxyfile.SDK.build;\
	done


Doxyfile.SDK.build.layout.xml: $(top_srcdir)/src/doxygen/Doxyfile.SDK.layout.xml
	cp $(srcdir)/Doxyfile.SDK.layout.xml Doxyfile.SDK.build.layout.xml

SDKDEPENDENCIES = Doxyfile.SDK.build Doxyfile.SDK.build.layout.xml \
	$(srcdir)/add-bindings-deviations-to-dox.py \
	$(srcdir)/images/arcsdk.png \
	$(srcdir)/adapt-and-filter-mapping-attributes.sed \
	$(SWIG_DEPENDS) \
	$(wildcard $(addsuffix /*.h, $(INPUT))) \
	$(wildcard $(addsuffix /*.cpp, $(CPP_EXAMPLES))) \
	$(wildcard $(addsuffix /*.py, $(PYTHON_EXAMPLES))) \
	$(addsuffix _Mapping.dox, $(SPECIALISATION_MAPPINGS))

SDK: $(SDKDEPENDENCIES)
	doxygen -v | awk -F . '{ exit !($$1 >= 2 || $$1 == 1 && $$2 >= 8) }' || (echo "doxygen version 1.8.0 or greater required (version $$(doxygen -v) found)" && exit 1)
	doxygen Doxyfile.SDK.build
# Postprocessing: Add deviations from SDK API for language bindings (Python).
	for file in $(SWIG_DEPENDS); do $(PYTHON) $(srcdir)/add-bindings-deviations-to-dox.py $${file} SDK/html; done

EXTRA_DIST = Doxyfile.SDK Doxyfile.SDK.layout.xml images/arcsdk.png \
	     add-bindings-deviations-to-dox.py \
	     adapt-and-filter-mapping-attributes.sed \
	     create-mapping-documentation.py

CLEANFILES = SDK
