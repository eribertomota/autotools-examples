pythondir = $(PYTHON_SITE_ARCH)/arc

if PYTHON_LRMS_ENABLED
    PYTHON_LRMS = SLURMPYmod.pm
else
    PYTHON_LRMS =
endif

pkgdata_SCRIPTS = CEinfo.pl PerfData.pl

dist_pkgdata_DATA = ARC0mod.pm SGEmod.pm FORKmod.pm PBS.pm PBSPRO.pm \
	LL.pm LSF.pm Condor.pm condor_env.pm SLURM.pm SLURMmod.pm Boinc.pm \
	IniParser.pm LogUtils.pm Sysinfo.pm \
	LRMSInfo.pm GMJobsInfo.pm HostInfo.pm RTEInfo.pm \
	InfoChecker.pm \
	ARC0ClusterInfo.pm ARC1ClusterInfo.pm \
	SGE.pm Fork.pm \
	XmlPrinter.pm GLUE2xmlPrinter.pm \
	LdifPrinter.pm GLUE2ldifPrinter.pm \
	NGldifPrinter.pm InfosysHelper.pm $(PYTHON_LRMS)

pkgdata_DATA = ConfigCentral.pm

if LDAP_SERVICE_ENABLED
dist_pkgdata_SCRIPTS = glue-generator.pl glite-info-provider-ldap
arcldapschemadir = $(pkgdatadir)/ldap-schema
dist_arcldapschema_DATA = schema/nordugrid.schema
endif

PERL = @PERL@

PERLSCRIPTS = $(dist_pkgdata_DATA) CEinfo.pl

TESTS_ENVIRONMENT = \
	PYTHONPATH=$(abs_top_builddir)/python/python:$(abs_top_builddir)/python/python/arc/.libs:$(abs_top_srcdir)/src/services/a-rex/infoproviders:$(abs_builddir) \
	$(PERL) -I$(srcdir) -Mstrict -wc
TESTS = $(PERLSCRIPTS)

check_SCRIPTS = $(PERLSCRIPTS)

# Check if BDI module is available, if not exclude Boinc.pm from TESTS variable.
Boinc.pm: FORCE
	$(eval TESTS := $(shell if `$(PERL) -e "use BDI; exit;" > /dev/null 2>&1`; then echo "$(TESTS)"; else echo "$(TESTS)" | sed 's/Boinc.pm//'; fi))
FORCE:

DIST_SUBDIRS = test
SUBDIRS = $(PERL_TEST_DIR)
