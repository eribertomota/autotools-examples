dist_pkgdata_DATA = cancel_common.sh submit_common.sh scan_common.sh
pkgdata_DATA = lrms_common.sh

if PYTHON_LRMS_ENABLED
PYTHON_LRMS = slurmpy arc
else
PYTHON_LRMS =
endif

SUBDIRS = pbs pbspro fork sge condor lsf ll slurm boinc test $(PYTHON_LRMS)

DIST_SUBDIRS = pbs pbspro fork sge condor lsf ll slurm boinc test \
	       slurmpy arc
